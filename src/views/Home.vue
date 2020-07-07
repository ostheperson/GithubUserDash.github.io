<template>
	<div id="osContainer">
		<os-search @osSearch="getRepos" @clear="clear" :exist="exist"/>
		<div v-show="searched">
			<os-profile :user = "user"/>
			<os-content :repos="repos"/>
		</div>
		<div v-show="!searched">
			<h5>Enter a Github username</h5>
		</div>
		<div v-show="!exist">
			<h6>Have you entered a valid username?</h6>
		</div>
	</div>
</template>

<script>
// @ is an alias to /src
import oscontent from "@/components/os-Content"
import ossearch from "@/components/os-Search"
import osprofile from "@/components/user"

export default {
	name: 'Home',
	components : {
		"os-content" : oscontent,
		"os-search" : ossearch,
		"os-profile" : osprofile
	},
	data () {
		return {
			user : {},
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
				repo["url"] = item.html_url
				repo["forked"] = item.fork
				objj.push(repo)
				
			})
			this.repos = objj
			this.searched = true
			//console.log(objj)
		}
	}
}
</script>

<style scoped>
#osContainer {
	width: fit-content;
	margin: auto;
}
</style>
