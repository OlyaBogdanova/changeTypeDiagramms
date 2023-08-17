<template>
  <div>
    <div class="horizontal-diagram_label">{{ label }}</div>
    <div class="horizontal-diagram_container w-100">
      <iHorizontalDiagramElement
        v-for="(elem, index) in dataValueInPercent"
        :key="elem.id"
        :elem="elem"
        :index="index"
      />
    </div>
  </div>
</template>
<script>
import { inject } from 'vue'
import iHorizontalDiagramElement from '../iHorizontalDiagram/iHorizontalDiagramElement.vue'

export default {
  components: {
    iHorizontalDiagramElement
  },
  setup() {
    const dataValueInPercent = inject('dataValueInPercent')

    const label = inject('label')

    return {
      label,
      dataValueInPercent
    }
  }
}
</script>
<style lang="scss"></style>
