<template>
  <div id="app">
    <header>
      <div class="input-wrapper">
      <div v-if="showIdeasOptions" @click="showIdeasOptions = false" class="back-button">←</div>
      <input type="text" placeholder="Pretraži..." :class="{'expanded': showIdeasOptions}">

    </div>
      <nav class="header-nav" v-if="!showIdeasOptions">
        <IdeasView @clicked="showIdeasOptions = true"/>
        <ProsView name="Pros">Pros</ProsView>
        <ProductsView name="Products">Products</ProductsView>
        <AdviceView name="Advice">Advice</AdviceView>
      </nav>
    </header>
    <main v-if="!showIdeasOptions">
      <div class="trending-section">
        <h2>Trending home office ideas and designs</h2>
    <div class="image-slider" @scroll="onScroll">
      <div v-for="(image, index) in images" :key="index" class="image-wrapper">
    <img :src="image.url" alt="Design Image">
    <div class="image-attribution">
        Photo by <a :href="image.profile" target="_blank">{{ image.photographer }}</a> on <a href="https://unsplash.com" target="_blank">Unsplash</a>
    </div>
    <div class="image-index" v-if="currentImageIndex === index">{{ currentImageIndex + 1 }}/{{ images.length }}</div>
</div>
    </div>
    <div class="pagination-dots">
      <span v-for="(image, index) in images" :key="index" :class="{'active': currentImageIndex === index}"></span>
    </div>
     </div>

     <div class="kitchen-section">
  <h2>Trending kitchen ideas and designs</h2>
  <div class="image-slider" @scroll="onKitchenScroll">
    <div v-for="(kitchenImage, index) in kitchenImages" :key="index" class="image-wrapper">
    <img :src="kitchenImage.url" alt="Kitchen Design Image">
    <div class="image-attribution">
        Photo by <a :href="kitchenImage.profile" target="_blank">{{ kitchenImage.photographer }}</a> on <a href="https://unsplash.com" target="_blank">Unsplash</a>
    </div>
    <div class="image-index" v-if="currentKitchenImageIndex === index">{{ currentKitchenImageIndex + 1 }}/{{ kitchenImages.length }}</div>
</div>
  </div>
  <div class="pagination-dots">
    <span v-for="(kitchenImage, index) in kitchenImages" :key="index" :class="{'active': currentKitchenImageIndex === index}"></span>
  </div>
</div>


    </main>
    <div v-if="showIdeasOptions" class="ideas-options">
      <div v-for="(idea, index) in ideaOptions" :key="index" class="idea-option">
        <img :src="idea.image" :alt="idea.name">
        <p>{{ idea.name }}</p>
      </div>
    </div>
    <footer>
      <nav class="footer-nav">
        <div>
          <img src="@/assets/logo.png" alt="Home Icon" @click="showHomepage">
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



export default {
  data() {
    return {
    images: [],
    kitchenImages: [],
    currentImageIndex: 0,
    currentKitchenImageIndex: 0,
    showIdeasOptions: false,
    categories: ["kitchen", "living room", "bedroom", "home office"],
    ideaOptions: [
  { image: './assets/bell.png', name: 'Title 1' },
  { image: '@/assets/bell.png', name: 'Title 2' },
  { image: '@/assets/bell.png', name: 'Title 3' },
  { image: '@/assets/bell.png', name: 'Title 4' }
]

  };
},
  methods: {
    fetchTrendingImages() {
    const promises = this.categories.map(category => this.fetchImageForCategory(category));
    
    Promise.all(promises)
      .then(images => {
        this.ideaOptions = images;
      })
  },

  fetchImageForCategory(category) {
    const ACCESS_KEY = 'pWxdlp-fbNBN_ZiSGOcHjy6G4ds0f7uwHFK-8lJVHss'; 
    const apiUrl = `https://api.unsplash.com/search/photos?query=${category}&client_id=${ACCESS_KEY}&per_page=1`;
    
    return fetch(apiUrl)
      .then(response => response.json())
      .then(data => {
        if (data.results[0]) {
          return {
            image: data.results[0].urls.regular,
            name: `Title ${this.categories.indexOf(category) + 1}`
          };
        } else {
          return {
            image: '', // Fallback image or blank
            name: `Title ${this.categories.indexOf(category) + 1}`
          };
        }
      });
  },
    fetchImages(query, count = 4) {
    const ACCESS_KEY = 'pWxdlp-fbNBN_ZiSGOcHjy6G4ds0f7uwHFK-8lJVHss'; 
    const apiUrl = `https://api.unsplash.com/search/photos?query=${query}&client_id=${ACCESS_KEY}&per_page=${count}`;

    fetch(apiUrl)
      .then(response => response.json())
      .then(data => {
        const transformedData = data.results.map(photo => ({
          url: photo.urls.regular,
          photographer: photo.user.name,
          profile: photo.user.links.html
        }));

        if (query === "home office") {
          this.images = transformedData;
        } else if (query === "kitchen") {
          this.kitchenImages = transformedData;
        }
      });
},
    showHomepage() {
    this.showIdeasOptions = false;
  },
    onScroll(event) {
      const container = event.target;
      const containerWidth = container.clientWidth;
      this.currentImageIndex = Math.round(container.scrollLeft / containerWidth);
    },
    onKitchenScroll(event) {
    const container = event.target;
    const containerWidth = container.clientWidth;
    this.currentKitchenImageIndex = Math.round(container.scrollLeft / containerWidth);
  }
  },
  mounted() {
  this.fetchImages("home office");
  this.fetchImages("kitchen");
  this.fetchTrendingImages();
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

.input-wrapper {
  display: flex;
  align-items: center;
  width: 100%;
  position: relative;
}

.back-button {
  position: absolute;
  left: 0;
  font-size: 24px;
  cursor: pointer;
  color: white;
  z-index: 10;
  padding-right: 0.5em;
}

input[type="text"].expanded {
  flex-grow: 1;
  margin-left: 3em;
}

input[type="text"] {

  width: 100%;
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

.kitchen-section h2 {
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

.image-attribution {
    font-size: 10px;
    color: white;
    background: rgba(0, 0, 0, 0.6);
    padding: 5px;
    position: absolute;
    bottom: 10px;
    left: 10px;
    border-radius: 3px;
    z-index: 10;
}

.image-attribution a {
    color: white;
    text-decoration: underline;
    font-weight: bold;
}

.image-attribution a:hover {
    color: #ccc;
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

.ideas-options {
  display: grid;
  grid-template-columns: 1fr 1fr; /* 2 ideas per row */
  gap: 1em;  /* Adjusted to 1em */
  width: 100%;
  box-sizing: border-box;
}


.ideas-options {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1em;
  width: 100%;
  box-sizing: border-box;
}


.idea-option img {
  width: 100%;
  height: auto;
  border-radius: 0%; /* Making it square */
  object-fit: cover;  /* Resize the image properly */
}

.idea-option p {
 text-align: center;
 
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