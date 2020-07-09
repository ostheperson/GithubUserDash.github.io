<template>
	<div>
		<a class="os-profile" :href="user.url">
			<img :src="user.avatar" alt="User Avatar">
			{{ user.name }}
		</a>
	</div>
</template>

<script>
export default {
	props: {
		"user" : {
			type : Object,
			required: true
		}
	}
}
</script>

<style scoped>
img {
	border-radius: 50%;
	border: 1px solid grey;
	width: 70px;
	height: 70px;
	margin: 0px 10px;
}
a{
	text-decoration-line: none;
	width: fit-content
}
.os-profile {
	display: flex;
	align-items: center;
	margin: auto;
	color: inherit;
	font-size: 1.5em;;
}

</style>
