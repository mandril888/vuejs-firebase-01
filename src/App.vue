<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view></router-view>
  </div>
</template>

<script src="https://www.gstatic.com/firebasejs/4.0.0/firebase.js"></script>
<script>
  import Vue from 'vue'
  import Firebase from 'firebase'

  // Initialize Firebase
  let config = {
    apiKey: 'AIzaSyA8_JgoOz1mr8o9T6Wvhlf9YCh4BT6raBw',
    authDomain: 'infante-abogados.firebaseapp.com',
    databaseURL: 'https://infante-abogados.firebaseio.com',
    projectId: 'infante-abogados',
    storageBucket: 'infante-abogados.appspot.com',
    messagingSenderId: '796651083135'
  }

  let app = Firebase.initializeApp(config)
  let db = app.database()
  let abogadosRef = db.ref('abogados')

  Vue.component('firebase', {
    abogados: abogadosRef
  })

  export default {
    name: 'app',
    firebase: {
      abogados: abogadosRef
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
