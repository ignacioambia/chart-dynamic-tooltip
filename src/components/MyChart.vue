<template>
  <div class="chart-container">
    <canvas :id="chart_id"></canvas>
  </div>
</template>

<script>
import Chart from 'chart.js'
import Vue from 'vue'
import CustomTooltip from './CustomTooltip'


export default {

    data(){
        return {
            chart : {}
        }
    },


    props : {
        name : String,
        info : Object
    },
    computed : {
        chart_id(){
            return this.name + '-chart'
        }
    },

    methods : {
        labels(){
            return Object.keys(this.info)
        },

        values(){
            let values = []
            for (const prop in this.info){
                values.push(
                {
                    y : this.info[prop].filter(obj=>obj.item == 'Average')[0].average,
                    details : this.info[prop].filter(obj=>obj.item != 'Average')
                } 
                )
            }

            return values
        }

    },

    

    // methods : {
    //     labels(){
    //         return Object.keys(this.info)
    //     },

    //     values(){
    //         let values = []
    //         for (const prop in this.info){
    //             values.push(
    //             {
    //                 y : this.info[prop].filter(obj=>obj.item == 'Average')[0].average,
    //                 details : this.info[prop].filter(obj=>obj.item != 'Average')
    //             } 
    //             )
    //         }

    //         return values
    //     }
    // },

    mounted(){


        let tooltip = Vue.extend(CustomTooltip)

        this.tooltip = new tooltip()

        this.tooltip.$mount()

        console.log(this.$root)


        this.$root.$el.appendChild(this.tooltip.$el)
        console.log(this.tooltip)



        this.chart = new Chart(document.getElementById(this.chart_id),{
            type : 'line',
            data : {
                labels : this.labels(),
                datasets : [
                    {
                        label : 'queso',
                        data : this.values()
                    }
                ]
            },
                        options :{

            onClick : (evt,chartElement) => {
                if(chartElement.length > 0){

                    this.tooltip.keepTooltipOpen(chartElement[0]._index)

                }
            },

            tooltips : {
                enabled : false,
                custom : tooltipModel => {


                if(tooltipModel.opacity == 0 ){
                    this.tooltip.opacity = 0
                    return;
                }

                let index = tooltipModel.dataPoints[0].index

                //as there is already an open tooltip showing this info, we shouldn't
                //show another one with the same info
                if( this.tooltip.isKeptOpen(index)){
                    return
                }

                this.tooltip.title = tooltipModel.title[0]
                
                this.tooltip.averages = this.chart.data.datasets[0].data[index].details
                this.tooltip.average = this.chart.data.datasets[0].data[index].y



                this.tooltip.opacity = 1

                let chartPosition = this.chart.canvas.getBoundingClientRect()
                let tooltipPosition = this.tooltip.$el.getBoundingClientRect()

                //assigning top position of tooltip
                this.tooltip.top =  chartPosition.top + window.pageYOffset + tooltipModel.caretY + 'px'

                //assigning left position of tooltip
                let finalPosition = chartPosition.left + window.pageXOffset + tooltipModel.caretX
                if(window.innerWidth < finalPosition + tooltipPosition.width ){
                    this.tooltip.left = finalPosition - tooltipPosition.width - 10 + 'px'
                }else{
                    this.tooltip.left = finalPosition +'px'
                }
                

     
            }
            }
                        }


        })

    }
}
</script>

<style>

</style>