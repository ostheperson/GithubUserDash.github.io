<template>
	<div id="project-app">
		<div class="os-top-urls">
			<a class="os-top-links" :href="parent_repo.parent_url">{{ parent_repo.name }}</a>
			<h3 class="os-top-links"><a :href="$route.params.repo.url">{{ $route.params.repo.name }}</a></h3>
			<div id="os-date">
				<p class="os-top-links">last updated at: {{ parent_repo.created }}</p>
				<p class="os-top-links">created at: {{ parent_repo.created }}</p>
			</div>
		</div>
		<!-- <div class="os-top-urls">
			<a class="os-top-links" href="#">name/proj</a>
			<h3 class="os-top-links"><a href="#">name of curr</a></h3>
		</div> -->
		<div class="os-description">
			{{ $route.params.repo.description }}
		</div>
		<div class="os-icon-row">
			<div class="os-icon-item os-stars">
				<span class="logo-name" >Stars</span>
				<b-icon icon="star" class="h4" variant="success"></b-icon> 
				<span class="logoName">{{ $route.params.repo.stars }}</span>
			</div>
			<div class="os-icon-item os-forks">
				<span class="logo-name">Forks</span>
				<img src="../../public/assets/fork.svg"/> 
				<span class="logoName">{{ $route.params.repo.forks }}</span>
			</div>
			<div class="os-icon-item os-issues">
				<span class="logo-name">Issues</span>
				<b-icon class="h4" icon="exclamation-triangle" variant="danger"></b-icon> 
				<span class="logoName">{{ parent_repo.issues }}</span>
			</div>
			<div class="os-icon-item os-licence">
				<span class="logo-name">Licence</span>
				<b-icon class="h4" icon="book" variant="secondary"></b-icon>  
				<span class="logoName">{{ parent_repo.license }}</span>
			</div>
		</div>
		<!-- <footer>
			<span class="footer mb-2">Stars <b-icon icon="star"></b-icon> </span>
		</footer> -->
	</div>
</template>

<script>
export default {
	data () {
		return {
			parent_repo : {},
			cloned : false,
			api_url : ""
		}
	},
	beforeMount () {
		this.api_url = this.$route.params.repo.api_url
		this.getParent()
		this.cloned = this.$route.params.repo.forked
	},
	methods: {
		async getParent () {
			//console.log("runnign")
			//let api_url = this.$route.params.repo.api_url
			// const header = {
			// 	"Authorization" :`Token 798563c74f165541177a65ff6e31fbe479c8c4af`
			// }
			let response = await fetch(this.api_url);
			//console.log(response)
			if (response.status == 404){
				return 1
			}
			let data = await response.json();
			let res = data
			//console.log(res)
			let objj = {}
			if (this.cloned){
				objj["name"] = res.parent.full_name
				objj["parent_url"] = res.parent.html_url					
			}
			
			objj["created"] = res.created_at
			objj["created"] = objj.created.substring(0,10)
			objj["updated"] = res.updated_at
			objj["updated"] = objj.updated.substring(0,10)
			objj["issues"] = res.open_issues_count
			if (res.license){
				objj["license"] = res.license.key
			}else {
				objj["license"] = "none"
			}
			
			this.parent_repo = objj
			//console.log(objj)
		}
	}
}
</script>

<style scoped>
#project-app {
	width: fit-content;
	margin: auto;
	min-width: 500px;
	max-width: 1000px;
}
.os-top-urls{
	display: flex;
	flex-direction: column;
	align-items: flex-start;
	margin: 10px;
}
.os-top-links{
	padding: 5px;
}
#os-date{
	display: flex;
	flex-direction: column;
	align-items: flex-end;
	width: 100%;
	font-weight: lighter;
}

#os-date .os-top-links{
	margin: 0px;
	padding: 0px;
}
.os-description{
	margin: 30px;
	width: fit-content;
	text-align: center;
}
div img {
	width: 30px;
	height: 30px;
}
div a{
	text-decoration-line: none;
	color:#42b983;
	transition: font-weight .3s;
}
div a:hover{
	font-weight: bolder;
}
.os-icon-row {
	display: flex;
	justify-content: space-around;
	margin: auto;
	background-color: #DCE9FF;
	border-radius: 5px;
}
span.logo-name {
	margin: 0px 10px;
}
.os-icon-item {
	display: flex;
	padding: 7px 5px 0px 5px;
	justify-content: space-around;
}
.logoName {
	margin: 0px 10px;
}
</style>
