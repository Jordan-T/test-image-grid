<template>
  <div class="c-image-grid">
    <slot />
  </div>
</template>

<style lang="scss">
.c-image-grid {
  --gap: 5px;
  display: grid;
  gap: var(--gap);
  grid-template-columns: 1fr 1fr;
}
</style>
