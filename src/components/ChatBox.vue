<template>
  <div class="ChatBox">
    <div class="chat-header">
      <h2>Chat with Zerepy</h2>
    </div>
    <div class="chat-messages">
      <div 
        v-for="(message, index) in messages" 
        :key="index" 
        :class="['message', message.user === 'user' ? 'sent' : 'received']"
      >
        <span class="text">{{ message.text }}</span>
      </div>
    </div>
    <div class="chat-input">
      <SearchInput @send-message="addMessage" />
    </div>
  </div>
</template>

<script>
import OpenAI from "openai";
import SearchInput from "./SearchInput.vue";

export default {
  name: "ChatBox",
  components: {
    SearchInput,
  },
  data() {
    return {
      messages: [
        { user: "Zerepy", text: "Hello! How can I help you today?" },
      ],
      loading: false, 
      assistant_id: "asst_LfeV805QSqtqLQ7AQWRk9tiB",
    };
  },
  methods: {
    async addMessage(userMessage) {
      const openai = new OpenAI({
        apiKey: process.env.VUE_APP_OPENAI_API_KEY,
        dangerouslyAllowBrowser: true, // Ensure this is your correct API key
      });

      // Add user message to the conversation
      this.messages.push({ user: "user", text: userMessage });

      const assistant = await openai.beta.assistants.retrieve(this.assistant_id);
      // Show loading response
      this.loading = true;
      this.messages.push({ user: "Zerepy", text: "Thinking..." });

      // Retrieve the assistant and create a thread
      const thread = await openai.beta.threads.create();



      try {
        // Send the user message to the created thread
        await openai.beta.threads.messages.create(thread.id, {
          role: "user",
          content: userMessage,
        });

        // Monitor the run and get the assistant response
        let run = await openai.beta.threads.runs.create(thread.id, {
          assistant_id: assistant.id,
        });

        while (run.status !== "completed") {
          run = await openai.beta.threads.runs.retrieve(run.thread_id, run.id);
        }

        // Fetch the messages from the run and display them
        const messages = await openai.beta.threads.messages.list(run.thread_id);

        // Replace "Thinking..." message with the assistant's response
        const assistantMessage = messages.data.find(
          (msg) => msg.role === "assistant"
        );

        if (assistantMessage) {
          this.messages[this.messages.length - 1] = {
            user: "Zerepy",
            text: assistantMessage.content[0].text.value,
          };
        }
      } catch (error) {
        console.error(error);
        this.messages[this.messages.length - 1] = {
          user: "Zerepy",
          text: "Sorry, I encountered an error while processing your request.",
        };
      } finally {
        this.loading = false;
      }
    },
  },
};
</script>

<style scoped>
.ChatBox {
  display: flex;
  flex-direction: column;
  width: 90%;
  height: 80%;
  max-width: 800px;
  max-height: 90vh;
  background: #f9f9f9;
  border-radius: 15px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  margin: auto;
}
.chat-header {
  background: #001167;
  color: #fff;
  padding: 15px;
  text-align: center;
}
.chat-messages {
  flex: 1;
  padding: 10px;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.message {
  display: flex;
  flex-direction: column;
  max-width: 75%;
  padding: 10px;
  border-radius: 10px;
}
.sent {
  align-self: flex-end;
  background: #CEE5FF;
  color: #001167;
}
.received {
  align-self: flex-start;
  background: #ffffff;
  color: #001167;
  border: 1px solid #CEE5FF;
}
.chat-input {
  border-top: 1px solid #ddd;
  padding: 10px;
  background: #f5f5f5;
}
</style>
