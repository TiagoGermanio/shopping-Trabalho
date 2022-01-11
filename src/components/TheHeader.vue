<template>
<header>
  <nav>
    <router-link  to="/" class="logo">
      <img id="custom-img" src="@/assets/new.svg" alt="techno" />
    </router-link>
     <router-link  to="/carrinho" class="carrinho">                   
      <img src="@/assets/carrinho.svg" alt="carrinho" />
    </router-link>
  </nav>
</header>
</template>
<script>
export default {
  nome: 'TheHeader'
}
</script>
<style>
#custom-img{
width: 7%;
}
</style>
<style scoped>
nav{
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px 20px;
  box-shadow: 0 2px 4px rgba(30, 60, 90, 0.1);
}
</style>
