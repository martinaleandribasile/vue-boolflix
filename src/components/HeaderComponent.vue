<template>
  <header>
    <div class='container-header'>
        <h1>BOOTFLIX</h1>
        <div class="d-flex gap-3">
            <input @keyup.enter="$emit('sendInputText', searchText),inputsave()" type="text" placeholder="Ricerca per titolo" v-model="searchText">
            <button @click="$emit('sendInputText', searchText), inputsave()"  class="btn btn-success">Search</button>
        </div>

    </div>
  </header>
</template>

<script>
export default {
name:'HeaderComponent',
data(){
    return{
        searchText:''
    }
},
props:{
inpusave:Boolean
},
methods:{
    inputsave(){
        if(this.inputsave){
            this.searchText=''
        }
    }
}
}
</script>

<style lang="scss" scoped>
header{
    background-color: black;
    height: 10vh;
    .container-header{
        padding: 0px 40px;
        height: 100%;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        h1{
            color: red;
        }
        input{
            outline: none;
            width: 300px;
        }
    }
}
</style>