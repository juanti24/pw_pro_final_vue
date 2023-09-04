<template>
  <h1>Noticia</h1>
  <div>
    <form class="row g-3 needs-validation">
      <div class="mb-3">
        <label for="fechaInput" class="form-label">Fecha</label>
        <input type="date" class="form-control" id="fechaInput" v-model="noticia.fecha" required>
      </div>
      <div class="mb-3">
        <label for="textoInput" class="form-label">Texto</label>
        <textarea class="form-control" id="exampleFormControlTextarea1" rows="3" required v-model="noticia.texto"></textarea>
      </div>
      <div class="mb-3">
        <label for="imagenInput" class="form-label">Imagen</label>
        <input type="text" class="form-control" id="imagenInput" required v-model="noticia.imagen">
      </div>
      <div class="mb-3">
        <label for="videoInput" class="form-label">Video</label>
        <input type="text" class="form-control" id="videoInput" required v-model="noticia.video">
      </div>
      <button class="btn btn-primary" @click="insertarNoticia">Insertar</button>
    </form>
    <button class="btn btn-primary" @click="insertarNoticia">Insertar</button>
  </div>
  <div v-if="msj" class="alert alert-primary" role="alert">
    {{ mensaje }}
  </div>
</template>

<script>
import { ingresarNoticiaFachada } from "../helpers/NoticiaCliente.js";
export default {
  mounted() {

  },
  data() {
    return {
      noticia: {
        texto: "",
        video: "",
        fecha: "",
        imagen: "",
        msj: false,
        mensaje: ""
      },
    };
  },
  methods: {
    async insertarNoticia() {
      var newDate = new Date(this.noticia.fecha + 'T00:00');
      this.noticia.fecha = newDate;
      console.log(this.noticia);
      await ingresarNoticiaFachada(this.noticia);
      this.msj = true;
      this.mensaje = "Noticia insertada con éxito";
    },
  },
};
</script>

<style scoped>
/* Estilos para centrar verticalmente el contenido */
form {
  margin: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

/* Ajustar el ancho de los elementos de entrada de texto */
.form-control {
  max-width: 100%;
  width: 100%;
  margin-bottom: 10px;
}

/* Ajustar el ancho del botón */
button {
  width: auto;
  padding: 10px 20px;
}

/* Estilos para el mensaje de éxito */
.alert {
  max-width: 100%;
  width: 100%;
  margin-top: 10px;
}
</style>