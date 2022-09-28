<template>
    <div class="element-card p-3" v-if="arrayElement.poster_path">
        <img :src="imgUrl + arrayElement.poster_path" alt="">
    </div>
</template>

<script>
export default {
    name:'CardComponent',
    data(){
        return{
            imgUrl:'https://image.tmdb.org/t/p/w185'
        }
    },
    props:
        ['arrayElement'],
    
}

</script>

<style lang="scss" scoped>

</style>