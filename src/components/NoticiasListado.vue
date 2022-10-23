<template>
  <nav class="navbar navbar-expand-sm navbar-light bg-light">
    <div class="container">
      <a class="navbar-brand" href="#">Stetic News ({{totalNoticias}})</a>
      <button class="navbar-toggler d-lg-none" type="button" data-bs-toggle="collapse"
        data-bs-target="#collapsibleNavId" aria-controls="collapsibleNavId" aria-expanded="false"
        aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="collapsibleNavId">
        <!-- <form class="d-flex my-2 my-lg-0" action=""> -->
        <input class="form-control me-sm-2" id="search" type="text" placeholder="Search" v-model="search.contenido">
        <button class="" @click="filtrarNoticias()">Buscar</button>
        <!-- </form> -->
      </div>
    </div>
  </nav>

  <div v-for="noticia in noticias" :key="noticia.id">
    <div class="card">
      <div class="card-header">
        <div class="row">
          <div class="col"><mark>{{noticia.categoriaTxt}}</mark></div>
          <div class="col">{{noticia.regionTxt}}</div>
        </div>
      </div>
      <div class="card-body">
        <p class="card-text">{{noticia.contenido}}</p>
      </div>
      <div class="card-footer text-muted">

        <div class="row">
          <div class="col">{{noticia.fecha}}</div>
          <div class="col"></div>
        </div>
      </div>
    </div>
    <br>
  </div>
</template>

<script>
export default {
  data() {
    return {
      noticias: [],
      search: {},
    };
  },
  created: function () {
    this.listarNoticias();
  },
  methods: {
    listarNoticias() {
      const options = {
        method: "GET",
        headers: { Accept: "application/json" },
      };

      fetch("http://localhost:8000/api/noticias/", options)
        .then(response => response.json())
        .then(response => {
          this.noticias = response;
        })

        .catch(err => console.error(err));
    },
    filtrarNoticias() {
      const options = { method: 'GET', headers: { Accept: 'application/json' } };

      fetch('http://127.0.0.1:8000/api/noticias/?contenido=' + this.search.contenido, options)
        .then(response => response.json())
        .then(response => {
          this.noticias = response;
        })
        .catch(err => console.error(err));
    }
  },
  computed: {
    totalNoticias() {
      return this.noticias.length;
    }
  }
};
</script>
