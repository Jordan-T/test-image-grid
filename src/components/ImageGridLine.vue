<template>
  <div class="c-image-grid-line">
    <picture
      v-for="image in images"
      :key="image"
      class="c-image-grid-line__img"
    >
      <img :src="image" alt="" draggable="false" loading="lazy" />
    </picture>
  </div>
</template>

<script setup lang="ts">
type Image = string;

const props = defineProps<{
  images: Image[];
}>();
</script>

<style lang="scss">
.c-image-grid-line {
  grid-column: 1 / -1;
  display: flex;
  align-items: stretch;
  justify-content: stretch;
  gap: var(--gap);

  &__img {
    aspect-ratio: 1;
    flex-grow: 1;
    position: relative;

    img {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
}
</style>
