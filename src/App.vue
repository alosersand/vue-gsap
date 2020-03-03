<template>
	<div id="app">
		<circles />
	</div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Animation from './components/Animation'
import Circles from './components/Circles'
export default {
	name: 'App',
	components: {
		HelloWorld,
		Animation,
		Circles,
	},
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
	overflow: hidden;
}
</style>
