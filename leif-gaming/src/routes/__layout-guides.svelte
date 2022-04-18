<script>
	import Title from '$lib/title.svelte';
	import '../styles/global.css';
</script>

<header class="guides">
	<nav>
		<Title title="Leif Gaming Guides" />
		<div class="links">
			<a href="/">Home</a>
			<a href="/about">About</a>
			<a href="/guides">Guides</a>
		</div>
	</nav>
</header>
<main class="guides">
	<slot />
</main>
<footer class="guides">
	<p>Copyright &copy; 2022 Leif Eggenfellner</p>
</footer>

<style>
	header {
		text-align: center;
		background-color: rgba(0, 0, 0, 0.1);
	}

	main {
		max-width: 960px;
		margin: 20px auto;
	}

	footer {
		text-align: center;
	}

	.links {
		margin-left: auto;
	}

	a {
		margin-left: 10px;
	}

	nav {
		display: flex;
		align-items: center;
		max-width: 960px;
		margin: 0 auto;
	}
</style>
