<template>
  <header>
    <div class="header">
      <span> <RouterLink to="/editoras">Editoras</RouterLink> </span>
      <span> <RouterLink to="/categorias">Categorias</RouterLink> </span>
      <span> <RouterLink to="/autores">Autores</RouterLink> </span>
      <span> <RouterLink to="/livros">Livros</RouterLink> </span>
    </div>
  </header>
</template>

<style>
header span {
  padding: 0 20px;
}

header {
  background-image: linear-gradient(
    90deg,
    #222121 0,
    #49494b 35%,
    #747474 100%
  );
  height: 11%;
  font-size: 1.5rem;
  color: #ffffff;
  display: flex;
  align-items: center;
  font-size: 20px;
  justify-content: center;
}
.views {
  margin: 0 auto;
}
</style>
