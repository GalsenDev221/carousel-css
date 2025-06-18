<script lang="ts" setup>
import { onMounted, reactive, ref, watch } from 'vue'

type CarouselProps = {
  width: number
  itemCount: number
  scrollStep: number
}

const carousel: CarouselProps = reactive({
  width: 0,
  itemCount: 10,
  scrollStep: 300,
})

const carouselContainer = ref<HTMLUListElement | null>(null)
const currIdx = ref(0)

function handleNext() {
  currIdx.value++
}

function handlePrev() {
  currIdx.value--
}

onMounted(() => {
  if (carouselContainer.value) {
    carousel.width = carouselContainer.value.offsetWidth
  }
})

watch(currIdx, () => {
  if (carouselContainer.value) {
    const translateX = Math.max(
      0,
      Math.min(
        currIdx.value * carousel.scrollStep,
        carouselContainer.value.scrollWidth - carousel.width,
      ),
    )
    carouselContainer.value.style.transform = `translateX(-${translateX}px)`
  }
})
</script>

<template>
  <main>
    <div class="carousel-wrapper">
      <ul ref="carouselContainer" class="carousel">
        <li v-for="i in carousel.itemCount" :key="i" class="carousel__item">{{ i }}</li>
      </ul>
    </div>

    <footer>
      <button @click="handlePrev">Prev</button>
      <button @click="handleNext">Next</button>
    </footer>
  </main>
</template>

<style scoped>
.carousel-wrapper {
  overflow-x: auto;
  scrollbar-width: none;
  scroll-snap-type: x mandatory;
}

.carousel {
  width: 500px;
  display: flex;
  align-items: center;
  gap: 1rem;
  transition: transform 0.5s ease;

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

footer {
  margin-block-start: 2rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;

  button {
    background-color: hsl(0 0% 30%);
    padding: 1rem 2rem;
    font-size: 1.3rem;
    color: white;
  }
}
</style>
