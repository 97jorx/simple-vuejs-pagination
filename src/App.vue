<template>
  
  <div class="container flex flex-col">

    <div class="h-96">
      <ol class="list-decimal">
        <li  v-for="fruit, index in pages" :key="fruit.id">
          {{ fruit.name }}
          <ul class="list-disc mx-5">
            <li>{{fruit.id}}$</li>
            <li>{{fruit.count}}</li>
          </ul> 
        </li>
      </ol>
    </div>
  
    <div class="block">
      <button 
        type="button" 
        class="border-2 rounded-lg">
        Previous
      </button>
      
      <button
        type="button" 
        class="border-2 rounded-lg"
        v-for="pageNumber in totalPages()"
        v-on:click="paginate(pageNumber)"
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
          fruits: [],
          page: 1,
          eachPages: 5,
          pages: [],
        };
      },
      created() {
         this.getTrees();
      },
      methods: {
        async getTrees() {
          const res = await axios.get('https://www.fruitmap.org/api/trees');
          this.fruits = res.data;
        },
        totalPages() {
          return Math.ceil(this.fruits.length / this.eachPages); // 
        },
        paginate(currentPage) {
          let start = (currentPage * this.eachPages) - this.eachPages; // (1 * 5) - 5 -> 0
          let end = (currentPage * this.eachPages); // (1 * 5) -> 5
          this.pages = this.fruits.slice(start, end) // show 0 - 5 elements with slice
        },
      },
      watch: {
        fruits() {
          this.paginate(1);
        }
      },
    }

  </script>
  
  