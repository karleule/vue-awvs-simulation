<template>
    <svg xmlns="http://www.w3.org/2000/svg" version="1.1" class="svg-triangle" :width='size' :height='size'>
    <path d="M 50,5 95,97.5 5,97.5 z"/>
  </svg>
</template>

<style>
  /* .svg-triangle {
  /*   border: 1px solid gray;
  } */

  .svg-triangle path {
    stroke-width: 5;
    stroke: black;
  }
</style>


<script>
export default {
  props: ['size']
}
</script>

