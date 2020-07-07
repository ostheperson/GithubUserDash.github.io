<template>
	<div>
        <a :href="user.url"><img :src="user.avatar" alt="User Avatar"><p>{{ user.name }}</p></a>
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
    width: 64px;
    height: 64px;
}
</style>
