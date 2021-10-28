<template>
<q-page>
    <hr>
    <div class="q-ml-md">
		<p class= "totalFont">Работа колл-центра</p>
		<div class = "call_date">
			<q-input v-model="date" mask="##.##.####">
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

    <div class="row section q-mt-xl q-ml-md">				
		<div class="col-12 col-md-6">								
			<div class="row">
				<div class="col-12 col-md-4 q-mt-lg">
					<p class="callsText"> {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[0].totalcalls) }} </p>
					<p class="callsNames">Общее количество звонков</p>
				</div>
				<div class="col-12 col-md-4 q-mt-lg">
					<p class="callsText"> {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[0].totalleads) }} </p>
					<p class="callsNames"> Общее количество лидов </p>
				</div>
	    		<div class="col-12 col-md-4 q-mt-lg">
		    		<p class="callsText" > {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[0].totalgreenzone) }} </p>
						<p class="callsNames">Передано в зеленую зону</p>
					</div>
					<div class="col-12 col-md-12 q-mt-lg">
						<p class="totalFont">Всего</p>
					</div>
					<div class="col-md-4 q-mt-lg">
						<p class="totalCall callsText"> {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[1].totalcalls) }} </p> 
						<p class="callsNames">Общее количество звонков</p>
					</div>
					<div class="col-md-4 q-mt-lg">
						<p class="totalCall callsText"> {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[1].totalleads) }} </p>
						<p class="callsNames">Общее количество лидов</p>
					</div>
					<div class="col-md-4 q-mt-lg">
						<p class="totalCall callsText"> {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[1].totalgreenzone) }} </p>
						<p class="callsNames">Передано в зеленую зону</p>
					</div>
				</div>
			</div>
			<div class="col-12 col-md-6 q-mt-lg q-px-lg reestr" style="background: LightPink;">
				<div class="row">
					<div class="col-12 q-mt-lg">
						<p class="callsNames">Добавление в реестры и официальный перечень площадок субсидий</p>
					</div>
					<div class="col-6 q-mt-lg">
						<p class="callsText"> {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[2].mik_participants) }} </p>
						<p class="callsNames">Участники МИК</p>
					</div>
					<div class="col-6 q-mt-lg">
						<p class="callsText"> {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[2].reestr_soc) }} </p>
						<p class="callsNames">Заявки на вступление в реестр соц.предприятий</p>
					</div>
					<div class="col-6 q-mt-lg">
						<p class="callsText"> {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[2].list_ploshadki) }} </p>
						<p class="callsNames">Заявки на добавление в список площадок</p>
					</div>
					<div class="col-6 q-mt-lg font-arial">
						<p class="callsText"> {{ Intl.NumberFormat('ru-RU').format(apiCallCenter[2].req_approved) }} </p>
						<p class="callsNames">Одобрено заявок</p>
					</div>
				</div>
			</div>
		</div>
</q-page>
</template>

<script>
  import axios from 'axios';
  import { date } from 'quasar';

  export default {
    name: "callCenter",
    data() {
      return {
        date: date.formatDate(Date.now(), "DD.MM.YYYY"),
        apiCallCenter: [],
        link: "https://mec.standsystematic.ru/api/leads/calls/greenzone/day/",
        fullLink: "",
      }
    },

    async mounted()
    {
        this.fullLink = this.link + this.date;
        await axios
      .get(this.fullLink) //0
      .then(response => (this.apiCallCenter.push(response.data)));
    
        await axios
      .get('https://mec.standsystematic.ru/api/leads/calls/greenzone') //1
      .then(response => (this.apiCallCenter.push(response.data))); 
    
        await axios
      .get('https://mec.standsystematic.ru/api/leads/mik/reestr/sum') //2
      .then(response => (this.apiCallCenter.push(response.data)));
    },

    watch:
    {
        date : function(val)
        {
            this.date = val;
            this.fullLink = this.link + this.date;
            axios
			.get(this.fullLink)
			.then(response => (this.apiCallCenter[0] = response.data));
        }
    }
  }
</script>