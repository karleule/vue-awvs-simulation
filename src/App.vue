<template>
  <v-app id="inspire">
    <v-content>
      <v-container fluid fill-height>
        <v-layout justify-center align-center column>
          <awvs-simulation></awvs-simulation>
        </v-layout>
      </v-container> 
    </v-content>
  </v-app>
</template>

<script>
import AwvsSimulation from './components/AwvsSimulation'

export default {
  components: {
    AwvsSimulation
  }
}
</script>
