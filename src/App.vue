<script setup>
  
  const name = "Vue dinámico";
  const styleColor = "color: blue"
  const array = [
    {
      name: 'Manzána',
      price: '1€',
      stock: '10'
      
    },
    {
      name: 'Plátano',
      price: '0.75€',
      stock: '15'
    },
    {
      name: 'Coco',
      price: '2€',
      stock: '20',
    },
    {
      name: 'Pera',
      price: '0.8€',
      stock: '12',
    },
    {
      name: 'Naranja',
      price: '0.6€',
      stock: '11',
    }

  ];

</script>
<template>
  <h1 :style="styleColor">Hello, {{ name.toUpperCase() }}!</h1>
  <ol>
    <li v-for="fruta in array" 
    :key="fruta.name">
        {{ fruta.name }}
       <ul>
         <li>{{fruta.price}}</li>
         <li>{{fruta.stock}}</li>
        </ul> 
      </li>
  </ol>
</template>