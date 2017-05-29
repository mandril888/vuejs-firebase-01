<template>
  <div class="hello">
    <div class="panel-body">
      <h2>{{ msg }}</h2>
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Abogado</th>
            <th>Email</th>
            <th>Remove</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="abogado in abogados">
            <td><a v-bind:href="abogado.url">{{abogado.name}}</a></td>
            <td>{{abogado.email}}</td>
            <td><span class="glyphicon glyphicon-trash" aria-hidden="true" v-on:click="removeLawyer(abogado)"></span></td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="panel panel-default">
      <div class="panel-heading">
        <h3 class="panel-title">Add New Lawyer</h3>
      </div>
      <div class="panel-body">
         <form id="form" class="form-inline" v-on:submit.prevent="addLawyer">
          <div class="form-group">
            <label for="lawyerName">Name:</label>
            <input type="text" id="lawyerName" class="form-control" v-model="newLawyer.name">
          </div>
          <div class="form-group">
            <label for="layerEmail">Email:</label>
            <input type="text" id="layerEmail" class="form-control" v-model="newLawyer.email">
          </div>
          <div class="form-group">
            <label for="lawyerUrl">Url:</label>
            <input type="text" id="lawyerUrl" class="form-control" v-model="newLawyer.url">
          </div>
          <input type="submit" class="btn btn-primary" value="Add Lawyer">
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import Firebase from 'firebase'
import toastr from 'toastr'

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
      msg: 'Welcome to my Vue.js App',
      newLawyer: {
        name: '',
        email: '',
        url: 'http://'
      }
    }
  },
  firebase: {
    abogados: abogadosRef
  },
  methods: {
    addLawyer: function () {
      abogadosRef.push(this.newLawyer)
      this.newLawyer.name = ''
      this.newLawyer.gmail = ''
      this.newLawyer.url = 'http://'
    },
    removeLawyer: function (abogado) {
      abogadosRef.child(abogado['.key']).remove()
      toastr.success('Book removed successfully')
    }
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
