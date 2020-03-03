<template>
	<div>
		<button @click="isVisible = !isVisible">PRESS ME</button>

		<transition-group
			tag="ul"
			@before-enter="beforeEnter"
			@enter="enter"
			@leave="leave"
		>
			<li v-for="item in items" :key="item">
				<p v-if="isVisible">{{ item }}</p>
			</li>
		</transition-group>

		<div>
			<input v-model="query" />

			<transition-group
				name="staggered-fade"
				tag="ul"
				v-bind:css="false"
				v-on:before-enter="beforeEnter"
				v-on:enter="enter"
				v-on:leave="leave"
			>
				<li
					v-for="(item, index) in computedList"
					v-bind:key="item.msg"
					v-bind:data-index="index"
				>
					{{ item.msg }}
				</li>
			</transition-group>
		</div>
	</div>
</template>

<script>
import gsap from 'gsap'

export default {
	name: 'Animation',
	data: () => ({
		isVisible: false,
		items: [0, 1, 2, 4, 5],
		query: '',
		list: [
			{ msg: 'Bruce Lee' },
			{ msg: 'Jackie Chan' },
			{ msg: 'Chuck Norris' },
			{ msg: 'Jet Li' },
			{ msg: 'Kung Fury' },
		],
	}),
	computed: {
		computedList: function() {
			let vm = this

			return this.list.filter(item => {
				return item.msg.toLowerCase().indexOf(vm.query.toLowerCase()) !== -1
			})
		},
	},
	methods: {
		beforeEnter: el => {
			el.style.opacity = 0
			el.style.height = 0
		},
		enter: (el, done) => {
			gsap.to(el, {
				opacity: 1,
				height: '1.6em',
				duration: 0.5,
				onComplete: () => done(),
			})
		},
		leave: (el, done) => {
			gsap.to(el, {
				opacity: 0,
				height: 0,
				duration: 0.5,
				onComplete: () => done(),
			})
		},
	},
}
</script>

<style scoped></style>
