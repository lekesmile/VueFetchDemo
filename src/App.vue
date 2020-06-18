<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to fetch App"/>
    <div class="superDiv">
     
    <div  v-for="item in info" v-bind:key="item.id">
             <p>{{item.some}}</p>
             <p> {{item.name}}</p>
             <p> {{item.street}}</p>
             <p v-if="error">{{error.message}} </p>
    </div>
  <h4>Foods (Double click to delete)</h4>
    <CardsTemp 
       class="card"
       v-for="food in food" 
       v-bind:key="food.id" 
       v-on:dblclick.native="deleteDiv"
       :nameTitle= "food.food"
       :gid= "food.id"
       :imageTemp= "food.image"
      
     />
     
    </div>
    <input  
      type="text"
      v-model="addFoodInput"
     >
    <button v-on:click="addToDiv">Add a food</button>

    <Form />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Form from './components/Form'
import axios from 'axios'
import { v4 as uuidv4 } from 'uuid';
import CardsTemp from './components/CardsTemp'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Form,
    CardsTemp
  },
  data(){
    return{
      info:[],
      error:'',
      inputText: '',
      addFoodInput:'',
       food:[ 
         {id: uuidv4(), food: "yams", image: 'https://images.unsplash.com/photo-1521834029104-b056ecebbb05?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1269&q=80'},
         {id:uuidv4(), food: "rice", image: 'https://images.unsplash.com/photo-1502447533750-9860c1269ae3?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=634&q=80'},
         {id: uuidv4(), food: "potatoes", image: 'https://images.unsplash.com/photo-1572716680685-c71db7198f09?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=634&q=80'},],
    }
  },
  async mounted () {
  
   await axios.get('https://api.openbrewerydb.org/breweries/5494')
   .then(response => {
        this.info = response
        console.log(this.info)
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
   },
 methods: {
   deleteDiv :function(){
     this.food.pop()
   },
    addToDiv:function(){
       const inputMsg ={
        id: uuidv4(),
        food: this.addFoodInput,
        image: 'https://images.unsplash.com/photo-1586777730558-9a08ac2bfec2?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=675&q=80'
      }
     this.food.push(inputMsg)
     this.addFoodInput= ''
     
   }
 },
 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.superDiv{
  width: 50%;
  align-content: center;
  padding: 50px ;
  margin: 5px auto;
  background-color: rgb(160, 180, 150);
  color: darkred;

}

.card{
  text-align: center;
  align-items: center;
  justify-content: center;
  margin: 10px auto;
}

input[type=text]{
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
}

button{
  padding: 12px 20px;
  margin: 0 5px;
}
</style>
