<template>

    <div>
        <div>
            <!-- <user-card 
                @toggle-supervisor="toggle" 
                :user_info="item" 
                :key="item.id_user"
                @child-is-shown="showSupervisor"></user-card> -->
                <tooltip-bar  :arrow="item.children ? true : false"
                    :info="{'average' : item.average}"
                    @show-details = "toggle()"
                    >{{item.item}}</tooltip-bar>
        </div>
        <div v-show="isOpen" v-if="isFolder" class="ml-3" style="margin-left : 25px; margin-bottom : 12px;">
            <tree-item 
            v-for="(child, index) in item.children"
            :key="index"
            :item="child"
            ></tree-item>
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
      isFolder() {
        return this.item.children &&
          this.item.children.length
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