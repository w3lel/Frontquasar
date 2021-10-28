<template>
  <q-page style="min-height: 800px; min-width: 600px;">

    <q-card>
      <q-card-section>
        <div class="text-grey-8 text-weight-bolder" style="font-size: 24px; margin-bottom: 20%;">
          <div class = "column" style="border-right: 50%; min-width:60%;">
            Объём выданных средств Департаментом по каждой субсидии и количество предпринимателей-получателей
          </div>
          <div>
            <div class = "column">
    					<q-input filled v-model="date" mask="##.##.####">
      					<template v-slot:append>
    							<q-icon name="event" class="cursor-pointer">
  									<q-popup-proxy ref="qDateProxy" transition-show="scale" transition-hide="scale">
     									<q-date v-model="date" mask="DD.MM.YYYY">
     										<div class="row items-center justify-end">
       										<q-btn v-close-popup label="Close" color="primary" flat />
     										</div>
     									</q-date>
   									</q-popup-proxy>
   								</q-icon>
 								</template>
    					</q-input>
            </div>
          </div>
        </div>
        
      </q-card-section>
      <q-card-section class="q-pa-none echarts">
        <IEcharts :option="barChartOption" :resizable="true" />
      </q-card-section>
    </q-card>
  </q-page>
</template>
<script>
  import IEcharts from 'vue-echarts-v3/src/full.js';
  import axios from 'axios';
  import { date } from 'quasar';

  export default {
    name: "charts",
    data() {
      return {
        date: date.formatDate(Date.now(), "DD.MM.YYYY"),
        apiBudget: "",
        link: "https://mec.standsystematic.ru/api/budget/total/day/",
        fullLink: "",
        barChartOption: {
          grid:{

            left: '20%'
          },
          legend: {},
          tooltip: {},
          dataset: {
            dimensions: ['category', 'Объём средств, млн'],
            source: [
            ]
          },
          yAxis: {type: 'category',
          axisLabel:{
          }},

          xAxis: {},
          // Declare several bar series, each will be mapped
          // to a column of dataset.source by default.
          series: [
            {type: 'bar'}
          ]
        },
      }
    },
    async mounted()
    {
      this.barChartOption.dataset.source.splice(0);
      this.fullLink = this.link + this.date;
      await axios
      .get(this.link + this.date)
      .then(response => (this.apiBudget = (response.data)));
      this.apiBudget.forEach(element => 
      {
        this.barChartOption.dataset.source.push({category: element.pipename.replace(/\d+\. /i ,''),
        'Объём средств, млн' : element.total_budget});
      });
    },

    watch:
    {
      date : async function(val)
      {
        this.date = val;
        this.barChartOption.dataset.source.splice(0);
        this.fullLink = this.link + this.date;
        await axios
        .get(this.fullLink)
        .then(response => (this.apiBudget = (response.data)));
        this.apiBudget.forEach(element => 
        {
          if (element.total_budget != 0)
          {
            this.barChartOption.dataset.source.push({category: "" + element.pipename.replace(/\d+\. /i ,''),
             'Объём средств, млн' : element.total_budget});
          }
        });
      }
    },
    components: {
      IEcharts
    },
  }
</script>

<style scoped>
  .echarts {
    width: 1050px;
    height: 373px;
  }

  .column {
       float: left;
       width: 33%;
  }
</style>