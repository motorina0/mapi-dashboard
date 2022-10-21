<!-- @format -->

<template>
	<v-container fluid :style="$vuetify.breakpoint.mdAndUp ? 'width: 1660px' : 'width: 100%' ">
		<!-- FIRST ROW with header table card and basic tab cards -->
		<v-row class="d-flex align-start mb-1">
			<!-- First DATA TABLE Card -->
			<v-col col md="4">
				<MaterialfyHeaderCard
					cardTitle="OnChain Accounts"
					:cardShowInnerList="false"
					:cardShowActions="false"
					:cardShowDivider="false"
				>
					<!-- mobile-breakpoint =0 disables the table cells wrapping on mobile like in tables page -->
					<template #crdInner>
						<v-data-table
							:headers="tableHeaders"
							:items="tableItems"
							hide-default-footer
							:mobile-breakpoint="0"
							class="primary"
						>
							<template slot="headerCell" slot-scope="{ header }">
								<span class="font-weight-light text-warning text--darken-3 text--red" v-text="header.text" />
							</template>
							<!-- use a scoped slot to send data to child to be processed and returned -->
							<template slot="items" slot-scope="{ index, item }">
								<td>{{ index + 1 }}</td>
								<td>{{ item.name }}</td>
								<td class="text-right">
									{{ item.salary }}
								</td>
								<td class="text-right">
									{{ item.country }}
								</td>
								<td class="text-right">
									{{ item.city }}
								</td>
							</template>
						</v-data-table>
					</template>
				</MaterialfyHeaderCard>
			</v-col>
			<!-- V-TAB TO-DO CARD -->
			<v-col col md="3">
				<MaterialfyColorCard
					cardMaxWidth="500"
					cardInnerText="Used Addresses"
					:cardShowDivider="false"
					:cardShowActions="false"
					cardColor="primary"
				>
					<template v-slot:crdInner>
						<materialfy-apex-donut />
					</template>
				</MaterialfyColorCard>
			</v-col>
			<!-- LAST CARD -->
			<v-col  md="5">
				<MaterialfyDataTable />
			</v-col>
		</v-row>
		<!-- SECOND ROW  -->
		<!-- Used named slots and props to overide the default card content below -->
		<v-row class="d-flex align-start justify-center mb-2">
			<!-- FIRST COLOR CARD with default content -->
			<v-col md="4" class="my-2">
				<MaterialfyColorCard
					cardMaxWidth="500"
					cardInnerText="Horse Power"
					:cardShowDivider="false"
					:cardShowActions="false"
					cardColor="tertiary"
				>
					<template v-slot:crdInner>
						<materialfy-apex-polar-map />
					</template>
				</MaterialfyColorCard>
			</v-col>
			<!-- SECOND COLOR CARD with secondary color -->
			<v-col md="4">
			
			</v-col>
			<v-col md="4">
				<MaterialfyColorCard
					cardMaxWidth="500"
					cardInnerText="Wallet Type"
					:cardShowDivider="false"
					:cardShowActions="false"
					:cardShowInnerText="false"
					cardColor="accent"
				>
					<template v-slot:crdInner>
						<materialfy-apex-multiple-radial-bars />
					</template>
				</MaterialfyColorCard>
			</v-col>
		</v-row>

		<!-- THIRD ROW -->
		<!-- Used named slots and props to overide the default card content below -->
		<v-row class="d-flex align-start mb-2">
			<v-col>
				<MaterialfyColorCard cardInnerText="$$$$$$$ emoji" :cardShowDivider="false" :cardShowActions="false">
					<template v-slot:crdInner>
						<materialfy-apex-y-axis />
					</template>
				</MaterialfyColorCard>
			</v-col>
			<v-col>
				<MaterialfyColorCard
					cardInnerText="User Engagement"
					:cardShowDivider="false"
					:cardShowActions="false"
					cardColor="secondary"
				>
					<template v-slot:crdInner>
						<materialfy-apex-line-graph />
					</template>
				</MaterialfyColorCard>
			</v-col>
		</v-row>
		<!-- FOURTH ROW with calendar -->
		<v-row class="ma-3 d-flex align-start justify-center">
			<v-col md="9">
				<v-responsive :aspect-ratio="16 / 9">
					<MaterialfyCalendar />
				</v-responsive>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
	// this is where the line chart sparkline gets its colors
	import { watchonlyApi } from '../../plugins/lnbits'
	
	const gradients = [
		['#222'],
		['#42b3f4'],
		['red', 'orange', 'yellow'],
		['purple', 'violet'],
		['#00c6ff', '#F0F', '#FF0'],
		['#f72047', '#ffd200', '#1feaea'],
	]
	export default {
		data: () => ({
			labels: ['Feb', 'March', 'April', '420', 'May', 'June', 'July', 'Aug'],
			sparklineValue: [200, 300, 410, 390, 420, 460, 420, 420],
			width: 2,
			radius: 10,
			padding: 8,
			lineCap: 'round',
			gradient: gradients[5],
			sparklineValue2: [0, 2, 5, 9, 5, 10, 3, 5, 0, 0, 1, 8, 2, 9, 10],
			gradientDirection: 'top',
			gradients,
			fill: false,
			type: 'trend',
			autoLineWidth: false,
			tableHeaders: [
				{
					sortable: false,
					text: 'ID',
					value: 'id',
					class: 'tertiary--text text-h6',
				},
				{
					sortable: false,
					text: 'Name',
					value: 'title',
					class: 'tertiary--text text-h6',
				},
				{
					sortable: false,
					text: 'Balance',
					value: 'balance',
					align: 'float-right',
					class: 'tertiary--text text-h6',
				},
				{
					sortable: false,
					text: 'Type',
					value: 'type',
					align: 'float-right',
					class: 'tertiary--text text-h6',
				},
				{
					sortable: false,
					text: 'Fingerprint',
					value: 'fingerprint',
					align: 'float-right',
					class: 'tertiary--text text-h6',
				},
			],
			tableItems: [],
			tab: null,
			tabItems: [
				{ tab: 'Bugs', icon: 'mdi-bug' },
				{ tab: 'Server Issues', icon: 'mdi-cloud' },
				{ tab: 'Tickets', icon: 'mdi-alert' },
				{ tab: 'New Issues', icon: 'mdi-access-point' },
				{ tab: 'To-Do', icon: 'mdi-alert-box-outline' },
			],
			textList: [
				'You just read a sentence',
				'Second sentence with a lot of merit',
				'Fix bugs',
				'Look at Pull Requests',
				'Hope pull request fix bugs?',
				'Figure out some other text to put here',
			],
		}),
		methods: {
			throwError: function () {
				throw new Error('Sentry Error')
			},
		},
		created: async function () {
			const hostKey = this.$store.state.hostname
			const tokenKey = this.$store.state.token
			console.log('#### tokenKey', tokenKey)
			console.log('### watchonlyApi.hostname', watchonlyApi.hostname)
			const wallet = { inkey: tokenKey.token }
			watchonlyApi.hostname = hostKey.hostname
			const resp2 = await watchonlyApi.getAccounts(wallet)
			console.log('#### resp2', resp2.data)
			this.tableItems = resp2.data
		}
	}
</script>

<style>
@media only screen and (min-width: map-get($grid-breakpoints, 'xl')) {
.container {
max-width: 1440px !important;
}
}
</style>
