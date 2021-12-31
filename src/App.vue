<template>
  <div class="container">
    <form class="card" @submit.prevent="createPerson">
      <h2>Работа с базой данных</h2>
      <div class="form-control">
        <label for="name">Введите имя</label>
        <input type="text" id="name" v-model.trim="name">
      </div>
      <button class="btn primary" :disabled="!name.length">Создать человека</button>
    </form>
    <app-people-list :people="people" @load="loadPeople"></app-people-list>
  </div>
</template>

<script>
import AppPeopleList from "./AppPeopleList";
import axios from 'axios'
export default {
  data() {
    return {
      name: '',
      people: []
    }
  },
  mounted() {
    this.loadPeople()
  },
  methods: {
    async createPerson () {
      const response = await fetch('https://vue-with-http-d3b6e-default-rtdb.firebaseio.com/people.json', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          firstName: this.name
        })
      })

      const firebaseData = await response.json()

      this.people.push({
        firstName: this.name,
        id: firebaseData.name
      })
      this.name = ''
    },
    async loadPeople() {
      const { data } = await axios.get('https://vue-with-http-d3b6e-default-rtdb.firebaseio.com/people.json')
      this.people = Object.keys(data).map((key) => {
        return {
          id: key,
          // firstName: data[key].firstName
          ...data[key]
        }
      })
    }
  },
  components: {
    AppPeopleList
  }
}
</script>

<style>

</style>
