<template>
  <main>
    <ul ref="carouselContainer" class="carousel">
      <li v-for="i in 10" :key="i" class="carousel__item">{{ i }}</li>
    </ul>
  </main>
</template>

<style scoped>
.carousel {
  overflow-x: auto;
  scrollbar-width: none;
  scroll-snap-type: x mandatory;
  scroll-behavior: smooth;

  width: 500px;
  display: flex;
  align-items: center;
  gap: 1rem;
  position: relative;
  anchor-name: --carousel;

  /* NOTE: carousel buttons */
  &::scroll-button(*) {
    position: fixed;
    position-anchor: --carousel;
    width: 64px;
    aspect-ratio: 1;
    border-radius: 50%;
    margin: 2rem;
    background-color: transparent;
    border: 3px solid hsl(0 0% 30%);
    cursor: pointer;
  }

  &::scroll-button(*):disabled {
    cursor: not-allowed;
  }

  &::scroll-button(left) {
    content: '👈' / 'Defilez a gauche';
    position-area: inline-start center;
  }

  &::scroll-button(right) {
    content: '👉' / 'Defilez a droite';
    position-area: inline-end center;
  }

  /* NOTE: carousel items */
  .carousel__item {
    scroll-snap-align: center;
    width: 250px;
    aspect-ratio: 3/4;
    background-color: hsl(0 0% 20%);
    border: 1px solid hsl(0 0% 30%);
    border-radius: 6px;
    flex-shrink: 0;
    font-size: 4rem;
    font-weight: 800;
    display: grid;
    place-content: center;
  }
}
</style>
