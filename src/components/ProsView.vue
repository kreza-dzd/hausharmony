<template>
   <div class="pros-view">
    <img src="@/assets/pros.jpg" alt="Pros">
    <p>Pros</p>
  </div>
</template>

<script>
export default {
  name: 'ProsView',
};
</script>

<style>
.pros-view {
  text-align: center;
  color: white;
}
.pros-view img {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}

p {
  font-weight: 600;
}
</style>
