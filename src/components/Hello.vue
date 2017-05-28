<template>
  <div class="hello">
    <div class="panel-body">
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Abogado</th>
            <th>Email</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="abogado in abogados">
            <td><a v-bind:href="abogado.url">{{abogado.name}}</a></td>
            <td>{{abogado.email}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
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

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  firebase: {
    abogados: abogadosRef
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
