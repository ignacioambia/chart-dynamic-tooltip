<template>
    <div
    v-if="!destroyTooltip"
    class="custom-tooltip  noselect"
    :style="{'top' : top, 'left' : left, 'opacity' :  opacity}">
        <div class="custom-tooltip-header">
            <div>
                {{title}}
            </div>
            
            <div>
                <div 
                v-show="forceKeepOpen" 
                @click="closeTooltip"
                class="tooltip-cross">
                    &#10005;
                </div>
            </div>
           
        </div>

        <tree-item v-for="item in averages" :key="item.item" :item="item">

        </tree-item>

        <tooltip-bar :info="{'average' : average}" bold style="margin-top: 20px;">Average</tooltip-bar>


    </div>
</template>

<script>
import TooltipBar from './TooltipBar'
import TreeItem from './TreeItem'
import _ from 'lodash'

_.remove()

    export default {
        name : 'custom-tooltip',
        components : {
            TooltipBar, TreeItem
        },

        data(){
            return {
                top : '',
                left : '',
                opacity : 0,
                title : '',
                averages : [],
                average : 0,
                forceKeepOpen : false,
                destroyTooltip : false,
                

            }
        },

        computed : {

        },

        methods : {
            closeTooltip(){
                this.destroyTooltip = true
                _.remove(this.chart.tooltipsToKeepOpen,num=>{
                   return  num == this.index
                })
            },

        },

        watch : {
            opacity(){
                if(this.opacity != 0){
                    //bringing element to the front of the screen
                    this.$el.style.zIndex = 1
                }else{
                    //sending element to the back of the screen
                    this.$el.style.zIndex = -1
                }
            }
        },

        mounted(){
            
              this.$el.addEventListener('mouseout',()=>{
                if(!this.forceKeepOpen)
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
    padding : 5px;
    padding-top: 10px;
}

.custom-tooltip-header{
    text-align: center;
    font-size: 13px;
    font-weight: bold;
    margin-bottom: 12px;
    display : flex;
    justify-content: space-between;

}

.tooltip-cross{
    margin-top: -.3rem;
    cursor: pointer;
}

.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
     -khtml-user-select: none; /* Konqueror HTML */
       -moz-user-select: none; /* Old versions of Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
            user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome, Edge, Opera and Firefox */
}


</style>