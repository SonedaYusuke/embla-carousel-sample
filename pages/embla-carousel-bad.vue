<script setup lang="ts">
import emblaCarouselVue from 'embla-carousel-vue';

const [emblaRef, emblaApi] = emblaCarouselVue({ loop: true });

const scrollNext = () => {
  if (emblaApi.value) {
    emblaApi.value.scrollNext();
  }
};

const scrollPrev = () => {
  if (emblaApi.value) {
    emblaApi.value.scrollPrev();
  }
};

const skip = (index: number) => {
  if (emblaApi.value) {
    emblaApi.value.scrollTo(index);
  }
};

const currentIndex = ref(0);

onMounted(() => {
  if (emblaApi.value) {
    emblaApi.value.on('select', () => {
      currentIndex.value = emblaApi.value!.selectedScrollSnap() % cardList.length;
    })
  }
})

const cardList = [
  { color: '#f1c1c1', text: 'Card 1' },
  { color: '#f1e0c1', text: 'Card 2' },
  { color: '#d9f1c1', text: 'Card 3' },
];
</script>

<template>
  <div class="slider-wrapper">
    <div ref="emblaRef" class="slider">
      <div class="container">
        <div v-for="(card, index) in cardList" :key="`card-${index}`" :style="{ backgroundColor: card.color }" class="card">
          {{ card.text }}
        </div>
      </div>
    </div>
    <div class="indicator-wrapper">
      <button v-for="index in cardList.length" :key="`button-${index}`" class="indicator" @click="skip(index - 1)" :data-active="index - 1 === currentIndex"></button>
    </div>
    <button class="prev" @click="scrollPrev">Prev</button>
    <button class="next" @click="scrollNext">Next</button>
  </div>
</template>

<style scoped>
.slider {
  overflow: hidden;
}
.slider-wrapper {
  position: relative;
}
.container {
  display: flex;
}
.card {
  flex: 0 0 auto;
  width: 400px;
  height: 200px;
  border-radius: 8px;
  margin: 0 10px;
}
.prev, .next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  padding: 10px;
  border: none;
  background-color: #333;
  color: white;
  cursor: pointer;
}
.prev {
  left: 0;
}
.next {
  right: 0;
}
.indicator-wrapper {
  display: flex;
  justify-content: center;
  margin-top: 10px;
  gap: 10px;
}
.indicator {
  border: none;
  padding: 0;
  background-color: #aaa;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  cursor: pointer;
}
.indicator[data-active="true"] {
  background-color: #333;
}
</style>
