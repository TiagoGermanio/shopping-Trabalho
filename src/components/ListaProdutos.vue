
<template>
  <section class="produtos-container">
    
    <transition mode="out-in">
      <div v-if="produtos" class="produtos" key="produtos">
        <div class ="produto" v-for="produto in produtos" :key="produto.id">
            <router-link :to="{name:'produto', params: {id: produto.id}}">
            <img v-if="produto.fotos" :src="produto.fotos[0].src" :alt="produto.fotos[0].titulo" >
            <center><h2 class="titulo">{{produto.nome}} </h2></center>
            <center><p class="descricao">{{produto.descricao}} </p></center>
            <br><center><p class="preco">{{produto.preco | numeroPreco}} </p></center>
            </router-link>
        </div>
      </div>
      <PaginaCarregando v-else key="carregando" />
    </transition>
  </section>
</template>
<script>

import { api } from '@/services.js'
import { serialize } from '@/helpers.js'

export default {
  data () {
    return {
      produtos: null
    }
  },
  computed: {
    url () {
      const query = serialize(this.$router.query)
      return `/produtos?_limit=8${query}`
    }
  },
  methods: {
    getProduto () {
      this.produtos = null
      api.get(this.url).then((response) => {
        this.produtos = response.data
      })
    }
  },
  created () {
    this.getProduto()
  },
  watch: {
    url () {
      this.getProduto()
    }
  }
}
</script>
<style scoped>
.produtos-container{
max-width: 2000px;
margin: 0 auto;
}
.produtos {
  display: grid;
  grid-template-columns: repeat(4,1fr);
  grid-gap: 30px;
  margin: 30px;
}
.produto{
  box-shadow:0 4px 8px rgba(30, 60, 90, 0.1);
  padding: 10px;
  background: #fff;
  border-radius: 4px;
  transition: all 0.2s;
}
.produto:hover{
  box-shadow: 0 6px 12px rgba(30, 60, 90, 0.2);
  transform: scale(1.4);
  position: relative;
  z-index: 1;
}
.produto img {
  border-radius: 4px;
  margin-bottom: 10px;
}
.titulo{
  margin-bottom: 8px;
}
.preco{
  color:#a9a9a9;
  font-weight: bold;
}
</style>
