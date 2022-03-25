<script setup>
import { ref } from 'vue'
import AccordionEntry from './AccordionEntry.vue'

defineProps({
  msg: String
})

const activeEntry = ref(0)

const setActive = (index) => {
  if (activeEntry.value === index) {
    return activeEntry.value = null
  }
  activeEntry.value = index
}
</script>

<template>
  <TransitionGroup name="list" tag="ul" class="list-none">
    <li v-for="num in 3" :key="num">
      <accordion-entry @setActive="setActive" :index="num" :active="activeEntry === num"></accordion-entry>
    </li>
  </TransitionGroup>
</template>

<style scoped>
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
.list-leave-active {
  position: absolute;
}
</style>
