<template>
	<div class="slider" ref="slider">
		<div class="slider-group" ref="sliderGroup">
			<slot>
			</slot>
		</div>
		<div class="dots">
			<span class="dot" :class="{active: currentPageIndex === index}" v-for="(item, index) in dots"></span>
		</div>
	</div>
</template>

<script type="text/ecmascript-6">
	import {addClass} from 'common/js/dom'
	import BScroll from 'better-scroll'

	export default {
		name: 'slider',
		props: {
			loop: {
				type: Boolean,
				default: true
			},
			autoPlay: {
				type: Boolean,
				default: true
			},
			interval: {
				type: Number,
				default: 4000
			}
		},
		data() {
			return {
				dots: [],
				currentPageIndex: 0
			}
		},
		mounted() {
			setTimeout(() => {
				this._setSliderWidth()
				this._initDots()
				this._initSlider()

				if (this.autoPlay) {
					this._play()
				}
			}, 20)

			window.addEventListener('resize', () => {
				if (!this.slider) {
					return
				}
				this._setSliderWidth(true)
				this.slider.refresh()
			})
		},
		destroyed() {
			clearTimeout(this.timer)
		},
		methods: {
			_setSliderWidth(isResize) {
				this.children = this.$refs.sliderGroup.children

				let width = 0
				let silderWidth = this.$refs.slider.clientWidth
				for (let i=0; i<this.childer.length; i++) {
					let child = this.children[i]
					addClass(child, 'slider-item')

					child.style.width = sliderWidth + 'px'
					width += sliderWidth
				}
				if (this.loop && !isResize) {
					width += 2 * sliderWidth
				}
				this.$refs.sliderGroup.style.width = width + 'px'
			}
		}
	}
</script>