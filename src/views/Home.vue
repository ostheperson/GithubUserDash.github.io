<template>
	<div id="osContainer">
		<os-search @osSearch="search" @clear="clear" :exist="exist"/>
		<div v-show="searched">
			<os-profile :user="user"/>
			<div>
				<div class="os-content os-content-heading">
					<div class="os-name">projects</div>
					<div class="os-description">description</div>
					<div >stars</div>
					<!-- <div class="os-content-item">forks</div> -->
				</div>
				<div class="os-content" v-for="(value, repo, index) in repos" :key="index">
					<router-link :to="{ name : 'repo', params: { repo : value }}" class= "os-content-item os-link ">
						<p class="os-name">
							{{ value.name }}
							<em v-if="value.forked">*</em>
						</p>
					</router-link>
					<div class="os-content-item os-description">{{ value.description }}</div>
					<div class="os-content-item os-stars">{{ value.stars }}</div>
				</div>
				<!-- <div class="os-content">
					<a class="os-link"><div class="os-content-item os-name">Name of Repo</div></a>
					<div class="os-content-item os-description">Dsecroinevev rvre vreve rvewvjwbvweb wv eivuw vw viwvwuv  reovoiernv</div>
					<div class="os-content-item os-stars">400 stars</div>
				</div> -->
			</div>
			<footer>
				<p class="footer">Key <em>*</em> => forked repository</p>
			</footer>
		</div>
		
		<!-- <div v-show="!searched">
			<h5>Enter a Github username</h5>
		</div>
		<div v-show="!exist">
			<h6>Have you entered a valid username?</h6>
		</div> -->
		
	</div>
</template>

<script>
// @ is an alias to /src

import ossearch from "@/components/os-Search"
import osprofile from "@/components/User"

export default {
	name: 'Home',
	props: {
		"exist" : {
			type: Boolean
		},
		"repos" : {
			type: Array
		},
		"searched" : {
			type: Boolean
		},
		"user" : {
			type: Object
		}
	},
	components : {
		"os-search" : ossearch,
		"os-profile" : osprofile,
	},
	data () {
		return {
			
		}
	}, 
	methods: {
		search(usrname) {
			this.$emit("search", usrname)
			
		},
		clear() {
			this.$emit("clear")
		}
	},
	// watch: {
	// 	logger () {
	// 		console.log()
	// 	}
	// }
}
</script>

<style scoped>
#osContainer {
	width: fit-content;
	margin: auto;
}

div .os-content-heading {
    background-color:inherit;
    font-weight: bolder;
}

.os-content {
    display: flex;
    padding:10px;
    margin: 10px;
    min-width: 500px;
    /* width: 80%; */
    justify-content: space-between;
    border-radius: 5px;
    background-color: rgb(220, 233, 255);
}

.os-description {
    flex: 2;
    padding: 0px 10px;
} 

div.os-content-item {
    margin: 0px 20px;
    flex-shrink: 0.5;
    align-self: center;
}

.os-content .os-link{
    margin: 0px;
    flex-shrink: 0.3;
    align-self: center;
    /* border-radius: 5px; */
    color:#1db94c;
}
.os-content .os-link:hover {
    font-weight: bolder;
}
.footer {
	position: relative;
	top: auto;
}
</style>
