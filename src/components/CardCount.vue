<template>
    <div class="alert alert-info">
      Totale carte trovate: {{ total }}
    </div>
  </template>
  
  <script>
  export default {
    props: {
      total: Number
    }
  };
  </script>
  
  <style scoped>
  .alert {
    margin-top: 20px;
  }
  </style>