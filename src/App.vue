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
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: ''
    }
  },
  methods: {
    createPerson () {
      // https://vue-with-http-d3b6e-default-rtdb.firebaseio.com/
      // this.name
    }
  }
}
</script>

<style>

</style>
