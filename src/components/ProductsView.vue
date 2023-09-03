<template>
  <div class="products-view">
   <img src="@/assets/products.jpg" alt="Products">
   <p>Products</p>
 </div>
</template>

<script>
export default {
 name: 'ProductsView',
};
</script>

<style>
.products-view {
 text-align: center;
 color: white;
}
.products-view img {
 width: 50px;
 height: 50px;
 border-radius: 50%;
}

p {
  font-weight: 600;
}
</style>
