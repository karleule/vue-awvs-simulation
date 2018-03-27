<template>
  <v-layout align-center justify-center style="border: 1px solid black;" fill-height pa-2>
    <v-layout :style="style">
      {{id}}
    </v-layout>
  </v-layout>
</template>

<style>
  
</style>


<script>
export default {
  props: ['shape', 'color', 'id'],
  data () {
    return {
      style: {
        background: this.color
      }
    }
  }
}
</script>

