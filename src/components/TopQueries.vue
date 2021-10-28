<template>
        <div class="col-12 col-md-7">
			<div class="col q-mt-lg">
				<div class="q-table__container q-table--horizontal-separator column no-wrap q-table__card q-table--no-wrap my-sticky-header-column-table bg-white-5">
					<div class="q-table__middle scroll">
						<table class="q-table">
							<thead>
								<tr>
									<th class="text-left table-header">Топ 5</th>
									<th class="text-left table-header">Объём средств, млн</th>
									<th class="text-left table-header">Количество заявок</th>
								</tr>
							</thead>
							<tbody>
								<tr class="">
									<td class="text-left my-special-class"> {{ apiQueries[0][0].pipename.replace(/\d+\. /i ,'') }} </td>
									<td class="text-left"> {{ Intl.NumberFormat('ru-RU').format(apiQueries[0][0].total_budget) }} </td>
									<td class="text-left">{{ Intl.NumberFormat('ru-RU').format(apiQueries[0][0].amount) }} </td>
								</tr>
								<tr class="">
									<td class="text-left my-special-class">{{ apiQueries[0][1].pipename.replace(/\d+\. /i ,'') }}</td>
									<td class="text-left">{{ Intl.NumberFormat('ru-RU').format(apiQueries[0][1].total_budget) }}</td>
									<td class="text-left">{{ Intl.NumberFormat('ru-RU').format(apiQueries[0][1].amount) }}</td>
								</tr>
								<tr class="">
									<td class="text-left my-special-class">{{ apiQueries[0][2].pipename.replace(/\d+\. /i ,'') }}</td>
									<td class="text-left">{{  Intl.NumberFormat('ru-RU').format(apiQueries[0][2].total_budget) }}</td>
									<td class="text-left">{{ Intl.NumberFormat('ru-RU').format(apiQueries[0][2].amount) }}</td>
							</tr>
							<tr class="">
									<td class="text-left my-special-class">{{ apiQueries[0][3].pipename.replace(/\d+\. /i ,'') }}</td>
									<td class="text-left">{{ Intl.NumberFormat('ru-RU').format(apiQueries[0][3].total_budget) }}</td>
									<td class="text-left">{{ Intl.NumberFormat('ru-RU').format(apiQueries[0][3].amount) }}</td>
								</tr>
								<tr class="">
									<td class="text-left my-special-class">{{ apiQueries[0][4].pipename.replace(/\d+\. /i ,'') }}</td>
									<td class="text-left">{{ Intl.NumberFormat('ru-RU').format(apiQueries[0][4].total_budget) }}</td>
									<td class="text-left">{{ Intl.NumberFormat('ru-RU').format(apiQueries[0][4].amount) }}</td>
								</tr>
							</tbody>
						</table>
					</div>
				</div>
			</div>
			<div class="col q-mt-lg">
				<div class="q-table__container q-table--horizontal-separator column no-wrap q-table__card q-table--no-wrap my-sticky-header-column-table bg-white-5">
					<div class="q-table__middle scroll">
						<table class="q-table">
							<thead>
								<tr>
									<th class="text-left table-header">Топ 5</th>
									<th class="text-left table-header">Количество заявок</th>
								</tr>
							</thead>
							<tbody>
								<tr class="">
									<td class="text-left"> {{ apiQueries[1][0].pipename.replace(/\d+\. /i ,'')}} </td>
									<td class="text-left"> {{ Intl.NumberFormat('ru-RU').format(apiQueries[1][0].totalcount) }} </td>
								</tr>
								<tr class="">
									<td class="text-left"> {{ apiQueries[1][1].pipename.replace(/\d+\. /i ,'')}} </td>
									<td class="text-left"> {{ Intl.NumberFormat('ru-RU').format(apiQueries[1][1].totalcount) }} </td>
								</tr>
								<tr class="">
									<td class="text-left"> {{ apiQueries[1][2].pipename.replace(/\d+\. /i ,'')}} </td>
									<td class="text-left"> {{ Intl.NumberFormat('ru-RU').format(apiQueries[1][2].totalcount) }} </td>
								</tr>
								<tr class="">
									<td class="text-left"> {{ apiQueries[1][3].pipename.replace(/\d+\. /i ,'')}} </td>
									<td class="text-left"> {{ Intl.NumberFormat('ru-RU').format(apiQueries[1][3].totalcount) }} </td>
								</tr>
								<tr class="">
									<td class="text-left"> {{ apiQueries[1][4].pipename.replace(/\d+\. /i ,'')}} </td>
									<td class="text-left"> {{ Intl.NumberFormat('ru-RU').format(apiQueries[1][4].totalcount) }} </td>
								</tr>
							</tbody>
						</table>
					</div>
				</div>
			</div>
		</div>

</template>

<script>
import axios from 'axios';

  export default {
    name: "topQueries",
    data() {
      return {
        apiQueries: [],
        link: "https://mec.standsystematic.ru/api/budget/total",
      }
    },

    async mounted()
    {
       await axios
      .get("https://mec.standsystematic.ru/api/budget/total")
      .then(response => (this.apiQueries.push(response.data)));

	  await axios
      .get("https://mec.standsystematic.ru/api/leads/docprepared")
      .then(response => (this.apiQueries.push(response.data)));
    },
  }
</script>

<style scoped>
.table-header
{
	background: LightPink;
}
</style>