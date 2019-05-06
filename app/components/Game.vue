<template>
  <div class="big-header">
    <h1></h1>
    <br />
    <!-- <router-link class="button" to="/game/">Go to Game</router-link> -->
    <div v-for="msg in messages" :key="msg">{{msg}}</div>
    <br>
    <router-link class="button" :to="actionA">{{btnA}}</router-link>
    <br>
    <router-link class="button" :to="actionB">{{btnB}}</router-link>
  </div>
</template>

<script>
import json from '../assets/data.json'

export default {
  computed : {
    id(){
      return this.$route.params.id;
    },
    messages(){
      return json[this.id].messages
    },
    btnA(){
      return json[this.id].btnA
    },
    actionA(){
      return json[this.id].actionA
    },
    btnB(){
      return json[this.id].btnB
    },
    actionB(){
      return json[this.id].actionB
    },
  }
};
</script>