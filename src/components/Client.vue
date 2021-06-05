<template>
  <div class="client">
    <Message :messages_prop="messages" :clientId_prop="clientId" />

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
  props: ["messages", "clientId"],
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
        senderId: this.clientId,
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
  background-color: #22B872;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
</style>
