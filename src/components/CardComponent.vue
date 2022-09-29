<template>
    <div class="element-card p-3 " v-if="arrayElement.poster_path">
        <img v-if="!hover" @mouseover="displayDettails()" class=" img-poster-title img-fluid" :src="imgUrl + arrayElement.poster_path" alt="">
        <div  @mouseout='displayDettails()' v-else class="gap-2 info-container"> 
            <h5  v-if="arrayElement.title"><span>Titolo: </span>{{arrayElement.title}}</h5>
            <h5 v-else><span>Titolo: </span>{{arrayElement.name}}</h5>
            <h6 v-if="arrayElement.title"> <span>Titolo originale: </span>{{arrayElement.original_title}}</h6>
            <h6 v-else><span>Titolo originale: </span>{{arrayElement.original_name}}</h6>
            <p>Language: 
                <img class="flag" 
                    :src="getFlag(arrayElement.original_language)"
                    :alt="arrayElement.original_language"
                    @error="fixImageError($event)" />     
            </p> 
            <div class="star-icon">
                <i v-for="key in 5" :key="key" :class='createIntegerVote(arrayElement.vote_average) >= key ? "fa-solid" : "fa-regular"' class="fa-star"></i>
            </div>
            <p> <span>Overwiev: </span>{{arrayElement.overview}}</p>
        </div>
    </div>
</template>

<script>
export default {
    name:'CardComponent',
    data(){
        return{
            imgUrl:'https://image.tmdb.org/t/p/w342',
            integerVote:'',
            hover:false
        }
    },
    props:
        ['arrayElement'],
    methods:{
        createIntegerVote(n){
            let vote = Math.floor(n / 2)
            return vote
        },

        getFlag(country){
            switch(country){
                case 'en':{
                country = 'gb';
                break;
                }
                case 'ja':{
                country = 'jp'
                break;
                }
        }
        return `https://flagicons.lipis.dev/flags/1x1/${country}.svg`
        },

        fixImageError(event){
        event.target.src=`https://flagicons.lipis.dev/flags/1x1/xx.svg`
        },

        displayDettails(){
            if(!this.hover){
                this.hover=true
            }else{
                this.hover= false
            }
            
        },
  }
    
   
}

</script>

<style lang="scss" scoped>
    .element-card{
        color: white;
        width: 342px;
        display: flex;
        flex-direction: column;
        column-gap: 10px;
        .img-poster-title{
            height: 500px;
        }
        .info-container{
            display: flex;
            flex-direction: column;
            .star-icon{
                color: yellow;
            }
            span{
                color: orange;
            }
            .flag{
                width: 20px;
            }
        }
    }
</style>

