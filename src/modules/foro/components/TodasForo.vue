<template>
  <div>
    <h1>Bienvenido al foro de la Universidad Central del Ecuador</h1>
  </div>
  <div class="row">
    <ul class="nav flex-column col-lg-2">

      <li class="nav-item" v-for="(foro) in foros" :key="foro">
        <div class="row">
          <div class="col">

            <a class="nav-link" @click="cambiarForo(foro.id)">{{ foro.tema }}</a>
          </div>
          <div class="col col-lg-1">
            <span class="badge bg-secondary" v-if="foro.comentarios!=null">{{foro.comentarios.length }}</span>
          </div>

        </div>

      </li>
    </ul>
    <div class="container-foros col">
      <Foro :foro="foro"></Foro>

    </div>
  </div>
</template>
  
<script>
import { obtenerTodasForoFachada } from "../helpers/ForoCliente.js";
import { obtenerForoFachada } from "../helpers/ForoCliente.js";

import Foro from "./Foro.vue";
export default {
  components: { Foro },
  mounted() {
    this.obtenerTodo();
    this.cambiarForo(1);
  },
  data() {
    return {
      foros: null,
      foro:this.cambiarForo(1)
    };
  },
  methods: {
    async obtenerTodo() {
      const data = await obtenerTodasForoFachada();
      this.foros = data;
    },
    async cambiarForo(id) {
      console.log(id)
      const data = await obtenerForoFachada(id);
      this.foro=data
    }
  },
};
</script>
  
<style scoped>
/* Estilos para centrar verticalmente el contenido */
.row {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

/* Establecer un ancho máximo para evitar que los elementos se vuelvan demasiado grandes en pantallas pequeñas */
.container-foros {
  display: grid;
  max-width: 100%;
  gap: 20px;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

/* Añadir espacio entre los elementos de navegación */
.nav-link {
  margin-bottom: 5px;
}

/* Cambiar color al pasar el mouse por encima del enlace */
a:hover {
  color: red;
}

/* Estilos para el badge de comentarios */
.badge {
  font-size: 14px;
}

/* Media query para dispositivos pequeños (móviles) */
@media screen and (max-width: 576px) {
  .container-foros {
    grid-template-columns: 1fr; /* Mostrar elementos uno debajo del otro en dispositivos pequeños */
  }

  .nav-link {
    text-align: center; /* Centrar el texto en dispositivos pequeños */
  }
}
</style>