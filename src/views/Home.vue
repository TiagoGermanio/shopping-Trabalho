<template>
  <section>
    <h1>the better for you</h1>
    <ListaProdutos />
  </section>
</template>

<script>
import ListaProdutos from '@/components/ListaProdutos.vue'

export default {
  name: 'home',
  components: {
  
    ListaProdutos
  }
}
</script>
1
<style scoped>
h1 {
  font-size: 2rem;
  color: #345;
  margin-top: 40px;
  text-align: center;
}
</style>
