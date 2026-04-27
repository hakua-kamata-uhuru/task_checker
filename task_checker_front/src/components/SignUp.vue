<script setup>
import Header from './Header.vue'
import { ref } from 'vue' //追加
import { auth, createUserWithEmailAndPassword } from '../firebase'; //追加
import { useRouter } from 'vue-router'; //追加

const email = ref('');  //  追加
const password = ref('') //  追加

const router = useRouter();  //追加

const handleSignUp = async() => {
  try {
    await createUserWithEmailAndPassword(auth, email.value, password.value)
    router.push("/home");
  }catch(error) {
    console.log('ユーザー登録できませんでした', error)
  }
}

</script>

<template>
  <Header />
  <div class="form-body">
    <h1>新規登録</h1>
    <input type="text" id="email" v-model="email" placeholder="email"> <!--v-modelディレクティブの追加-->
    <input type="password" id="password" v-model="password" placeholder="password">  <!-- v-modelディレクティブの追加-->
    <button value="新規登録" @click="handleSignUp">新規登録</button>  <!--追加-->
    <p>既にアカウントをお持ちの方はこちらへ<router-link to="/">こちら</router-link></p>  <!--追加-->
  </div>
</template>

<style scoped>
.form-body {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 50vh;
  padding: 2vw 10vw;
  text-align: center;
}

input {
  margin-bottom: 16px;
}

button {
  background-color: rgb(66, 163, 247);
  color: white;
  border-radius: 25px;
  border-style: none;
  padding: 8px 20px;
  margin-bottom: 8px;
  font-size: 15px;
  width: 246px;
}
</style>