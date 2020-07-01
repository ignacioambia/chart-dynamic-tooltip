<template>
    <div class="bar" >
        <div class="text-content" :class="{'text-bold' : bold}" >
            <div>
                <slot></slot>
            </div>
            <div>
                {{percentage.toFixed(2)}} {{concept}}
            </div>
        </div>
        <div class="bar-content " :class="background_color" :style="{'width' : percentage + '%'}"></div>
    </div>
</template>

<script>
    export default {
       name : 'tooltip-bar',

       props : {
           percentage : {
               type : Number,
               default : 0
           },
           concept : {
               type : String,
               default : '%'
           },

           bold : {
               type : Boolean,
               default : false
           }
       },

       methods : {
           action(){
               console.log('Taking action directly')
           }
       },

       created(){
           console.log('Per : ' + this.percentage)
           console.log('Bold : ' + this.bold)
       },

       computed : {
           background_color(){
               if(this.percentage >= 50){
                   return 'green'
               }

               if(this.percentage >= 50/2 && this.percentage<50){
                   return 'yellow'
               }
               return 'red'
           }
       }
    }
</script>

<style scoped>
.bar{
    background-color: gray;
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
    margin : 5px;
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

</style>