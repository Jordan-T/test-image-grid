<template>
  <div class="c-image-grid-square" :class="`c-image-grid-square--${type}`">
    <picture
      v-for="image in images"
      :key="image"
      class="c-image-grid-square__img"
    >
      <img :src="image" alt="" draggable="false" loading="lazy" />
    </picture>
  </div>
</template>

<script setup lang="ts">
type Image = string;

const props = defineProps<{
  images: Image[];
  /** @values 1, 2, 3, 4 */
  type?: string;
}>();
</script>

<style lang="scss">
.c-image-grid-square {
  aspect-ratio: 1;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  align-items: stretch;
  justify-content: stretch;
  gap: var(--gap);

  &__img {
    position: relative;

    &:first-child:last-child,
    &:nth-child(1):nth-last-child(3) {
      grid-column: 1 / -1;
    }

    // 3 childs
    &:nth-child(1):nth-last-child(3) {
      grid-area: img1;
    }
    &:nth-child(2):nth-last-child(2) {
      grid-area: img2;
    }
    &:nth-child(3):nth-last-child(1) {
      grid-area: img3;
    }

    // 2 childs
    &:nth-child(1):nth-last-child(2) {
      grid-area: img1;
    }
    &:nth-child(2):nth-last-child(1) {
      grid-area: img2 / img2 / img3 / img3;
    }

    &:first-child:last-child {
      grid-row: 1 / -1;
    }

    img {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }

  &--1 {
    grid-template-areas: 'img1 img1' 'img2 img3';
  }

  &--2 {
    grid-template-areas: 'img2 img1' 'img3 img1';
  }

  &--3 {
    grid-template-areas: 'img2 img3' 'img1 img1';
  }

  &--4 {
    grid-template-areas: 'img1 img2' 'img1 img3';
  }
}
</style>
