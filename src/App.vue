<template>
  <div id="app">
    <TheHeader />
    <main id="main">
      <router-view />
    </main>
    <TheFooter />
  </div>
</template>
<script>
import TheHeader from "@/components/TheHeader.vue";
import TheFooter from "@/components/TheFooter.vue";

export default {
  components: {
    TheHeader,
    TheFooter,
  },
};
</script>
<style>
* {
  box-sizing: border-box;
}
body,
ul,
li,
h1,
h2,
p {
  padding: 0px;
  margin: 0px;
}
ul {
  list-style: nome;
}
body {
  font-family: Arial, Helvetica, arial, sans-serif;
  color: #345;
  background: url("./assets/agora.svg") repeat top;
}
a {
  color: #345;
  text-decoration: nome;
}
img {
  width: 160%;
  display: block;
}
.carrinho {
  display: block;
  padding: 20px 25px;
  transition: all 0.3;
  border: nome;
  border-radius: 100px;
  cursor: pointer;
}
.carrinho:hover {
  box-shadow: 0 4px 8px rgba(30, 60, 90, 0.2);
}
#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
#main {
  flex: 1;
}
</style>
