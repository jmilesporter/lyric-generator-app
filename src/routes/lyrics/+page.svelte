<script>
	import { onMount } from 'svelte';
	import { navigate } from 'svelte-routing';
	import { lyrics, loading } from '../../stores/OverlayStore.js';

	onMount(() => {
		if (!$lyrics) {
			navigate('/');
		}
	});
	let clicked = false;
	function copyText() {
		/* Copy selected text into clipboard */
		navigator.clipboard.writeText($lyrics);
	}
	function isClicked() {
		clicked = true;
		setTimeout(() => {
			clicked = false;
		}, 2000);
	}
</script>

<section class="container">
	{#if $loading}
		<span class="loading">
			<span class="letter" style="animation-delay: 0s;">l</span>
			<span class="letter" style="animation-delay: 0.1s;">o</span>
			<span class="letter" style="animation-delay: 0.2s;">a</span>
			<span class="letter" style="animation-delay: 0.3s;">d</span>
			<span class="letter" style="animation-delay: 0.4s;">i</span>
			<span class="letter" style="animation-delay: 0.5s;">n</span>
			<span class="letter" style="animation-delay: 0.6s;">g</span>
		</span>
	{/if}
	{#if !$loading}
		{#if !clicked}
			<span class="lyrics">{$lyrics} </span>
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<i
				class="fa-solid fa-copy copy-button "
				on:click={() => {
					copyText();
					isClicked();
				}}
			/>
		{/if}
		{#if clicked}
			<span class="lyrics">{$lyrics} </span>

			<i class="fa-solid fa-copy copy-button-2" />
		{/if}
	{/if}
</section>

<style>
	.container {
		display: flex;
		justify-content: center;
		align-items: flex-start;
		height: 100%;
		width: 100%;
	}

	.lyrics {
		white-space: pre-wrap;
		line-height: 1.5rem;
		font-family: 'Courier New', Courier, monospace;
		color: #e5e7eb;
	}

	.loading {
		color: #e5e7eb;
		font-family: 'Courier New', Courier, monospace;
		text-align: center;
		margin-top: calc(40% - 20px); /* adjust this value to move the loading text down */
	}

	@keyframes loadingBounce {
		0%,
		100% {
			transform: translateY(0);
		}
		50% {
			transform: translateY(-10px);
		}
	}
	.letter {
		display: inline-block;
		animation: loadingBounce 1s infinite;
	}

	.copy-button {
		position: absolute;
		top: 1.5rem;
		right: 1.5rem;
		cursor: pointer;
		font-family: 'Font Awesome 5 Free';
		font-weight: 400;
		font-style: regular;
		font-size: 1.5rem;
		color: #e5e7eb;
		opacity: 0.3;
		transition: opacity 300ms ease-in-out 300ms;
		margin: 1rem;
	}
	.copy-button-2 {
		position: absolute;
		top: 1.5rem;
		right: 1.5rem;
		cursor: pointer;
		font-family: 'Font Awesome 5 Free';
		font-weight: 400;
		font-style: regular;
		font-size: 1.5rem;
		color: #10b981;
		opacity: 1;
		transition: opacity 300ms ease-in-out 300ms;
		margin: 1rem;
	}

	.copy-button:hover {
		opacity: 1;
	}
	section {
		position: relative;
	}
</style>
