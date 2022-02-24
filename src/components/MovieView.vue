<template>
  <div>
    <div id="searchResult">
      <h2 v-if="title">{{ title }}</h2>
      <h2 v-else>Movie Search</h2>
      <img :src="posterImgSrc" />
      <p>Director: {{ directors }}</p>
      <p>Genre: {{ movieGenres }}</p>
      <p>Released: {{ released }}</p>
    </div>
    <div id="search">
      <h2>Search</h2>
      <label for="searchBox">Search</label>
      <input type="text" id="searchBox" />
      <button @click="searchForMovie" id="searchBtn">Search</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieView",
  components: {},
  data() {
    return {
      movieTitle: "",
      directedBy: "",
      releaseDate: "",
      posterImgUrl: "",
      genre: "",
      xhttp: new XMLHttpRequest(),
    };
  },
  computed: {
    title() {
      return this.movieTitle;
    },
    directors() {
      return this.directedBy;
    },
    released() {
      return this.releaseDate;
    },
    movieGenres() {
      return this.genre;
    },
    posterImgSrc() {
      return this.posterImgUrl;
    },
  },
  methods: {
    searchForMovie(e) {
      e.preventDefault();
      let searchVal = document
        .getElementById("searchBox")
        .value.replace(" ", "+");

      this.xhttp.open(
        "GET",
        "http://www.omdbapi.com/?t=" + searchVal + "&apikey=eee0805f",
        true
      );

      this.xhttp.onload = () => {
        const responseData = JSON.parse(this.xhttp.response);
        this.movieTitle = responseData.Title;
        this.directedBy = responseData.Director;
        this.releaseDate = responseData.Released;
        this.posterImgUrl = responseData.Poster;
        this.genre = responseData.Genre;
      };

      this.xhttp.send();
      document.getElementById("searchBox").value = "";
    },
  },
};
</script>

<style scoped>
#search {
  display: inline-flex;
  border: 3px solid gray;
}
#searchResult {
  display: inline-block;
}
</style>
