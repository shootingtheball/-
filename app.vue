<template>
	<div id="app">
		<v-header :seller="seller"></v-header>
	</div>
</template>

<script>

	import vHeader from './components/head/v-header';

	export default {
		name: 'app',
		data() {
			return{
				seller:""
			}
		},
		components: {
			vHeader
		},
		created() {
			this.$http.get('api/seller').then((response) => {
				response=response.body;
				if (response.errno ===0) {
					this.seller = response.data;
				}
			})
		}
	}
</script>

<style>
	*{
		margin:0;
		padding: 0;
	}
</style>
