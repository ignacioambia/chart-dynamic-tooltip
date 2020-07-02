<template>
    <div class="custom-tooltip"
    :style="{'top' : top, 'left' : left, 'opacity' :  opacity}">
        <div class="custom-tooltip-header">
            {{title}}
        </div>

        <div>
            <slot></slot>
        </div>

        <div v-for="item in averages" :key="item.item">
            <tooltip-bar :percentage="item.average">{{item.item}}</tooltip-bar>
        </div>

        <tooltip-bar :percentage="average" bold style="margin-top: 20px;">Average</tooltip-bar>


    </div>
</template>

<script>
import TooltipBar from './TooltipBar'

    export default {
        name : 'custom-tooltip',
        components : {
            TooltipBar
        },

        data(){
            return {
                top : '0px',
                left : '0px',
                opacity : 0,
                title : '',
                averages : [],
                average : 0

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
    background-color: rgb(24, 24, 24);
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
}

.custom-tooltip-header{
    text-align: center;
    font-size: 13px;
    font-weight: bold;
    margin-bottom: 12px;

}
</style>