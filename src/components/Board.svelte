<script lang="ts">
	import vacuum from "../assets/aspiradora.png";
	import garbage from "../assets/basura.png";

	export let matriz: number[][];
</script>

<div id="board">
	{#each matriz as row}
		{#each row as column}
			<div class="cell">
				{#if column === 1}
					<img src={garbage} alt="g" />
				{:else if column === 2}
					<img src={vacuum} class="move" alt="v" />
				{/if}
			</div>
		{/each}
	{/each}
</div>

<style>
	#board {
		width: fit-content;
		height: auto;
		display: grid;
		grid-template-rows: repeat(12, 1fr);
		grid-template-columns: repeat(12, 1fr);
		border: 1px solid #999;
	}

	.cell {
		width: 55px;
		height: 55px;
		border: 1px solid #999;
		background-color: #ddd;
	}

	.cell img {
		width: 100%;
	}
</style>
