<template>
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
                    <img height="64px; width: 64px;" :src="item.image" style="max-height:64px; max-width:64px;">
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
                  <div v-if="item.data === null" style="height:64px; width:64px; border: 1px solid lightgrey;">        
                  </div>
                  <div v-else style="height:64px; width:64px; border: 1px solid lightgrey;">                   
                    <img height="64px; width: 64px;" :src="item.data.image" style="max-height:64px; max-width:64px;">
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
      <v-btn v-if="!solved" :disabled="!introSoundEnded" @click.stop="solve" style="background: #5A2572; color: white;">
        Aufdecken
      </v-btn>
      <v-btn v-else :disabled="!introSoundEnded" color="success">
        Fertig
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import ShapeCard from './components/ShapeCard'
import findIndex from 'lodash/findIndex'
import cloneDeep from 'lodash/cloneDeep'
import isNil from 'lodash/isNil'

export default {
    components: {
    ShapeCard
  },
  data: () => ({
    title: 'awvs',
    solved: false,
    introSoundEnded: false,
    startItems: [
      {
        id: 0,
        image: './static/white.png',
        data: {
          color: 'red',
          shape: 'square',
          goal: -1,
          image: './static/white.png',
        }  
      },
      { 
        id: 1,
        image: './static/Logo_AVWS-Forschung_RGB_1.png',
        data: {
          color: 'green',
          shape: 'circle',
          goal: 1,
          image: './static/Logo_AVWS-Forschung_RGB_2.png',
        }
      },
      {
        id: 2,
        image: './static/Logo_AVWS-Forschung_RGB_2.png',
        data: {
          color: '#e6e600',
          shape: 'circle',
          goal: 2,
          image: './static/Logo_AVWS-Forschung_RGB_3.png',
        }
      },
      {
        id: 3,
        image: './static/Logo_AVWS-Forschung_RGB_3.png',
        data: {
          color: 'red',
          shape: 'triangle',
          goal: 4,
          image: './static/Logo_AVWS-Forschung_RGB_5.png'
        }
      },
      {
        id: 4,  
        image: './static/white.png',
        data: {
          color: 'blue',
          shape: 'circle',
          goal: -1,
          image: './static/white.png',
        }
      },
      {
        id: 5,
        image: './static/Logo_AVWS-Forschung_RGB_4.png',
        data: {
          color: 'green',
          shape: 'square',
          goal: 5,
          image: './static/Logo_AVWS-Forschung_RGB_6.png',
        }
      },
      {
        id: 6,
        image: './static/Logo_AVWS-Forschung_RGB_5.png',
        data: {
          color: 'red',
          shape: 'circle',
          goal: 3,
          image: './static/Logo_AVWS-Forschung_RGB_4.png',
        }
      },
      {
        id: 7,
        image: './static/Logo_AVWS-Forschung_RGB_6.png',
        data: {
          color: 'blue',
          shape: 'square',
          goal: 6,
          image: './static/Logo_AVWS-Forschung_RGB_7.png',
        }
      },
      {
        id: 8,
        image: './static/white.png',
        data: {
          color: 'blue',
          shape: 'triangle',
          goal: 8,
          image: './static/Logo_AVWS-Forschung_RGB_9.png',
        }
      },
      {
        id: 9,
        image: './static/Logo_AVWS-Forschung_RGB_7.png',    
        data: {
          color: 'green',
          shape: 'triangle',
          goal: 0,
          image: './static/Logo_AVWS-Forschung_RGB_1.png',
        }
      },
      {
        id: 10,
        image: './static/Logo_AVWS-Forschung_RGB_8.png',
        data: {
          color: '#e6e600',
          shape: 'triangle',
          goal: 7,
          image: './static/Logo_AVWS-Forschung_RGB_8.png',
        }
      },
      {
        id: 11,
        image: './static/Logo_AVWS-Forschung_RGB_9.png',
        data: {
          color: '#e6e600',
          shape: 'square',
          goal: -1,
          image: './static/white.png',
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
      let audio = new Audio('./static/BBW_AVWS_SOUND_BROWSERGAME_FINAL_Zusatz_320kb.mp3')
      audio.play();   
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
  },
  mounted () {
    let audio = new Audio('./static/BBW_AVWS_SOUND_BROWSERGAME_FINAL_320kb.mp3')
    audio.play()
    audio.onended = () => {
      this.introSoundEnded = true
    }
  }
}
</script>



