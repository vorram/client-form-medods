<template>
  <div class="submit-message">
    <div class="message-container">
      <div class="message"><img src="../assets/check-bold.png" />Клиент успешно создан</div>
      <button v-on:click="$emit('reset-form')">Новый Клиент</button>
    </div>
  </div>
</template>

<script>
export default {}
</script>
