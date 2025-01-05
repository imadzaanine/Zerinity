<template>
    <div class="Search">
        <div class="questions">
            <div class="question">
                What is Zerepy?
            </div>
            <div class="question">
                How to create Zerepy AI agent?
            </div>
        </div>
        <div class="SearchArea">
            <input 
                v-model="message" 
                type="text" 
                placeholder="Search for answers" 
                @keyup.enter="sendMessage"
            />
            <button @click="sendMessage">Send</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SearchInput',
    data() {
        return {
            message: '', // Holds the user's input
        };
    },
    methods: {
        sendMessage() {
            if (this.message.trim()) {
                // Emit the message to the parent component
                this.$emit('send-message', this.message);
                // Clear the input field
                this.message = '';
            }
        },
    },
};
</script>


<style scoped>
.Search {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 20px;
}
.questions {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
}
.question {
    border-radius: 25px;
    background: #CEE5FF;
    box-shadow: 0px 2px 5px 0px #CEE5FF;
    color: #001167;
    font-family: "Inter", sans-serif;
    font-size: 20px;
    font-style: normal;
    font-weight: 600;
    line-height: normal;
    padding: 10px 20px;
}
button {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100px;
    font-family: "Inter", sans-serif;
    font-size: 20px;
    font-weight: 800;
    color: #001167;
    background: #CEE5FF;
    border: 3px solid #001167;
    border-radius: 78px;
    cursor: pointer;
}
input {
    width: 100%;
    height: 100%;
    border: none;
    background: #CEE5FF;
    font-family: "Inter", sans-serif;
    font-size: 20px;
    font-weight: 600;
    color: rgb(0, 0, 0, 0.31);
}
button:hover {
    background: #001167;
    color: #CEE5FF;
}
.SearchArea {
    display: flex;
    width: 653px;
    height: 55px;
    padding: 10px 10px 10px 20px;
    align-items: center;
    gap: 10px;
    flex-shrink: 0;
    border-radius: 177px;
    background: #CEE5FF;
    box-shadow: 0px 2px 5px 0px #CEE5FF;
}
</style>
