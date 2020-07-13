<template>
    <div class="custom-tooltip"
    :style="{'top' : top, 'left' : left, 'opacity' :  opacity}">
        <div class="custom-tooltip-header">
            {{title}}
        </div>

        <div>
            <slot></slot>
        </div>

        <!-- <div v-for="item in averages" :key="item.item">
            <tooltip-bar :info="item" arrow>{{item.item}}</tooltip-bar>
        </div> -->
        <tree-item v-for="item in averages" :key="item.item" :item="item">

        </tree-item>

        <tooltip-bar :info="{'average' : average}" bold style="margin-top: 20px;">Average</tooltip-bar>


    </div>
</template>

<script>
import TooltipBar from './TooltipBar'
import TreeItem from './TreeItem'

    export default {
        name : 'custom-tooltip',
        components : {
            TooltipBar, TreeItem
        },

        data(){
            return {
                top : '0px',
                left : '0px',
                opacity : 0,
                title : '',
                averages : [],
                average : 0,
                tooltipsToKeepOpen : []

            }
        },

        computed : {

        },

        methods : {
            keepTooltipOpen(index){
                if(!this.tooltipsToKeepOpen.includes(index)){
                    console.log('Adding tooltip to those that we must keep open')
                    this.tooltipsToKeepOpen.push(index)
                    let openTooltip = Object.assign({},this)
                    openTooltip.opacity = 1
                }else{
                    console.log('Tooltip already added to list')
                }

                console.log(this.tooltipsToKeepOpen)

            },

            isKeptOpen(index){
                if(this.tooltipsToKeepOpen.includes(index)){
                    return true
                }
                return false
            }
        },

        watch : {
            opacity(){
                if(this.opacity != 0){
                    //bringing element to the front of the screen
                    this.$el.style.zIndex = 1000
                }else{
                    //sending element to the back of the screen
                    this.$el.style.zIndex = -1000
                }
            }
        },

        mounted(){
            
              this.$el.addEventListener('mouseout',()=>{
                  this.opacity = 0
              })

                this.$el.addEventListener('mouseover',()=>{
                  this.opacity = 1
              })
        }
    }
</script>

<style scoped>
.custom-tooltip{
    background-color: rgb(26, 26, 26);
    color : white!important;
    position: absolute;
    font-family: 'Helvetica Neue', 'Helvetica', 'Arial', sans-serif;
    font-size: 12px;
    padding: 6px 6px;
    font-style: normal;
    border-radius: 5px;
    padding: 5px;
    margin: 5px;
    transition : .2s;
    z-index: -1000;
}

.custom-tooltip-header{
    text-align: center;
    font-size: 13px;
    font-weight: bold;
    margin-bottom: 12px;

}

</style>