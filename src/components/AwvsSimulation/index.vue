<template>
  <div style="width: 552px; height:312px;">
    <transition v-if="started" enter-active-class="animated fadeIn">
      <simulation ></simulation>          
    </transition>  
    <transition v-else leave-active-class="animated fadeOut">
      <hello @start="started = true"></hello>
    </transition> 
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

