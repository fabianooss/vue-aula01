<template>
  <div id="app">
    <h1>{{ nomeProjeto.toUpperCase() }}</h1>        

    <p :title="getMensagem()">Autor: {{ autor }} </p>

    <p>Ano: {{ ano }} </p>

    <p>Data: {{ data.toLocaleString() }}</p>

    <div v-show="isAutorOriginal()">
      <p>Informações do projeto:</p>
      <ul>
        <li>bla</li>
      </ul>
    </div>


    <button @click="alterarAutor()">Alterar autor</button>

    <button @click="alterarAutor(true)">Alterar para autor original</button>


  </div>
</template>

<script>

export default {
  // atributos
  data() {
    // JSON - JavaScript object notation
    return {
      nomeProjeto: 'Meu primeiro projeto',
      autor: 'Fabiano Oss',
      ano: 2019,
      data: new Date()
    }
  },
  methods: {
    alterarAutor(voltarParaOriginal = false) {
      if (voltarParaOriginal) {
        this.autor = 'Fabiano Oss'
      }
      else {
        this.autor = "José da Silva"  
      }
      this.data = new Date()
    },
    getMensagem() {
      if (this.autor.startsWith('Fabiano')) {
        return "Este é o verdadeiro autor"
      }
      return "Este autor é fake"
    },
    isAutorOriginal() {
      return this.autor.startsWith('Fabiano')
    }
  }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
  margin-top: 60px;
}
</style>
