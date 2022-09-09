<script>
import AutoresApi from "@/api/autores.js";
const autoresApi = new AutoresApi();
export default {
  data() {
    return {
      autor: {},
      autores: [],
    };
  },
  async created() {
    this.autores = await autoresApi.buscarTodosOsAutores();
  },
  methods: {
    async salvar() {
      if (this.autor.id) {
        await autoresApi.atualizarAutor(this.autor);
      } else {
        await autoresApi.adicionarAutor(this.autor);
      }
      this.autores = await autoresApi.buscarTodosOsAutores();
      this.autor = {};
    },
    async excluir(autor) {
      await autoresApi.excluirAutor(autor.id);
      this.autores = await autoresApi.buscarTodosOsAutores();
    },
    editar(autor) {
      Object.assign(this.autor, autor);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Gerenciamento de Autores</h2>
    </div>
    <div class="form-input">
      <input
        type="text"
        v-model="autor.nome"
        @keyup.enter="salvar"
        placeholder="Autor do livro..."
      />
      <button @click="salvar">Adicionar</button>
    </div>
    <div class="list-autores">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Nome</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="autor in autores" :key="autor.id">
            <td>{{ autor.id }}</td>
            <td>{{ autor.nome }}</td>
            <td>
              <button class="delete" @click="excluir(autor)">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.delete {
  background-color: #f32222;
  color: #fafafa;
  border: #fca311;
  border-radius: 5px;
  width: 50%;
  height: 30px;
  font-weight: bold;
  cursor: pointer;
  margin: 0 0 0 25%;
}
.delete:hover {
  background-color: rgb(216, 32, 32);
}
.title {
  margin-top: 2rem;
  display: flex;
  justify-content: center;
  font-size: 20px;
  font-style: oblique;
}
.form-input {
  margin-top: 20px;
  display: flex;
  justify-content: center;
}

.form-input input {
  width: 10%;
  height: 40px;
  border: 2px solid #ccc;
  border-radius: 5px;
  padding: 1 10px;
  margin: 0 0 0 5px;
}

.form-input button {
  margin-left: 1%;
  width: 5%;
  height: 40px;
  border: 1px solid rgb(15, 124, 50);
  border-radius: 5px;
  background-color: rgb(15, 124, 50);
  color: white;
  font-weight: bold;
  cursor: pointer;
}

.form-input button:hover {
  background-color: rgb(51, 180, 51);
  border: rgb(51, 180, 51);
}

.list-livros {
  display: flex;
  justify-content: center;
}

table {
  width: 80%;
  margin: 2% auto;
  border-collapse: collapse;
}

table tr th {
  border: 1px solid rgb(0, 0, 0);
  padding: 10px;
  font-weight: bold;
}

table tr td {
  border: 1px solid rgb(0, 0, 0);
  padding: 10px;
}

table tr:nth-child(odd) {
  background-color: rgb(211, 211, 211);
}
</style>
