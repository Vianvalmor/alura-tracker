<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <CronometroTarefa :tempoEmSegundos="tempoEmSegundos" />
    <button class="button" @click="iniciar" :disabled="cronometroRodadndo">
      <span class="icon">
        <i class="fas fa-play"></i>
      </span>
      <span>play</span>
    </button>
    <button class="button" @click="finalizar" :disabled="!cronometroRodadndo">
      <span class="icon">
        <i class="fas fa-stop"></i>
      </span>
      <span>stop</span>
    </button>
</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CronometroTarefa from './CronometroTarefa.vue'

export default defineComponent({
  name: 'TemporizadorTarefa',
  emits: ['aoTemporizadorFinalizado'],
  components: {
    CronometroTarefa
  },
  data () {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodadndo: false
    }
  },
  methods: {
    iniciar () {
      // começar a contagem
      // 1 seg = 1000 ms
      this.cronometroRodadndo = true
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1        
      }, 1000)
    },
    finalizar () {
      this.cronometroRodadndo = false
      clearInterval(this.cronometro)
      this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
      this.tempoEmSegundos = 0
    }
  }
});
</script>