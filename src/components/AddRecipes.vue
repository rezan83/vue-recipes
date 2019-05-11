<template>
	<div class="container">
	<h2>Add New Recipe</h2>
	<div class="row">
    <form class="col m8" @submit.prevent="addRecipe">
      
      <div class="row">
        <div class="input-field col m8 s12">
          <input id="title" type="text" class="validate" v-model="title">
          <label for="title">Title</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col m8 s12">
          <input id="ingr" type="text" class="validate" v-model="ingr" @keydown.down="addIngr">
          <label for="ingr">Ingredient</label>
        </div>

      </div>
      <div class="row">
      	
      <p v-if="notification" class="red-text left">{{ notification }}</p>
      </div>
      <button class="btn waves-effect waves-light left" type="submit" name="action">Submit
	    <i class="material-icons right">send</i>
	  </button>
    </form>

    <div class="card col m4">	
     <div class="card-content">
        <i class="material-icons right delete" @click="delRecipe">delete</i>
     	<h6>new Recipe</h6>
        <h3 class="indigo-text">{{title}}</h3>
        <ul class="ingr">
          <li v-for="(ingr, index) in ingredients" :key="index">
            <span class="chip"><i class="material-icons right delete" @click="delIngr(ingr)">close</i>{{ingr}}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
  </div>

</template>

<script>
	import slugify from 'slugify'
export default {

  name: 'AddRecipes',

  data () {
    return {
    	title: null,
    	ingr : null,
    	ingredients: [],
    	notification: null,
    	slug: null
    }
  },
  methods: {
  	addIngr(){
  		if (this.ingr) {
  			this.ingredients.push(this.ingr)
  			this.ingr = null
  			this.notification = null
  		}else{
  			this.notification = 'add some value for Ingredients'
  		}
  	},
  	delIngr(ingr){
  		this.ingredients = this.ingredients.filter(item => item !== ingr)
  		console.log('delete '+ ingr)
  	},
  	addRecipe(){
  		if (this.title) {
  			this.slug = slugify(this.title, {
  			replacement: '-',
  			remove: /[$*_~+.()'"!@:\-]/g,
  			lower: true
	  		})
	  		db.collection('recipes').add({
	  			title: this.title,
	  			slug: this.slug,
	  			ingr: this.ingredients
	  		}).then(()=> {
	  			this.$router.push( {name: 'home'})
	  		}).catch((err) => {
	  			console.log(err)
	  		})
	  		this.title = null
  			this.notification = null
  		}else{
  			this.notification = 'add some value for title'
  		}
  		
  	},
  	delRecipe(){
  		this.title = null,
    	this.ingr = null,
    	this.ingredients = [],
    	this.notification = null,
    	this.slug = null
  	}

  }
}
</script>

<style lang="css">

.delete{
	cursor: pointer;
}
</style>