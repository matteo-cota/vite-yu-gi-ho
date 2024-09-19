<template>
  <div id="app" class="container-fluid p-0">
    <!-- Navbar -->
    <nav class="navbar navbar-light bg-warning">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">
          <img src="logo.png" alt="Yu-Gi-Oh" width="30" height="30" class="d-inline-block align-text-top">
          Yu-Gi-Oh Api
        </a>
        <!-- Dropdown per selezionare l'archetipo -->
        <select class="form-select w-auto" v-model="selectedArchetype" @change="fetchCards">
          <option value="" disabled>Seleziona un archetipo</option>
          <option v-for="archetype in archetypes" :key="archetype" :value="archetype">{{ archetype }}</option>
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
      archetypes: [],
      loading: true,
      selectedArchetype: '',
    };
  },
  async created() {
    await this.fetchArchetypes();
    this.fetchCards();
  },
  methods: {
    async fetchArchetypes() {
      try {
        const response = await axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php');
        this.archetypes = response.data.map(archetype => archetype.archetype_name);
      } catch (error) {
        console.error("Errore nel caricamento degli archetipi:", error);
      }
    },
    async fetchCards() {
      if (!this.selectedArchetype) return;
      this.loading = true;
      try {
        const response = await axios.get(`https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=${this.selectedArchetype}&num=20&offset=0`);
        this.cards = response.data.data;
      } catch (error) {
        console.error("Errore nel caricamento delle carte:", error);
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
