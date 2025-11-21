<template>
  <div>{{ state.color }}</div>
  <NovaColorPicker
    :preset="preset"
    :value="state.color"
    @update="onUpdate"
    alpha
  ></NovaColorPicker>
</template>

<script>
import { reactive } from 'vue'
import { NovaColorPicker } from '@jiangshengdev/nova-next'
import '@jiangshengdev/nova-next/dist/css/themes.css'
import '@jiangshengdev/nova-next/dist/css/dropdown.css'
import '@jiangshengdev/nova-next/dist/css/color-picker.css'

const preset = [
  '#dc143c',
  '#f0e68c',
  '#8fbc8f',
  '#00ced1',
  '#1e90ff',
  '#663399',
  '#708090',
]

export default {
  components: {
    NovaColorPicker,
  },
  setup() {
    const state = reactive({
      color: '#663399',
    })

    function onUpdate(color) {
      state.color = color
    }

    return {
      state,
      onUpdate,
      preset,
    }
  },
}
</script>
