<template>
  <div class="wrapper-chat">
    <div class="wrapper-user-enter" v-if="!isFirstClientEnter">
      <div class="user-enter user-enter--blue">
        <input
          class="user-enter__input"
          type="text"
          v-model="FirstClientName"
          placeholder="Username"
          @keyup.enter="isFirstClientEnter = !isFirstClientEnter"
        />
        <button
          class="user-enter__button"
          @click="isFirstClientEnter = !isFirstClientEnter"
        >
          Enter
        </button>
      </div>
    </div>
    <Client
      v-if="isFirstClientEnter"
      :messages="messages"
      :clientId="FirstClientName"
      @addMessasgeEvent="addMessasge"
    />
    <div class="split"></div>
    <div class="wrapper-user-enter" v-if="!isSecondClientEnter">
      <div class="user-enter user-enter--yellow">
        <input
          class="user-enter__input"
          type="text"
          v-model="SecondClientName"
          placeholder="Username"
          @keyup.enter="isSecondClientEnter = !isSecondClientEnter"
        />
        <button
          class="user-enter__button"
          @click="isSecondClientEnter = !isSecondClientEnter"
        >
          Enter
        </button>
      </div>
    </div>
    <Client
      v-if="isSecondClientEnter"
      :messages="messages"
      :clientId="SecondClientName"
      @addMessasgeEvent="addMessasge"
    />
  </div>
</template>

<script>
import Client from "./components/Client.vue";

export default {
  name: "App",
  components: {
    Client,
  },
  data() {
    return {
      isFirstClientEnter: false,
      FirstClientName: "Username1",
      isSecondClientEnter: false,
      SecondClientName: "Username2",
      messages: [],
    };
  },
  methods: {
    addMessasge(messageInfo) {
      this.messages.push({
        senderId: messageInfo.senderId,
        text: messageInfo.text,
        id: this.messages.length,
        senderName: "Second",
      });
    },
  },
  computed: {
    FirstClient() {
      return this.msg.filter((item) => {
        return item.senderId === 1;
      });
    },
    SecondClient() {
      return this.msg.filter((item) => {
        return item.senderId === 2;
      });
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

ul > li {
  list-style-type: none;
}

button,
input {
  font-size: 20px;
  padding: 3px 10px;
  border-radius: 6px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.wrapper-chat {
  display: flex;
  min-height: 100vh;
}

.split {
  width: 3px;
  background: black;
}

.wrapper-user-enter {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.user-enter {
  display: flex;
  border: 2px solid black;
  border-radius: 10px;
  flex-direction: column;
  padding: 18px;
}

.user-enter--blue {
  background-color: #2E81FD;
}

.user-enter--yellow {
  background-color: #ffca2c;
}

.user-enter__button {
  margin-top: 20px;
}
</style>
