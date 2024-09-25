<template>
  <!-- Carousel Section Start -->
  <div class="hero">
    <div class="carousel">
      <div 
        class="carousel-item" 
        v-for="(slide, index) in slides" 
        :key="index" 
        :style="{ backgroundImage: `url(${slide.image})` }"
        :class="{ active: index === currentIndex }"
      >
        <div class="overlay" :class="{ 'float-in': index === currentIndex }"></div>
        <div class="carousel-content" :class="{ 'float-in-text': index === currentIndex }">
          <h2>{{ slide.title }}</h2>
          <p>{{ slide.description }}</p>
          <button class="btn-get-started">Get Started</button>
        </div>
      </div>
      <div class="carousel-control-prev" @click="prevSlide">
        <i class="fa-solid fa-arrow-left"></i>
      </div>
      <div class="carousel-control-next" @click="nextSlide">
        <i class="fa-solid fa-arrow-right"></i>
      </div>
    </div>
  </div>
  <!-- Carousel Section End -->
</template>

<script>
export default {
  name: "CarouselComponent",
  data() {
    return {
      slides: [
        { image: require('@/assets/maize.jpg'), title: 'Welcome to Green', description: 'Lorem ipsum dolor sit amet...' },
        { image: require('@/assets/grape.jpg'), title: 'At vero eos et accusamus', description: 'Nam libero tempore...' },
        { image: require('@/assets/hydroponics.jpg'), title: 'Temporibus autem quibusdam', description: 'Beatae vitae dicta sunt explicabo...' }
      ],
      currentIndex: 0,
      intervalId: null,
    };
  },
  mounted() {
    this.startCarousel();
  },
  beforeUnmount() {
    clearInterval(this.intervalId);
  },
  methods: {
    startCarousel() {
      this.intervalId = setInterval(this.nextSlide, 6000); // Set interval to 6 seconds
    },
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.slides.length;
    },
    prevSlide() {
      this.currentIndex = (this.currentIndex - 1 + this.slides.length) % this.slides.length;
    },
  },
}
</script>

<style scoped>
.hero {
  padding: 0;
}

.carousel {
  width: 100%;
  min-height: 70vh;
  padding: 0;
  margin: 0;
  position: relative;
  overflow: hidden; /* Prevents overflow gaps */
}

.carousel-item {
  position: absolute;
  inset: 0; /* Fills the parent container */
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  opacity: 0;
  transition: opacity 1.5s ease; /* Increased transition duration */
}

.carousel-item.active {
  opacity: 1; /* Fade in active item */
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 128, 0, 0.5); /* Darker green transparent overlay */
  z-index: 2; /* Overlay above the image but below the text */
}

.overlay.float-in {
  animation: floatIn 1.5s forwards; /* Float-in animation duration */
}

.carousel-content {
  position: absolute;
  inset: 90px 64px 64px 64px;
  display: flex;
  flex-direction: column;
  align-items: center;
  z-index: 3;
  color: white; /* Ensures text is visible over the overlay */
  opacity: 0; /* Initially hidden for float-in effect */
  transition: opacity 1.5s ease 1.5s; /* Float-in for text */
}

.float-in-text {
  opacity: 1; /* Show text after the overlay */
  animation: floatInText 1.5s forwards; /* Float-in animation duration for text */
}

.carousel-content h2,
.carousel-content p,
.carousel-content .btn-get-started {
  margin-bottom: 20px; /* Add margin for spacing */
}

.carousel-content h2 {
  font-size: 48px;
  font-weight: 700;
}

.carousel-content p {
  font-size: 18px; /* Adjust font size */
}

.carousel-content .btn-get-started {
  color: white; /* Text color for button */
  background: rgba(0, 255, 0, 0.8); /* Lighter green for visibility */
  font-family: 'Arial', sans-serif; /* Adjust font family */
  font-weight: 500;
  font-size: 15px;
  letter-spacing: 1px;
  display: inline-block;
  padding: 10px 36px; /* Increased padding for better aesthetics */
  border-radius: 50px;
  border: 2px solid white; /* White border for contrast */
  transition: all 0.5s; /* Smooth transition */
  margin: 10px;
}

.carousel-content .btn-get-started:hover {
  background: rgba(255, 255, 255, 0.8); /* Change background on hover */
  color: #28a745; /* Change text color on hover */
}

.carousel-control-prev,
.carousel-control-next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 32px;
  line-height: 1;
  opacity: 0.5;
  transition: opacity 0.3s;
  z-index: 4; /* Ensures arrows are on top */
}

.carousel-control-prev {
  left: 10px;
}

.carousel-control-next {
  right: 10px;
}

.carousel-control-prev:hover,
.carousel-control-next:hover {
  opacity: 0.9;
}

@keyframes floatIn {
  from {
    opacity: 0;
    transform: translateY(20px); /* Start from 20px below */
  }
  to {
    opacity: 1;
    transform: translateY(0); /* End at the original position */
  }
}

@keyframes floatInText {
  from {
    opacity: 0;
    transform: translateY(10px); /* Start from 10px below */
  }
  to {
    opacity: 1;
    transform: translateY(0); /* End at the original position */
  }
}
</style>
