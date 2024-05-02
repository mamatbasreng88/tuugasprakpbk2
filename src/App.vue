<template>
  <div class="background">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSBB1MPjjN9OnSRF3-NHDci50nSc6zY55BRXg&s" alt="background"/>
  </div>
  <div class="content">
    <h1>Selamat Datang Di Chikallow</h1>
    <div :class="{ app: true, 'logged-in': isLogged, 'logged-in-pressed': isLoggedPressed }">
      <br>
      <br>
      <h2>Login</h2>
      <form @submit.prevent="login">
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="email" required :class="{ 'input-error': emailError }">
          
          <span v-show="emailError" class="error-message">Email harus diisi</span>
        </div>
        <div>
          <label for="password">Password:</label>
          <input type="password" id="password" v-model="password" required :class="{ 'input-error': passwordError }">
          
          <span v-show="passwordError" class="error-message">Password harus diisi</span>
        </div>
        <button type="submit">Login</button>
      </form>
      
      <div v-show="isLogged" class="notification">
        <p>Email dan Password berhasil login:</p>
        <p>Email: {{ email }}</p>
        <p>Password: {{ password }}</p>
      </div>
      
      <div v-show="isLoggedPressed" class="notification">
        <p>Email dan Password berhasil login</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const email = ref('');
const password = ref('');
const isLogged = ref(false);
const isLoggedPressed = ref(false);
const emailError = ref(false);
const passwordError = ref(false);

function login() {
  if (!email.value) {
    emailError.value = true;
    return;
  }
  if (!password.value) {
    passwordError.value = true;
    return;
  }

  console.log('Email:', email.value);
  console.log('Password:', password.value);

  isLogged.value = true;
  isLoggedPressed.value = true;

  setTimeout(resetPage, 3000);
}

function resetPage() {
  email.value = '';
  password.value = '';
  isLogged.value = false;
  isLoggedPressed.value = false;

  emailError.value = false;
  passwordError.value = false;
}
</script>

<style scoped>

.background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.background img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(0.8);
}


.content {
  position: relative;
  z-index: 1;
  padding: 20px;
  text-align: center;
}

h1 {
  color: rgb(255, 255, 255);
}

.app {
  max-width: 300px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  color: white;
}

.logged-in {
  background-color: rgb(49, 31, 49); 
}

.logged-in-pressed {
  background-color: rgb(210, 147, 209);
}

h2 {
  margin-top: -50px;
}

form div {
  margin-bottom: 10px;
}

input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
}


.input-error {
  border-color: red;
}

.error-message {
  color: red;
  font-size: 0.8em;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}


.notification {
  margin-top: 20px;
  background-color: rgba(0, 255, 0, 0.1);
  padding: 10px;
  border-radius: 5px;
}
</style>
