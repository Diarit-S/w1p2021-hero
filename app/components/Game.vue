<template>
  <div class="big-header" :class="addScene">
    <h1></h1>
    <br />
    <ul ref="msgList" class="msg-list">
      <li class="message" :class="{'user-choice': isUserChoice(msg) }" v-for="msg in msgTable" :key="msg">{{msg}}</li>
    </ul>
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
      msgTable : [],
      test : true,
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
      this.doScroll();
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
    addMsgOnTable(){ // Add each messages of the new step, based on the id in data.json file      
        let stepMsgList = json[this.id].messages
        Object.keys(stepMsgList).forEach(item => {
          if (!this.msgTable.includes(stepMsgList[item])) { // if the message still does not exist 
            this.msgTable.push(stepMsgList[item]);
          }
        });
        console.log(this.msgTable);
    },
    addChoiceOnTable(value){ // Add the chosen button value on the ul message list, called on btn click and receive the btn value on parameter
      this.msgTable.push(value);
    },
    doScroll(){ // Function called on each uptade, to let the ul list always scrolled to bottom
      setTimeout(() => {
        let x = document.querySelector('.msg-list');
        x.scrollTop = x.scrollHeight;
      }, 200);
    },
    isUserChoice(text){ // This function is used to see if the message pushed on the list is a button value
      let msg = text;
      let regex = /^ /;  // regex to see if the parameter start width a space character (all button values start widh a space) 
      return regex.test(msg);
    }
  }
};
</script>