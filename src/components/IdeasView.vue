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
.idea-options {
  display: grid;
  grid-template-columns: 1fr 1fr; /* 2 ideas per row */
  gap: 16px;
}

.idea-option img {
  width: 80px;
  height: 80px;
  border-radius: 50%;
}
</style>
