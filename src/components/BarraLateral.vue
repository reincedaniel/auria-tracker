<template>
  <header>
    <h1 style="margin-top: 15em;"><img src="../assets/logo-bai.svg" alt="" style="width: 48%;" /></h1>
    <button style="margin-top: 1.1em;" class="button" @click="alterarTema()">
      <i class="fa-solid fa-repeat"></i> {{textoBotao}}
    </button>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "BarraLateral",
  emits:['aoTemaAlterado'],
  data(){
    return{
      isModoEscuroActivo: false
    }
  },
  computed:{
    textoBotao(): string{
      if(this.isModoEscuroActivo)
      return 'Desactivar modo Escuro'
      return 'Activar modo Escuro'
    }
  },
  methods:{
    alterarTema(){
      this.isModoEscuroActivo = !this.isModoEscuroActivo
      this.$emit('aoTemaAlterado', this.isModoEscuroActivo);
    }
  }
});
</script>

<style scoped>
.button{
  border-radius: 25px;
}
.button i{
  margin-right: 1rem;
}
header {
  
  padding: 1rem;
  background: #002d74;
  width: 100%;
  height: 100vh;
  text-align: center;
}

@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>
