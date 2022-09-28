<template>
  <div id="app">
   <HeaderComponent @sendInputText="saveInputText"/>
   <MainComponent :movies='arrayMovies' :series='arraySeries' :input="textInput" />
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
      arraySeries:[]
    }
  },
  methods:{
    callApiMovies(){ 
      if(this.textInput.length>0){
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.queryKey}&query=${this.textInput}`)
        .then((response)=>{
          console.log(response, "film")
          this.arrayMovies=response.data.results
        })
      }
    },
    callApiSeries(){
      if(this.textInput.length>0){
        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.queryKey}&query=${this.textInput}`)
        .then((response)=>{
          console.log(response)
          this.arraySeries=response.data.results
        })
      }
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
