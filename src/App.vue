<script setup lang="ts">
import { ref, watch } from 'vue';
import imageUrls from './imageUrls.ts';
import ImageGrid from './components/ImageGrid.vue';
import ImageGridSquare from './components/ImageGridSquare.vue';
import ImageGridLine from './components/ImageGridLine.vue';
import ImageGridSpecial from './components/ImageGridSpecial.vue';

let currentImageIndex = 0;

const useImages = ref(true);
const generateImages = (count: number, background?: string = 'CCC') => {
  const images: string[] = [];
  for (let i = 0; i < count; i++) {
    if (useImages.value) {
      const imageUrl = imageUrls[currentImageIndex % imageUrls.length];
      currentImageIndex += 1;
      images.push(imageUrl);
    } else {
      images.push(
        `https://via.placeholder.com/640x640/${background}?text=${i + 1}`
      );
    }
  }

  return images;
};

watch(useImages, () => {
  currentImageIndex = 0;
});
</script>

<template>
  <div class="p-default">
    <h1>Image grid</h1>

    <label>
      <input type="checkbox" v-model="useImages" />
      Utiliser des images
    </label>

    <h2>Final example</h2>
    <ImageGrid class="p-default__grid">
      <ImageGridSquare :images="generateImages(1)" type="1" />
      <ImageGridSquare :images="generateImages(3, 'FCC')" type="4" />
      <ImageGridLine :images="generateImages(3, 'FCF')" />
      <ImageGridSpecial :images="generateImages(4, 'CFC')" type="3" />
      <ImageGridSpecial :images="generateImages(2, 'CCF')" type="4" />
      <ImageGridSquare :images="generateImages(1, 'FFC')" type="1" />
      <ImageGridSquare :images="generateImages(2, 'CFF')" type="1" />
    </ImageGrid>

    <h2>Square block</h2>
    <h2>type 1 with X images</h2>
    <ImageGrid class="p-default__grid">
      <ImageGridSquare :images="generateImages(1)" type="1" />
      <ImageGridSquare :images="generateImages(2)" type="1" />
      <ImageGridSquare :images="generateImages(3)" type="1" />
      <ImageGridSquare :images="generateImages(4)" type="1" />
    </ImageGrid>

    <h2>type 1 and 2 with 2 images</h2>
    <ImageGrid class="p-default__grid">
      <ImageGridSquare :images="generateImages(2)" type="1" />
      <ImageGridSquare :images="generateImages(2)" type="2" />
    </ImageGrid>

    <h2>type 1, 2, 3 and 4 with 3 images</h2>
    <ImageGrid class="p-default__grid">
      <ImageGridSquare :images="generateImages(3)" type="1" />
      <ImageGridSquare :images="generateImages(3)" type="2" />
      <ImageGridSquare :images="generateImages(3)" type="3" />
      <ImageGridSquare :images="generateImages(3)" type="4" />
    </ImageGrid>

    <h2>Line block</h2>
    <ImageGrid class="p-default__grid">
      <ImageGridLine :images="generateImages(1)" />
      <ImageGridLine :images="generateImages(2)" />
      <ImageGridLine :images="generateImages(3)" />
      <ImageGridLine :images="generateImages(4)" />
    </ImageGrid>

    <h2>Special block</h2>
    <ImageGrid class="p-default__grid">
      <ImageGridSpecial :images="generateImages(5)" type="1" />
      <ImageGridSpecial :images="generateImages(5)" type="2" />
      <ImageGridSpecial :images="generateImages(4)" type="3" />
      <ImageGridSpecial :images="generateImages(2)" type="4" />
    </ImageGrid>
  </div>
</template>

<style lang="scss" scoped>
.p-default {
}
.p-default__grid {
  margin-bottom: 3rem;
}
</style>
