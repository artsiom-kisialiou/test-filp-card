<template>
  <div class="container">
    <div class="main-card">
      <CardComponent :card="currentCard" />
    </div>
    <div class="low-button">
      <ActionButton
        type="secondary"
        @click="flipCard(true)"
      />
    </div>
    <div class="card-row">
      <div class="hidden-cards">
        <div
          v-for="card in cards"
          :key="card.id"
          :class="{
            'card-on-top': !card.hidden,
            'card-on-bottom': card.hidden,
          }"
        >
          <CardComponent :card="card" />
        </div>
      </div>
    </div>
    <div class="high-button">
      <ActionButton @click="flipCard(false)" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import CardComponent from "../shared/CardComponent.vue";
import ActionButton from "../shared/ActionButton.vue";
import { Card } from "../types";

const currentCard: Card = ref({
  id: 0,
  hidden: false,
  title: "12",
  suit: "clubs",
});

const cards: Card[] = ref([
  { id: 1, title: "12", suit: "clubs", hidden: true },
  { id: 2, title: "A", suit: "ace", hidden: true },
  { id: 3, title: "12", suit: "clubs", hidden: true },
]);

const flipCard = (flip: boolean) => {
  cards.value.find((card: Card) => {
    if (card.id === 2) {
      card.hidden = flip;
    }
  });
};
</script>

<style scoped>
@keyframes move-on-top {
  from {
    bottom: 0px;
  }
  to {
    bottom: 350px;
  }
}

@keyframes move-to-bottom {
  from {
    bottom: 350px;
  }
  to {
    bottom: 0px;
  }
}
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, 1fr);
  align-items: center;
  justify-content: center;
}

.main-card {
  display: grid;
  grid-column-start: 2;
  justify-content: center;
  margin-top: 50px;
}
.card-row {
  display: grid;
  grid-column-start: 2;
}
.hidden-cards {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  margin-top: 50px;
}

.low-button {
  display: grid;
  grid-column-start: 1;
  grid-row-start: 2;
  padding-right: 64px;
  justify-items: right;
}
.high-button {
  display: grid;
  grid-column-start: 3;
  grid-row-start: 2;
  padding-left: 64px;
  justify-items: left;
}
.card-on-top {
  z-index: 2;
  animation: move-on-top 1s forwards;
  position: relative;
}
.card-on-bottom {
  z-index: 1;
  animation: move-to-bottom 1s forwards;
  position: relative;
}

@media only screen and (max-width: 920px) {
  .card-row {
    grid-column-start: 1;
    grid-column-end: 23;
    justify-items: center;
    align-items: center;
  }
  .low-button {
    grid-column-start: 1;
    grid-row-start: 1;
    padding-right: 41px;
  }
  .high-button {
    grid-column-start: 3;
    grid-row-start: 1;
    padding-left: 41px;
  }
}

@media only screen and (max-width: 660px) {
  @keyframes move-on-top {
    from {
      bottom: 0px;
    }
    to {
      bottom: 220px;
    }
  }

  @keyframes move-to-bottom {
    from {
      bottom: 220px;
    }
    to {
      bottom: 0px;
    }
  }
  .low-button {
    padding-right: 20px;
  }
  .high-button {
    padding-left: 20px;
  }
}
</style>
