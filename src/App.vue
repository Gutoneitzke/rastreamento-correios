<script setup lang="ts">
import { ref, defineProps } from 'vue'
import axios from 'axios'

let username = ref<String>('')
let token = ref<String>('')
let code = ref<String>('')

const submitForm = () => {
  if(!username.value || !token.value)
  {
    alert('Complete os campos corretamente')
    return;
  }
  axios.get(`https://api.linketrack.com/track/json?user=${username.value}&token=${token.value}&codigo=${code.value}`)
    .then((response: Object) => {
      console.log(response)
    })
    .catch((e: Object) => {
      console.log(e)
    })
}

</script>

<template>
  <div class="content">
    <div class="login">
      <h1>Insira suas <b>credenciais</b> da <b>(https://linketrack.com)</b><br>para realizar o <b>rastreio</b></h1>
      <form @submit.prevent="submitForm()">
        <div class="box-field">
          <label for="username">Username</label>
          <input type="text" class="input-form" id="username" name="username" v-model="username" placeholder="Digite seu username">
        </div>
        <div class="box-field">
          <label for="token">Token</label>
          <input type="password" class="input-form" id="token" name="token" v-model="token" placeholder="Digite seu token">
        </div>
        <div class="box-field">
          <label for="code">Código</label>
          <input type="text" class="input-form" id="code" name="code" v-model="code" placeholder="Digite o código do produto">
        </div>
        <input type="submit" value="Enviar" name="submit">
      </form>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .content{
    background-color: $dark;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    .login{
      display: flex;
      flex-direction: column;
      align-items: center;
      h1{
        margin: 0;
        text-align: center;
        b{
          color: $green;
        }
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
  }
</style>