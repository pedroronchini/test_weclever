<template>
  <transition name="modal">
    <div class="modal-mask" @click="$emit('close')">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            <slot name="header">
              <h1>Lista de Filmes</h1>
              <button class="close" @click="$emit('close')">X</button>
            </slot>
          </div>
          <div class="modal-body">
              <ul v-for="list_films in list_films" :key="list_films.name">
                <li>{{ list_films.title}}</li>
              </ul>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import axios from 'axios';

export default {
  name: 'modal',

  data () {
    return {
      list_films: [],
      films: []
    }
  },

  methods: {
    close() {
      this.$emit('close');
    },
  },

  mounted () {
    axios.get('https://swapi.dev/api/films')
      .then(response => {
        const jsonobjecta = JSON.stringify(response.data)
        const object = JSON.parse(jsonobjecta)
        console.log(object)
        
        this.list_films = object.results
        console.log(this.list_films[0].films)
    })
  }
};
</script>

<style scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 400px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: rgb(0, 0, 0);
  border-radius: 10%;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
  color: #FFe81F;
}

.modal-header {
  margin-top: 0;
  margin-left: 40px;
  display: flex;
  flex-direction: row;
}


.close {
  height: 20px;
  border: 1px solid #000000;
  border-style: none;
  background: none;
  margin-left: 180px;
  color: #FFe81F;
}

.modal-body {
  margin: 20px 0;
}


.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

li {
  list-style: none;
}

</style>