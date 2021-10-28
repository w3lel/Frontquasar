<template>
  <div class="col-12 col-md-4 col-lg-3 line q-mr-lg">
	  <div class="col q-mt-lg">
		  <div class = "borderrig">
				<p class="queriesName">Заявки в Департаменте</p>
				<p class="queriesText"> {{ Intl.NumberFormat('ru-RU').format(apiData[0].totalcount) }} </p>
				<p class="queriesText" style="margin-bottom: 40%;"> {{ Intl.NumberFormat('ru-RU').format(apiData[0].totalsum) }} млн</p>
					
				<p class="queriesName">Готовят документы </p>
				<p class="queriesText"> {{ Intl.NumberFormat('ru-RU').format(apiData[1].totalcount) }} </p>
				<p class="queriesText">предпринимателей</p>
			</div>
		</div>
  </div>
</template>

<script>
import axios from 'axios';

export default 
{
  name: 'departmentQueries',
  data: function () 
  {
  return {
    apiData: [],
  }
},
  async mounted()
  {
    await axios
      .get('https://mec.standsystematic.ru/api/budget/specialist') //0
      .then(response => (this.apiData.push(response.data)));
    
    await axios
      .get('https://mec.standsystematic.ru/api/leads/docprepared/total') //1
      .then(response => (this.apiData.push(response.data)));
  },	
};

</script>