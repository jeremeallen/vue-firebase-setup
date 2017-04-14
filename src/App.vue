<template>
  <div class="App">
    <div class="App--header">
      <h2>Welcome to Vue and Firebase</h2>
    </div>
    <pre class="App--data">
      {{ $data }}
    </pre>

    <form class='App--form' @submit.prevent='handleSubmit'>
      <input type='text' v-model="newData" />
      <input type='submit' />
    </form>
  </div>
</template>

<script>

import { database } from './firebase';

export default {
  name: 'app',
  data() {
    return {
      data: null,
      newData: '',
    };
  },
  created() {
    database.ref().on('value', (snapshot) => {
      this.data = snapshot.val();
      this.newData = '';
    });
  },
  methods: {
    handleSubmit() {
      database.ref().child('AMAZING NEW DATA').set(this.newData);
    },
  },
};
</script>

<style>
.App--header {
  background-color: #222;
  height: 150px;
  padding: 20px;
  color: white;
  text-align: center;
}

.App--data {
  margin: auto;
  padding: 1em;
  background-color: #EEE;
  border: 1px solid #CCC;
}

.App-form {
  text-align: center;
  font-size: 1.4em;
}
</style>

