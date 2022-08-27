<template>
  <div id="app">
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
            <div
              class="col-3"
              v-for="game in searchedGames"
              :key="game.id"
              @click="selected(game)"
            >
              <img :src="game.thumbnail" alt="game.title" />
              <h3>{{ game.title }}</h3>
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
      favoriteGames: [],
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
    selected(element) {
      //this.element = element.title;
      console.log(element.title);
      console.log("this is the element i clicked: ", element.title);
      /* bug può inserire lo stesso elemento più volte */
      this.favoriteGames.push(element.title);
      console.log(this.favoriteGames);
    },
  },
};
</script>

<style lang="scss">
@use "@/assets/scss/style.scss";
</style>
