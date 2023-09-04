<template>
  <div class="card" style="margin: 1rem; padding: 1rem;">
    <p>{{ noticia.id }}</p>
    <p>{{ noticia.fecha }}</p>
    <div v-if="noticia.texto != null" class="card-body">
      <p>{{ noticia.texto }}</p>
    </div>
    <img :src="noticia.imagen" alt="">
    <iframe :src="noticia.video" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
  </div>
</template>

<script>
export default {
  mounted() {
    console.log(this.id);
  },
  props: {
    noticia: {
      name: Object,
      required: true,
    },
  },
  methods: {},
};
</script>

<style scoped>
.card {
  margin: 1rem;
  padding: 1rem;
  max-width: 100%;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

.card img {
  max-width: 100%;
  height: auto;
}

.card iframe {
  width: 100%;
  height: auto;
}
</style>