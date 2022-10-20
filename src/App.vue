<template>
  <ol>
    <li v-for="fruit in fruits" 
      :key="fruit.name">
      {{ fruit.name }}
      <ul>
        <li>{{fruit.id}}$</li>
        <li>{{fruit.color}}$</li>
        <li>{{fruit.count}}</li>
      </ul> 
    </li>
  </ol>
  </template>
  <script>
    import axios from 'axios'
    
  
    export default {
      data () {
        return {
          fruits:null
        }
      },
      mounted() {
         console.log('Hello World!')
         this.getFruits()
      },
      methods: {
        getFruits() {
          console.log('Hello World! x2')
          axios.get('https://www.fruitmap.org/api/trees')
          .then( response => {
              this.fruits = response.data
          })
          .catch( error => console.log(error))
        }
      }
    }
  </script>
  
  