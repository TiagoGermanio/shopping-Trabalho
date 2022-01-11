<template>
<section>
  <div v-if="produto" class="produto">
    <div class="informacoes">
      <h1>{{produto.nome}}</h1>
      <p class="preco">{{produto.preco | numeroPreco}}</p>
      <p  class="descricao">{{produto.descricao}}<br><br></p>
      <p  class="especificacao">{{produto.especificacao}}</p>
      <button @click="comprar" class="btn" v-if="produto.vendido === 'false'">Adicioar ao carrinho</button>
      <button class="btn" v-else>Produto adicionado ao carrinho</button>
    </div>
      <div class="imgProdutos" v-if="url">
        <center><img :src="url" :alt="produto.name"/></center>
      </div>
    <div class="alerta" :class="{ativo : alertaAtivo}">
        <p class="alerta_mensagem">{{mensagemAlerta}}</p>
      </div>
  </div>
  
</section>
</template>
<script>
import { api } from '@/services.js'
export default {
  name: 'Produto',
  props: ['id'],
  data () {
    return {
      produto: null,
      mensagemAlerta: '',
      alertaAtivo: false
    }
  },
  computed:{
    url(){
      return require(`@/api/produtos/${this.id}.png`)
    }
  },
  methods: {
    comprar () {
      this.alerta(`${this.id} adicionado ao carrinho!`)
    },
    alerta (mensagem) {
      this.mensagemAlerta = mensagem
      this.alertaAtivo = true
      setTimeout(() => {
        this.alertaAtivo = false
      }, 1500)
    },
    getProduto () {
      this.produto = null
      api.get(`/produtos/${this.id}`).then((response) => {
        this.produto = response.data
      })
    }
  },
  created () {
    this.getProduto()
  }
}
</script>
<style scoped>
.produto{
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 30px;
  max-width: 900px;
  padding: 60px 20px;
  margin: 0 auto
}
.informacoes{
   box-shadow:0 4px 8px rgba(30, 60, 90, 0.1);
  padding: 10px;
  background: #fff;
  border-radius: 20px;
  transition: all 0.2s;

}
.preco{
  color: #70A8CC;
  font-weight: bold;
  font-size: 1.5rem;
  margin-bottom: 40px;
}
.descricao{
  font-size: 1.2rem;
}
.especificacao{
  font-size: 1.2rem;
}
.btn{
  margin-top: 60px;
  width: 180px;
  height: 35px;
  border-radius: 18px;
  font-weight: bold;

}
.alerta_mensagem {
  background: #FFFFFF;
  display: inline-block;
  padding: 20px 40px;
  border: 2px solid  #70A8CC;
  box-shadow: 0px 3px 4px rgba(0, 0, 0, 0.1), 0px 4px 10px rgba(0, 0, 0, 0.2);
}
.alerta {
  position: absolute;
  top: 20px;
  left: 0px;
  z-index: 10;
  width: 100%;
  text-align: center;
  display: none;
}
.alerta.ativo {
  display: block;
  animation: fadeInDown 0.3s forwards;
}
.informacoes{
  border-radius: 5%;
  box-shadow: 0 4px 8px rgba(30, 60, 90, 0.1);
  grid-gap: 30px;
  padding: 20px 20px;
  margin: 0 auto
}
.imgProdutos{

  max-width: 300px;
  max-height: 200px;
  border-radius: 5%;
  display: grid;
  grid-gap: 30px;
  padding: 20px 20px;
  margin: 0 auto
}
.imgProdutos img:hover{
  cursor:pointer;
  transform: scale(1.6);
  position: relative;
  z-index: 1;
}
</style>