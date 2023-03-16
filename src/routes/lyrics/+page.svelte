<script>
	import { lyrics } from '../../stores/OverlayStore.js';
</script>

<section>
	<span class="lyrics">{$lyrics} </span>
</section>

<style>
	.lyrics {
		white-space: pre-wrap;
		line-height: 1.5rem;
		font-family: 'Courier New', Courier, monospace;
		color: #e5e7eb;
		height: 100%;
		width: 100%;
	}
</style>
