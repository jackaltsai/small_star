<script setup>
import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Navigation } from 'vue3-carousel';
import { ref } from 'vue';

const currentSlide = ref(0);

const slideTo = (nextSlide) => (currentSlide.value = nextSlide);

const galleryConfig = {
  itemsToShow: 1,
  wrapAround: true,
  mouseDrag: false,
  touchDrag: false,
};

const thumbnailsConfig = {
  itemsToShow: 6,
  wrapAround: true,
  gap: 10,
};

const urls = [
  `https://i.imgur.com/kVGBMWH.png`,
  `https://i.imgur.com/Xn8ygmh.png`,
  `https://i.imgur.com/WSeRFeg.png`,
  `https://i.imgur.com/GNkZ23Z.png`,
  `https://i.imgur.com/56WzQ2Y.png`,
  `https://i.imgur.com/CKVe9oR.png`,
  `https://i.imgur.com/MrMCkiS.png`,
  `https://i.imgur.com/6cogJyg.png`,
  `https://i.imgur.com/7Imt8o4.png`,
  `https://i.imgur.com/tN3VVzX.png`,
];

const images = urls.map((url, index) => ({
  id: index + 1, // Unique ID starting from 1
  url: url,      // Assigns the current URL from the array
}));


</script>

<template>
  <Carousel id="gallery" v-bind="galleryConfig" v-model="currentSlide">
    <Slide v-for="image in images" :key="image.id">
      <div class="carousel__item">
        <img :src="image.url" alt="Gallery Image" class="gallery-image" />
      </div>
    </Slide>
  </Carousel>

  <Carousel id="thumbnails" v-bind="thumbnailsConfig" v-model="currentSlide">
    <Slide v-for="image in images" :key="image.id">
      <div class="carousel__item" @click="slideTo(image.id - 1)">
        <img :src="image.url" alt="Thumbnail Image" class="thumbnail-image" />
      </div>
    </Slide>

    <template #addons>
      <Navigation />
    </template>
  </Carousel>
</template>
