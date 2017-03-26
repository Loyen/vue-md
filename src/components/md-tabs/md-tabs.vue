<template>
	<div class="tabs">

		<div class="tabsBar background--primary" :class="positionClass">

			<div class="tabsBar-container">

				<div class="tabs-selections" ref="tabSelectors">
					<div class="tabs-tab" v-for="tab,position in tabs" :class="{ 'foreground--primaryLight': tab.isActive, 'foreground--primaryAlternateDark': !tab.isActive }" @click="selectTab(position)">
						{{ tab.name }}
					</div>
				</div>

				<div class="tabs-indicator" :class="{ 'background--secondary': this.accent, 'background--primaryAlternate': !this.accent }" ref="tabIndicator"></div>

			</div>

		</div>

		<slot></slot>

	</div>
</template>

<script>
export default {
	props: {
		accent: { default: true, required: false },
		position: { default: 'fill' }
	},
	data() {
		return {
			tabs: [],
			currentTab: 0,
			positionClass: 'tabsBar--fill'
		};
	},
	created() {
		this.tabs = this.$children;

	},
	mounted() {
		this.positionClass = 'tabsBar--'+this.position;

		this.tabs.forEach((tab,position) => {
			if (tab.isActive)
				this.currentTab = position;
		});

		this.setActive();
	},
	methods: {
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
.tabsBar {
	position: relative;
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

.tabs-selections {
	display: flex;
}

.tabs-tab {
	cursor: pointer;

	flex: 1;
	text-align: center;
	line-height: 2em;

	transition-property: color;
	transition-duration: 0.1s;
	transition-timing-function: linear;
}

.tabs-indicator {
	height: 0.2em;

	position: absolute;

	bottom: 0;

	width: 0;
	left: 0;

	transition-property: left,width;
	transition-duration: 0.1s;
	transition-timing-function: linear;
}
</style>