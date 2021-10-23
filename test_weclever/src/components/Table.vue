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
      <tr v-for="list in list " :key="list">
        <td>{{ list.name }}</td>
        <td>{{ list.height }}</td>
        <td>{{ list.mass }}</td>
        <td>{{ list.birth_year }}</td>
        <td>{{ list.gender }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Table',

  data () {
    return {
      list: []
    }
  },

  mounted () {
    axios.get('https://swapi.dev/api/people/')
        .then(response => {
          const jsonobjecta = JSON.stringify(response.data)
          const object = JSON.parse(jsonobjecta)
        console.log(object.results[1])
          this.list = object.results[0]
    })
    

  }
}
</script>

<style scoped>
table {
  width:100%;
}

table, th, td {
  border-top: 2px solid #FFFFFF;
  border-collapse: collapse;
  color: #FFe81F;
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
</style>
