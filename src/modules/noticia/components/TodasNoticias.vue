<template>
  <main>
    <h1>Noticias Facultad</h1>
    <div class="container-noticias">
      <Noticia v-for="noticia in noticiasPaginadas" :key="noticia.id" :noticia="noticia"></Noticia>
    </div>
    <nav aria-label="Page navigation example">
      <ul class="pagination">
        <li class="page-item" :class="{ 'disabled': currentPage === 1 }">
          <a class="page-link" href="#" @click="previousPage">Previous</a>
        </li>
        <li class="page-item" v-for="page in paginas" :key="page" :class="{ 'active': currentPage === page }">
          <a class="page-link" href="#" @click="goToPage(page)">{{ page }}</a>
        </li>
        <li class="page-item" :class="{ 'disabled': currentPage === paginas }">
          <a class="page-link" href="#" @click="nextPage">Next</a>
        </li>
      </ul>
    </nav>
  </main>
</template>

<script>
import { obtenerTodasNoticiasFachada } from "../helpers/NoticiaCliente.js";
import Noticia from "./Noticia.vue";

export default {
  components: { Noticia },
  mounted() {
    this.obtenerTodasNoticias();
  },
  data() {
    return {
      noticias: [],
      noticiasPorPagina: 10,
      totalNoticias: 0,
      paginas: 0,
      currentPage: 1,
    };
  },
  computed: {
    noticiasPaginadas() {
      const startIndex = (this.currentPage - 1) * this.noticiasPorPagina;
      const endIndex = startIndex + this.noticiasPorPagina;
      return this.noticias.slice(startIndex, endIndex);
    },
  },
  methods: {
    async obtenerTodasNoticias() {
      const data = await obtenerTodasNoticiasFachada();
      this.noticias = data;
      this.totalNoticias = this.noticias.length;
      this.paginas = Math.ceil(this.totalNoticias / this.noticiasPorPagina);
    },
    goToPage(page) {
      if (page >= 1 && page <= this.paginas) {
        this.currentPage = page;
      }
    },
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.paginas) {
        this.currentPage++;
      }
    },
  },
};
</script>

<style scoped>
.container-noticias {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}

/* Media query para ajustar las columnas en tamaños de pantalla más pequeños */
@media screen and (max-width: 768px) {
  .container-noticias {
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  }
}

/* Media query para tamaños de pantalla aún más pequeños */
@media screen and (max-width: 480px) {
  .container-noticias {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>

En este código, hemos utilizado grid-template-columns para crear una cuadrícula de noticias responsiva. En tamaños de pantalla más pequeños, hemos ajustado el número de columnas utilizando media queries. La cuadrícula comenzará con 3 columnas en pantallas grandes, luego cambiará a 2 columnas en pantallas medianas y finalmente a una sola columna en pantallas pequeñas. Esto hará que el diseño sea más adaptable a diferentes tamaños de pantalla.
