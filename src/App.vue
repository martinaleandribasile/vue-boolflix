<template>
  <div id="app">
   <HeaderComponent @sendInputText="saveInputText"/>
   <MainComponent :castSerie='castSeries' :castMovie='castMovies' :movies='arrayMovies' :series='arraySeries' :input="textInput" />
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue';
import MainComponent from './components/MainComponent.vue';
import axios from 'axios'

export default {
  name: 'App',
  created(){
    
    
  },
  data(){
    return{
      textInput:"",
      queryKey:'64a886681191c335aec070e4355d176f',
      arrayMovies:[],
      arraySeries:[],
      indexMoviesArr:[],
      indexSeriesArr:[],
      castMovies:[],
      castSeries:[]
    }
  },
  methods:{
    callApiMovies(){ 
      if(this.textInput.length>0){
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.queryKey}&query=${this.textInput}&include_adult=true`)
        .then((response)=>{
          this.arrayMovies=response.data.results
          this.getIndexArray(this.arrayMovies, this.indexMoviesArr);
          this.callCastArray(this.indexMoviesArr, this.castMovies, "movie")
         
        })
       
      }
    },
    callApiSeries(){
      if(this.textInput.length>0){
        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.queryKey}&query=${this.textInput}&include_adult=true`)
        .then((response)=>{
          this.arraySeries=response.data.results  
          this.getIndexArray(this.arraySeries, this.indexSeriesArr);  
          this.callCastArray(this.indexSeriesArr, this.castSeries, "tv")   
        })
      }
    },
    callCastArray(array, cast, type){
      array.forEach((element)=>{
        axios.get(`https://api.themoviedb.org/3/${type}/${element}/credits?api_key=${this.queryKey}`)
        .then((response)=>{
          cast.push(response.data.cast)
        })
      })
    },
    getIndexArray(array, arrayIndex){
        array.forEach((item)=>{
        arrayIndex.push(item.id)
      })
    },
    saveInputText(value){
      console.log(value)
      this.textInput=value
      this.callApiMovies()
      this. callApiSeries()
    }
 
  },
  components: {
    HeaderComponent,
    MainComponent
}
}
</script>

<style lang="scss">
@import '@/style/reset.scss';
#app{
  height: 100vh;
}
</style>
