<template>
  <div class="message">
    <ul class="message__list">
      <li
        v-for="msg in messages_prop"
        :key="msg.id"
        class="message__item"
        :class="{
          'message__item--left': msg.senderId !== clientId_prop,
          'message__item--right': msg.senderId === clientId_prop,
        }"
      >
        {{ msg.text }}
        <p class="message__name">{{msg.senderId}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Messages",
  props: ["messages_prop", "clientId_prop"],
};
</script>

<style scoped>
.message {
  flex: 1;
}

.message__list {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.message__item {
  border: 2px solid black;
  border-radius: 10px;
  padding: 10px 20px;
  margin-top: 10px;
  max-width: 50%;
}

.message__item:first-child {
  margin-top: 0;
}

.message__item--left {
  align-self: flex-start;
  text-align: left;
  background-color: #2E81FD;
  /* background-color: #0b5ed7; */
  /* color: white; */
}

.message__item--right {
  align-self: flex-end;
  text-align: right;
  background-color: #ffca2c;
}

.message__name {
  font-size: 12px;
  opacity: .6;
}
</style>
