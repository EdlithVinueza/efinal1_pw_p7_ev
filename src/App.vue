<template>
  <div id="app">
    <div>
      <ComponenteUno @aniadir-candidato="aniadirCandidatos" />
    </div>
    <div v-if="presentarTabla"> <!-- si existen elementos en el arreglo se muestra el componente -->
      <ComponenteDos :candidatos="candidatos" />
    </div>
  </div>
</template>

<script>
import ComponenteUno from './components/ComponenteUno.vue';
import ComponenteDos from './components/ComponenteDos.vue';

export default {
  name: 'App',
  components: {
    ComponenteUno, //componente del formulario
    ComponenteDos //componente de la tabla de los candidatos 
  },
  data() {
    return {
      presentarTabla: false, //para presentar la tabla de elementos si existen elementos
      candidatos: [] //arreglo para almacenar los candidatos
    };
  },
  methods: {
    aniadirCandidatos(candidate) { //metodo para agregar candidatos al arreglo
      this.candidatos.push(candidate);
      this.existenCandidatos();
    },

    existenCandidatos() { //metodo para validar si presentar tabla o no 
      this.presentarTabla = this.candidatos.length > 0 && this.candidatos.some(c => c.nombre && c.nombre.trim() !== "");
    }
  }
};
</script>

<style>

</style>