<template>
  <div>
    
    <h2>{{ msg }}</h2>
  <div class="home container">

    <div class="card"  v-for="(item, index) in recipes" :key="index">  
      <div class="card-content">
        <i class="material-icons delete" @click="deleteRecipe(index)">delete</i>
        <i class="material-icons edit">edit</i>
        <h2 class="indigo-text">{{item.title}}</h2>
        <ul class="ingr">
          <li v-for="(ingr, index) in item.ingr" :key="index">
            <span class="chip">{{ingr}}</span>
          </li>
        </ul>
      </div>
      
    </div>
   
  </div>
  </div>
</template>

<script>
  import db from '@/firebase/init'
export default {
  data: function() {
    return ({
      name: 'Home',
      recipes: []
    })

  },
  props: {
    msg: String
  },
  methods: {
    deleteRecipe(index){
      console.log(index + ' index clicked')
      this.recipes = this.recipes.filter(item => this.recipes.indexOf(item) !== index)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 30px;
  margin-top: 30px;
}
.home h2{
  font-size: 1.8em;
}
.home .delete{
  position: absolute;
  top: 4px;
  right: 4px;
  cursor: pointer;
  font-size: 1.4em;
  color: #DC5EA6;
}
.home .edit{
  position: absolute;
  top: 4px;
  left: 30px;
  cursor: pointer;
  font-size: 1.4em;
  color: dodgerblue;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
