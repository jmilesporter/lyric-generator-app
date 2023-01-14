<script>
	import { isOverlayOpen } from '../stores/OverlayStore.js';
	import { lyrics } from '../stores/OverlayStore.js';
	import { loading } from '../stores/OverlayStore.js';

	export let data;
	const apiKey = data.key;
	const temperature = 2000

	async function onClick() {
		$lyrics = '';
		isOverlayOpen.set(true);
		try {
			$loading = true;
			const response = await fetch('https://api.openai.com/v1/completions', {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json',
					Authorization: `Bearer ${apiKey}`
				},
				body: JSON.stringify({
					model: 'text-davinci-003',
					prompt: lyricPrompt,
					temperature: temperature,
					max_tokens: 4000
				})
			});
			const data = await response.json();
			$loading = false;

			$lyrics = data.choices[0].text;

			if (response.status !== 200) {
				$loading = false;
				throw data.error || new Error(`Request failed with status ${response.status}`);
			}
		} catch (error) {
			// Consider implementing your own error handling logic here
			console.error(error);
			// alert(error.message);
		}
	}

	$: subject = '';
	$: genre = '';
	$: artist = '';
	$: songTitle = '';

	$: lyricPrompt = '';
	if (genre) {
	lyricPrompt = `${genre} lyrics `;
	}
	if (subject) {
	lyricPrompt = lyricPrompt.concat(` on the subject of ${subject}`)
	}
	if (artist) {
	lyricPrompt = lyricPrompt.concat(` in the style of ${artist}`)
	}
	if (songTitle) {
	lyricPrompt = lyricPrompt.concat(` called ${songTitle}`)
	}

</script>

<div class="grid place-items-center bg-slate-500 h-screen ">
	<input
		placeholder="s u b j e c t ( s )"
		class="absolute top-0 placeholder-white focus:placeholder-transparent text-center bg-slate-700 p-8 w-72 shadow-xl rounded-3xl text-white hover:translate-y-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-300  "
		bind:value={subject}
	/>
	<input
	placeholder="g e n r e ( s )"
	class="absolute top-0 placeholder-white focus:placeholder-transparent text-center bg-slate-700 p-8 w-72 shadow-xl rounded-3xl text-white hover:translate-y-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-300  "
	bind:value={genre}
	/>
	<input
		placeholder="a r t i s t ( s )"
		class="absolute bottom-0 placeholder-white focus:placeholder-transparent text-center bg-slate-700  p-8 w-72 shadow-xl rounded-3xl text-gray-200 hover:-translate-y-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-300  "
		bind:value={artist}
	/>
	<input
	placeholder="s u b j e c t ( s )"
	class="absolute top-0 placeholder-white focus:placeholder-transparent text-center bg-slate-700 p-8 w-72 shadow-xl rounded-3xl text-white hover:translate-y-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-300  "
	bind:value={songTitle}
	/>

	<button
		id="generate"
		class="bg-slate-900  p-8 w-72 shadow-xl rounded-3xl text-gray-200 hover:-translate-y-1 hover:scale-110 hover:bg-slate-800 hover: transition ease-in-out duration-500 delay-300  "
		on:click={() => {
			onClick();
		}}>g e n e r a t e &nbsp; l y r i c s</button
	>
</div>

<style>
	select {
		appearance: none;
		cursor: pointer;
	}
</style>
