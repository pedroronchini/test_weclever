<template>
  <div class="hello">
    <table class="table">
      <tr>
        <th>Name</th>
        <th>Height</th>
        <th>Mass</th>
        <th>Birth year</th>
        <th>Gender</th>
      </tr>
      <tr v-for="list in list " :key="list.id">
        <td><button @click="showModal = true">{{ list.name }}</button></td>
        <td>{{ list.height }}</td>
        <td>{{ list.mass }}</td>
        <td>{{ list.birth_year }}</td>
        <td>{{ list.gender }}</td>
      </tr>
    </table>
    <modal v-if="showModal" @close="showModal =  false" />
  </div>


</template>

<script>
import axios from 'axios';
import Modal from './Modal.vue';


export default {
  name: 'Table',

  data () {
    return {
      list: [],
      showModal: false,
    }
  },

  mounted () {
    axios.get(`https://swapi.dev/api/people/`)
        .then(response => {
          const jsonobjecta = JSON.stringify(response.data)
          const object = JSON.parse(jsonobjecta)
          console.log(object)
          this.list = object.results
    })
  },

  components: {
    Modal
  }
}
</script>

<style scoped>
table {
  width:100%;
}

table, th, td {
  border-top: 2px solid #FFE81F;
  border-collapse: collapse;
  color: #FFFFFF;
}

th, td {
  padding: 15px;
  text-align: left;
}

#t01 tr:nth-child(even) {
  background-color: #eee;
}

#t01 tr:nth-child(odd) {
 background-color: #FFFFFF;
}

#t01 th {
  background-color: #000000;
  color: #FFFFFF;
}

button {
  border: none;
  background: none;
  color: #FFFFFF;
}
</style>
