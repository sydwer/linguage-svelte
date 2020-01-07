<script>
	import { Router, Route } from "svelte-routing";
	import Navbar from './layout/Navbar.svelte';
	import Home from './pages/Home.svelte'
	import Explore from './pages/Explore.svelte'
	import Compare from './pages/Compare.svelte'
	import Create from './pages/Create.svelte'
</script>



<style>
	
</style>

<Router>
	<Navbar/>
	<div class="container">
		<Route path="/" component="{Home}" />
		<Route path="/explore" component="{Explore}" />
		<Route path="/compare" component="{Compare}" />
		<Route path="/create" component="{Create}" />
	</div>
</Router>