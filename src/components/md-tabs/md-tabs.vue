<template>
	<div class="tabs">

		<div class="tabsBar" :class="[ positionClass, barClass ]">

			<div class="tabsBar-container">

				<div class="tabs-selections" ref="tabSelectors">
					<div class="tabs-tab" v-for="tab,position in tabs" @click="selectTab(position)">
						{{ tab.name }}
						<md-ripple :accent="rippleAccent" />
					</div>
				</div>

				<div class="tabs-indicator" :class="indicatorClass" ref="tabIndicator"></div>

			</div>

		</div>

		<slot></slot>

	</div>
</template>

<script>
import mdRipple from '../md-ripple/md-ripple.vue';

export default {
	components: {
		'md-ripple': mdRipple
	},
	props: {
		accent: { default: 'default', required: false },
		position: { default: 'fixed' }
	},
	data() {
		return {
			tabs: [],
			currentTab: 0,
			positionClass: '',
			barClass: '',
			indicatorClass: '',
			rippleAccent: ''
		};
	},
	mounted() {
		this.setAccent();

		this.initTabs();
	},
	methods: {
		setAccent() {
			this.barClass = [ 'background--'+this.accent, 'foreground--'+this.accent+'Alternate'];
			this.indicatorClass = [ 'background--'+this.accent ];

			let rippleAccent = this.accent == 'default' ? 'dark' : this.accent+'Alternate';
			let indicatorAccent = this.accent+'Alternate';

			this.rippleAccent = rippleAccent;
			this.indicatorClass = [ 'background--'+indicatorAccent ];
		},

		initTabs() {
			this.positionClass = 'tabsBar--'+this.position;

			this.tabs.forEach((tab,position) => {
				if (tab.isActive)
					this.currentTab = position;
			});

			this.setActive();
		},

		setTab(tab) {
			this.tabs.push(tab);
		},

		selectTab(position) {
			this.currentTab = position;
			this.setActive();
		},

		setActive() {
			this.tabs.forEach((tab,position) => {
				tab.isActive = (position == this.currentTab);
			});
			this.moveIndicator();
		},

		moveIndicator() {
			let tabsCount = this.tabs.length;
			let tabWidth = 100/tabsCount;
			let tabLeft = tabWidth*this.currentTab;

			this.$refs.tabIndicator.style.width = tabWidth+'%';
			this.$refs.tabIndicator.style.left = tabLeft+'%';
		}
	}
}
</script>


<style>
.tabsBar-container {
	position: relative;
}

.tabs-selections {
	display: flex;
}

.tabs-tab {
	position: relative;
	cursor: pointer;
	flex: 1;

	text-align: center;
	line-height: 3em;

	padding-left: 0.125em;
	padding-right: 0.125em;

	transition-property: color;
	transition-duration: 0.1s;
	transition-timing-function: linear;
}


.tabsBar--left .tabsBar-container,
.tabsBar--center .tabsBar-container,
.tabsBar--right .tabsBar-container {
	width: 33.333333%;
}

.tabsBar--center .tabsBar-container {
	margin-left: auto;
	margin-right: auto;
}

.tabsBar--right .tabsBar-container {
	margin-left: auto;
}


.tabs-indicator {
	height: 0.125em;

	position: absolute;

	pointer-events: none;

	bottom: 0;

	width: 0;
	left: 0;

	transition-property: left,width;
	transition-duration: 0.1s;
	transition-timing-function: linear;
}
</style>