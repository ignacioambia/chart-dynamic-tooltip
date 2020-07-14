<template>
  <div id="mydiv">
    <p>Move</p>
    <p>this</p>
    <p>DIV</p>
</div>
</template>

<script>
export default {

    methods : {

        dragElement() {
        var pos1 = 0, pos2 = 0, pos3 = 0, pos4 = 0;

            const  dragMouseDown = e => {
                e = e || window.event;
                e.preventDefault();
                // get the mouse cursor position at startup:
                pos3 = e.clientX;
                pos4 = e.clientY;
                document.onmouseup = closeDragElement;
                // // call a function whenever the cursor moves:
                document.onmousemove = elementDrag;
                console.log('We must drag element')
            }

            const elementDrag = e  => {
                console.log('dragging element')
                e = e || window.event;
                console.log(e)
                e.preventDefault();
                // calculate the new cursor position:
                pos1 = pos3 - e.clientX;
                pos2 = pos4 - e.clientY;
                pos3 = e.clientX;
                pos4 = e.clientY;
                // set the element's new position:
                this.$el.style.top = (this.$el.offsetTop - pos2) + "px";
                this.$el.style.left = (this.$el.offsetLeft - pos1) + "px";
            }

            const  closeDragElement = ()=> {
                /* stop moving when mouse button is released:*/
                document.onmouseup = null;
                document.onmousemove = null;
            }

            this.$el.onmousedown = dragMouseDown
        }

},
    mounted(){
        this.dragElement()
    }
}
</script>

<style scoped>
#mydiv {
  position: absolute;
  /* z-index: 9; */
  /* background-color: #f1f1f1;
  text-align: center;
  border: 1px solid #d3d3d3; */
}

#mydivheader {
  padding: 10px;
  cursor: move;
  z-index: 10;
  background-color: #2196F3;
  color: #fff;
}
</style>