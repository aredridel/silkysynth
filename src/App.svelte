<script>
	import webaudio from "webaudio";
	import { spring } from 'svelte/motion';

	const tau = Math.PI * 2;
	let frequency = 555
	let volume = 0;
	let type = 'sine';

	function wave(time, i) {
		if (type == 'sine') {
			return Math.sin(time * tau * frequency) * volume
		} else if (type == 'square') {
			return (Math.sin(time * tau * frequency) > 0 ? 1 : -1) * volume
		}
	}

	const channel = webaudio(wave);

	channel.play();
</script>

<div>
	<label>
		<h3>volume ({volume})</h3>
		<input bind:value={volume} type="range" min="0" max="1" step="0.01">
	</label>
	<label>
		<h3>frequency ({frequency})</h3>
		<input bind:value={frequency} type="range" min="20" max="2000" step="0.01">
	</label>
	<fieldset>
		<legend>
			<h3>type ({type})</h3>
		</legend>
		<label><input type=radio bind:group={type} value='sine'> Sine</label>
		<label><input type=radio bind:group={type} value='square'> Square</label>
	</fieldset>
</div>
