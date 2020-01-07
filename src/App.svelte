<script>
	import { Router, Route } from "svelte-routing";
	import Navbar from './layout/Navbar.svelte';
	import Home from './pages/Home.svelte'
</script>



<style>
	
</style>

<Router>
	<Navbar/>
	<div class="container">
		<Route path="/" component="{Home}" />
		<!-- placeholder until components are made -->
		<Route path="/" component="{Home}" />
		<Route path="/" component="{Home}" />
	</div>
</Router>