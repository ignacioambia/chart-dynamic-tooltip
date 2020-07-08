<template>
  <div>
      <div @click="toggle()">
          <tooltip-bar
          :arrow="isFolder"
          :info="{'average' : item.average}"> 
              {{item.item}} 
          </tooltip-bar>
      </div>
      <div v-show="isOpen" style="margin-left : 10px; margin-bottom : 15px">
          <div v-if="isFolder" >
              <tree-item v-for="(item, index) in item.children" :key="index" :item="item">

              </tree-item>
          </div>

      </div>
      
  </div>

</template>


<script>
import TooltipBar from './TooltipBar'

export default {
    name : 'tree-item',
    components : {
        TooltipBar
    },

    props : {
        item : Object
    },

    data() {
      return {
        isOpen: false,
        previousFolderState : null
      }
    },

    computed: {
        isFolder(){
            let result = (this.item.children && this.item.children.length) ? true : false
            return result
        }
    },

    methods: {
      toggle() {
        if (this.isFolder) {
          this.isOpen = !this.isOpen
        }

      },

      showSupervisor(){
          console.log(this.$parent.$children)
      },

      storeCurrentState(){
          this.previousFolderState = this.isOpen
      },

      restoreToPreviousState(){
          this.isOpen = this.previousFolderState
      }

    }


}
</script>

<styles scoped>
.ml-3{
    margin-left : 3em;
}
</styles>