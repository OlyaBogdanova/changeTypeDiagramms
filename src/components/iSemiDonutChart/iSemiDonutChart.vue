<template>
  <div class="mb-5">{{ title }}</div>
  <div class="d-flex justify-content-between diagram_container">
    <iCircleComponent
      :percentage="percentage"
      :height="height"
      :width="width"
      :strokeWidth="strokeWidth"
      :sectorColors="sectorColors"
      :gap="gap"
    />
    <div>
      <div v-for="(label, index) in labelsList" :key="label" class="d-flex mb-3">
        <div class="color" :style="{ background: sectorColors[index] }"></div>
        <div>{{ label }}</div>
      </div>
    </div>
  </div>
</template>
<script>
import iCircleComponent from '@/components/iSemiDonutChart/iCircleComponent.vue'
export default {
  components: { iCircleComponent },
  props: {
    title: {
      type: String
    },
    labelsList: {
      type: Array
    },
    percentage: {
      type: Array,
      required: false,
      default: () => [20, 30, 20, 20, 10]
    },
    height: {
      type: Number,
      required: false,
      default: 256
    },
    width: {
      type: Number,
      required: false,
      default: 256
    },
    strokeWidth: {
      type: Number,
      required: false,
      default: 30
    },
    sectorColors: {
      type: Array,
      required: false,
      default: () => ['#762af0', '#a858f8', '#a8a8eb', '#ececfd', '#fff']
    },
    gap: {
      type: Number,
      required: false,
      default: 0.1
    }
  },
  setup() {
    return {}
  }
}
</script>
<style lang="scss">
.color {
  width: 20px;
  height: 20px;
}
.diagram_container{
    width: 30%;
}
</style>
