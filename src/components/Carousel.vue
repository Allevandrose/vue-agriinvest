<template>
  <!-- Carousel Section Start -->
  <div class="carousel-wrapper">
    <!-- Carousel 1 -->
    <section class="splide" aria-label="Splide Carousel 1">
      <div class="splide__track">
        <ul class="splide__list">
          <li class="splide__slide">
            <div class="content-wrapper">
              <div class="description">
                <h3>Slide 1 Title</h3>
                <p>This is a description of the first slide.</p>
              </div>
              <img src="@/assets/car1.jpeg" alt="Slide 1 Image" />
            </div>
          </li>
          <li class="splide__slide">
            <div class="content-wrapper">
              <div class="description">
                <h3>Slide 2 Title</h3>
                <p>This is a description of the second slide.</p>
              </div>
              <img src="@/assets/car3.jpeg" alt="Slide 2 Image" />
            </div>
          </li>
          <li class="splide__slide">
            <div class="content-wrapper">
              <div class="description">
                <h3>Slide 3 Title</h3>
                <p>This is a description of the third slide.</p>
              </div>
              <img src="@/assets/car4.jpeg" alt="Slide 3 Image" />
            </div>
          </li>
          <li class="splide__slide">
            <div class="content-wrapper">
              <div class="description">
                <h3>Slide 4 Title</h3>
                <p>This is a description of the fourth slide.</p>
              </div>
              <img
                style="height: 300px; width: 370px"
                src="@/assets/chinese cabbage.jpeg"
                alt="Slide 4 Image"
              />
            </div>
          </li>
        </ul>
      </div>

      <!-- Custom Arrows -->
      <div class="splide__arrows">
        <button class="splide__arrow splide__arrow--prev">
          <i class="fa-solid fa-arrow-left"></i>
        </button>
        <button class="splide__arrow splide__arrow--next">
          <i class="fa-solid fa-arrow-right"></i>
        </button>
      </div>
    </section>
  </div>
  <!-- Carousel Section End -->
</template>

<script>
import { onMounted } from "vue";
import Splide from "@splidejs/splide";
import "@splidejs/splide/dist/css/splide.min.css";

export default {
  name: "CarouselComponent",
  setup() {
    onMounted(() => {
      new Splide(".splide", {
        type: "loop",
        heightRatio: 0.5,
        autoplay: true,
        interval: 3000,
        pauseOnHover: true,
        arrows: false, // Disable default arrows
      }).mount();

      // Manual navigation arrows
      const splide = document.querySelector(".splide").splide;
      document
        .querySelector(".splide__arrow--prev")
        .addEventListener("click", () => splide.go("<"));

      document
        .querySelector(".splide__arrow--next")
        .addEventListener("click", () => splide.go(">"));
    });
  },
};
</script>

<style scoped>
.carousel-wrapper {
  height: calc(100vh - 80px); /* Adjust height based on navbar */
  position: relative;
  margin: 20px 0;
}

.splide__slide {
  display: flex;
  justify-content: center; /* Center the content wrapper */
  align-items: center;
  height: 100%;
}

.content-wrapper {
  display: flex;
  justify-content: space-between; /* Space between content and image */
  align-items: center; /* Center content vertically */
  width: 100%; /* Full width */
  padding: 20px; /* Add some padding */
}

.splide__slide img {
  max-width: 50%; /* Adjust max width of images */
  height: auto; /* Maintain aspect ratio */
}

.description {
  max-width: 40%; /* Adjust the width of the description */
  font-size: 1.2rem;
  color: black; /* Change text color to black */
  /* Remove background */
  padding: 10px;
}

/* Custom navigation arrows */
.splide__arrows {
  display: flex;
  justify-content: center;
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
}

.splide__arrow {
  background-color: #00d27c; /* Background color for arrows */
  border: 2px solid #00d27c; /* Border color */
  border-radius: 50%; /* Rounded corners */
  width: 40px; /* Width of the arrow button */
  height: 40px; /* Height of the arrow button */
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  cursor: pointer;
  color: white; /* Color of the arrow icon */
  transition: background-color 0.3s, border-color 0.3s, color 0.3s;
}

.splide__arrow:hover {
  background-color: white; /* Background color on hover */
  border-color: white; /* Border color on hover */
  color: #333; /* Arrow icon color on hover */
}

/* Remove the pagination */
.splide__pagination {
  display: none;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .description {
    max-width: 60%; /* Adjust description width for smaller screens */
    font-size: 1rem; /* Smaller font size */
  }

  .splide__slide img {
    max-width: 70%; /* Adjust image size for smaller screens */
  }

  .content-wrapper {
    flex-direction: column; /* Stack content and image */
    align-items: center; /* Center align content */
  }

  .splide__arrows {
    bottom: 20px; /* Adjust arrow position */
  }
}
</style>
