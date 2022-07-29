<template>
  <div class="c-image-grid">
    <slot />
  </div>
</template>

<style lang="scss">
.c-image-grid {
  // TODO: set your gap here
  --gap: 3px;

  display: grid;
  gap: var(--gap);
  grid-template-columns: 1fr;

  // TODO set the bootstrap variable
  // @include media-breakpoint-up(sm) {
  @media (min-width: 576px) {
    grid-template-columns: 1fr 1fr;
  }
}
</style>
