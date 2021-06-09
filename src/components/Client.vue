<template>
  <div class="client">
    <div class="buttons-inline">
      <button class="exit" @click="$emit('clientExitEvent')" style="margin-right: 20px">exit</button>
      <button class="exit" @click="$emit('clientRemoveEvent', client)">remove user</button>
    </div>

    <Message :messages_prop="messages" :clientId_prop="client.name" />

    <div class="send-message">
      <input
        class="send-message__input"
        type="text"
        v-model="newMessageText"
        placeholder="New message"
        @keyup.enter="newMessage"
      />
      <button class="send-message__button" @click="newMessage">Send</button>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue";

export default {
  name: "Client",
  props: ["messages", "client"],
  components: {
    Message,
  },
  data() {
    return {
      newMessageText: "",
    };
  },
  methods: {
    newMessage() {
      this.$emit("addMessasgeEvent", {
        text: this.newMessageText,
        senderId: this.client.name,
      });
      this.newMessageText = "";
    },
  },
};
</script>

<style scoped>
.client {
  flex: 1;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  padding: 30px;
}

.client--first {
  background: green;
}

.client--second {
  background: red;
}

.send-message {
  display: flex;
  margin-top: 15px;
}

.send-message__input {
  flex: 1;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}

.send-message__button {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}

.buttons-inline {
  display: flex;
}

.buttons-inline > button {
  flex: 1;
}

.exit {
  margin-bottom: 20px;
}
</style>
