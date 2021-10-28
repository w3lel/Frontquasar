<template>
<div data-v-7c94da36="" class="q-pa-md q-ml-sm q-mt-xl">
	<div class="row title">
		<div class="col-12" style="margin-right:10%;">
			<p class="totalFont">Основные показатели<br> о ходе субсидийной кампании</p>
		</div>
	</div>
	<SumIssued />
	<div class="col-12 subtitle">
		<p class="totalFont">Потенциальный объем средств к выдаче</p> <hr>
	</div>
	
	<div class="row section q-mt-lg">
		<DepartmentQueries />
		<TopQueries />
	</div>

	<CallCenter />
</div>
</template>

<script>
import CallCenter from "components/CallCenter";
import SumIssued from "components/SumIssued";
import TopQueries from "components/TopQueries";
import DepartmentQueries from "components/DepartmentQueries";

export default 
{
  name: 'PageIndex',
  components: {CallCenter, SumIssued, TopQueries, DepartmentQueries},
  data: function () 
  {
  return {
    apiData: [],
	date: ''
  }
},
}
</script>
