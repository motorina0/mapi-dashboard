<!-- @format -->

<!-- <nav-bar /> in the DashboardView.vue -->
<template>
	<div></div>
</template>

<script>
	import { mapActions, mapGetters } from 'vuex'

	export default {
		name: 'AppBar',
		data() {
			return {
				//if the app is on mobile devices it changes the title
				title: 'LNbits Dashboard',
				group: null,
				message: null,
				btnColor: 'tertiary',
				crdBottom: true,
			}
		},
		computed: {
			...mapGetters(['authorized', 'getAvatar']),
		},
		watch: {},
		created() {},
		beforeDestroy() {},
		methods: {
			...mapActions(
				'drawertoggle', // chooses which namespaced state module to get the mutations from
				['drawerOn']
			),
			drawerButton() {
				// this calls the action drawerOn which then commits the toggle mutation
				this.drawerOn()
			},
		},
	}
</script>

<style>
	.v-app-bar-title__content {
		width: 280px;
	}
</style>
