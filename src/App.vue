<template>
	<div id="app">

		<h1>Buttons</h1>

		<md-button>Default</md-button>
		<md-button accent="primary">Primary</md-button>
		<md-button accent="secondary">Secondary</md-button>

		<md-button type="flat">Default</md-button>
		<md-button type="flat" accent="primary">Primary</md-button>
		<md-button type="flat" accent="secondary">Secondary</md-button>

		<h1>Tabs</h1>

		<md-tabs accent="primary" position="fill">

			<md-tab name="Tab 1">
				<h1>Tab 1</h1>
				<p>I am tab 1</p>
			</md-tab>

			<md-tab name="Tab 2" :selected="true">
				<h1>Tab 2</h1>
				<p>I am tab 2</p>
			</md-tab>

			<md-tab name="Tab 3">
				<h1>Tab 3</h1>
				<p>I am tab 3</p>
			</md-tab>

		</md-tabs>

	</div>
</template>

<script>
import mdRipple from './components/md-ripple/md-ripple.vue';
import mdButton from './components/md-button/md-button.vue';

import mdTabs from './components/md-tabs/md-tabs.vue';
import mdTab from './components/md-tabs/md-tab.vue';

export default {
	name: 'app',
	components: {
		'md-ripple': mdRipple,

		'md-button': mdButton,

		'md-tabs': mdTabs,
		'md-tab': mdTab
	},
	data () {
		return {
			msg: 'Welcome to Your Vue.js App'
		}
	}
}
</script>

<style>
body {
	margin: 0;
	font-size: 16px;
	line-height: 1.5em;
}

#app {
	font-family: 'Roboto', Helvetica, Arial, sans-serif;
	font-smoothing: antialiased;

	margin: 0 auto;
	width: 720px;
}

/* Raise */
.raise {
}

.raise--1 {
	box-shadow: 0 0.1em 0.1em 0 rgba(0,0,0,0.25);
	z-index: 1;
}

.raise--2 {
	box-shadow: 0 0.25em 0.25em 0 rgba(0,0,0,0.25);
	z-index: 2;
}

.raise--3 {
	box-shadow: 0 0.4em 0.4em 0 rgba(0,0,0,0.25);
	z-index: 3;
}

.raise--4 {
	box-shadow: 0 0.6em 0.6em 0 rgba(0,0,0,0.25);
	z-index: 4;
}

.raise--5 {
	box-shadow: 0 0.8em 0.8em 0 rgba(0,0,0,0.25);
	z-index: 5;
}

.raise--6 {
	box-shadow: 0 1em 1em 0 rgba(0,0,0,0.25);
	z-index: 6;
}

/* Colors */

.foreground--light { color: #ffffff; }
.foreground--dark { color: #000000; }

.background--light { background-color: #ffffff; }
.background--dark { background-color: #000000; }

/*
 * Primary
 * Blue 500 100 700
 */

.foreground--primary { color: #2196F3; }
.foreground--primaryLight { color: #E3F2FD; }
.foreground--primaryDark { color: #1976D2; }

.background--primary { background-color: #2196F3; }
.background--primaryLight { background-color: #E3F2FD; }
.background--primaryDark { background-color: #1976D2; }

/*
 * Primary Alternate
 * White Black White
 */

.foreground--primaryAlternate { color: #FFFFFF; }
.foreground--primaryAlternateLight { color: #000000; }
.foreground--primaryAlternateDark { color: #FFFFFF; }

.background--primaryAlternate { background-color: #FFFFFF; }
.background--primaryAlternateLight { background-color: #000000; }
.background--primaryAlternateDark { background-color: #FFFFFF; }

/*
 * Secondary
 * Red 500 100 700;
 */

.foreground--secondary { color: #F44336; }
.foreground--secondaryLight { color: #FFCDD2; }
.foreground--secondaryDark { color: #D32F2F; }

.background--secondary { background-color: #F44336; }
.background--secondaryLight { background-color: #FFCDD2; }
.background--secondaryDark { background-color: #D32F2F; }

/*
 * Secondary Alternate
 * White Black White
 */

.foreground--secondaryAlternate { color: #FFFFFF; }
.foreground--secondaryAlternateLight { color: #000000; }
.foreground--secondaryAlternateDark { color: #FFFFFF; }

.background--secondaryAlternate { background-color: #FFFFFF; }
.background--secondaryAlternateLight { background-color: #000000; }
.background--secondaryAlternateDark { background-color: #FFFFFF; }
</style>
