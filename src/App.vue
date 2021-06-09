<template>
  <div class="wrapper-chat">
    <div class="wrapper-user-enter" v-if="!firstClientLogin.isEnter">
      <div class="user-enter user-enter--blue">
        <input
          class="user-enter__input"
          type="text"
          v-model="firstClientLogin.name"
          placeholder="Username"
        />
        <input
          class="user-enter__input"
          type="password"
          v-model="firstClientLogin.pass"
          placeholder="Password"
          style="margin-top: 14px"
        />
        <button class="user-enter__button" @click="userEnter(firstClientLogin)">
          Enter
        </button>
      </div>
    </div>
    <Client
      v-if="firstClientLogin.isEnter"
      :messages="messages"
      :client="firstClientLogin"
      @addMessasgeEvent="addMessasge"
      @clientExitEvent="firstClientLogin.isEnter = false"
      @clientRemoveEvent="clientremove"
    />
    <div class="split"></div>
    <div class="wrapper-user-enter" v-if="!secondClientLogin.isEnter">
      <div class="user-enter user-enter--yellow">
        <input
          class="user-enter__input"
          type="text"
          v-model="secondClientLogin.name"
          placeholder="Username"
        />
        <input
          class="user-enter__input"
          type="password"
          v-model="secondClientLogin.pass"
          placeholder="Password"
          style="margin-top: 14px"
        />
        <button
          class="user-enter__button"
          @click="userEnter(secondClientLogin)"
        >
          Enter
        </button>
      </div>
    </div>
    <Client
      v-if="secondClientLogin.isEnter"
      :messages="messages"
      :client="secondClientLogin"
      @clientExitEvent="secondClientLogin.isEnter = false"
      @addMessasgeEvent="addMessasge"
      @clientRemoveEvent="clientremove" 
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
      firstClientLogin: {
        name: "",
        pass: "",
        isEnter: false,
        messages: [],
        id: 1,
      },
      secondClientLogin: {
        name: "",
        pass: "",
        isEnter: false,
        messages: [],
        id: 1,
      },
      reg: [],
      messages: [],
    };
  },
  methods: {
    clientremove(user) {
      this.reg = this.reg.filter((item) => {
        return item.name !== user.name;
      });
      this.messages = this.messages.filter((item) => {
        return item.senderId !== user.name;
      });
      user.isEnter = false
    },
    addMessasge(messageInfo) {
      this.messages.push({
        senderId: messageInfo.senderId,
        text: messageInfo.text,
        id: this.messages.length,
        senderName: "Second",
      });
    },
    clientExit(isClientEnter) {
      isClientEnter = false;
      console.log(isClientEnter);
    },
    userEnter(user) {
      let check = false;
      this.reg.forEach((item) => {
        if (item.name === user.name && item.password === user.pass) {
          check = !check;
          item.messages = this.messages.filter((element) => {
            return element.senderId === item.name;
          });
        }
      });
      if (!check) {
        this.reg.push({
          name: user.name,
          password: user.pass,
        });
      }
      user.isEnter = true;
    },
  },
  computed: {},
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
  background-color: #2e81fd;
}

.user-enter--yellow {
  background-color: #ffca2c;
}

.user-enter__button {
  margin-top: 20px;
}
</style>
