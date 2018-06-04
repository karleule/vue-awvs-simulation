<template>
  <div style="width: 552px; height:312px;">
      <simulation v-if="started"></simulation>
      <hello v-else @start="started = true"></hello>
  </div>
</template>

<script>
import Simulation from './components/Simulation'
import Hello from './components/Hello'

export default {
  components: {
    Simulation,
    Hello
  },
  data () {
    return {
      started: false
    }
  }
}
</script>

