<template>
  <div :class="flipped ? 'flip-container flipped' : 'flip-container'">
    <div class="flipper">
      <div
        class="front"
        :style="cardSuite"
      ></div>
      <div class="back"></div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from "vue";
import { Card } from "../types";

const props = defineProps<{
  card: Card;
}>();

const flipped = computed(() => {
  return props.card.hidden;
});

const cardSuite = computed(() => {
  return props.card.suit
    ? `background-image: url("/src/assets/${props.card.suit}_card.png");`
    : null;
});
</script>

<style scoped>
.flip-container {
  -webkit-perspective: 1000;
  -moz-perspective: 1000;
  -o-perspective: 1000;
  perspective: 1000;
}
.flipper {
  -moz-transform: perspective(1000px);
  -moz-transform-style: preserve-3d;
  position: relative;
  border: 1px solid black;
  border-radius: 20px;
}

.front,
.back {
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
  -o-backface-visibility: hidden;
  backface-visibility: hidden;
  -webkit-transition: 0.6s;
  -webkit-transform-style: preserve-3d;
  -moz-transition: 0.6s;
  -moz-transform-style: preserve-3d;
  -o-transition: 0.6s;
  -o-transform-style: preserve-3d;
  -ms-transition: 0.6s;
  -ms-transform-style: preserve-3d;
  transition: 0.6s;
  transform-style: preserve-3d;
  top: 0;
  left: 0;
  background-color: rgb(255, 255, 255);
  width: 185px;
  height: 276px;
  border: 8px solid rgb(255, 255, 255);
  border-radius: 20px;
}

.back {
  -webkit-transform: rotateY(-180deg);
  -moz-transform: rotateY(-180deg);
  -o-transform: rotateY(-180deg);
  -ms-transform: rotateY(-180deg);
  transform: rotateY(-180deg);
  position: absolute;
  background-color: #1661b66d;
  background-image: url("../assets/union.png");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  border: 8px solid #565864;
}
.flip-container.flipped .back {
  -webkit-transform: rotateY(0deg);
  -moz-transform: rotateY(0deg);
  -o-transform: rotateY(0deg);
  -ms-transform: rotateY(0deg);
  transform: rotateY(0deg);
}
.flip-container.flipped .front {
  -webkit-transform: rotateY(180deg);
  -moz-transform: rotateY(180deg);
  -o-transform: rotateY(180deg);
  -ms-transform: rotateY(180deg);
  transform: rotateY(180deg);
}
.front {
  background-image: url("../assets/clubs_card.png");
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  z-index: 2;
}

@media only screen and (max-width: 660px) {
  .front,
  .back {
    width: 85px;
    height: 146px;
  }
}
</style>
