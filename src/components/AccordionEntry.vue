<script setup>
import { computed } from 'vue'

const props = defineProps({
  index: {
    type: Number,
    required: true
  },
  active: {
    type: Boolean,
    default: false
  }
})
const isFirst = computed(() => {
  return props.index === 1;
})
const isLast = computed(() => {
  return props.index === 3;
})
const isLastAndActive = computed(() => {
  return isLast.value && props.active
})

const emit = defineEmits(['setActive'])
const toggleActive = () => {
  emit('setActive', props.index)
}
</script>

<template>
  <transition-group tag="ul" class="list-none" name="desc">
    <li>
      <button
        @click="toggleActive"
        type="button"
        class="w-full border border-solid border-slate-200 bg-slate-100 py-3 px-5 hover:bg-blue-200"
        :class="{ 'rounded-t-md border-b-0': isFirst, 'rounded-b-md border-t-0': isLast, 'rounded-b-none border-t-0': isLastAndActive }"
      >
        <div class="flex justify-between items-center">
          <h2 class="text-lg text-left">Accordion Entry #{{ index }}</h2>
          <transition name="downArrow" mode="out-in">
            <div v-if="!active"  class="w-2 h-2 border-r-2 border-b-2 border-slate-900 rotate-45"></div>
            <div v-else class="w-2 h-2 border-t-2 border-r-2 border-slate-900 -rotate-45"></div>
          </transition>
        </div>
      </button>
    </li>
    <li v-if="active">
      <div
        class="container p-6 border-l border-r border-slate-200"
        :class="{ 'border-t-0 border-b rounded-b-md': isLast }"
      >
        <p>The accordion #{{ index }} item's text goes here! It remains hidden, until the accordion item is clicked. It could also be supplied as a prop!</p>
      </div>
    </li>
  </transition-group>
</template>

<style scoped>
.downArrow-enter-from,
.downArrow-leave-to {
  transform: rotate(180deg);
  opacity: 0;
}
/* .downArrow-enter-to,
.downArrow-leave-from {
  transform: rotate(-180deg);
} */
.downArrow-enter-active,
.downArrow-leave-active {
  transition: all 0.5s ease;
}


.desc-move,
.desc-enter-active,
.desc-leave-active {
  transition: all 0.5s ease;
}

.desc-enter-from,
.desc-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
.desc-leave-active {
  position: absolute;
}
</style>