<template>
  <div class="big-header" :class="addScene">
    <h1></h1>
    <br />
    <!-- <router-link class="button" to="/game/">Go to Game</router-link> -->
    <!-- <div v-for="elt in messages" :key="elt">{{'ok'}}</div> -->
    <ul class="msg-list"><li v-for="msg in msgTable" :key="msg">{{msg}}</li></ul>
    <br>
    <router-link class="button" :to="actionA">{{btnA}}</router-link>
    <br>
    <!-- <router-link class="button" @click="addStepOnTable">{{btnB}}</router-link> -->
    <router-link class="button" :to="actionB" >{{btnB}}</router-link>
  </div>
</template>

<script>
import json from '../assets/data.json'

export default {
  data(){
    return {
      msgTable : []
    }
  },
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
      this.addMsgOnTable();
      return json[this.id].actionA
    },
    btnB(){
      return json[this.id].btnB
    },
    actionB(){
      return json[this.id].actionB
    },
    addScene(){
      return json[this.id].scene
    }
  },
  methods : {
    addMsgOnTable(){    
        let stepMsgList = json[this.id].messages
        Object.keys(stepMsgList).forEach(item => {
          this.msgTable.push(stepMsgList[item]);
        });
        console.log(this.msgTable);
    }
  }
};
</script>