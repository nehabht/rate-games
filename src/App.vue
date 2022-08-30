<template>
  <div id="app">
    <header>
      <div class="selectedGames">
        <h5>{{ favorites.length }} saved games</h5>
      </div>
    </header>
    <main>
      <div class="container w-25 my-4">
        <form class="search">
          <input
            type="text"
            class="form-control"
            v-model="searchQuery"
            v-on:change="inputResults"
          />
          <button class="btn btn-dark mt-2" type="submit">Search</button>
        </form>
      </div>
      <section v-if="!loading">
        <div class="container">
          <div class="row">
            <div class="col-3" v-for="game in searchedGames" :key="game.id">
              <img :src="game.thumbnail" alt="game.title" />
              <h3>{{ game.title }}</h3>
              <button class="btn btn-primary" @click="addToFavorites(game)">
                add to favorites
              </button>
            </div>
          </div>
        </div>
      </section>
      <div class="d-flex align-items-center justify-content-center" v-else>
        <h1>loading...</h1>
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  data() {
    return {
      link: "https://www.freetogame.com/api/games?platform=pc",
      searchQuery: "",
      games: null,
      searchedGames: [],
      loading: true,
      favorites: [],
      favesLocalStorage: JSON.parse(
        localStorage.getItem("storedGames") || "[]"
      ),
    };
  },
  created: function () {
    axios
      .get(this.link)
      .then((response) => {
        console.log(response);
        this.games = response.data;
        this.searchedGames = this.games;
        this.loading = false;
      })
      .catch((error) => {
        console.log(error);
      });
    this.favorites = this.favesLocalStorage;
  },
  methods: {
    inputResults: function () {
      console.log(this.searchQuery);
      this.searchedGames = [];
      this.games.forEach((game) => {
        if (game.title.toLowerCase().includes(this.searchQuery.toLowerCase())) {
          console.log(game.title);
          this.searchedGames.push(game);
          return game;
        }
      });
      return this.games;
    },
    addToFavorites(product) {
      this.favorites.push(product);
      console.log(this.favorites);
      localStorage.setItem("storedGames", JSON.stringify(this.favorites));
    },
  },
};
</script>

<style lang="scss">
@use "@/assets/scss/style.scss";
</style>
