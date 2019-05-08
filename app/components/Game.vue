<template>
  <div class="big-header" :class="addScene">
    <h1></h1>
    <br />
    <!-- <router-link class="button" to="/game/">Go to Game</router-link> -->
    <!-- <div v-for="elt in messages" :key="elt">{{'ok'}}</div> -->
    <ul class="msg-list"><li class="message" v-for="msg in msgTable" :key="msg">{{msg}}</li></ul>
    <br>
    <br>
    <div class="btn-container">
      <router-link class="button" :to="actionA">{{btnA}}
        <button class="in-button" v-on:click="addChoiceOnTable(btnA)"></button>
      </router-link>
      <router-link class="button" :to="actionB">{{btnB}}
        <button class="in-button" v-on:click="addChoiceOnTable(btnB)"></button>
      </router-link>
    </div>
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
    },
    
  },
  methods : {
    addMsgOnTable(){    
        let stepMsgList = json[this.id].messages
        Object.keys(stepMsgList).forEach(item => {
          if (!this.msgTable.includes(stepMsgList[item])) {
            this.msgTable.push(stepMsgList[item]);
          }
        });
        console.log(this.msgTable);
    },
    addChoiceOnTable(value){
      this.msgTable.push(value);
    },
  }
};
</script>