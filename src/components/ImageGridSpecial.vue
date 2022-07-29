<template>
  <div class="c-image-grid-special" :class="`c-image-grid-special--${type}`">
    <picture
      v-for="image in images"
      :key="image"
      class="c-image-grid-special__img"
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
.c-image-grid-special {
  aspect-ratio: 0.75;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  align-items: stretch;
  justify-content: stretch;
  gap: var(--gap);

  &__img {
    position: relative;

    @for $i from 1 through 5 {
      &:nth-child(#{$i}) {
        grid-area: #{'img#{$i}'};
      }
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
    grid-template-areas: 'img1 img1' 'img2 img3' 'img4 img5';
  }

  &--2 {
    grid-template-areas: 'img2 img3' 'img4 img5' 'img1 img1';
  }
}
</style>
