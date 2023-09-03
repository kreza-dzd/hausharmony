<template>
  <div id="app">
    <header>
      <input type="text" placeholder="Pretraži...">
      <nav>
        <IdeasView name="Ideas">Ideas</IdeasView>
        <ProsView name="Pros">Pros</ProsView>
        <ProductsView name="Products">Products</ProductsView>
        <AdviceView name="Advice">Advice</AdviceView>
      </nav>
    </header>
    <main>
      <!-- Ovde možete dodati vaše komponente i sadržaj -->
    </main>
  </div>
</template>

<script>
import IdeasView from './components/IdeasView.vue'
import ProsView from './components/ProsView.vue'
import ProductsView from './components/ProductsView.vue'
import AdviceView from './components/AdviceView.vue'

export default {
  name: 'App',
  components: {
    IdeasView,
    ProsView,
    ProductsView,
    AdviceView
  }
};
</script>

<style>
body {
  background-color: darkgreen;

}
#app {
  font-family: Arial, sans-serif;
}
header {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1em;
  border-bottom: 1px solid #ccc;
}
nav {
  display: flex;
  justify-content: space-around;
  width: 100%;
  margin-top: 1em;
}
input[type="text"] {
  width: 100%;
  padding: 1em;
  border-radius: 5px;
  border: 1px solid #ccc;
}
</style>
