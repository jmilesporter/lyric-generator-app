<script>
	import { isOverlayOpen, lyrics, loading } from '../stores/OverlayStore.js';

	export let data;
	const apiKey = data.key;
	let rangeValue = 70;

	function formatPayload() {
		if (genre) {
			lyricPrompt = `${genre} `;
		}
		lyricPrompt = `lyrics`;
		if (subject) {
			lyricPrompt = lyricPrompt.concat(` on the subject of ${subject}`);
		}
		if (artist) {
			lyricPrompt = lyricPrompt.concat(` in the style of ${artist}`);
		}
		// if (songTitle) {
		// 	lyricPrompt = lyricPrompt.concat(` of a song named ${songTitle}`);
		// }
		if (lyricPrompt === 'lyrics') {
			lyricPrompt = 'lyrics on any subject in any style';
		}
	}

	function helpModal() {
		lyrics.set(
			`This is a prompt engineering interface for OpenAI's GPT-3 API. It's a text generator that can write lyrics in the style of any artist. You can also specify a subject to write about. The more specific you are, the better the results.`
		);
		isOverlayOpen.set(true);
	}
	let clicked = false;

	function preventMultiClick() {
		if (clicked) return;

		clicked = true;
		setTimeout(() => {
			clicked = false;
		}, 3000);

		// console.log('click');
	}

	async function generateLyrics() {
		preventMultiClick();

		$lyrics = '';
		isOverlayOpen.set(true);
		formatPayload();
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
					temperature: (150 - rangeValue) / 100,
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
	// $: songTitle = '';
	$: lyricPrompt = '';
</script>

<div class="grid place-items-center bg-slate-900 h-screen ">
	<button
		class="absolute full:top-4 full:right-4 xs:bottom-48 placeholder-white focus:placeholder-transparent text-center bg-slate-700 w-12 h-12 shadow-xl rounded-full text-gray-200 hover:-translate-x-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-400  "
		on:click={() => {
			helpModal();
		}}>?</button
	>
	<input
		placeholder="s u b j e c t ( s )"
		class="absolute xs:top-0 full:top-0 full:top-none placeholder-white focus:placeholder-transparent text-center bg-slate-700 p-8 w-72 shadow-xl rounded-3xl text-white hover:translate-y-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-300  "
		bind:value={subject}
	/>
	<input
		placeholder="g e n r e ( s )"
		class="absolute xs:top-24 full:right-0 placeholder-white focus:placeholder-transparent text-center bg-slate-700 p-8 w-72 shadow-xl rounded-3xl text-white hover:-translate-x-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-300  "
		bind:value={genre}
	/>
	<input
		placeholder="a r t i s t ( s )"
		class="absolute xs:top-48 full:left-0 placeholder-white focus:placeholder-transparent text-center bg-slate-700  p-8 w-72 shadow-xl rounded-3xl text-gray-200 hover:translate-x-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-300  "
		bind:value={artist}
	/>
	<!-- <input
		placeholder="s o n g   t i t l e"
		class="absolute xs:top-72 full:left-0 placeholder-white focus:placeholder-transparent text-center bg-slate-700 p-8 w-72 shadow-xl rounded-3xl text-white hover:translate-y-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-300  "
		bind:value={songTitle}
	/> -->
	<!-- <div class="absolute bottom-60 placeholder-white focus:placeholder-transparent text-center bg-slate-700 p-8 w-72 shadow-xl rounded-3xl text-white "> -->
	<div
		class="absolute xs:bottom-24 full:bottom-60 placeholder-white focus:placeholder-transparent text-center bg-slate-700 p-2 w-60 shadow-xl rounded-3xl text-white "
	>
		<div>p r e d i c t a b i l i t y</div>
		<label>
			<input
				class="hover:translate-x-1 hover:scale-110 hover:bg-slate-600 hover: transition ease-in-out duration-500 delay-300 hover:accent-[#ffa64c] accent-[#fb8200]"
				type="range"
				bind:value={rangeValue}
				min="0"
				max="150"
			/>
		</label>
	</div>

	<button
		id="generate"
		class=" absolute bg-[#fb8200] xs:top-96  p-8 w-72 shadow-xl rounded-3xl text-slate-900 hover:-translate-y-1 hover:scale-110 hover:bg-[#ffa64c] hover: transition ease-in-out duration-500 delay-300  "
		on:click={() => {
			generateLyrics();
		}}>g e n e r a t e &nbsp; l y r i c s</button
	>
	<a
		href="https://docs.google.com/forms/d/e/1FAIpQLSdMJ0woyXr-PSIVSFEBsI9Vk5ofXol2F4JXR6mbUL2VHYBvkQ/viewform"
		class="absolute xs:bottom-12 full:bottom-12 placeholder-white focus:placeholder-transparent text-center rounded-3xl text-white "
		>s u b m i t &nbsp; f e e d b a c k</a
	>
</div>

<style>
	select {
		appearance: none;
		cursor: pointer;
	}
</style>
