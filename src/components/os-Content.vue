<template>
    <div>
        <div class="os-content os-content-heading">
            <div class="os-name">projects</div>
            <div class="os-description">description</div>
            <div >stars</div>
            <!-- <div class="os-content-item">forks</div> -->
        </div>
        <!-- <div class="os-content" v-for="(value, repo, index) in repos" :key="index">
            <a class="os-link os-content-item" :href="value.url">
                <p class="os-name">
                    {{ value.name }}
                    <em v-if="value.forked">*</em>
                </p>
            </a>
            <div class="os-content-item os-description">{{ value.description }}</div>
            <div class="os-content-item os-stars">{{ value.stars }}</div>
            <div class="os-content-item os-stars">{{ value.forks }}</div>
        </div> -->
        <div class="os-content">
            <a class="os-link"><div class="os-content-item os-name">Name of Repo</div></a>
            <div class="os-content-item os-description">Dsecroinevev rvre vreve rvewvjwbvweb wv eivuw vw viwvwuv  reovoiernv</div>
            <div class="os-content-item os-stars">400 stars</div>
        </div>
    </div>
</template>

<script>

export default {
    props: {
        "repos" : {
            type : Array,
            required: true
        }
    },
}
</script>

<style scoped>

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

/* .os-content .os-stars {
    
} */

div.os-content-item {
    margin: 0px 20px;
    flex-shrink: 0.5;
    align-self: center;
}

.os-content .os-link {
    text-decoration-line: none;
    margin: 0px;
    flex-shrink: 0.3;
    align-self: center;
    /* border-radius: 5px; */
    color: black;
}
.os-content .os-link:hover {
    color: rgb(34, 41, 133);
    font-weight: bold;
}
</style>
