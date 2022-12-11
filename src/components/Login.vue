<script setup lang="ts">
import { ref, defineProps } from 'vue'
import axios from 'axios'

const props = defineProps({
  status: { 
    type: String, 
    required: true 
  }
})

let username = ref<String>('')
let token = ref<String>('')

const submitForm = () => {
  if(!username.value || !token.value)
  {
    alert('Complete os campos corretamente')
    return;
  }
  axios.get(`https://api.linketrack.com/track/json?user=${username.value}&token=${token.value}`)
    .then((response: Object) => {
      console.log(response)
    })
    .catch((e: Object) => {
      console.log(e)
    })
}

</script>

<template>
  <div>
    <h1>Insira suas credenciais para realizar o rastreio</h1>
    <form @submit.prevent="submitForm()">
      <div class="box-field">
        <label for="username">Username</label>
        <input type="text" class="input-form" id="username" name="username" v-model="username" placeholder="Digite seu username">
      </div>
      <div class="box-field">
        <label for="token">Token</label>
        <input type="text" class="input-form" id="token" name="token" v-model="token" placeholder="Digite seu token">
      </div>
      <input type="submit" value="Enviar" name="submit">
    </form>
  </div>
</template>

<style lang="scss" scoped>
  div{
    h1{
      margin: 0;

    }
    form{
      margin-top: 3rem;
      display: flex;
      flex-direction: column;
      gap: 1rem;
      width: 25rem;
      .box-field{
        display: flex;
        flex-direction: column;
        gap: .4rem;
        .input-form{
          padding: .6rem;
        }
      }
      .input-form,
      input[type='submit']{
        box-sizing: border-box;
        width: 100%;
        border: none;
        font-size: 1rem;
        border-radius: .4rem;
        transition: .4s;
        outline: none;
      }
      input[type='submit']{
        color: $white;
        padding: .8rem;
        margin-top: 1rem;
        background-color: $green;
        cursor: pointer;
        &:hover{
          background-color: $green2;
        }
      }
    }
  }
</style>
