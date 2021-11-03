<template>
  <div>
    <nav class="navbar is-dark">
      <div class="navbar-brand">

          <img
            src="https://www.themoviedb.org/assets/2/v4/logos/v2/blue_long_2-9665a76b1ae401a510ec1e0ca40ddcb3b0cfe45f1d51b77a308fea0845885648.svg"
            width="300"
            @click="home"
          />

      </div>
    </nav>
    <div class="control">
      <input
        class="input"
        type="text"
        placeholder="Buscar..."
        style="width: 50%; padding: 20px"
        v-model="nome"
        @keyup.enter="buscar"
      />
      <button @click="buscar" class="button is-primary">Buscar</button>
    </div>

    <div
      class="columns is-centered is-multiline"
      style="display: inline-flex; flex-wrap: wrap"
    >
      <div class="container" v-for="(movie, index) in movies" :key="index">
        <movieCard
          class="column card is-full-mobile is-12-desktop"
          :name="movie.title"
          :release="movie.release_date"
          :overview="movie.overview"
          :url="movie.poster_path"
          :burl="movie.backdrop_path"
          :pop="movie.vote_average"
        />
      </div>
    </div>
    <nav class="pagination" role="navigation" aria-label="pagination">
      <a @click="previous" class="pagination-previous">Previous</a>
      <a @click="next" class="pagination-next">Next</a>
    </nav>

    <footer class="footer">
      <div class="content has-text-centered">
        <p>
          <strong>TMBD Project</strong> by
          <a
            href="https://br.linkedin.com/in/andr%C3%A9-souza-264031152"
            target="_blank"
            >André Souza</a
          >
          <a href="https://bulma.io" style="margin: 20px">
            <img
              src="https://bulma.io/images/made-with-bulma.png"
              alt="Made with Bulma"
              width="128"
              height="24"
            />
          </a>
        </p>
      </div>
    </footer>
  </div>
</template>

<script>
import movieCard from "./components/movieCard.vue";
import axios from "axios";

export default {
  name: "App",
  created: function () {
    axios
      .get(
        `https://api.themoviedb.org/3/movie/now_playing?api_key=1bb45b326c46ff35f358c8545e66ed7d&language=pt-BR&page=${this.page}`
      )
      .then((response) => {
        this.movies = response.data.results;
        console.log(this.movies);
      });
  },
  data() {
    return {
      movies: [],
      page: 1,
      nome: "",
    };
  },
  components: {
    movieCard,
  },
  methods: {
    previous() {
      if (this.page > 1) {
        this.page = this.page - 1;
        axios
          .get(
            `https://api.themoviedb.org/3/movie/now_playing?api_key=1bb45b326c46ff35f358c8545e66ed7d&language=pt-BR&page=${this.page}`
          )
          .then((response) => {
            this.movies = response.data.results;
            console.log(this.movies);
          });
      }
    },
    next() {
      this.page = this.page + 1;
      axios
        .get(
          `https://api.themoviedb.org/3/movie/now_playing?api_key=1bb45b326c46ff35f358c8545e66ed7d&language=pt-BR&page=${this.page}`
        )
        .then((response) => {
          this.movies = response.data.results;
          console.log(this.movies);
        });
    },
    buscar() {
      axios;
      if (this.nome != "" && this.nome != " ") {
        let nome = this.nome;

        axios
          .get(
            `https://api.themoviedb.org/3/search/movie?api_key=1bb45b326c46ff35f358c8545e66ed7d&language=pt-BR&query=${nome}`
          )
          .then((response) => {
            this.movies = response.data.results;
            console.log(this.movies);
          });
      } else {
        axios
          .get(
            `https://api.themoviedb.org/3/movie/now_playing?api_key=1bb45b326c46ff35f358c8545e66ed7d&language=pt-BR&page=${this.page}`
          )
          .then((response) => {
            this.movies = response.data.results;
            console.log(this.movies);
          });
      }
    },
    home() {
      axios
        .get(
          `https://api.themoviedb.org/3/movie/now_playing?api_key=1bb45b326c46ff35f358c8545e66ed7d&language=pt-BR&page=${this.page}`
        )
        .then((response) => {
          this.movies = response.data.results;
          console.log(this.movies);
        });
    },
  },
};
</script>

<style>
.navbar {
  height: 140px;
  display: flex;
  justify-content: space-evenly;
  text-align: center;
}

.control {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin: 20px;
}

.is-12-desktop {
  height: 100%;
}
</style>
