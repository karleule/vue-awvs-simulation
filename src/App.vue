<template>
  <v-app id="inspire">
    <v-content>
      <v-container fluid fill-height>
        <v-layout justify-center align-center column>
          <v-card>
            <v-card-text>            
              <v-layout>
                <div class="pa-3" style="border: 1px solid lightgrey;" >
                  <v-container grid-list-xs>
                    <v-layout row wrap style="max-height: 192px; max-width:256px;"> 
                     <v-flex xs3 v-for="(item,index) in startItems" :key="item.id">    
                       <template v-if="!solved">
                          <drag v-if="item.data !== null" :transfer-data="item.data" style="height:64px; width:64px; border: 1px solid lightgrey;">
                            <shape-card :color="item.data.color" :shape="item.data.shape"></shape-card>
                          </drag>
                          <drop v-else @drop="handleStartDrop(index, ...arguments)"  style="height:64px; width:64px; border: 1px solid lightgrey;">
                            {{item.data}}
                          </drop>
                       </template>    
                       <template v-else>
                         <div style="height:64px; width:64px; border: 1px solid lightgrey;">
                         </div>
                       </template>            
                    </v-flex>
                    </v-layout>
                  </v-container>
                </div>
                <div class="pa-3" style="border: 1px solid lightgrey;">
                  <v-container grid-list-xs>
                    <v-layout row wrap style="max-height: 192px; max-width:192px;">
                      <v-flex xs4 v-for="(item, index) in goalItems" :key="item.id">
                        <template v-if="!solved">
                          <drop v-if="item.data === null" @drop="handleGoalDrop(index, ...arguments)"  style="height:64px; width:64px; border: 1px solid lightgrey;">
                            <shape-card :color="item.style.color" :shape="item.style.shape" outline></shape-card>
                          </drop>
                          <drag v-else :transfer-data="item.data" style="height:64px; width:64px; border: 1px solid lightgrey;">
                            <shape-card :color="item.data.color" :shape="item.data.shape"></shape-card>
                          </drag>
                       </template>    
                       <template v-else>
                         <div style="height:64px; width:64px; border: 1px solid lightgrey;">
                          <v-icon color="success" v-if="isCorrect(index)" x-large>
                            check
                          </v-icon>
                          <v-icon v-else color="error" x-large>
                            close
                          </v-icon>
                         </div>
                       </template>  
                      </v-flex>
                    </v-layout>
                  </v-container>
                </div>
            </v-layout>
            </v-card-text>
            <v-card-actions class="pr-3">
              <v-spacer></v-spacer>
              <v-btn @click.stop="solve" color="primary">
                Solve
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import ShapeCard from '@/components/ShapeCard'
import findIndex from 'lodash/findIndex'
import cloneDeep from 'lodash/cloneDeep'
import isNil from 'lodash/isNil'

export default {
  components: {
    ShapeCard
  },
  data: () => ({
    title: 'awvs',
    drawer: null,
    solved: false,
    startItems: [
      {
        id: 0,
        data: {
          color: 'red',
          shape: 'square',
          goal: -1
        }  
      },
      { 
        id: 1,
        data: {
          color: 'green',
          shape: 'circle',
          goal: 1
        }
      },
      {
        id: 2,
        data: {
          color: '#e6e600',
          shape: 'circle',
          goal: 2
        }
      },
      {
        id: 3,
        data: {
          color: 'red',
          shape: 'triangle',
          goal: 4
        }
      },
      {
        id: 4,
        data: {
          color: 'blue',
          shape: 'circle',
          goal: -1
        }
      },
      {
        id: 5,
        data: {
          color: 'green',
          shape: 'square',
          goal: 5
        }
      },
      {
        id: 6,
        data: {
          color: 'red',
          shape: 'circle',
          goal: 3
        }
      },
      {
        id: 7,
        data: {
          color: 'blue',
          shape: 'square',
          goal: 6
        }
      },
      {
        id: 8,
        data: {
          color: 'blue',
          shape: 'triangle',
          goal: 8
        }
      },
      {
        id: 9,
        data: {
          color: 'green',
          shape: 'triangle',
          goal: 0
        }
      },
      {
        id: 10,
        data: {
          color: '#e6e600',
          shape: 'triangle',
          goal: 7
        }
      },
      {
        id: 11,
        data: {
          color: '#e6e600',
          shape: 'square',
          goal: -1
        }
      }
    ], 
    goalItems: [
      {
        id: 12,
        data: null,
        style: {
          color: 'red',
          shape: 'circle'
        }
      },
      {
        id: 13,
        data: null,
        style: {
          color: 'blue',
          shape: 'triangle'
        }
      },
      {
        id: 14,
        data: null,
        style: {
          color: 'blue',
          shape: 'square'
        }
      },
      {
        id: 15,
        data: null,
        style: {
          color: 'green',
          shape: 'square'
        }
      },
      {
        id: 16,
        data: null,
        style: {
          color: '#e6e600',
          shape: 'triangle'
        }
      },
      {
        id: 17,
        data: null,
        style: {
          color: 'red',
          shape: 'square'
        }
      },
      {
        id: 18,
        data: null,
        style: {
          color: 'red',
          shape: 'triangle'
        }
      },
      {
        id: 19,
        data: null,
        style: {
          color: '#e6e600',
          shape: 'circle'
        }
      },
      {
        id: 20,
        data: null,
        style: {
          color: 'green',
          shape: 'circle'
        }
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
    handleGoalDrop(index, data) {
      let deleteIndex = findIndex(this.startItems, (item) => {
        return item.data === data
      })
      let isStart = deleteIndex > -1
      if (isStart) {
        this.goalItems[index].data = data
        this.startItems[deleteIndex].data = null
      } else {
        deleteIndex = findIndex(this.goalItems, (item) => {
          return item.data === data
        })
        this.goalItems[index].data = data
        this.goalItems[deleteIndex].data = null
      }
    },
    handleStartDrop(index, data) {
      let deleteIndex = findIndex(this.goalItems, (item) => {
        return item.data === data
      })
      let isGoal = deleteIndex > -1
      if (isGoal) {
        this.startItems[index].data = data
        this.goalItems[deleteIndex].data = null
      } else {
        deleteIndex = findIndex(this.startItems, (item) => {
          return item.data === data
        })
        this.startItems[index].data = data
        this.startItems[deleteIndex].data = null
      }
    },
    solve() {
      this.solved = true
    },
    isCorrect (index) {
      let data = this.goalItems[index].data
      if (isNil(data)) {
        return false
      } else {
        if (data.goal === index) {
          return true
        } else {
          return false
        }
      }
    }
  }
}
</script>
