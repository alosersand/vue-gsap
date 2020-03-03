<template>
	<svg viewBox="0 0 1920 1080">
		<circle :cx="1920 / 2" :cy="1080 / 2" r="5" fill="red" />

		<transition
			@before-enter="beforeEnter"
			@enter="enter"
			@after-enter="afterEnter"
			@leave="leave"
			:css="false"
		>
			<circle
				v-if="isVisible"
				:cx="x"
				:cy="y"
				:r="r"
				fill="white"
				cursor="move"
			/>
		</transition>
	</svg>
</template>

<script>
import gsap from 'gsap'

export default {
	name: 'HelloWorld',
	data() {
		return {
			isVisible: false,
			r: 50,
			x: 0,
			y: 0,
			mouseX: 0,
			mouseY: 0,
		}
	},
	mounted() {
		console.clear()
		console.log('♦ MOUNTED')

		window.addEventListener('keydown', e => {
			console.log('♦ KEYDOWN', e.code)

			if (e.keyCode === 32) {
				this.isVisible = true
			}
		})

		window.addEventListener('keyup', e => {
			console.log('♦ KEYUP', e.code)

			if (e.keyCode === 32) {
				this.isVisible = false
			}
		})
	},
	methods: {
		beforeEnter: el => {
			console.log('♦ BEFOREENTER')

			el.style.opacity = 1
		},
		enter: (el, done) => {
			console.log('♦ ENTERING...')

			let scale = 1.5

			let tween = gsap.to(el, {
				opacity: 0.5,
				ease: 'sine.In',
				duration: 2,
				scale: scale,
				y: 1080 / 2 - 50 / 2,
				x: 1920 / 2 - 50 / 2,
				onComplete: () => {
					console.log('♦ DONE')
					done()
				},
			})
		},
		afterEnter: el => {
			console.log('♦ AFTERENTER')

			let scale = 2

			let tween = gsap.to(el, {
				ease: 'bounce',
				duration: 0.5,
				scale: scale,
				y: 1080 / 2 - (50 / 2) * scale,
				x: 1920 / 2 - (50 / 2) * scale,
				onComplete: () => {
					console.log('♦ DONE')
				},
			})
		},
		leave: (el, done) => {
			console.log('♦ LEAVING...')

			let scale = 50

			let tween = gsap.to(el, {
				opacity: 0,
				ease: 'sine.Out',
				duration: 2.5,
				scale: scale,
				y: 1080 / 2 - 50 * scale,
				x: 1920 / 2 - 50 * scale,
				onComplete: () => {
					console.log('♦ DONE')
					done()
				},
			})
		},
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
