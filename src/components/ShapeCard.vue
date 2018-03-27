<template>
  <v-layout align-center justify-center style="border: 1px solid black;" fill-height pa-2>
    <v-layout v-if="!isTriangle" :style="style" :class="shape">
    </v-layout>
    <triangle v-else :size="size">
    </triangle>
  </v-layout>
</template>

<style>
  .circle {
    border-radius: 50%
  }

  .square {
    border-radius: 0%
  }
</style>


<script>

import Triangle from '../components/Triangle.vue'

export default {
  props: ['shape', 'color', 'id'],
  components: {
    Triangle
  },
  data () {
    return {
      style: {
        background: this.color
      }
    }
  },
  computed: {
    size () {
      return 150
    },
    isTriangle () {
      return this.shape === 'triangle'
    }
  }
}
</script>

