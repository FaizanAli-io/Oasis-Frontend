<template>

  <div v-if="commands.length" class="grid grid-cols-3 gap-8">
    <button v-for="command in commands" v-bind:key="command[0]" @click="runCommand(command[0])"
      class="py-6 bg-green-600 text-white text-2xl rounded-lg"> {{ command[1] }} </button>
  </div>

  <div v-else>
    Nice try big boy, but you aren't authenticated to run commands.
  </div>

</template>

<script>

import axios from 'axios'

import { useUserStore } from '@/stores/user'
import { useToastStore } from '@/stores/toast'

export default {
  name: 'AdminView',

  setup() {
    const userStore = useUserStore()
    const toastStore = useToastStore()
    return { userStore, toastStore }
  },

  data() { return { commands: [] } },

  mounted() { this.getCommands() },

  methods: {
    getCommands() {
      axios
        .get('api/core/')
        .then(response => {
          console.log('Commands: ', response.data)
          this.commands = response.data
        })
        .catch(error => {
          console.log('Error: ', error)
        })
    },

    runCommand(command) {
      axios
        .get(`api/core/${command}`)
        .then(response => {
          console.log('Message: ', response.data)
        })
        .catch(error => {
          console.log('Error: ', error)
        })
    },
  }
}

</script>