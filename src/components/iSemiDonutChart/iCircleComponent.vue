<template>
  <div class="mr-6">
    <svg xmlns="http://www.w3.org/2000/svg" :height="height" :width="width" :viewBox="viewbox">
      <circle
        fill="transparent"
        stroke="#b9cad1"
        :cx="cx"
        :cy="cy"
        :r="radius"
        :stroke-dasharray="[C, C].join(', ')"
        :stroke-dashoffset="C"
        :stroke-width="strokeWidth"
      />

      <circle
        v-for="(item, index) in strokeDashOffsets"
        :key="index"
        fill="transparent"
        :cx="cx"
        :cy="cy"
        :r="radius"
        :stroke="calculateColor(index)"
        :stroke-dasharray="strokeDashArrays[index].join(', ')"
        :stroke-dashoffset="item"
        :stroke-width="strokeWidth"
      />
    </svg>
  </div>
</template>
<script>
import { computed } from 'vue'
export default {
  props: ['percentage', 'height', 'width', 'strokeWidth', 'sectorColors', 'gap'],

  setup({ width, height, strokeWidth, gap, percentage, sectorColors }) {
    //computed для svg
    const cx = computed(() => {
      return width / 2
    })
    const cy = computed(() => {
      return height / 2
    })
    const radius = computed(() => {
      return width / 2 - strokeWidth / 2
    })
    const C = computed(() => {
      return 2*Math.PI * radius.value
    })
    const computedGap = computed(() => {
      return (C.value * gap) / 100
    })
    const strokeDashArrays = computed(() => {
      const sumGapPercentage = (gap * (percentage.length - 1)) / 100
      return percentage.map((percent) => {
        return [
          (C.value * (1 - sumGapPercentage) * percent) / 100,
          C.value * (1 - (percent / 100) * (1 - sumGapPercentage))
        ]
      })
    })
    const strokeDashOffsets = computed(() => {
      return strokeDashArrays.value.map((value, index) => {
        return strokeDashArrays.value
          .slice(0, index)
          .reduce(
            (acc, item) => (index >= 1 ? acc - item[0] - computedGap.value : acc - item[0]),
            C.value
          )
      })
    })
    const viewbox = computed(() => {
    
      return `0 0 ${width} ${height}`
    })
    function calculateColor(index) {
      return sectorColors[index]
    }

    return {
      cx,
      cy,
      radius,
      viewbox,
      strokeWidth,
      strokeDashOffsets,
      width,
      height,
      C,
      strokeDashArrays,
      calculateColor
    }
  }
}
</script>
<style lang=""></style>
