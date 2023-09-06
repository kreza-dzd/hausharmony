<template>
  <div class="ideas-view" @click="onIdeaClick">
    <img src="@/assets/ideas.jpg" alt="Ideas">
    <p>Ideas</p>
  </div>
</template>

<script>
export default {
  name: 'IdeasView',
  methods: {
    onIdeaClick() {
      this.$emit('clicked');
    }
  }
};
</script>


<style>
.ideas-view {
  text-align: center;
  color: white;
}
.ideas-view img {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}


</style>
