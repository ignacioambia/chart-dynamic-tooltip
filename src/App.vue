<template>
<div>
  
   <canvas id="chart"></canvas>
  <custom-tooltip ref="custom_tooltip">
  </custom-tooltip>


  <tree-test v-for="item in list" :key="item.item" :info="item">

  </tree-test>

<hr>



  <div v-for="(elem,index) in list" :key="index">
    {{elem.item}}
  </div>

  <button @click="addChildren()">
    Add user
  </button>


</div>
</template>

<script>
import Chart from 'chart.js'
import CustomTooltip from './components/CustomTooltip'
import TreeTest from './components/TreeTest'

export default {
  name : 'app',
  components : {
    CustomTooltip, TreeTest
  },

  data(){
    return {

      tooltipsToKeepOpen : [],

      list : [
        {
          item : 'Jorge',
          average : '12',
          children : [
            {
              item : 'Alan',
              average : '15',
              children : []
            },
            {
              item : 'Ariel',
              average : '18',
              children : [
                { 
                  item : 'Susana',
                  average : '100',
                },
                { 
                  item : 'Antonio',
                  average : '95',
                },
              ]
            }
          ]
        },
        {
          item : 'Viridiana',
          average : '13',
          children : [
            {
              item : 'Angelica',
              average : '33'
            },
            {
              item : 'Naomi',
              average : '22',
              children : [
                { 
                  item : 'Fernanda',
                  average : '65',
                },
                { 
                  item : 'Sofia',
                  average : '48',
                },
              ]
            }
          ]
        },
      ],

      customKey : '',
      keyCount : 0,

      prop : 'queso',

      users : [
      {
          item : 'Susana',
          average :  22,
          children : [
            {
              item : 'Cholo x',
              average : 12,
              children : [
                {
                  item : 'Ignacio Ambia',
                  average : 15
                }
              ]
            },
            {
              item : 'Cholo y',
              average : 80
            }
          ]
        },
        {
          item : 'Ignacio',
          average : 45
        },
        {
          item : 'Jorge',
          average : 70
        },

      ],

       info : {"Paul Molive 2020":[{"item":"Petey Cruiser.","average":"0.0","month":"Paul Molive","month_number":"5","year":"2020","month_year":"Paul Molive 2020",
        children : [
        {item : 'Employee 1', average : 35},
        {item : 'Employee 2', average : 22}]},
        {"item":"Anna Mull","average":"49.132231404958674","month":"Paul Molive","month_number":"5","year":"2020","month_year":"Paul Molive 2020"},{"item":"Rick O'Shea","average":"96.014067995310668","month":"Paul Molive","month_number":"5","year":"2020","month_year":"Paul Molive 2020"},{"item":"Walter Melon","average":"57.04366610091035","month":"Paul Molive","month_number":"5","year":"2020","month_year":"Paul Molive 2020"},{"item":"Gail Forcewind.","average":"46.299483648881242","month":"Paul Molive","month_number":"5","year":"2020","month_year":"Paul Molive 2020"},{"item":"Anna Sthesia","average":"85.546875","month":"Paul Molive","month_number":"5","year":"2020","month_year":"Paul Molive 2020"},{"item":"Bob Frapples","average":"91.582229150428688","month":"Paul Molive","month_number":"5","year":"2020","month_year":"Paul Molive 2020"},{"item":"Monty Carlo","average":"49.390681003584227","month":"Paul Molive","month_number":"5","year":"2020","month_year":"Paul Molive 2020"},{"item":"Average","average":"62.564961311929778","month":"Paul Molive","month_number":"5","year":"2020","month_year":"Paul Molive 2020"}],"February 2020":[{"item":"Anna Mull","average":"73.781676413255354","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Rick O'Shea","average":"98.822463768115938","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Walter Melon","average":"67.258458767528623","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Gail Forcewind.","average":"63.30946957370648","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Anna Sthesia","average":"85.813630041724622","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Bob Frapples","average":"86.504217432052485","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Monty Carlo","average":"72.603406326034062","month":"February","month_number":"2","year":"2020","month_year":"February 2020"},{"item":"Average","average":"72.21297126510396","month":"February","month_number":"2","year":"2020","month_year":"February 2020"}],"March 2020":[{"item":"Anna Mull","average":"77.245308310991959","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Rick O'Shea","average":"99.487617421007684","month":"March","month_number":"3","year":"2020","month_year":"March 2020", children : [{item : 'John Wick', average :35}]},{"item":"Walter Melon","average":"63.771381747413699","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Gail Forcewind.","average":"57.767236998136539","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Anna Sthesia","average":"87.195121951219505","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Bob Frapples","average":"94.441974210760335","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Monty Carlo","average":"67.5137653536637","month":"March","month_number":"3","year":"2020","month_year":"March 2020"},{"item":"Average","average":"71.128251121076232","month":"March","month_number":"3","year":"2020","month_year":"March 2020"}],"January 2020":[{"item":"Anna Mull","average":"81.897555296856808","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Rick O'Shea","average":"99.196787148594382","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Walter Melon","average":"69.505428226779259","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Gail Forcewind.","average":"65.159809288363064","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Anna Sthesia","average":"90.347648261758692","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Bob Frapples","average":"83.217431617987941","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Monty Carlo","average":"67.917737789203088","month":"January","month_number":"1","year":"2020","month_year":"January 2020"},{"item":"Average","average":"74.762717922242956","month":"January","month_number":"1","year":"2020","month_year":"January 2020"}],"April 2020":[{"item":"Anna Mull","average":"82.926829268292678","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Rick O'Shea","average":"97.85407725321889","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Walter Melon","average":"40.0","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Gail Forcewind.","average":"53.896103896103895","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Anna Sthesia","average":"80.753138075313814","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Bob Frapples","average":"90.140845070422543","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Monty Carlo","average":"45.967741935483872","month":"April","month_number":"4","year":"2020","month_year":"April 2020"},{"item":"Average","average":"70.984126984126988","month":"April","month_number":"4","year":"2020","month_year":"April 2020"}]}

    }
  },

  computed:{
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

  methods : {


    forceRender(el){
      this.customKey =  el.item + this.keyCount
    },

    addChildren(){

      if(!this.users[1].children){
        this.users[1].children = [{item : 'Paco', average : 85}]
        this.forceRender(this.users[1])

      }else{
        this.users[1].children.push({item : 'Paco', average : 85})
      }

      this.list.push('platano')
    },

    updateChart(){
      this.chart = new Chart(document.getElementById('chart'),{
      type : 'line',
      data : {
        labels : this.labels,
        datasets : [
          {
            label : 'product',
             data  : this.values
          }
        ],

        },




        options :{

          onClick : (evt,x)=>{ 
            console.log('Chart is clickted')
            console.log(evt)
            console.log(x)
        },

          tooltips : {

            enabled : false,
            custom : (tooltipModel) => {

              console.log(tooltipModel)


              let customTooltip = this.$refs['custom_tooltip']

              if(tooltipModel.opacity == 0){
                customTooltip.opacity = 0
                return;
              }

              customTooltip.title = tooltipModel.title[0]
              let index = tooltipModel.dataPoints[0].index
              customTooltip.averages = this.chart.data.datasets[0].data[index].details
              customTooltip.average = this.chart.data.datasets[0].data[index].y



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
        this.prop = 'hola'
    },


  },

  mounted(){
    this.updateChart()

    console.log(this.$refs['custom_tooltip'])
  }
  
}

</script>

<style>

</style>
