<template>
  
  <div class="container ">

    <div class="h-full">
      <ol class="list-decimal">
        <li  v-for="fruit in pages" :key="fruit.id">
          {{ fruit.name }}
          <ul class="list-disc mx-5">
            <li>{{fruit.id}}$</li>
            <li>{{fruit.color}}$</li>
            <li>{{fruit.count}}</li>
          </ul> 
        </li>
      </ol>
    </div>
  
    <div class="">
      <button 
        type="button" 
        class="border-2 rounded-lg">
        Previous
      </button>
      
      <button
        type="button" 
        class="border-2 rounded-lg"
        v-for="pageNumber in totalPages()"
        @click="getPage(pageNumber)"
        :key="pageNumber">
        {{ pageNumber }}
      </button>
  
      <button 
        type="button" 
        class="border-2 rounded-lg">
        Next
      </button>
    </div>
  
  </div>
  
  </template>
  <script>

    import axios from 'axios'
  
    export default {
      data () {
        return {
          list: fruits,
          page: 1,
          pageSize: 5,
          pages: [],
        };
      },
      created() {
         this.getTrees();
      }, 
      methods: {
        async getTrees() {
          await axios.get('https://www.fruitmap.org/api/trees').then((res) => {
            this.list = res.data;
          })
          .catch(e => console.log(e));
        },
        totalPages() {
          return Math.ceil(this.fruits.length / this.pageSize); // 
        },
        getPage(pageNumber) {
          let pageSize = this.pageSize;
          let start = (pageNumber * pageSize) - pageSize; // (1 * 5) - 5 -> 0
          let end = (pageNumber * pageSize); // (1 * 5) -> 5
          return fruits.slice(start, end) // show 0 - 5 elements with slice
        },
      },
      
    }

  </script>
  
  