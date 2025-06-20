<template>
  <main>
    <ul ref="carouselContainer" class="carousel">
      <li v-for="i in 10" :key="i" :data-label="`Slide #${i}`" class="carousel__item">
        {{ i }}
      </li>
    </ul>
  </main>
</template>

<style scoped>
.carousel {
  overflow-x: auto;
  scrollbar-width: none;
  scroll-snap-type: x mandatory;
  scroll-behavior: smooth;
  scroll-marker-group: after;

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

  &::scroll-marker-group {
    position: fixed;
    position-anchor: --carousel;
    position-area: block-end;
    margin-block-start: 2rem;

    display: flex;
    align-items: center;
    gap: 20px;
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

    &::scroll-marker {
      content: '' / attr(data-label);
      cursor: pointer;
      width: 1.25rem;
      aspect-ratio: 1;
      border-radius: 50%;
      border: 1px solid hsl(0 0% 40%);
    }

    &::scroll-marker:target-current {
      background-color: white;
    }
  }
}
</style>
