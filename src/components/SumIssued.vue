<template>
<q-page>
        <div class="row section q-mt-lg q-mb-xl line">
			<div class="col-12 totalFont">
				<p>Текущий объем средств к выдаче <q-separator /></p>
			</div>
		</div>
		<div class="row section q-mt-lg">
			<div class="col-12 col-md-4 col-lg-3 line">
				<div class="col q-mt-lg">
					<div class="border_queries">
						<p class="queriesName">Одобрено заявок</p>
						<p class="queriesText"> {{Intl.NumberFormat('ru-RU').format(apiData[0].totalcount)}} </p>
						<p class="queriesText"> {{Intl.NumberFormat('ru-RU').format(apiData[0].totalsum)}} млн</p>
					</div>
				</div>
				
				<div class="border_queries">
					<p class="queriesName">Заключено соглашений</p>
					<p class="queriesText"> {{ Intl.NumberFormat('ru-RU').format(apiData[1].totalcount) }} </p>
					<p class="queriesText"> {{ Intl.NumberFormat('ru-RU').format(apiData[1].totalsum) }} млн</p>
				</div>
				
				<div class="border_queries">
					<p class="queriesName">Получили средства на счет</p>
					<p class="queriesText"> {{ Intl.NumberFormat('ru-RU').format(apiData[2].totalcount) }} </p>
					<p class="queriesText"> {{ Intl.NumberFormat('ru-RU').format(apiData[2].totalsum) }} млн</p>
				</div>
			</div>
			<div class="col-12 col-md-8">
				<div class="row">
					<Chart />
				</div>
			</div>
		</div>
</q-page>
</template>

<script>
import axios from 'axios'
import Chart from "components/Chart"

export default 
{
  name: 'sumIssued',
  components: {Chart},
  data: function () 
  {
  return {
    apiData: [],
	date: ''
  }
},
  async mounted()
  {
    await axios
      .get('https://mec.standsystematic.ru/api/budget/alleads') //0
      .then(response => (this.apiData.push(response.data)));
    await axios
      .get('https://mec.standsystematic.ru/api/budget/alleads/signed') //1
      .then(response => (this.apiData.push(response.data)));
    
    await axios
      .get('https://mec.standsystematic.ru/api/budget/alleads/given') //2
      .then(response => (this.apiData.push(response.data)));
  },	
};

</script>