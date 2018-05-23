<template>
  <v-app id="inspire">
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <div class="pa-3" style="border: 1px solid lightgrey;">
            <v-container grid-list-xs>
              <v-layout row wrap justify-space-around>
                <v-flex xs3 v-for="(item, index) in startItems" :key="index">
                  <drag v-if="item.payload !== null" :transfer-data="item.payload" style="height:64px; width:64px; border: 1px solid lightgrey;">
                    <shape-card :color="item.payload.color" :shape="item.payload.shape"></shape-card>               
                  </drag>
                  <div v-else style="height:64px; width:64px; border: 1px solid lightgrey;">
                  </div>
              </v-flex>
              </v-layout>
            </v-container>
          </div>
          <div class="pa-3" style="border: 1px solid lightgrey;">
            <v-container grid-list-xs>
              <v-layout row wrap>
                <v-flex xs4 v-for="(item, index) in goalItems" :key="index">
                  <drop @drop="handleDrop(index, ...arguments)" style="height:64px; width:64px; border: 1px solid lightgrey;">
                    <shape-card :color="item.color" :shape="item.shape" :outline="item.outline"></shape-card>  
                  </drop>
                </v-flex>
              </v-layout>
            </v-container>
          </div>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import ShapeCard from '@/components/ShapeCard'

export default {
  components: {
    ShapeCard
  },
  data: () => ({
    title: 'awvs',
    drawer: null,
    startItems: [
      {
        payload: {
          color: 'red',
          shape: 'square',
          index: 0
        }
      },
      {
        payload: {
          color: 'green',
          shape: 'circle',
          index: 1
        }
      },
      {
        payload: {
          color: '#e6e600',
          shape: 'circle',
          index: 2
        }
      },
      {
        payload: {
          color: 'red',
          shape: 'triangle',
          index: 3
        }
      },
      {
        payload: {
          color: 'blue',
          shape: 'circle',
          index: 4
        }
      },
      {
        payload: {
          color: 'green',
          shape: 'square',
          index: 5
        }
      },
      {
        payload: {
          color: 'red',
          shape: 'circle',
          index: 6
        }
      },
      {
        payload: {
          color: 'blue',
          shape: 'square',
          index: 7
        }
      },
      {
        payload: {
          color: 'blue',
          shape: 'triangle',
          index: 8
        }
      },
      {
        payload: {
          color: 'green',
          shape: 'triangle',
          index: 9
        }
      },
      {
        payload: {
          color: '#e6e600',
          shape: 'triangle',
          index: 10
        }
      },
      {
        payload: {
          color: '#e6e600',
          shape: 'square',
          index: 11
        }
      }
    ], 
    goalItems: [
      {
        color: 'red',
        shape: 'circle',
        outline : true
      },
      {
        color: 'blue',
        shape: 'triangle',
        outline : true
      },
      {
        color: 'blue',
        shape: 'square',
        outline : true
      },
      {
        color: 'green',
        shape: 'square',
        outline : true
      },
      {
        color: '#e6e600',
        shape: 'triangle',
        outline : true
      },
      {
        color: 'red',
        shape: 'square',
        outline : true
      },
      {
        color: 'red',
        shape: 'triangle',
        outline : true
      },
      {
        color: '#e6e600',
        shape: 'circle',
        outline : true
      },
      {
        color: 'green',
        shape: 'circle',
        outline : true
      }
    ], 
    startOptions: {
      sort: false,
      group: {
        name: 'awsList'
      }
    },
    goalOptions: {
      sort: false,
      group: {
        name: 'awsList',
        put: false
      }
    }
  }),
  methods: {
    handleDrop(index, data) {
      this.goalItems[index].shape = data.shape
      this.goalItems[index].color = data.color
      this.goalItems[index].outline = undefined
      this.startItems[data.index].payload = null
    }
  }
}
</script>
