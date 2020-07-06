<template>
	<div id="osContainer">
		<os-search/>
		<os-content/>
	</div>
</template>

<script>
// @ is an alias to /src
import oscontent from "../components/os-Content"
import ossearch from "../components/os-Search"

export default {
	// props : {

	// }
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
