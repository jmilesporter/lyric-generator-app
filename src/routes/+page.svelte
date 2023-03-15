<!-- App.svelte -->
<script>
	import { lyrics } from '../stores/OverlayStore.js';

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
		// isOverlayOpen.set(true);
		formatPayload();
		try {
			// $loading = true;
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

			// $loading = false;

			$lyrics = data.choices[0].text;

			if (response.status !== 200) {
				// $loading = false;
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

	export let title = 'Lyric Generator';
</script>

<head>
	<title>{title}</title>
</head>

<header>
	<div class="header-container">
		<div class="header-wrapper">
			<h1 class="title">{title}</h1>
			<p class="subtitle">Lyrics generated with AI</p>
			<div class="border-container" />
		</div>
	</div>
</header>

<main>
	<div class="container">
		<section>
			<h2 class="subtitle">
				Do you struggle with writing lyrics for your songs? Look no further than Lyric Generator!
			</h2>
			<p>
				Our powerful AI algorithm will help you create catchy and meaningful lyrics in no time.
				Simply input a few keywords, and our software will do the rest.
			</p>
		</section>

		<section>
			<h2 class="subsubtitle">How it Works</h2>

			<ol>
				<li>Choose a genre that has lyrics, like 60's pop or psychedelic folk.</li>
				<li>Enter a subject for your song. This can be a single word or a whole line!</li>
				<li>Choose an artist you want the lyrics to sound like.</li>
				<li>
					Be creative! What would a New Wave version of Kendrick Lamar sound like? A reggaeton
					version of Nirvana?
				</li>
				<li>Click the "Generate Lyrics" button.</li>
				<li>Enjoy your new lyrics!</li>
			</ol>
		</section>

		<div class="wrapper">
			<div class="input-wrapper-left">
				<label for="genre-input">g e n r e</label>
				<div class="input-container">
					<input
						class="custom-input"
						type="text"
						id="genre-input"
						placeholder="enter your genre..."
						bind:value={genre}
					/>
				</div>
			</div>

			<div class="input-wrapper-center">
				<label for="subject-input">s u b j e c t</label>
				<div class="input-container-top">
					<input
						class="custom-input"
						type="text"
						id="subject-input"
						placeholder="enter your subject..."
						bind:value={subject}
					/>
				</div>
			</div>

			<div class="input-wrapper-right">
				<label for="artist-input">a r t i s t</label>
				<div class="input-container-right">
					<input
						class="custom-input"
						type="text"
						id="artist-input"
						placeholder="enter your artist..."
						bind:value={artist}
					/>
				</div>
			</div>

			<button
				class="generate-lyrics"
				on:click={() => {
					generateLyrics();
				}}
			>
				g e n e r a t e &nbsp; l y r i c s
			</button>
			<div class="predictability-container">
				<div>p r e d i c t a b i l i t y</div>
				<label>
					<input class="range-slider" type="range" bind:value={rangeValue} min="0" max="150" />
				</label>
			</div>
		</div>

		<div class="ads">
			<!-- ad code here -->
		</div>

		<section>
			<h2 class="subsubtitle">Benefits of Using Lyric Generator</h2>
			<ul>
				<li>
					<h3>Save time and effort</h3>
					Never again will you have to struggle to come up with the perfect words to match your melody.
					Lyric Generator does the hard work for you, leaving you free to focus on what really matters
					- making music!
				</li>
				<li>
					<h3>Improve the quality of your lyrics</h3>
					Our AI algorithm takes your input and generates lyrics that are not only catchy but also meaningful.
					Say goodbye to generic and uninspired lyrics, and hello to truly original and impactful songwriting.
				</li>
				<li>
					<h3>Explore new topics and themes</h3>
					Lyric Generator provides a wealth of inspiration and ideas for your songwriting. Whether you're
					looking to write a love ballad or a protest anthem, our software can help you explore new topics
					and themes to create truly unique and memorable songs.
				</li>
				<li>
					<h3>Find inspiration for new songs</h3>
					Stuck in a creative rut? Lyric Generator can help! Our powerful software generates fresh and
					exciting lyrics that can inspire you to create your next hit song.
				</li>
			</ul>
		</section>
		<section>
			<h2 class="subsubtitle">What Our Users Are Saying</h2>
			<!-- <div class="border-container" /> -->
			<div class="testimonial-container">
				<div class="testimonial-wrapper">
					<div class="testimonial">
						<p class="testimonial-text">
							"As someone who struggles with writing lyrics, Lyric Generator has been a
							game-changer. I highly recommend it to anyone looking to improve their songwriting."
						</p>
						<p class="testimonial-author">- Alex James, Singer-Songwriter</p>
					</div>

					<div class="testimonial">
						<p class="testimonial-text">
							"I was blown away by how accurate and relevant the lyrics generated by Lyric Generator
							were. It's like the software could read my mind!"
						</p>
						<p class="testimonial-author">- Sarah Parker, Music Producer</p>
					</div>

					<div class="testimonial">
						<p class="testimonial-text">
							"I've tried other lyric generators before, but Lyric Generator is by far the best.
							It's easy to use and produces amazing results."
						</p>
						<p class="testimonial-author">- David Lee, Singer</p>
					</div>

					<div class="testimonial">
						<p class="testimonial-text">
							"Thanks to Lyric Generator, I've been able to write more songs in less time. It's
							truly a lifesaver!"
						</p>
						<p class="testimonial-author">- Maria Rodriguez, Musician</p>
					</div>
				</div>
			</div>
		</section>
	</div>
	<div><span>{$lyrics}</span></div>
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
		padding: 1rem;
		max-width: 800px;
		margin: 0 auto;
		background-color: #334155;
	}
	ol {
		/* list-style-position: inside; */
		list-style-type: none; /* remove the default numbering */
		padding-left: 1em; /* add some left padding for the list items */
	}
	ul {
		list-style-position: inside;
	}
	li {
		text-align: center;
		margin-bottom: 0.5em; /* add some space between list items */
	}
	.wrapper {
		position: relative;
		display: flex;
		justify-content: center;
		align-items: flex-start;
		margin: 1rem;
		padding: 1rem;
		border: 1px solid #ccc;
		border-radius: 1.5rem;
		max-width: 800px;
		height: 400px;
	}

	.ads {
		display: flex;
		justify-content: space-between;
		margin: 1rem 0;
	}

	.header-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 1rem;
		max-width: 800px;
		margin: 0 auto;
		background-color: #334155;
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

	.header-wrapper {
		text-align: center;
		/* padding-bottom: 1rem; */
		margin-bottom: 1rem;
	}

	.title {
		font-size: 4rem;
		font-family: Arial, sans-serif;
		margin: 0;
	}

	.subtitle {
		font-size: 1.5rem;
		margin: 0;
		margin-bottom: 1.5rem;
		color: #888;
		text-align: center;
		color: #9ca3af;
	}

	.subsubtitle {
		font-size: 2rem;
		margin: 1rem 0 0.5rem;
		font-weight: bold;
		text-align: center;
	}
	.sub-section-title {
		text-align: center;
		font-weight: bold;
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
	.testimonial-container {
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 1rem;
	}

	.testimonial-wrapper {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-evenly;
	}

	.testimonial {
		margin: 1rem;
		padding: 1rem;
		border: 1px solid #e5e7eb;
		border-radius: 1.5rem;
		width: 300px;
		height: 200px;
	}

	.testimonial-text {
		font-style: italic;
	}

	.testimonial-author {
		text-align: right;
		font-weight: bold;
		margin-top: 0.5rem;
		margin-bottom: 0;
	}
	/* Input styling */
	.input-wrapper-center {
		display: flex;
		flex-direction: column;
		margin-bottom: 1rem;
		position: absolute;
		outline: none;
		font-family: Arial, Helvetica, sans-serif;
		/* transition: transform 500ms ease-in-out 300ms, background-color 500ms ease-in-out; */
	}
	.input-wrapper-left {
		display: flex;
		flex-direction: column;
		margin-bottom: 1rem;
		position: absolute;
		left: 0%;
		font-family: Arial, Helvetica, sans-serif;
	}
	.input-wrapper-right {
		display: flex;
		flex-direction: column;
		margin-bottom: 1rem;
		position: absolute;
		right: 0%;
		font-family: Arial, Helvetica, sans-serif;
	}

	.input-container {
		position: relative;
		text-align: center;
		width: 15rem;
	}

	input[type='text'] {
		padding: 0.5rem 2rem 0.5rem 0.5rem;
		border-radius: 0.5rem;
		background-color: #1f2937;
		/* transition: all 0.2s ease-in-out; */
		width: 100%;
		max-width: 8rem;
		margin: 2rem;
		margin-top: 0rem;
		top: 0%;
		left: 0%;
	}
	input::placeholder {
		color: #e5e7eb;
		font-family: Arial, Helvetica, sans-serif;
	}

	input:focus {
		/* border-color: #e5e7eb; */
		outline: 1px solid #e5e7eb;
	}

	input[type='text']:focus {
		border: 1px solid #e5e7eb;
		/* box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3); */
	}

	label {
		margin-bottom: 0.5rem;
	}

	.input-icon {
		position: absolute;
		right: 0.5rem;
		top: 50%;
		transform: translateY(-50%);
		color: #e5e7eb;
	}

	.input-icon i {
		font-size: 1rem;
	}

	.input-icon:hover {
		color: #e5e7eb;
	}

	/* Button styling */
	.generator-btn {
		box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
	}

	.generate-lyrics {
		display: inline-block;
		border: none;
		background-color: #fb8200;
		padding: 2rem;
		position: absolute;
		top: 40%;
		width: 16rem;
		max-width: 18rem;
		max-height: 5rem;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		border-radius: 1.5rem;
		color: #0f172a;
		cursor: pointer;
		transform: translateY(0) scale(1);
	}
	.generator-btn:hover {
		transform: translateY(-1px);
		box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
	}

	.generator-btn:active {
		transform: translateY(1px);
		box-shadow: none;
	}

	.generate-lyrics:hover {
		transform: translateY(-0.25rem) translateX(0.75rem) scale(1.1);
		background-color: #ffa64c;
	}
	.submit-feedback {
		text-decoration: none;
		bottom: 3rem;
		color: #fff;
		text-align: center;
		margin-bottom: 1rem;
		border-radius: 1.5rem;
	}
	.submit-feedback::placeholder {
		color: #fff;
	}
	.submit-feedback:focus::placeholder {
		color: transparent;
	}

	.predictability-container {
		bottom: 10%;
		position: absolute;
		text-align: center;
		background-color: #1f2937;
		padding: 0.5rem;
		width: 15rem;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		border-radius: 1.5rem;
		color: #e5e7eb;
		cursor: pointer;
		font-family: Arial, Helvetica, sans-serif;
		font-size: small;
	}
	.predictability-container::placeholder {
		color: #e5e7eb;
	}
	.predictability-container:focus::placeholder {
		color: transparent;
	}

	.range-slider {
		cursor: pointer;
		transform: translateX(0) scale(1);
		background-color: #1f2937;
		/* transition: transform 500ms ease-in-out 300ms, background-color 500ms ease-in-out; */
	}
	.range-slider:hover {
		transform: translateX(0.25rem) scale(1.1);
		background-color: #29364d;
	}

	.custom-input {
		background-color: #1f2937;
		margin-top: 1rem;
		padding: 0.5rem;
		width: 100%;
		border: none;
		border-radius: 1.5rem;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		color: #e5e7eb;
		outline: none;
		/* transition: transform 500ms ease-in-out 300ms, background-color 500ms ease-in-out; */
	}

	.custom-input::placeholder {
		color: #e5e7eb;
	}

	.custom-input:focus::placeholder {
		color: transparent;
	}

	.custom-input:hover {
		/* transform: translateY(-0.25rem) scale(1.1); */
		transform: translateY(-0.25rem) translateX(0.75rem) scale(1.1);
		background-color: #29364d;
	}
</style>
