<template>
  <div id="app">
    <ClientForm v-show="!this.formSubmitted" v-on:form-submit="this.toggleDisplay" />
    <SubmitMessage v-show="this.formSubmitted" v-on:reset-form="this.toggleDisplay" />
  </div>
</template>

<script>
import ClientForm from './components/ClientForm.vue'
import SubmitMessage from './components/SubmitMessage.vue'

export default {
  name: 'App',
  components: {
    ClientForm,
    SubmitMessage,
  },
  data() {
    return {
      formSubmitted: false,
    }
  },
  methods: {
    toggleDisplay() {
      if (this.formSubmitted) {
        this.formSubmitted = false
      } else {
        this.formSubmitted = true
      }
    },
  },
}
</script>
