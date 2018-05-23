<template>
  <v-layout align-center justify-center fill-height pa-2>
    <v-layout v-if="!isTriangle" :style="style" :class="shape">
    </v-layout>
    <triangle v-else :size="size" :color="color" :outline="outline">
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
  props: ['shape', 'color', 'id', 'outline'],
  components: {
    Triangle
  },
  computed: {
    size () {
      return 64
    },
    isTriangle () {
      return this.shape === 'triangle'
    },
    style () {
      if(this.outline === null || this.outline === undefined) {
        return {
          background: this.color
        }
      }
      else {
        return {
          border: `2px solid ${this.color}`
        }
      }
    }
  }
}
</script>

