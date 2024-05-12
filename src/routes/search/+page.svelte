<script lang="ts">

	import Button from '$lib/components/ui/buttons/button.svelte';
	import '../style.css';
	import SearchBar from '$lib/components/ui/searchBar/searchBar.svelte';
	import Layout from '../../layout/Layout.svelte';

</script>
  

<svelte:head>
	<title>Pokédex</title>
	<meta name="description" content="Svelte demo app" />

</svelte:head>
<Layout>
	<section class="section">
		<h1>Find your pokemon</h1>
		<SearchBar />
	</section>
</Layout>

<style>


 </style>