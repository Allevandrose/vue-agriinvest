<template>
  <div id="app">
    <HomePage />
    <CarouselComponent />
    <!-- Change the name here -->
  </div>
</template>

<script>
import HomePage from "./components/HomePage.vue";
import CarouselComponent from "./components/Carousel.vue"; // Import using the new name

export default {
  name: "App",
  components: {
    HomePage,
    CarouselComponent, // Register the CarouselComponent
  },
};
</script>

<style>
/* Add any styles for your app here */
</style>
