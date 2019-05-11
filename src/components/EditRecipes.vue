<template>
	<div v-if="recipe" class="container">
		<h1 > Edit your Recipe: {{ recipe.title }}</h1>

		<div class="card col m4">	
	     <div class="card-content">
	        <i class="material-icons right delete" @click="delRecipe">delete</i>
	     	<h6>Edit Recipe</h6>
	        <h3 class="indigo-text">{{recipe.title}}</h3>
	        <ul class="ingr">
	          <li v-for="(ingr, index) in recipe.ingr" :key="index">
	            <span class="chip"><i class="material-icons right delete" @click="delIngr(ingr)">close</i>{{ingr}}</span>
	          </li>
	        </ul>
	      </div>
	    </div>
	  

		<form class="col m8" @submit.prevent="editRecipe">
		  
		  <div class="row">
		    <div class="input-field col m8 s12">
		      <input id="title" type="text" class="validate" v-model="recipe.title">
		      <label for="title">Title</label>
		    </div>
		  </div>

		  <div class="row">
		    <div class="input-field col m8 s12" v-for="(ingr, index) in recipe.ingr">
		      <input id="ingr" type="text" class="validate" v-model="recipe.ingr[index]" 
		      @keydown.down="addIngr(recipe.ingr[index])" >
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

	</div>
</template>

<script>
	import slugify from 'slugify'
export default {

  name: 'EditRecipes',

  data () {
    return {
    	recipe: null,
    	notification: null
    }
  },
  methods: {
  	delRecipe(){
  		this.recipe = null,
    	this.notification = null
  	},
  	editRecipe(){
  		if (this.recipe.title) {
  			this.recipe.slug = slugify(this.recipe.title, {
  			replacement: '-',
  			remove: /[$*_~+.()'"!@:\-]/g,
  			lower: true
	  		})
	  		db.collection('recipes').doc(this.recipe.id).update({
	  			title: this.recipe.title,
	  			slug: this.recipe.slug,
	  			ingr: this.recipe.ingr
	  		}).then(()=> {
	  			this.$router.push( {name: 'home'})
	  		}).catch((err) => {
	  			console.log(err)
	  		})
	  		this.recipe.title = null
  			this.recipe.notification = null
  		}else{
  			this.notification = 'add some value for title'
  		}

  	},
  	addIngr(ingr){
  		if (ingr) {
  			this.recipe.ingr.push(ingr)
  			this.recipe.notification = null
  		}else{
  			this.notification = 'add some value for Ingredients'
  		}
  	},
  	delIngr(ingr){
  		this.recipe.ingr = this.recipe.ingr.filter(item => item !== ingr)
  		console.log('delete '+ ingr)
  	},

  },
  created(){

	let recipe = db.collection("recipes").where('slug', '==', this.$route.params.recipes_slug)
	recipe.get().then( (querySnapshot) => {
		querySnapshot.forEach(doc => {
			this.recipe = doc.data()
			this.recipe.id = doc.id
		})
      	
      })
    }
}
</script>

<style lang="css" scoped>
</style>