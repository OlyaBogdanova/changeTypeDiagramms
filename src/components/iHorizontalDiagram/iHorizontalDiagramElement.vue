<template>
  <div class="d-flex align-items-center w-100">
    <div class="elem-number">{{ index+1 }}</div>
    <div class="elem-label bg-white mr-2">{{ elem.label }}</div>
    <div class="elem-value">
      <div class="horizontal-diagram_elem bg-secondary my-3" :style="{ width: elem.value }"></div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    elem: {
      type: Object,
      required: true
    },
    index:{
        type:Number,
        required:true
    }
  }
}
</script>
<style lang="scss">
.horizontal-diagram_elem {
  height: 20px;
  width: 100px;
}
.elem-value {
  flex: 1 0 70%;
}
.elem-label {
  flex: 0 0 25%;
  min-width: 95px;
}
.elem-number {
  flex: 0 0 2%;
}
</style>
