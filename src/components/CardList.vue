<template>
    <div class="row">
      <div v-for="card in cards" :key="card.id" class="col-md-3 mb-4">
        <Card :card="card" />
      </div>
    </div>
  </template>
  
  <script>
  import Card from './Card.vue';
  
  export default {
    props: {
      cards: Array
    },
    components: {
      Card
    }
  };
  </script>
  