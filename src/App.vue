<template>
  <main>
    <ul class="carousel">
      <li v-for="i in 10" :key="i" class="carousel__item">{{ i }}</li>
    </ul>
  </main>
</template>

<style scoped>
.carousel {
  overflow-x: auto;
  scrollbar-width: none;
  scroll-snap-type: x mandatory;

  width: 500px;
  display: flex;
  align-items: center;
  gap: 1rem;

  .carousel__item {
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
