<template>
<div>
    <div @click="toggle()">
        <tooltip-bar
        :arrow="isFolder"
        :info="{'average' : info.average}"> 
            {{info.item}} 
        </tooltip-bar>
    </div>
    <div v-show="isOpen" style="margin-left : 10px;">
        <div v-if="isFolder" >
            <tree-test v-for="(item, index) in info.children" :key="index" :info="item">

            </tree-test>
        </div>

    </div>
    
</div>

</template>

<script>

import TooltipBar from './TooltipBar'


export default {
    name : 'tree-test',
    components : { TooltipBar },

    data(){
        return {
            isOpen : false
        }
    },

    props : {
        info : Object
    },

    computed : {
        isFolder(){
            let result = (this.info.children && this.info.children.length) ? true : false
            return result
        }
    },

    methods : {
        toggle(){
            this.isOpen = !this.isOpen
        }
    },

    mounted(){
        console.log(this.info)
    }
}
</script>

<style>

</style>