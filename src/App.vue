<template>
  <div id="app">
    <h1>{{ nomeProjeto.toUpperCase() }}</h1>        

    <p :title="getMensagem()">Autor: {{ autor }} </p>

    <p>Ano: {{ ano }} </p>

    <p>Data: {{ data.toLocaleString() }}</p>

    <p>Cidade: {{ cidade }}
      <button @click="mudarParaMaiuscula()">Mudar para maiúscula</button>
      <input type="text" v-model="cidade"/>
    </p>

    <div v-show="isAutorOriginal()">
      <p>Informações do projeto:</p>

      <form @submit.prevent="adicionarInfo()">
        <input type="url" required
          v-model="urlParaAdicionar"/>

        <button type="submit">Adicionar</button> 
      </form>
      <ul v-for="(i, idx) in info" :key="i">
        <li>
           <a :href="i" target="_blank">{{i}} - {{idx}}</a>
           <button @click="remover(i)">Remover</button>
        </li>
      </ul>

      <table border=1>
        <tr>
          <th>Id</th>
          <th>Nome</th>
        </tr>
        <tr v-for="obj in info2" :key="obj.id">
          <td>{{obj.id}}</td>
          <td>{{obj.nome}}</td>
        </tr>
      </table>


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
      data: new Date(),
      info: [
        "http://www.vuejs.org", 
        "http://www.microsoft.com", 
        "http://www.google.com"
      ],
      info2: [
        {id: 1, nome:"info1"},
        {id: 2, nome:"info2"},
      ],
      urlParaAdicionar: null,

      cidade: 'Blumenau'
    }
  },
  methods: {
    mudarParaMaiuscula() {
      this.cidade = this.cidade.toUpperCase()
    },
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
    },
    remover(elemento) {
      let idx = this.info.indexOf(elemento)
      if (idx < 0)
        alert('Não existe')
      else {
        this.info.splice(idx, 1)
      }

    },
    adicionarInfo() {
      this.info.forEach((elemento,idx) => {
          console.log("idx:" + idx + " el:" + elemento)
      })

      let retorno = this.info.some(elemento => {
        return elemento.endsWith(".com.br")
      })
      console.log(retorno)

      let novoArray = this.info.filter(elemento => {
          return elemento.endsWith(".com")
      })
      console.log('novo array')
      console.log(novoArray)


    },
    limpaTela() {
      this.urlParaAdicionar = null
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
