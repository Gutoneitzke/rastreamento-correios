<script setup lang="ts">
import { ref } from 'vue'

let username = ref<String>('')
let token = ref<String>('')
let code = ref<String>('')
let result = ref<Object>([])

</script>

<template>
  <div>
    <h1>Insira suas credenciais para realizar o rastreio</h1>
    <form action="">
      <div class="box-field">
        <label for="username">Username</label>
        <input type="text" id="username" name="username" v-model="username" placeholder="Digite seu username">
      </div>
      <div class="box-field">
        <label for="token">Token</label>
        <input type="text" id="token" name="token" v-model="token" placeholder="Digite seu token">
      </div>
    </form>
  </div>
</template>

<style scoped>

</style>
