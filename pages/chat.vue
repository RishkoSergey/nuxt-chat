<template>
  <div class="c-wrap">
    <div class="c-chat" ref="block">
      <ul>
        <Message 
          v-for="message in messages" 
          :key="message.text" 
          :name="message.name"
          :text="message.text"
          :owner="message.id === user.id"
        />
      </ul>
    </div>
    <div class="c-form">
      <ChatForm />
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';
import Message from '../components/Message';
import ChatForm from '../components/ChatForm';

export default {
  components: {
    Message,
    ChatForm
  },
  head(){
    return {
      title: `Комната ${this.user.room}`
    }
  },
  middleware: ['chat'],
  computed: mapState(['user', 'messages']),
  watch: {
    messages() {
      setTimeout(() => {
        this.$refs.block.scrollTop = this.$refs.block.scrollHeight;
      }, 0);
    }
  }
}
</script>

<style scoped>
.c-wrap {
  height: 100%;
  position: relative;
  overflow: hidden;
}

.c-form {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 1rem;
  height: 80px;
  background: #212121;
}

.c-chat {
  position: absolute;
  bottom: 80px;
  top: 0;
  left: 0;
  right: 0;
  padding: 1rem;
  overflow-y: auto;
}
</style>