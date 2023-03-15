<script>
	import { lyrics } from '../../stores/OverlayStore.js';
</script>

<span>this is working</span>
<span class="lyrics">{lyrics}</span>

<style>
	.lyrics {
		font-size: 1.5rem;
		line-height: 1.5;
		font-family: 'Roboto', sans-serif;
		white-space: pre-wrap;
		color: white;
		height: 100%;
		width: 100%;
	}
</style>
