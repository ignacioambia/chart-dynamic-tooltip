<template>
  <div class="card">
    <div>
        Content goes here
    </div>
    <div class="details-btn noselect" @click="toggle">
        details  <i class=" ml-2 fas fa-plus-square"></i>
    </div>


        <div v-show="detailsOpen">
            Extra content goes here
        </div> 

   

  </div>
</template>

<script>
export default {
    data(){
        return {
            detailsOpen : false
        }
    },

    methods : {
        toggle(){
            this.detailsOpen = !this.detailsOpen
        }
    }
}
</script>

<style scoped>

.card{
    border-radius: 3px;
    border : 1px solid rgb(177, 177, 177);
    padding : 5px;
    margin: 5px;
    font-family: Arial, Helvetica, sans-serif;
    height: fit-content;
    transition: height 1s;

}

/* .card:hover{
    height : 100px;
} */

.details-btn{
    display: flex;
    justify-content: flex-end;
    color :rgb(136, 136, 136);
    cursor: pointer;
}


.ml-2{
    margin-left : .2rem;
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

.smooth-enter-active, .smooth-leave-active {
  transition: height .5s;
  /* overflow: hidden; */
}
.smooth-enter, .smooth-leave-to {
  height: 100px;
}

.display-none{
    display : none
}
</style>