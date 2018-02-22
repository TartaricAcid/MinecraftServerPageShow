<template>
	<div id="app">
		<img src="./assets/logo.png" alt="logo" id="logo">
		<ul>
			<list-item v-for="item in list" :data="item"></list-item>
		</ul>
	</div>
</template>

<script>
	import ListItem from './components/ListItem'

	export default {
		name: 'App',
		data () {
			return {
				list: []
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
		width: 100%;
		max-width: 400px;
		display: block;
		margin: 20px auto;
	}

	ul {
		list-style-type: none;
		margin: 0;
		padding: 0;
	}
</style>
