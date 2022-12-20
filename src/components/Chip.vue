<script>
import { onMounted } from 'vue'

export default {
  props: {
    position: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  setup(props) {
    onMounted(() => {
      const container = document.getElementsByClassName('container')[0]
      const chip = document.getElementsByClassName('chip')[props.index]
      const CHIP = {
        HEIGHT: chip.offsetHeight,
        WIDTH: chip.offsetWidth
      }

      chip.style.left = container.offsetWidth / 2 + 'px'
      chip.style.top = container.offsetHeight * .6 + 'px'

      setTimeout(() => {
        chip.style.left = (props.position.x - CHIP.WIDTH / 2)+ 'px'
        chip.style.top = (props.position.y - CHIP.HEIGHT / 2)+ 'px'
      }, 100)
      
    })
  }
}
</script>

<template>
<div class="chip">chip</div>
</template>

<style lang="scss" scoped>
.chip {
  @apply w-12 md:w-20 h-12 md:h-20 absolute flex justify-center items-center bg-[#c12a35] border-light-50 border-2 rounded-1/2 text-base md:text-3xl text-white select-none;
  transition: all 0.5s;
}
</style>