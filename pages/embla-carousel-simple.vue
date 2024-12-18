<script setup lang="ts">
import emblaCarouselVue from 'embla-carousel-vue';

const [emblaRef] = emblaCarouselVue({ loop: true });
</script>

<template>
  <div>
    <div ref="emblaRef" class="slider">
      <div class="container">
        <div style="background-color: #f1c1c1" class="card">Card 1</div>
        <div style="background-color: #f1e0c1" class="card">Card 2</div>
        <div style="background-color: #d9f1c1" class="card">Card 3</div>
        <div style="background-color: #c1f1d9" class="card">Card 4</div>
        <div style="background-color: #c1def1" class="card">Card 5</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.slider {
  overflow: hidden;
  width: 400px;
}
.container {
  display: flex;
}
.card {
  flex: 0 0 auto;
  width: 400px;
  height: 200px;
  border-radius: 8px;
}
</style>
