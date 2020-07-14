<template>
    <div class="bar " :class="{'hoverable': arrow}" @click="showDetails" >
        <div class="text-content" :class="{'text-bold' : bold}" >
            <div>
                <i v-if="arrow" class="fa fa-angle-down" style="margin-right: 5px; color: white; opacity: 50%;"></i>
                <slot></slot>
            </div>
            <div>
                {{parseFloat(info.average).toFixed(2)}} {{concept}}
            </div>
        </div>
        <div class="bar-content " :class="background_color" :style="{'width' : info.average + '%'}"></div>
    </div>
</template>

<script>
    export default {
       name : 'tooltip-bar',

       props : {
           info : {
               type : Object
           },
           concept : {
               type : String,
               default : '%'
           },

           bold : {
               type : Boolean,
               default : false
           },
           arrow : {
            type : Boolean,
           default : false
           }


       },

       methods : {
           showDetails(){
               if(this.arrow){
                    console.log('Show details on element')
                    this.$emit('show-details')
               }
           }
       },

       created(){
       },

       computed : {
           background_color(){
               if(this.info.average >= 50){
                   return 'green'
               }

               if(this.info.average >= 50/2 && this.info.average<50){
                   return 'yellow'
               }
               return 'red'
           }
       }
    }
</script>

<style scoped>
.bar{
    background-color: rgb(100, 100, 100);
    border-radius: 5px;
    color: white;
    font-size: 13px;
    min-height: 20px;
    display: flex;
    position: relative;
    min-width: 200px;
    font-family: 'Helvetica', 'Arial', sans-serif;
    font-weight: normal!important;
    align-items: center;
    cursor: context-menu;
    margin : 5px 0px;
}

.bar.hoverable:hover{
    opacity: 85%;
}


.text-content{
    display: flex;
    justify-content: space-between;
    width: 100%;
    z-index: 1;
    margin-left: 8px;
}

.text-content>div{
    margin-right: 8px;
    font-weight: 300;
}

.bar-content{
    border-radius: 5px;
    right: 0px;
    position: absolute;
    height: 100%;
    z-index: 0;
}

.red{
    background-color: #a02c2cff;
}

.green{
    background-color: #008000ff;
}

.yellow{
    background-color: #d4aa00ff;
}

.text-bold>div{
    font-weight : bold;
}

.fa {
    margin-right: 10rem;
}

</style>