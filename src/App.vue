<template>
	<div id="app">
		<img src="./assets/logo.png" alt="logo" id="logo">
		<div>
			<list-item v-for="item, i in list" :data="item" :key="i" :s="s" :index="i"></list-item>
		</div>
	</div>
</template>

<script>
	import ListItem from './components/ListItem'
	import url from 'url';

	export default {
		name: 'App',
		data () {
			let s = parseInt(url.parse(window.location.search, true).query.s) || 0;
			return {
				s: s - 1,
				list: [],
			}
		},
		components: {
			ListItem
		},
		created () {
			this.$http.get('./static/data.json').then(data => {
				this.list = data.body;
			});
		}
	}
</script>

<style>
	#app {
		max-width: 1024px;
		width: 98%;
		margin: 0 auto;
	}

	#logo {
		width: 400px;
		height: 120px;
		max-width: 100%;
		display: block;
		margin: 20px auto;
	}

</style>
