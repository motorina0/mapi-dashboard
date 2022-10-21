<!-- @format -->

<template>
	<apexchart v-if="chartOptions.labels.length" type="donut" height="250" :options="chartOptions" :series="series" />
</template>

<script>
import { watchonlyApi } from '../../plugins/lnbits'
export default {
	name: 'ApexDonut',
	data() {
		return {
			series: [],
			chartOptions: {
				colors: ['#008FFB', '#00E396', '#FEB019'],
				animations: {
					enabled: true,
					easing: 'easeinout',
					speed: 1000,
				},
				fill: {
					type: 'gradient',
					gradient: {
						shade: 'dark',
						type: 'vertical',
						shadeIntensity: 0.05,
						inverseColors: false,
						opacityFrom: 1,
						opacityTo: 0.9,
						stops: [0, 100],
					},
				},
				chart: {
					toolbar: {
						show: false,
					},
				},
				title: {
					text: 'OnChain',
					align: 'left',
					style: {
						color: '#FFF',
					},
				},
				labels: [],
				responsive: [
					{
						breakpoint: 480,
						options: {
							chart: {
								width: 250,
							},
							legend: {
								position: 'bottom',
							},
						},
					},
				],
				legend: {
					labels: {
						colors: '#FFF',
					},
				},
			},
		}
	},
	created: async function () {
		const hostKey = this.$store.state.hostname
		const tokenKey = this.$store.state.token
		const wallet = { inkey: tokenKey.token }
		watchonlyApi.hostname = hostKey.hostname
		const resp2 = await watchonlyApi.getAccounts(wallet)
		console.log('#### resp2', resp2.data)
		this.chartOptions.labels = resp2.data.map(w => w.title)
		this.series = resp2.data.map(w => w.address_no)
		console.log('### this.labels', this.chartOptions.series)
	}
}
</script>
