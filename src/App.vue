<template>
  <div id="app" class="container-fluid p-0">
    <!-- Navbar -->
    <nav class="navbar navbar-light bg-warning">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">
          <img src="/src/img/Yu-Gi-Oh!.png" alt="Yu-Gi-Oh" width="30" height="30" class="d-inline-block align-text-top">
          Yu-Gi-Oh Api
        </a>
        <select class="form-select w-auto" v-model="selectedArchetype" @change="fetchCards">
          <option value="Alien">Alien</option>
          <option value="Blue-Eyes">Blue-Eyes</option>
          <option value="Dark Magician">Dark Magician</option>
        </select>
      </div>
    </nav>

    <!-- Loader o Lista delle Carte -->
    <div class="container mt-3">
      <div v-if="loading" class="text-center">
        <Loader />
      </div>
      <div v-else>
        <h5 class="mt-3">Found {{ cards.length }} cards</h5>
        <CardList :cards="cards" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Loader from './components/Loader.vue';
import CardList from './components/CardList.vue';

export default {
  components: {
    Loader,
    CardList
  },
  data() {
    return {
      cards: [],
      loading: true,
      selectedArchetype: 'Alien'
    };
  },
  async created() {
    this.fetchCards();
  },
  methods: {
    async fetchCards() {
      this.loading = true;
      try {
        const response = await axios.get(`https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=${this.selectedArchetype}&num=20&offset=0`);
        this.cards = response.data.data;
      } catch (error) {
        console.error(error);
      } finally {
        this.loading = false;
      }
    }
  }
};
</script>

<style>
body {
  background-color: #f4f4f4;
}
</style>
