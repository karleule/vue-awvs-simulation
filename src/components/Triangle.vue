<template>
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="48" height="48" :style="style">
  <polygon :style="style" points="0,48 24,0 48,48"/>
</svg>
</template>

<script>
export default {
  props: ['size', 'outline', 'color'],
  computed: {
    style () {
      if(this.outline === null || this.outline === undefined) {
        return {
          fill: this.color
        }
      } else {
        return {
          fill: 'transparent',
          stroke: this.color,
          strokeWidth: 2
        }
      }
    }
  }
}
</script>

