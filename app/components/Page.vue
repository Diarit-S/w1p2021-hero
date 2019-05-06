<template>
  <div class="big-header">
    <h1>Page</h1>
    <br />
    <router-link class="button" to="/">Go to Home</router-link>
    <br>
    <router-link class="button" to="/Choix">Go to Choix</router-link>
    <div v-for="elt in myJson" v-bind:key="elt.id">{{elt.message[0] + elt.message[1]}}</div>
  </div>
</template>

<script>
import json from '../assets/data.json';

export default {
  data(){
    return{
      myJson : json
    }
  },
};
</script>
