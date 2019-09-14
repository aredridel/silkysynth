<script>
	import webaudio from "webaudio";
	import { spring } from 'svelte/motion';

	const tau = Math.PI * 2;
	let frequency = 555
	let volume = 0;

	function sine(time, i) {
		return Math.sin(time * tau * frequency) * volume
	}

	const channel = webaudio(sine);

	channel.play();
</script>

<div style="position: absolute; right: 1em;">
	<label>
		<h3>volume ({volume})</h3>
		<input bind:value={volume} type="range" min="0" max="1" step="0.01">
	</label>
	<label>
		<h3>frequency ({frequency})</h3>
		<input bind:value={frequency} type="range" min="20" max="2000" step="0.01">
	</label>
</div>
