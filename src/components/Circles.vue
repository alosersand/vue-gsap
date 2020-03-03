<template>
	<svg viewBox="0 0 1920 1080">
		<transition-group
			tag="g"
			v-for="(circle, index) in circles"
			:key="circle.id"
			@before-enter="beforeEnter"
			@enter="enter"
			@leave="leave"
			:css="false"
		>
			<circle
				:key="circle.id"
				:cx="circle.x"
				:data-index="index"
				cy="100"
				r="50"
				:fill="circle.color"
			/>
		</transition-group>
	</svg>
</template>

<script>
import gsap from 'gsap'

export default {
	name: 'Circles',
	data: () => ({
		circles: [],
		id: 0,
		x: 0,
	}),
	mounted() {
		window.addEventListener('keypress', e => {
			console.log(e.code)

			switch (e.code) {
				case 'KeyP':
					this.addCircle()
					break

				case 'KeyQ':
					this.removeCircle()
					break
			}
		})
	},
	methods: {
		addCircle() {
			this.id += 1
			this.x += 200

			let circle = {
				id: this.id,
				color: 'red',
				x: this.x,
			}

			this.circles.push(circle)
		},
		removeCircle() {
			if (this.id === 0 && this.x === 0) return
			else {
				this.id -= 1
				this.x -= 200
			}

			this.circles.pop()
		},
		beforeEnter(el) {
			console.log('beforeenter')

			el.style.opacity = 0
		},
		enter(el, done) {
			console.log('enter')

			gsap.to(el, {
				opacity: 1,
				duration: 1,
				ease: 'sine.In',
				onComplete: () => done(),
			})
		},
		leave(el, done) {
			console.log('leave')

			gsap.to(el, {
				opacity: 0,
				duration: 1,
				ease: 'sine.Out',
				onComplete: () => done(),
			})
		},
	},
}
</script>

<style></style>
