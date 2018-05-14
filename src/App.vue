<template>
  <v-app id="inspire">
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <div class="pa-3" style="border: 1px solid lightgrey;">
            <v-layout>
              <v-layout column>
                <v-flex v-for="(item,index) in startItems" :key="index">
                  <v-layout>
                    <v-flex v-for="(item2,index2) in item" :key="index2">
                      <drag drop-effect="copy" style="height:64px; width:64px; border: 1px solid lightgrey;">
                        <v-layout align-center justify-center class="title">
                          {{item2}}
                        </v-layout>
                      </drag>                  
                    </v-flex>
                  </v-layout>
                </v-flex>
              </v-layout>
            </v-layout>
          </div>
          <div class="pa-3" style="border: 1px solid lightgrey;">
            <v-layout>
              <v-layout column>
                <v-flex v-for="(item,index) in goalItems" :key="index">
                  <v-layout>
                    <v-flex v-for="(item2,index2) in item" :key="index2">
                      <drop @drop="dropItem(item2, ...arguments)" style="height:64px; width:64px; border: 1px solid lightgrey;">
                        <v-layout align-center justify-center class="title" style="color:red">
                          {{item2}}
                        </v-layout>
                      </drop>                  
                    </v-flex>
                  </v-layout>
                </v-flex>
              </v-layout>
            </v-layout>
          </div>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  components: {
  },
  data: () => ({
    title: 'awvs',
    drawer: null,
    startItems:[[1,2,3,4],[5,6,7,8],[9,10,11,12]],
    goalItems: [[1,2,3],[4,5,6],[7,8,9,]],
  }),
  methods: {
    dropItem: (index, transferData, nativeEvent) => {
      console.log(index)
    }
  }
}
</script>