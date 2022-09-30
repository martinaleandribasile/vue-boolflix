<template>
  <div id="app">
   <HeaderComponent :inputsave="inputsave" @sendInputText="saveInputText"/>
   <MainComponent :generi="generiApi" :castSerie='castSeries' :castMovie='castMovies' :movies='arrayMovies' :series='arraySeries' :input="textInput" />
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue';
import MainComponent from './components/MainComponent.vue';
import axios from 'axios'

export default {
  name: 'App',
  data(){
    return{
      inputsave:false,
      textInput:"",
      queryKey:'64a886681191c335aec070e4355d176f',
      arrayMovies:[],
      arraySeries:[],
      indexMoviesArr:[],
      indexSeriesArr:[],
      castMovies:[],
      castSeries:[],
      generiApi:[]
    }
  },
  created(){
    
      axios.get(`https://api.themoviedb.org/3/genre/movie/list?api_key=${this.queryKey}&language=en-US`)
      .then((response)=>{
        this.generiApi=response.data.genres
        console.log('generi',this.generiApi)
      })
    
  },
  methods:{
    callApiMovies(){ 
      if(this.textInput.length>0){
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.queryKey}&query=${this.textInput}&include_adult=true`)
        .then((response)=>{
          if(response.status===200){
            this.arrayMovies=response.data.results
            this.getIndexArray(this.arrayMovies, this.indexMoviesArr);
            this.callCastArray(this.indexMoviesArr, this.castMovies, "movie")
          }
        })
        .catch((e)=>{
          console.log(e)
        })
      }
    },
    callApiSeries(){
      if(this.textInput.length>0){
        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.queryKey}&query=${this.textInput}&include_adult=true`)
        .then((response)=>{
          if(response.status===200){
            this.arraySeries=response.data.results  
            this.getIndexArray(this.arraySeries, this.indexSeriesArr);  
            this.callCastArray(this.indexSeriesArr, this.castSeries, "tv")   
          }
        })
        .catch((e)=>{
          console.log(e)
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
      console.log(cast)
    },
    getIndexArray(array, arrayIndex){
        array.forEach((item)=>{
        arrayIndex.push(item.id)
      })
      console.log('index',arrayIndex)
    },
    saveInputText(value){
      console.log(value)
      this.textInput=value
      this.callApiMovies()
      this. callApiSeries()
      this.inputsave=true
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
