<template>
  <div class="align-items-center">
    <h1 class="label-title">Cálculo do IMC</h1>
    <h2 class="label-subtitle">Digite seu peso e altura para calcular o IMC</h2>

    <div class="div-imc">
      <span class="p-float-label">
        <InputText id="input-weight" type="text" v-model="weight" :disabled="imc"/>
        <label for="input-weight">Peso</label>
      </span>
    </div>

    <div class="div-imc">
      <span class="p-float-label">
        <InputText id="input-height" type="text" v-model="height" :disabled="imc"/>
        <label for="input-height">Altura</label>
      </span>
    </div>

    <div class="div-imc" v-if="!imc">
      <Button style="margin-right: 10px" label="Limpar" @click="clear"/>
      <Button label="Calcular" @click="calculate"/>
    </div>

    <div class="align-items-center" v-if="imc">
      <p class="label-result">Seu IMC é: {{imc}}</p>
      <p style="font-size: 1.3rem">A classificação do seu IMC é: {{classification}}</p>
      <Button @click="clear" label="Calcular Novamente"/>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      weight: null,
      height: null,
      imc: null,
      classification: ""
    }
  },
  methods: {
    calculate() {
      this.imc = (this.weight / (this.height * this.height)).toFixed(2)
      
      if(this.imc < 18.5) {
        this.classification = "Magreza"
      } else if (this.imc >= 18.5 && this.imc < 25) {
        this.classification = "Normal"
      } else if (this.imc >= 25 && this.imc < 30) {
        this.classification = "Sobrepeso"
      } else if (this.imc >= 30 && this.imc < 40) {
        this.classification = "Obesidade"
      } else {
        this.classification = "Obesidade Grave"
      }

    },

    clear() {
      this.weight = null
      this.height = null
      this.imc = null
      this.classification = ""
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.align-items-center {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.div-imc {
  margin-top: 2rem;
  width: 200px;
  display: flex;
  justify-content: space-between;
}

.label-title {
  font-size: 2rem;
}

.label-subtitle {
  font-size: 1.1rem;
}

.label-result {
  font-size: 2rem;
}

</style>
