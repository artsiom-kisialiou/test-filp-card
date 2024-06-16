<template>
  <button :class="buttonClass"></button>
</template>

<script setup lang="ts">
import { computed } from "vue";

const props = defineProps({
  type: {
    type: String,
    default: "primary",
    validator(value: string) {
      return ["primary", "secondary"].includes(value);
    },
  },
});

const buttonClass: string = computed(() => {
  return {
    [props.type]: true,
  };
});
</script>

<style scoped>
button {
  cursor: pointer;
  width: 64px;
  height: 64px;
  border-radius: 100%;
  border: 4px solid transparent;
  box-shadow: 7px 6px 28px 1px rgba(0, 0, 0, 0.24);
}

.primary {
  background-color: #71c658;
  background-image: url("../assets/arrow.png");
  background-position: center;
  background-repeat: no-repeat;
  border-color: #66ac52;
}

.primary:hover {
  background-color: #3e8e41;
}

.primary:active {
  box-shadow: 7px 6px 28px 1px rgba(0, 0, 0, 0.24);
  transform: translateY(4px);
}

.secondary {
  background-color: #dd385f;
  background-image: url("../assets/arrow.png");
  background-position: center;
  background-repeat: no-repeat;
  transform: rotate(180deg);
  border-color: #bc3353;
}

.secondary:hover {
  background-color: #9f0e30;
}

.secondary:active {
  box-shadow: 7px 6px 28px 1px rgba(0, 0, 0, 0.24);
  transform: rotate(180deg) translateY(4px);
}
@media only screen and (max-width: 600px) {
  button {
    width: 48px;
    height: 48px;
  }
}
</style>
