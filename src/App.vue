<script setup>
import { provide, ref } from 'vue'
import iToggleTypeOfDiagram from '@/components/iToggleTypeOfDiagram/iToggleTypeOfDiagram.vue'
import iSemiDonutChart from '@/components/iSemiDonutChart/iSemiDonutChart.vue'
import iHorizontalDiagram from '@/components/iHorizontalDiagram/iHorizontalDiagram.vue'
const diagramType = {
  1: 'horizintal diagram',
  2: 'semi donut chart'
}
const activeType = ref(diagramType[1])

const dataDistrictInfo = {
  type: 'horizontalBar', // пока не интересует
  label: 'Муниципальные образования',
  data: [
    {
      label: 'Вологодский',
      id: 1,
      value: 12
    },
    {
      label: 'Грязовецкий',
      id: 2,
      value: 6
    },
    {
      label: 'Сямженский',
      id: 3,
      value: 4
    },
    {
      label: 'Тотемский',
      id: 3,
      value: 1
    }
  ]
}
const { label, data } = dataDistrictInfo

    const values = data.map((elem) => elem.value)
    const maxValue = Math.max(...values)

    const dataValueInPercent = [...data].map((elem) => {
      return {
        label: elem.label,
        value: ((elem.value / maxValue) * 100).toString() + '%'
      }
    })
    const dataValueInAbsolute = [...data].map((elem) => {
      return {
        label: elem.label,
        value: elem.value 
      }
    })

    const dataValuesArr=dataValueInAbsolute.map(elem=>Object.values(elem)) //массив типа [["Вологодский", 12]]
    const dataLabels=dataValuesArr.map(elem=>elem[0])//массив типа [["Вологодский", "Грязовецкий"]]
    const dataValues=dataValuesArr.map(elem=>elem[1])//массив типа [[12, 2]]
    const summ=dataValues.reduce((a,b)=>a+b) //25
    const dataValuesPercent=dataValues.map(elem=>elem/summ*100)
  

provide('dataValueInPercent', dataValueInPercent)
provide('label', label)
provide('activeType', activeType)
provide('diagramType', diagramType)
</script>

<template>
  <iToggleTypeOfDiagram />
  <iHorizontalDiagram v-if="activeType === diagramType[1]" />
  <iSemiDonutChart v-else :title="label" :percentage="dataValuesPercent" :labelsList="dataLabels"  />
</template>

<style scoped></style>
