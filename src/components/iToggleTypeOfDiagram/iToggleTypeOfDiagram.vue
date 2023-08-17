<template>
  <div class="d-flex justify-content-center align-items-center">
    <button
      class="p-3 btn-outline-secondary btn rounded-2 mr-2"
      @click="changeActiveType(diagramType['1'])"
    >
      Горизонтальная диаграмма
    </button>
    <button
      class="p-3 btn-outline-secondary btn rounded-2"
      @click="changeActiveType(diagramType['2'])"
    >
      Semi donut chart
    </button>
  </div>
</template>
<script>
import { inject } from 'vue'
export default {
  setup() {
    const activeType = inject('activeType')
    const diagramType = inject('diagramType')
    function changeActiveType(val) {
      activeType.value = val
    }
    return {
      changeActiveType,
      diagramType
    }
  }
}
</script>
<style lang="scss">
.btn {
  &:hover,
  &.active {
    background: #a8a8eb;
    color: #fff;
  }
}
</style>
