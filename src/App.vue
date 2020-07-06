<template>
	<div id="app">
		<div id="nav">
			<router-link to="/">Home</router-link> |
			<router-link to="/about">About</router-link>
		</div>
		<router-view/>
	</div>
</template>

<script>


export default {
	data () {
		return {
			user : {},
			repos : []
		}
	},
	methods : {
		async getRepos (username) {
			let api_url = 'https://api.github.com/users/'
			const header = {
				"Authorization" :`Token 798563c74f165541177a65ff6e31fbe479c8c4af`
			}
			let response = await fetch(api_url + username, {
				"method": 'GET',
				"headers" : header
			});

			let data = await response.json();
			let res = data
			this.user.name = res.html_url
			this.user.avatar = res.avatar_url

			api_url = 'https://api.github.com/users/' + username + "/repos"
			response = await fetch(api_url, {
				"method": 'GET',
				"headers" : header
			});
			data = await response.json();
			res = data

			let objj = []
			objj.forEach((item) => {
				let repo = {}
				repo["name"] = item.name
				repo["url"] = item.html_url
				repo["description"] = item.description
				repo["forks"] = item.forks
				repo["name"] = item.name
				repo["url"] = item.html_url
				repo["forked"] = item.fork
				objj.push(repo)
			})
			this.repos = objj
		}
	}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-width: 500px;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
