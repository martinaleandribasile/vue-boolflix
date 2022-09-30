<template>
    <div class="element-card p-3 ">
       <div class="position-relative" v-if="!hover">
        <button class="btn btn-warning position-absolute end-0" @click="displayDettails()">Info</button>
         <img @error="errorImg"  class=" img-poster-title img-fluid" :src="imgUrl + arrayElement.poster_path" alt=""/>
        </div>
        <div   v-else class="gap-2 info-container">
            <button @click='displayDettails()' class="btn btn-dark w-20 align-self-end">Back</button> 
            <h5  v-if="arrayElement.title"><span>Titolo: </span>{{arrayElement.title}}</h5>
            <h5 v-else><span>Titolo: </span>{{arrayElement.name}}</h5>
            <h6 v-if="arrayElement.title"> <span>Titolo originale: </span>{{arrayElement.original_title}}</h6>
            <h6 v-else><span>Titolo originale: </span>{{arrayElement.original_name}}</h6>
            <span>Language: 
                <img class="flag" 
                    :src="getFlag(arrayElement.original_language)"
                    :alt="arrayElement.original_language"
                    @error="fixImageError($event)" />     
            </span> 
            <span>Generi:
                <ul>
                    <li v-show="arrayElement.genre_ids.includes(genere.id)" class="text-white" v-for="genere in generi" :key="genere.id">{{genere.name}}</li>
                </ul>
            </span>
            <div class="star-icon">
                <span>Voto: </span>
                <i v-for="key in 5" :key="key" :class='createIntegerVote(arrayElement.vote_average) >= key ? "fa-solid" : "fa-regular"' class="fa-star"></i>
            </div>
            <p> <span>Overwiev: </span>{{arrayElement.overview}}</p>
            <span>Cast: 
                <ul>
                    <li class='text-white' v-show='cast.order < 5 ' v-for="cast in cast[index]" :key="cast.id">{{cast.name}}</li>
                </ul>
            </span>
        </div>
    </div>
</template>

<script>
    import imgDef from '@/assets/img/filmdef.png'
export default {
    name:'CardComponent',
    data(){
        return{
            imgUrl:'https://image.tmdb.org/t/p/w342',
            integerVote:'',
            hover:false
        }
    },
    props:{
        arrayElement:Object,
        index:Number,
        cast:Array,
        generi:Array
    },
    methods:{
       errorImg(e){
        e.target.src=imgDef
       },
        createIntegerVote(n){
            let vote = Math.floor(n / 2)
            if(vote===0){
                vote=1
            }//solo per nn lasciare stelline vuote
            return vote
        },

        getFlag(country){
            switch(country){
                case 'en':{
                country = 'gb';
                break;
                }
                case 'uk':{
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
  },
    
   
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

