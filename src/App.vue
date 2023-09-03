<template>
  <div id="app">
    <header>
      <input type="text" placeholder="Pretraži...">
      <nav class="header-nav">
        <IdeasView name="Ideas">Ideas</IdeasView>
        <ProsView name="Pros">Pros</ProsView>
        <ProductsView name="Products">Products</ProductsView>
        <AdviceView name="Advice">Advice</AdviceView>
      </nav>
    </header>
    <main>
      <div class="trending-section">
        <h2>Trending home office ideas and designs</h2>
    <div class="image-slider" @scroll="onScroll">
      <div v-for="(image, index) in images" :key="index" class="image-wrapper">
        <img :src="image" alt="Design Image">
        <div class="image-index" v-if="currentImageIndex === index">{{ currentImageIndex + 1 }}/{{ images.length }}</div>
      </div>
    </div>
    <div class="pagination-dots">
      <span v-for="(image, index) in images" :key="index" :class="{'active': currentImageIndex === index}"></span>
    </div>
     </div>
    </main>
    <footer>
      <nav class="footer-nav">
        <div>
          <img src="@/assets/logo.png" alt="Home Icon">
          <a href="#home">Home</a>
        </div>
        <div>
          <img src="@/assets/bell.png" alt="Notifications Icon">
          <a href="#notifications">Notifications</a>
        </div>
        <div>
          <img src="@/assets/idea.png" alt="Ideabooks Icon">
          <a href="#ideabooks">Ideabooks</a>
        </div>
        <div>
          <img src="@/assets/profile.png" alt="Profile Icon">
          <a href="#profile">Profile</a>
        </div>
      </nav>
    </footer>
  </div>
</template>

<script>
import IdeasView from './components/IdeasView.vue'
import ProsView from './components/ProsView.vue'
import ProductsView from './components/ProductsView.vue'
import AdviceView from './components/AdviceView.vue'

import office1 from '@/assets/office1.jpg'
import office2 from '@/assets/office2.jpg'
import office3 from '@/assets/office3.jpg'
import office4 from '@/assets/office4.jpg'

export default {
  data() {
    return {
      images: [
        office1,
        office2,
        office3,
        office4
      ],
      currentImageIndex: 0
    }
  },
  methods: {
    onScroll(event) {
      const container = event.target;
      const containerWidth = container.clientWidth;
      this.currentImageIndex = Math.round(container.scrollLeft / containerWidth);
    }
  },
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
  background-color: darkgrey;

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
.header-nav {
  display: flex;
  justify-content: space-around;
  width: 100%;
  margin-top: 1em;
}

.trending-section {
  padding: 0;  
  margin: 0;  
}

.trending-section h2 {
  color: white;
  font-size: 12px;
  font-weight: 900;
}

.image-slider {
  display: flex;
  overflow-x: auto;
  margin: 0; 
  padding: 0; 
}

.image-slider img {
  width: 100vw;
  height: 300px;
  object-fit: cover;
  flex-shrink: 0; /* Prevents the image from shrinking in the flexbox layout */
}

.image-wrapper {
  position: relative;
  display: inline-block;
}

.image-wrapper img {
  width: 100vw;
  height: 300px;
  object-fit: cover;
}

.image-index {
  position: absolute;
  top: 10px;
  right: 20px;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  text-align: right;
}

.pagination-dots {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.pagination-dots span {
  width: 10px;
  height: 10px;
  margin: 0 5px;
  background: #ccc;
  border-radius: 50%;
}

.pagination-dots span.active {
  background: #333;
}


.footer-nav div {
  text-align: center;
}

.footer-nav img {
  display: block;
  margin: 0 auto;
  width: 24px;
  height: 24px;
}


.footer-nav a {
  display: block;
  color: white;
  text-decoration: none;
  padding-top: 0.5em;
}

.footer-nav {
  display: flex;
  justify-content: space-around;
  padding: 1em 0;
}


input[type="text"] {
  width: 100%;
  padding: 1em;
  border-radius: 5px;
  border: 1px solid #ccc;
}
main {
  flex-grow: 1;
}
footer {
  background: #333;
  color: white;
  padding-bottom: 1.5em;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
}

footer a {
  color: white;
  text-decoration: none;
  margin: 0 1em;
}

@media (max-width: 768px) {
  footer a {
    margin: 0 0.5em;
    font-size: 0.8em;
  }
}
</style>
