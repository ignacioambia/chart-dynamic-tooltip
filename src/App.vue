<template>
<div>
  <canvas id="chart"></canvas>
  <custom-tooltip ref="custom_tooltip"></custom-tooltip>


</div>
</template>

<script>
import Chart from 'chart.js'
import CustomTooltip from './components/CustomTooltip'


var data = {"May 2020":[{"item":"Chihuahua","average":"0.0","month":"May","month_number":"5","year":"2020","month_year":"May 2020"},{"item":"Guadalajara","average":"49.132231404958674","month":"May","month_number":"5","year":"2020","month_year":"May 2020"},{"item":"Merida","average":"96.014067995310668","month":"May","month_number":"5","year":"2020","month_year":"May 2020"},{"item":"Mexico City","average":"57.04366610091035","month":"May","month_number":"5","year":"2020","month_year":"May 2020"},{"item":"Mexico City Airport","average":"46.299483648881242","month":"May","month_number":"5","year":"2020","month_year":"May 2020"},{"item":"Monterrey","average":"85.546875","month":"May","month_number":"5","year":"2020","month_year":"May 2020"},{"item":"Puebla","average":"91.582229150428688","month":"May","month_number":"5","year":"2020","month_year":"May 2020"},{"item":"Querétaro","average":"49.390681003584227","month":"May","month_number":"5","year":"2020","month_year":"May 2020"},{"item":"Average","average":"62.564961311929778","month":"May","month_number":"5","year":"2020","month_year":"May 2020"}],"February 2020":[{"item":"Guadalajara","average":"73.781676413255354","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Merida","average":"98.822463768115938","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Mexico City","average":"67.258458767528623","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Mexico City Airport","average":"63.30946957370648","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Monterrey","average":"85.813630041724622","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Puebla","average":"86.504217432052485","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Querétaro","average":"72.603406326034062","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Average","average":"72.21297126510396","month":"February","month_number":"2","year":"2020","month_year":"February 2020"}],"March 2020":[{"item":"Guadalajara","average":"77.245308310991959","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Merida","average":"99.487617421007684","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Mexico City","average":"63.771381747413699","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Mexico City Airport","average":"57.767236998136539","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Monterrey","average":"87.195121951219505","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Puebla","average":"94.441974210760335","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Querétaro","average":"67.5137653536637","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Average","average":"71.128251121076232","month":"March","month_number":"3","year":"2020","month_year":"March 2020"}],"January 2020":[{"item":"Guadalajara","average":"81.897555296856808","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Merida","average":"99.196787148594382","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Mexico City","average":"69.505428226779259","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Mexico City Airport","average":"65.159809288363064","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Monterrey","average":"90.347648261758692","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Puebla","average":"83.217431617987941","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Querétaro","average":"67.917737789203088","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Average","average":"74.762717922242956","month":"January","month_number":"1","year":"2020","month_year":"January 2020"}],"April 2020":[{"item":"Guadalajara","average":"82.926829268292678","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Merida","average":"97.85407725321889","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Mexico City","average":"40.0","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Mexico City Airport","average":"53.896103896103895","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Monterrey","average":"80.753138075313814","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Puebla","average":"90.140845070422543","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Querétaro","average":"45.967741935483872","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Average","average":"70.984126984126988","month":"April","month_number":"4","year":"2020","month_year":"April 2020"}]}
export default {
  name : 'app',
  components : {
    CustomTooltip
  },

  data(){
    return {
      chart_info : {
        labels : ['hola','como','estas']
      },

      users : [
        {
          name : 'Ignacio',
          value : 45
        },
        {
          name : 'Jorge',
          value : 70
        },
        {
          name : 'Susana',
          value :  22
        },
      ]
    }
  },

  watch :{
    chart_info(){
      this.updateChart()
    }
  },

  methods : {
    updateChart(){
      this.chart = new Chart(document.getElementById('chart'),{
      type : 'line',
      data : {
        labels : this.chart_info.labels,
        datasets : [
          {
            label : 'product',
             data  : [1,2,4]
          }
        ]

        },

        options :{
          tooltips : {
            enabled : false,
            custom : tooltipModel => {

              let customTooltip = this.$refs['custom_tooltip']

              if(tooltipModel.opacity == 0){
                customTooltip.opacity = 0
                return;
              }

              customTooltip.$el.addEventListener('mouseout',()=>{
                  customTooltip.opacity = 0
              })

                customTooltip.$el.addEventListener('mouseover',()=>{
                  customTooltip.opacity = 1
              })

              customTooltip.opacity = 1

              let chartPosition = this.chart.canvas.getBoundingClientRect()
              let tooltipPosition = customTooltip.$el.getBoundingClientRect()

              //assigning top position of tooltip
              customTooltip.top =  chartPosition.top + window.pageYOffset + tooltipModel.caretY + 'px'

              //assigning left position of tooltip
              let finalPosition = chartPosition.left + window.pageXOffset + tooltipModel.caretX
              if(window.innerWidth < finalPosition + tooltipPosition.width ){
                customTooltip.left = finalPosition - tooltipPosition.width - 10 + 'px'
              }else{
                customTooltip.left = finalPosition +'px'
              }
              

            }
          }
        }
      })
    },

    action(){
        console.log('taking action')
    }
  },

  mounted(){
    this.updateChart()

    console.log(this.$refs['custom_tooltip'])
  }
  
}

</script>

<style>

</style>
