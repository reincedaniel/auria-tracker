<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroTask :tempo-em-segundos="tempoEmSegundos" />
        <ButtonForm :icon="'fas fa-play'" :is-disabled="cronometroRodando" :texto="'play'" @handle-click="iniciar" />
        <ButtonForm :icon="'fas fa-stop'" :is-disabled="!cronometroRodando" :texto="'stop'" @handle-click="finalizar" />
    </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import CronometroTask from "./CronometroTask.vue";
import ButtonForm from "./ButtonForm.vue";

export default defineComponent({
    name: "TemporizadorTask",
    emits: ['aoTemporizadorFinalizado', 'aoTemporizadorIniciado'],
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        };
    },
    methods: {
        iniciar() {
            this.cronometroRodando = !this.cronometroRodando
            this.$emit('aoTemporizadorIniciado', this.cronometroRodando)
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos++;
            }, 1000);
        },
        finalizar() {
            clearInterval(this.cronometro);
            this.cronometroRodando = !this.cronometroRodando
            this.$emit('aoTemporizadorIniciado', this.cronometroRodando)

            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos);
            this.tempoEmSegundos = 0

        }
    },
    components: { CronometroTask, ButtonForm }
});
</script>

<style lang="" scoped>

</style>