<script setup lang="ts">
import { ref, defineProps } from 'vue'
import axios from 'axios'

let username = ref<String>('')
let token = ref<String>('')
let code = ref<String>('')
let result = ref<Object>([])
let showLogin = ref<Boolean>(true)

const submitForm = () => {
  if(!username.value || !token.value || !code.value)
  {
    alert('Complete os campos corretamente')
    return;
  }
  axios.get(`https://api.linketrack.com/track/json?user=${username.value}&token=${token.value}&codigo=${code.value}`)
    .then((response: any) => {
      if(response.status == 200 && response.data.eventos.length > 0)
      {
        result.value = response.data.eventos
        showLogin.value = false
      }
    })
    .catch((e: Object) => {
      console.log(e)
    })
}

</script>

<template>
  <div class="content">
    <div v-if="showLogin" class="login">
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
        <input type="submit" class="button" value="Enviar" name="submit">
      </form>
    </div>
    <div v-else class="result">
      <button @click="showLogin = true" class="button">Nova consulta</button>
      <table>
        <thead>
          <tr>
            <th>Data</th>
            <th>Hora</th>
            <th>Local</th>
            <th>Status</th>
            <th>SubStatus</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(r,i) in result" :key="i">
            <td v-text="r.data"></td>
            <td v-text="r.hora"></td>
            <td v-text="r.local"></td>
            <td v-text="r.status"></td>
            <td v-html="r.subStatus"></td>
          </tr>
        </tbody>
      </table>
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
    .input-form,
    .button{
      box-sizing: border-box;
      border: none;
      font-size: 1rem;
      border-radius: .4rem;
      transition: .4s;
      outline: none;
    }
    .button{
      color: $white;
      padding: .8rem;
      margin-top: 1rem;
      background-color: $green;
      cursor: pointer;
      &:hover{
        background-color: $green2;
      }
    }
    h1{
      margin: 0;
      text-align: center;
      b{
        color: $green;
      }
    }
    .login{
      display: flex;
      flex-direction: column;
      align-items: center;
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
      }
    }
    .result{
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 2rem;
      table{
        padding: 1rem;
        th{
          border-bottom: 1px solid $green;
        }
        th,td{
          padding: .3rem 1rem;
        }
      }
    }
  }
</style>