<script>
	import Title from '$lib/title.svelte';
	import '../styles/global.css';
</script>

<header>
	<Title title="Leif Gaming Guides" />
</header>
<main>
	<slot />
</main>
<footer>
	<p>Copyright &copy; 2022 Leif Eggenfellner</p>
</footer>

<style>
	header {
		display: flex;
		justify-content: center;
	}

	main {
		max-width: 960px;
		margin: 20px auto;
	}

	footer {
		text-align: center;
	}
</style>
