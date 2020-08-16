<template>
  <div>
    <ul>
      <li v-for="message in messages" :key="message.text">
        {{ message.text }}
      </li>
    </ul>
  </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
  head(){
    return {
      title: `Комната ${this.user.room}`
    }
  },
  middleware: ['chat'],
  computed: mapState(['user', 'messages'])
}
</script>