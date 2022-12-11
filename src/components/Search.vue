<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'

let code = ref<String>('')
let result = ref<Object>([])

const submitForm = (e: any) => {
    e.preventDefault()
}

</script>

<template>
  <div>
    <h1>Insira o código para rastreio</h1>
    <form @submit.prevent="submitForm()">
      <div class="box-field">
        <label for="username">Username</label>
        <input type="text" id="username" name="username" v-model="username" placeholder="Digite seu username">
      </div>
      <input type="submit" value="submit" name="submit">
    </form>
  </div>
</template>

<style lang="scss" scoped>

</style>
