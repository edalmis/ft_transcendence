<script lang="ts">
	import { goto } from "$app/navigation";

	// Url Redirection Lorsque click Button   *-[ Login ]-*   .

	function handleLogin() {
		const host = import.meta.env.VITE_HOST;
		const loginUrl = `http://${host}:3000/auth/42`;
		// console.log("LoginButton ENV->host: ", host);
		goto(loginUrl);
	}

	// Colometrie Du 'et des' Button's'
	const colors = ["green", "yellow", "orange", "red"];
	let selected: string = colors[0];
	let a: number = 0;
	let b: number = colors.length - 1;
</script>

<div>
	<button
		class="bigButton"
		style="background-color: {selected}"
		on:click={handleLogin}
	>
		Log in</button
	>
	<div class="pick-a-color">
		{#each colors as color, i}
			<button
				class="round-button"
				aria-current={selected === color}
				aria-label={color}
				style="background: {color}"
				on:click={() => (selected = color)}>{i + 1}</button
			>
		{/each}
	</div>
</div>

<style>
	div {
		align-items: center;
		grid-template-columns: repeat(7, 1fr);
		grid-gap: 5px;
		max-width: 400px;
	}

	.pick-a-color {
		margin-top: 400px;
		align-items: center;
	}

	.round-button {
		width: 1em;
		height: 1em;
		border-radius: 50%;
		background: var(--color, #fff);
		transform: translate(-2px, -2px);
		filter: drop-shadow(2px 2px 3px rgba(0, 0, 0, 0.2));
		transition: all 0.1s;
		margin-right: 9%;
		font-size: small;
	}

	.bigButton {
		cursor: not-allowed;
		font: medium;
		width: 6em;
		height: 6em;
		border-radius: 50%;
		box-shadow:
			0 8px 0 hsl(0, 100%, 30%),
			2px 12px 10px rgba(0, 0, 0, 0.35);
		color: hsl(0, 100%, 30%);
		text-shadow:
			-1px -1px 2px rgba(0, 0, 0, 0.3),
			1px 1px 2px rgba(255, 255, 255, 0.4);
		text-transform: uppercase;
		letter-spacing: 0.05em;
		transform: translate(0, -8px);
		transition: all 0.2s;
		margin-top: 190%;
		transition: color 4.2s;
	}

	.bigButton:active {
		transform: translate(0, -2px);
		box-shadow:
			0 2px 0 hsl(0, 100%, 30%),
			2px 6px 10px rgba(0, 0, 0, 0.35);
	}

	button[aria-current="true"] {
		transition: color 0.2s;
		transform: none;
		filter: none;
		box-shadow: inset 3px 3px 4px rgba(0, 0, 0, 0.2);
	}
</style>
