<script>
import { ref } from 'vue'
import Chip from './Chip.vue'

export default {
  components: {
    Chip
  },
  setup() {
    const playTypeArray = ['BP', 'T', 'PP', 'B', 'P']
    const coinArray = [10, 10, 20, 30, 40, 50]
    let chipArray = ref([])
    const addChip = ($e) => {
      const { target } = $e
      showCircle($e, 100)
      const x = target.offsetLeft + target.offsetWidth / 2, y = target.offsetTop + target.offsetHeight / 2
      chipArray.value.push({ x, y })
    }
    const showCircle = ({ clientX, clientY }, diameter = 80) => {
      const circle = document.getElementsByClassName('circle')[0]
      circle.style.left = clientX - diameter / 2 + 'px'
      circle.style.top = clientY - diameter / 2 + 'px'
      if (diameter !== 80) circle.classList.add('big')
      circle.style.display = 'block'

      setTimeout(() => {
        circle.style.display = 'none'
        circle.classList.remove('big')
      }, 200)
    }
   return {
      playTypeArray,
      coinArray,
      chipArray,
      addChip,
      showCircle
    }
  }
}
</script>

<template>
  <div class="container" @click="showCircle">
    <div class="bet-table">
      <div class="grid grid-cols-3">
        <button class="bet-table__button" @click.stop="addChip">{{ playTypeArray[0] }}</button>
        <button class="bet-table__button" @click.stop="addChip">{{ playTypeArray[1] }}</button>
        <button class="bet-table__button" @click.stop="addChip">{{ playTypeArray[2] }}</button>
      </div>
      <div class="grid grid-cols-2">
        <button class="bet-table__button" @click.stop="addChip">{{ playTypeArray[3] }}</button>
        <button class="bet-table__button" @click.stop="addChip">{{ playTypeArray[4] }}</button>
      </div>
    </div>
    <div class="bet-amount">
      <button v-for="coin in coinArray" :key="coin" class="bet-amount__button">{{ coin }}</button>
    </div>
    <Chip v-for="(chip, index) in chipArray" :key="index" :position="chip" :index="index" />
    <div class="circle">
      <div class="mid">
        <div class="inner"></div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
button {
  @apply outline-none focus:outline-none  select-none;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}

.container {
  @apply w-full md:w-230 h-150 md:h-200 lg:h-220 p-10 md:p-20 lg:p-40 flex flex-col justify-between;
  .bet-table {
    @apply w-full bg-[#1f7000] text-2xl text-white font-semibold grid grid-flow-row p-1 pr-3 pb-2;
    &__button {
      @apply h-20 md:h-30 border-light-200 border-1 flex justify-center items-center hover:bg-[#87b980] active:bg-[#87b980];
      box-shadow: rgba(0, 0, 0, 0.35) 1px 0px 15px;
    }
  }
  .bet-amount {
    @apply w-full h-20 md:h-30 bg-[#1f7000] rounded-md flex flex-row justify-start items-center px-4 gap-2;
    &__button {
      @apply w-10 md:w-20 h-10 md:h-20 border-light-50 border-1 rounded-1/2 text-white text-2xl hover:bg-[#87b980] active:bg-[#87b980];
    }
  }
  .circle {
    @apply absolute border-white border-2 w-15 md:w-20 h-15 md:h-20 rounded-1/2 hidden;
    .mid {
      @apply border-black border-4 w-14 md:w-19 h-14 md:h-19 rounded-1/2;
      .inner {
        @apply border-white border-2 w-12 md:w-17 h-12 md:h-17 rounded-1/2;
      }
    }
    &.big {
      @apply w-20 h-20 md:w-25 md:h-25;
      .mid {
        @apply w-19 h-19 md:w-24 md:h-24;
        .inner {
          @apply w-17 h-17 md:w-22 md:h-22;
        }
      }
    }
  }
}
</style>
