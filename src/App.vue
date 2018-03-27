<template>
  <v-app id="inspire">
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>      
        <v-container fluid fill-height>
          <v-layout row wrap>
            <v-flex
              xs4
              v-for="item in items"
              :key="item.id"
            >
              <shape-card v-bind="item">
              </shape-card>
            </v-flex>
          </v-layout>
        </v-container>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
  import ShapeCard from '././components/ShapeCard.vue'

  export default {
    components: {
      ShapeCard
    },
    data: () => ({
      title: 'awvs',
      drawer: null,
      items:[
        {
          id: 1,
          shape: 'triangle',
          color: 'green'
        },
        {
          id: 2,
          shape: 'triangle',
          color: 'green'
        },
        {
          id: 3,
          shape: 'triangle',
          color: 'green'
        },
        {
          id: 4,
          shape: 'triangle',
          color: 'green'
        },
        {
          id: 5,
          shape: 'triangle',
          color: 'green'
        },
        {
          id: 6,
          shape: 'triangle',
          color: 'green'
        },
        {
          id: 7,
          shape: 'triangle',
          color: 'green'
        },     
        {
          id: 8,
          shape: 'triangle',
          color: 'green'
        },   
        {
          id: 9,
          shape: 'triangle',
          color: 'green'
        },                
      ] 
    })
  }
</script>