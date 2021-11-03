<template>
  <div class="card" style="margin-bottom: 15px">
    <div class="card-image">
      <figure class="image">
        <img :src="`https://image.tmdb.org/t/p/w342${url}`" />
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-6">{{ name }}</p>
          <p class="subtitle is-6">Lançamento: {{ release }}</p>
          <p>Nota média: {{pop}}</p>
          <progress class="progress is-small is-info" :value="`${pop}`" max="10">{{ pop }}</progress>

          <div class="container">
            <button class="button" @click="showModal">Detalhes</button>
          </div>
          <div class="modal" :class="{ 'is-active': showModalFlag }">
            <div class="modal-background"></div>
            <div class="modal-card">
              <header class="modal-card-head">
                <button class="delete" aria-label="close" @click="cancelModal" style="margin-right: 10px;">
                </button>
                <h1 class="modal-card-title">{{ name }}</h1>
              </header>
              <figure class="image">
                <img :src="`https://image.tmdb.org/t/p/w780${burl}`" />
              </figure>
              <section class="modal-card-body">
                <p>{{ overview }}</p>
              </section>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movie: {},
      showModalFlag: false,
      okPressed: false,
      message: "Press'Ok' or 'Cancel'.",
    };
  },
  props: {
    name: String,
    release: String,
    overview: String,
    url: String,
    burl: String,
    pop: Number,
  },
  methods: {
    showModal() {
      this.okPressed = false;
      this.showModalFlag = true;
    },
    okModal() {
      this.okPressed = true;
      this.showModalFlag = false;
    },
    cancelModal() {
      this.okPressed = false;
      this.showModalFlag = false;
    },
  },
};
</script>

<style>
.card-image {
  display: flex;
  text-align: center;
}
</style>
