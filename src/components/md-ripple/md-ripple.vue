<template>
	<div class="ripples" ref="ripplesContainer" v-if="!disabled" @mousedown="createRipple" @mouseup="fadeRipples" @mouseleave="fadeRipples">
		<div
			v-for="ripple in ripples"
			class="ripples-wave"
			:class="[
				'background--'+accent,
				{ 'isActive': ripple.active },
				{ 'isFading': ripple.fading }
			]"
			:style="{
				left: ripple.left+'px',
				top: ripple.top+'px',
				width: ripple.size+'px',
				height: ripple.size+'px'
			}"></div>
	</div>
</template>

<script>
export default {
	props: {
		accent: { default: 'default' },
		disabled: { default: false }
	},
	data() {
		return {
			ripples: [],
			fadeTimeout: null
		};
	},
	methods: {
		createRipple(e) {
			if (this.fadeTimeout) {
				clearTimeout(this.fadeTimeout);
			}

			let ripplesContainer = this.$refs.ripplesContainer;

			let rippleContainerWidth = ripplesContainer.offsetWidth;
			let rippleContainerHeight = ripplesContainer.offsetHeight;

			let rippleSize = 0;

			if (rippleContainerWidth > rippleContainerHeight) {
				rippleSize = rippleContainerWidth;
			} else {
				rippleSize = rippleContainerHeight;
			}

			let clickX = e.offsetX;
			let clickY = e.offsetY;

			clickX = clickX - (rippleSize/2);
			clickY = clickY - (rippleSize/2);

			let ripple = { left: clickX, top: clickY, size: rippleSize, active: false };

			this.ripples.push(ripple);

			let self = this;

			setTimeout(_ => {
				self.ripples[self.ripples.length-1].active = true;
			}, 1);
		},

		fadeRipples() {
			this.ripples.forEach(ripple => {
				ripple.fading = true;
				ripple.active = false;
			});

			let self = this;
			this.fadeTimeout = setTimeout(_ => {
				let lastPos = 0;
				self.ripples.forEach((ripple, pos) => {
					if (!ripple.active)
						lastPos = pos;
				});

				self.ripples.splice(0, lastPos+1);
			}, 400);
		}
	}
}
</script>


<style>
.ripples {
	position: absolute;
	left: 0;
	top: 0;

	width: 100%;
	height: 100%;

	overflow: hidden;
	border-radius: inherit;

	/*
	 * will-change: transform; triggers a
	 * compositing layer which fixes a bug
	 * that allows ripples to show up outside
	 * of border-radius til' it has finished
	 * its transition.
	 */
	will-change: transform;
}

.ripples-wave {
	border-radius: 100%;
	opacity: 0.2;
	top: 0;
	left: 0;
	position: absolute;
	pointer-events: none;
	transform: scale(0);
	transition-duration: 0.4s;
	transition-property: transform,opacity;
}

.ripples-wave.isActive,
.ripples-wave.isFading {
	transform: scale(2);
}

.ripples-wave.isFading {
	opacity: 0;
}
</style>
