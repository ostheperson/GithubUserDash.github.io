<template>
	<div>
		<b-form @submit.prevent="onSubmit()" @reset="onReset()" id="osForm"> 
			<!-- <label class="sr-only os-form-items" for="inline-form-input-username" description="Make sure to not misspell usernames">Username</label> -->
			<b-input-group  prepend="@" class="mb-2 mr-sm-3 mb-sm-0 os-form-items os-form-input">
				<b-input v-model.lazy="form.username" class="os-input" :state="exist" id="inline-form-input-username" placeholder="Username" name="username"></b-input>
			</b-input-group>
			<b-button id="os-button" class="mb-2 mr-sm-3 mb-sm-0 os-form-items" variant="outline-dark" type="submit" ><b-icon icon="search"></b-icon></b-button>
			<b-button class="mb-2 mr-sm-3 mb-sm-0 os-form-items" type="reset" variant="outline-danger"><b-icon icon="x"></b-icon></b-button>
		</b-form>
	</div>
</template>

<script>
export default {
	props: {
        "exist" : {
            type : Boolean,
            required: false
        }
    },
	data () {
		return {
			form : {
				username : ""
			}
		}
	},
	methods : {
		onSubmit() {
			//this.getRepos(this.form.username)
			if (this.form.username == ""){
				this.exist = false
				alert("Input box is empty, enter a username to see repositories")
			}else {
				let usrname = this.form.username
				this.$emit("osSearch", usrname)
			}
			//console.log(username)
		},
		onReset() {
			// Reset our form values
			this.form.username = ''
			this.$emit("clear")
		}
	}
}
</script>

<style scoped>
#osForm {
	display: flex;
	width: fit-content;
	margin: auto;
	margin-bottom: 50px;
	min-height: 40px;
	justify-content: center;
}

.os-input {
	height: 100%;
}

.os-form-items {
	flex: 0.5;
}

.os-form-input {
	flex: 2;
	flex-grow: 3;
}
</style>
