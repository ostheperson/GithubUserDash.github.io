<template>
	<div id="app">
		<h3 class="os-heading">Github  User Dashboard</h3>
		<div id="nav">
			<router-link to="/">Dashboard</router-link> |
			<router-link to="/about">About</router-link>
		</div>
		<router-view @search="getRepos" @clear="clear" :user = "user" :repos="repos" :exist="exist" :searched="searched"/>
	</div>
</template>

<script>
export default {
	data () {
		return {
			user : {
				name: "",
				avatar: "",
				url: ""
			},
			repos : [],
			exist : true,
			searched : false
		}
	},
	methods : {
		clear () {
			this.repos = []
		},
		async getRepos (username) {
			let api_url = 'https://api.github.com/users/'
			// const header = {
			// 	"Authorization" :`Token 798563c74f165541177a65ff6e31fbe479c8c4af`
			// }
			let response = await fetch(api_url + username);
			
			if (response.status == 404){
				this.exist = false
				return 1
			}
			this.exist = true

			let data = await response.json();
			let res = data
			
			this.user["name"] = res.name
			this.user["url"] = res.html_url
			this.user["avatar"] = res.avatar_url
			
			//console.log(this.user)
			api_url = 'https://api.github.com/users/' + username + "/repos"
			response = await fetch(api_url);
			
			// response = await fetch(api_url, {
			// 	"method": 'GET',
			// 	"headers" : header
			// });

			if (response.status == 404){
				this.exist = false
				return 1
			}
			this.exist = true
			data = await response.json();
			res = data

			let objj = []
			res.forEach((item) => {
				let repo = {}
				repo["name"] = item.name
				repo["url"] = item.html_url
				repo["description"] = item.description
				repo["forks"] = item.forks
				repo["name"] = item.name
				repo["stars"] = item.stargazers_count
				repo["forked"] = item.fork
				repo["api_url"] = item.url
				objj.push(repo)
				
			})
			this.repos = objj
			this.searched = true
			//console.log(objj)
		}
	}
}
</script>

<style>
#app {
	font-family: Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	min-width: 500px;
}

.os-heading {
	margin: 15px auto;
}

#nav {
	padding: 20px;
}

#nav a {
	font-weight: bold;
	color: #2c3e50;
}

#nav a.router-link-exact-active {
	color: #42b983;
}
</style>
