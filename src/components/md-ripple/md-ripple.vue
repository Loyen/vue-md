<template>
	<div class="ripples" ref="ripplesContainer" @mousedown="createRipple" @mouseup="fadeRipples" @mouseleave="fadeRipples">
		<div class="shit"></div>
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
		accent: { default: 'default' }
	},
	data() {
		return {
			ripples: []
		};
	},
	methods: {
		createRipple(e) {
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
			setTimeout(_ => {
				self.ripples.forEach((ripple, pos) => {
					if (!ripple.active)
						self.ripples.splice(pos, 1);
				});
			}, 500);
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
	transform: scale(1);
}

.ripples-wave.isFading {
	opacity: 0;
}
</style>