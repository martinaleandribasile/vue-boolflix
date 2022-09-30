<template>
  <main>
    <div class="text-container gap-3">
        <h2 v-if="input.length<=0">Search your Films or Tv Series</h2>
        <div v-if="movies.length>0" class="d-flex flex-column card-container align-items-center">
            <h2 class="p-3 border border-light border-3 rounded-3">Film</h2>
            <div class="d-flex flex-wrap justify-content-start"><CardComponent :generi="generi" :cast="castMovie" :index="index" :arrayElement='film' v-for="(film,index) in movies" :key='film.id'/></div>
        </div>
        <div class="d-flex flex-column card-container align-items-center" v-if="series.length>0">
            <h2 class="p-3 border border-light border-3 rounded-3 series">Series</h2>
           <div class="d-flex flex-wrap justify-content-start"> <CardComponent :generi="generi" :cast="castSerie" :arrayElement='serie' :index="index"  v-for='(serie,index) in series' :key='serie.id'/></div>
        </div>
    </div>   
  </main>
</template>

<script>
import CardComponent from './CardComponent.vue';
export default {
    name: "MainComponent",
    components: {
         CardComponent
         },
    props:{
        movies:Array,
        series:Array,
        input:String,
        castMovie:Array,
        castSerie:Array,
        generi:Array,
    },
    data(){
        return{
            
        }
    },
}
</script>

<style lang="scss" scoped>
main{
    height: 90vh;
    background-image: url('@/assets/img/bkg-img.png');
    background-size: cover;
    overflow-y: auto;
    color: white;
    padding: 100px 0;
    .text-container{
        width: 90%;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        .card-container{
            width: 80%;
            margin: 150px auto;
            h2{
                width: 100px;
                color: white;
            }
            .series{
                width: 130px;
            }
        }
        
    }
}
</style>