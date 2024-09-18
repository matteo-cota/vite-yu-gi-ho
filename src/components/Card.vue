<template>
    <div class="card text-center">
      <img :src="card.card_images[0].image_url" class="card-img-top" :alt="card.name" />
      <div class="card-body bg-warning">
        <h5 class="card-title text-uppercase">{{ card.name }}</h5>
        <p class="card-text">{{ card.type }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      card: Object
    }
  };
  </script>
  
  <style scoped>
  .card-img-top {
    height: 379px;
    object-fit: cover;
  }
  </style>
  