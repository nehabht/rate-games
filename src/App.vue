<template>
  <div id="app">
    <div class="container w-25 my-4">
      <div class="search">
        <input type="text" class="form-control" />
        <button class="btn btn-dark mt-2" type="submit">Search</button>
      </div>
    </div>
    <div class="container">
      <div class="row">
        <div class="col">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsam
          mollitia quas vel est, voluptate laboriosam perferendis laborum
          excepturi nemo, officiis aperiam minus harum beatae, nulla quae dolor
          non. Numquam, sit!
        </div>
        <div class="col">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsam
          mollitia quas vel est, voluptate laboriosam perferendis laborum
          excepturi nemo, officiis aperiam minus harum beatae, nulla quae dolor
          non. Numquam, sit!
        </div>
        <div class="col">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsam
          mollitia quas vel est, voluptate laboriosam perferendis laborum
          excepturi nemo, officiis aperiam minus harum beatae, nulla quae dolor
          non. Numquam, sit!
        </div>
        <div class="col">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsam
          mollitia quas vel est, voluptate laboriosam perferendis laborum
          excepturi nemo, officiis aperiam minus harum beatae, nulla quae dolor
          non. Numquam, sit!
        </div>
      </div>
    </div>
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
      response: null,
    };
  },
  mounted() {
    console.log(axios);

    axios
      .get(this.link)
      .then((response) => {
        console.log(response);
        this.response = response.data;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style lang="scss">
@use "@/assets/scss/style.scss";
</style>
