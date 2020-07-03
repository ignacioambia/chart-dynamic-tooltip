<template>

<div class="card">
    <div>
        Content goes here
    </div>
    <div class="details-btn noselect" @click="toggle">
        details  <i class=" ml-2 fas fa-plus-square"></i>
    </div>

    <div class="card-extra-section" :class="{'collapsed': !detailsOpen}">
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        <p>Extra content goes here</p>
        
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

    ,

    mounted(){
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

.card-extra-section{
    overflow: hidden;
    transition: max-height 0.5s ease-out;
    height : auto;
    max-height: 1000px;

}

.card-extra-section.collapsed{
    max-height: 0;
}

</style>