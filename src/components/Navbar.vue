<template>
	<div class="navbar" id="nav">
		<nav>
		<div class="nav-wrapper">
			<a href="#!" class="right brand-logo ">Recipes</a>
			<a href="#" data-target="mobile-demo" class="sidenav-trigger"><i class="material-icons">menu</i></a>
			<ul class="left hide-on-med-and-down">
				<li><router-link :to="{ name: 'home' }">Home</router-link></li>
				<li><router-link :to="{ name: 'about' }">About</router-link></li>
				<li><router-link :to="{ name: 'AddRecipes' }"><i class="material-icons">add_circle</i></router-link></li>
			</ul>
		</div>
		</nav>

		<ul class="sidenav" id="mobile-demo">
			<li><router-link to="/">Home</router-link></li>
			<li><router-link to="/about">About</router-link></li>
		</ul>
	</div>
</template>

<script>
	export default{
		data: () => ({
			name: 'Navbar'
		}),
		mounted(){
			
			document.addEventListener('DOMContentLoaded', function() {
				var elems = document.querySelectorAll('.sidenav');
				var instances = M.Sidenav.init(elems);
			});
		}


	}
</script>

