<template>
    <div>
      <h1>Foro</h1>
      <div>
        <form class="row g-3 needs-validation">
  
          <div class="mb-3 col-md-6">
            <label for="temaInput" class="form-label">Tema</label>
            <input type="text" class="form-control" id="temaInput" required v-model="foro.tema">
          </div>
  
          <div class="col-md-6">
            <button class="btn btn-primary" @click="insertarForo">Insertar</button>
          </div>
        </form>
  
        <button class="btn btn-primary" @click="insertarForo">Insertar</button>
  
      </div>
  
      <div class="alert alert-success" role="alert">
        Se insertó el foro correctamente
      </div>
    </div>
  </template>
  
  <script>
  import { ingresarForoFachada } from "../helpers/ForoCliente.js";
  
  export default {
    mounted() {
  
    },
    data() {
      return {
        foro: {
          tema: "",
        },
      };
    },
    methods: {
      async insertarForo() {
        await ingresarForoFachada(this.foro);
      },
    },
  };
  </script>
  
  <style scoped>
  /* Estilos para centrar verticalmente el contenido */
  .row {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  /* Ajustar el ancho del botón al contenido */
  button {
    width: auto;
    padding: 10px 20px;
    margin-top: 10px;
  }
  
  /* Ajustar el ancho de la etiqueta "Tema" */
  label {
    width: 100%;
    text-align: center;
  }
  
  /* Ajustar el ancho del campo de entrada "Tema" */
  #temaInput {
    width: 100%;
  }
  
  /* Media query para ajustar estilos en pantallas más pequeñas */
  @media screen and (max-width: 768px) {
    /* Redefinir estilos según tus necesidades para dispositivos móviles */
    .row {
      flex-direction: column; /* Colocar los elementos uno debajo del otro */
    }
  
    label, #temaInput, button {
      width: 100%; /* Ocupar todo el ancho disponible en dispositivos móviles */
    }
  }
  </style>