<script>
import LivrosApi from "@/api/livros.js";
const livrosApi = new LivrosApi();
export default {
  data() {
    return {
      livro: {},
      livros: [],
    };
  },
  async created() {
    this.livros = await livrosApi.buscarTodosOsLivros();
  },
  methods: {
    async salvar() {
      if (this.livros.id) {
        await livrosApi.atualizarLivro(this.livro);
      } else {
        await livrosApi.adicionarLivro(this.livro);
      }
      this.livros = await livrosApi.buscarTodosOsLivros();
      this.livro = {};
    },
    async excluir(livro) {
      await livrosApi.excluirLivro(livro.id);
      this.livros = await livrosApi.buscarTodosOsLivros();
    },
    editar(livro) {
      Object.assign(this.livro, livro);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Gerenciamento de Livros</h2>
    </div>
     <div class="form-input">
      <input
        type="text"
        v-model="livro.nome"
        @keyup.enter="salvar"
        placeholder="título..."
      />
      <input
        type="text"
        v-model="livro.isbn"
        @keyup.enter="salvar"
        placeholder="isbn..."
      />
      <input
        type="number"
        v-model="livro.qntd"
        @keyup.enter="salvar"
        placeholder="quantidade..."
      />
      <input
        type="text"
        v-model="livro.preco"
        @keyup.enter="salvar"
        placeholder="preço..."
      />
      <button @click="salvar">Adicionar</button>
    </div>
    <div class="list-livros">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Título</th>
            <th>ISBN</th>
            <th>Quantidade</th>
            <th>Preço</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="livros in livros" :key="livros.id">
            <td>{{ livros.id }}</td>
            <td>{{ livros.nome }}</td>
            <td>{{ livros.isbn }}</td>
            <td>{{ livros.qntd }}</td>
            <th>{{ livros.preco }}</th>
            <td>
              <button class="delete" @click="excluir(livros)">Excluir</button>
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
