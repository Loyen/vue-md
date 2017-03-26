<template>
	<div id="app">

		<md-tabs :accent="true" position="fill">

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
import mdAlert from './components/md-alert/md-alert.vue';
import mdCard from './components/md-card/md-card.vue';
import mdTabs from './components/md-tabs/md-tabs.vue';
import mdTab from './components/md-tabs/md-tab.vue';

export default {
	name: 'app',
	components: {
		'md-alert': mdAlert,
		'md-card': mdCard,
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
}

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
 * Grey 500
 * Blue     600 200
 */

.foreground--primaryAlternate { color: #FFFFFF; }
.foreground--primaryAlternateLight { color: #1E88E5; }
.foreground--primaryAlternateDark { color: #BBDEFB; }

.background--primaryAlternate { background-color: #FFFFFF; }
.background--primaryAlternateLight { background-color: #1E88E5; }
.background--primaryAlternateDark { background-color: #BBDEFB; }

/*
 * Secondary
 * Yellow 500 100 700;
 */

.foreground--secondary { color: #FFEB3B; }
.foreground--secondaryLight { color: #FFF8E1; }
.foreground--secondaryDark { color: #FFA000; }

.background--secondary { background-color: #FFEB3B; }
.background--secondaryLight { background-color: #FFF8E1; }
.background--secondaryDark { background-color: #FFA000; }

/*
 * Secondary Alternate
 * Grey 500
 * Yellow   600 200
 */

.foreground--secondaryAlternate { color: #FFFFFF; }
.foreground--secondaryAlternateLight { color: #FDD835; }
.foreground--secondaryAlternateDark { color: #FFF59D; }

.background--secondaryAlternate { background-color: #FFFFFF; }
.background--secondaryAlternateLight { background-color: #FDD835; }
.background--secondaryAlternateDark { background-color: #FFF59D; }
</style>
