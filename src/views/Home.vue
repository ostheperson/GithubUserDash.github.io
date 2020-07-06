<template>
	<div id="osContainer">
		<os-search @osSearch="getRepos"/>
		<os-content :repos="repos"/>
	</div>
</template>

<script>
// @ is an alias to /src
import oscontent from "@/components/os-Content"
import ossearch from "@/components/os-Search"

export default {
	props: {
        "repos" : {
            type : Array,
            required: false
		},
		"getRepos" : {
			type : Function,
		}
    },
	name: 'Home',
	components : {
		"os-content" : oscontent,
		"os-search" : ossearch
	}
}
</script>

<style scoped>
#osContainer {
	border: 1px solid black;
	width: fit-content;
	margin: auto;
}
</style>
