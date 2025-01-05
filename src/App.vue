<template>
  <AppNavBar />
  <div class="mid-container" v-if="!showChat">
    <MidText />
  </div>
  <div class="last-container" v-if="!showChat"> 
    <SearchInput />
  </div>
  <div class="Chatopen" v-if="showChat">
    <ChatBox />
  </div>

</template>

<script>
import AppNavBar from './components/AppNavBar.vue';
import MidText from './components/MidText.vue';
import ChatBox from './components/ChatBox.vue';
import SearchInput from './components/SearchInput.vue';

export default {
  name: 'App',
  components: {
    AppNavBar,
    MidText,
    SearchInput,
    ChatBox,
  },
  data() {
    return {
      showChat: true,
    };
  },
};
</script>


<style>
#app{
  background: url(./assets/Background.png);
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 100vh; 
  display: flex;
  flex-direction: column;
}
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Inter", sans-serif;
}
.mid-container{
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: auto;
  margin-bottom: auto;
}
.last-container{
  margin-top: auto;
  margin-bottom: 20px;
}
.Chatopen{
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: auto;
  margin-bottom: auto;
  height: 100%;
  width: 100%;
}
</style>
