<script>
</script>

<header>
	<div class="header-container">
		<div class="header-wrapper">
			<a href="/"> <h1 class="title">Lyric Generator</h1> </a>
			<div>
				<a href="/"><img class="logo" src="/generatorlogo.png" alt="Logo" /></a>

				<p class="subtitle">Lyrics generated with AI</p>
			</div>
			<div class="border-container" />
		</div>
	</div>
</header>
<main>
	<div class="container">
		<slot />
	</div>
</main>
<footer>
	<a
		href="https://docs.google.com/forms/d/e/1FAIpQLSdMJ0woyXr-PSIVSFEBsI9Vk5ofXol2F4JXR6mbUL2VHYBvkQ/viewform"
		class="submit-feedback"
	>
		s u b m i t &nbsp; f e e d b a c k
	</a>
	<p>
		l y r i c &nbsp; g e n e r a t o r &nbsp; 2 0 2 3 &nbsp; - &nbsp; v e r s i o n &nbsp; 0 . 1 . 0
	</p>
</footer>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		padding-left: 1rem;
		padding-right: 1rem;
		padding-top: 0;
		padding-bottom: 2rem;
		max-width: 800px;
		margin: 0 auto;
		background-color: #334155;
		min-height: 1000px;
	}

	.container {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
		width: 100%;
	}
	.header-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 1rem;
		max-width: 800px;
		margin: 0 auto;
		background-color: #334155;
		padding-bottom: 0;
		padding-top: 0;
		position: relative;
	}
	.header-wrapper {
		text-align: center;
		gap: 10px;
		position: relative;
		padding-top: 1rem;
		/* padding-bottom: 1rem; */
		/* margin-bottom: 1rem; */
	}
	.logo {
		position: absolute;
		width: 4rem;
		height: 4rem;
		object-fit: contain;
		left: 8%;
		bottom: 41%;
		cursor: pointer;
	}
	.title {
		font-size: 4rem;
		font-family: Arial, sans-serif;
		margin: 0;
		display: inline-block;
	}
	.subtitle {
		font-size: 1.5rem;
		margin: 0;
		margin-bottom: 1.5rem;
		color: #888;
		text-align: center;
		color: #9ca3af;
	}
	.border-container {
		max-width: 730px;
		width: 750px;
		border-bottom: 1px solid #ccc;
		bottom: 0%;
		display: flex;
		flex-direction: column;
		align-items: center;
		margin: 0 auto;
		background-color: #334155;
	}
	.submit-feedback {
		text-decoration: none;
		bottom: 3rem;
		color: #fff;
		text-align: center;
		margin-bottom: 1rem;
		border-radius: 1.5rem;
	}

	footer {
		text-align: center;
		margin-top: 2rem;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 1rem;
		max-width: 800px;
		margin: 0 auto;
		background-color: #334155;
	}

	a {
		text-decoration: none;
		color: inherit;
	}

	a:hover,
	a:focus {
		text-decoration: none;
		color: inherit;
	}
</style>
