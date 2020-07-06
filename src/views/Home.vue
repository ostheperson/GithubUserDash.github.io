<template>
	<div id="os-container">
		<os-search/>
		<os-content/>
	</div>
</template>

<script>
// @ is an alias to /src
import oscontent from "../components/os-Content"
import ossearch from "../components/os-Search"

export default {
name: 'Home',
	components : {
		"os-content" : oscontent,
		"os-search" : ossearch
	}
}
</script>

<style scoped>
#os-container {
	widows: 80%;
}
</style>
