<script>
import CategoriasApi from "@/api/categorias.js";
const categoriasApi = new CategoriasApi();
export default {
  data() {
    return {
      categoria: {},
      categorias: [],
    };
  },
  async created() {
    this.categorias = await categoriasApi.buscarTodasAsCategorias();
  },
  methods: {
    async salvar() {
      if (this.categoria.id) {
        await categoriasApi.atualizarCategoria(this.categoria);
      } else {
        await categoriasApi.adicionarCategoria(this.categoria);
      }
      this.categorias = await categoriasApi.buscarTodasAsCategorias();
      this.categoria = {};
    },
    async excluir(categoria) {
      await categoriasApi.excluirCategoria(categoria.id);
      this.categorias = await categoriasApi.buscarTodasAsCategorias();
    },
    editar(categoria) {
      Object.assign(this.categoria, categoria);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Gerenciamento de Categorias</h2>
    </div>
    <div class="form-input">
      <input
        type="text"
        v-model="categoria.nome"
        @keyup.enter="salvar"
        placeholder="Categoria do Livro..."
      />
      <button @click="salvar">Adicionar</button>
    </div>
    <div class="list-categorias">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Descrição</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="categoria in categorias" :key="categoria.id">
            <td>{{ categoria.id }}</td>
            <td>{{ categoria.nome }}</td>
            <td>
              <button class="delete" @click="excluir(categoria)">
                Excluir
              </button>
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
    width: 30%;
    height: 30px;
    font-weight: bold;
    cursor: pointer;
    margin: 0 0 0 35%;
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
    background-color: rgb(211, 211, 211)}
  </style>
  