<template>
    <div class="custom-tooltip"
    :style="{'top' : top, 'left' : left, 'opacity' :  opacity}">
        <div class="custom-tooltip-header">
            January autorating
        </div>
        <tooltip-bar :percentage="44" >Ignacio Ambia</tooltip-bar>
        <tooltip-bar :percentage="70">Jorge Rangel</tooltip-bar>
        <tooltip-bar :percentage="22">Susana Torres</tooltip-bar>

        <tooltip-bar :percentage="35" bold style="margin-top: 20px;">Average</tooltip-bar>
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
                opacity : 0
            }
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