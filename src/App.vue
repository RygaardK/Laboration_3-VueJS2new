<template>
	<div id="app">
		<Header v-on:sendData="sendToLatest($event)" />
		<Latest v-bind:passthru="snipps" v-on:deleteSnippet="deleteSnipp($event)" />
		<p v-if="submitting" class="submittingText">Submitting...</p>
		<p v-if="loading" class="loadingText">Loading our Snippets...</p>
	</div>
</template>

<script>
import Header from './components/Header'
import Latest from './components/Latest'
import axios from 'axios'

const apiUrl = 'https://www.forverkliga.se/JavaScript/api/api-snippets.php';
const apiLatest = '?latest';

export default {
	
	name: 'App',
	data: () => {
		return {
			snipps: [],	
			loading: false,
			submitting: false,
			title: '',
			content: '',
		}
	},
	created() {
		this.loading = true;
		this.snipps = [];

		axios.get(apiUrl+apiLatest)
		.then((response) => {
			const data = response.data;
			this.snipps = data;
			this.loading = false;
		});
  
	},
	methods: {
		sendToLatest(titleContent) {
			this.title = titleContent[0];
			this.content = titleContent[1];
			this.addSnipp()
			console.log('(APP)This is sendToLatest: ', titleContent )
		},
		
		fetchSnipps() {
			this.loading = true;
			this.snipps = [];

			axios.get(apiUrl+apiLatest)
			.then((response) => {
				const data = response.data;
				this.snipps = data;
				this.loading = false;
			});
		},
		addSnipp() {
			this.submitting = true;
			console.log('(APP)addSnipp: ',this.title, this.content)
			axios.post('https://forverkliga.se/JavaScript/api/api-snippets.php?', { add:'add',
			title: this.title,
			content: this.content,
			
			})
			.then(response => {
				console.log('axios returned: ', response);
				this.submitting = false;
				this.fetchSnipps();
			});
		
		},
		deleteSnipp(id) {
			this.submitting = true;

			axios.post('https://forverkliga.se/JavaScript/api/api-snippets.php?', { delete:'delete',
			id:id
			})
			.then(response => {
				console.log('axios returned: ', response);
				this.submitting = false;
				this.fetchSnipps();
			});
		}
	},
	components: {
		"Header": Header,
		"Latest": Latest
	}
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
}
.submittingText, .loadingText {
	text-align: center;
}
</style>
