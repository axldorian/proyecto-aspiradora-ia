<script lang="ts">
	import { onMount } from "svelte";
	import Board from "./components/Board.svelte";
	import Details from "./components/Details.svelte";

	let matriz: number[][] = Array.apply(null, Array(12)).map(() =>
		Array.apply(null, Array(12)).map(() => 0)
	);

	let basuras = 3;
	let remaining = 0;

	let isWorking = false;

	const iniciarMatriz = () => {
		matriz = Array.apply(null, Array(12)).map(() =>
			Array.apply(null, Array(12)).map(() => 0)
		);
	};

	const coordenada = () => {
		const c: number = Math.floor(
			Math.random() * (Math.floor(11) - Math.ceil(0) + 1) + Math.ceil(0)
		);
		return c;
	};

	const iniciarAspiradora = () => {
		const x = coordenada();
		const y = coordenada();

		matriz[x][y] = 2;
	};

	const generarBasuras = (basuras: number) => {
		for (let i = 0; i < basuras; i++) {
			const x = coordenada();
			const y = coordenada();

			if (matriz[x][y] === 0 && matriz[x][y] != 2) {
				matriz[x][y] = 1;
			} else {
				i--;
			}
		}
	};

	const reiniciarAspiradora = () => {
		iniciarMatriz();
		iniciarAspiradora();
	};

	onMount(() => reiniciarAspiradora());
</script>

<main>
	<section id="panel">
		<h1>AGENTE ASPIRADORA</h1>
		<div style="margin: 1em; text-align: center">
			<p style="display: inline;">Basuras para Agregar:</p>
			<input
				type="number"
				min="1"
				max="143"
				bind:value={basuras}
				disabled={isWorking}
			/>
			<button
				on:click={() => {
					if (remaining + basuras > 143) return;
					remaining += basuras;
					generarBasuras(basuras);
				}}
				disabled={isWorking}
			>
				Agregar
			</button>
		</div>

		<div style="margin: 1em; text-align: center; margin-bottom: 60px">
			<button
				style="margin-right: 10px;"
				on:click={() => {
					isWorking = true;
				}}>Iniciar agente</button
			>
			<button
				on:click={() => {
					isWorking = false;
					remaining = 0;
					reiniciarAspiradora();
				}}>Reiniciar</button
			>
		</div>

		<Details />
	</section>

	<Board {matriz} />
</main>

<style>
	main {
		display: flex;
		width: 100vw;
		height: 100vh;
		gap: 120px;
		padding: 26px;
		justify-content: center;
		align-items: center;
	}

	h1 {
		font-size: 30px;
		margin-bottom: 40px;
		font-family: "Pixeled", consolas;
	}

	p {
		font-size: 20px;
	}

	input {
		padding: 8px;
		border: 1px solid #e1e1e1;
		font-size: 16px;
	}

	button {
		padding: 10px 14px;
		border: none;
		background-color: #c23334;
		cursor: pointer;
		color: #ffffff;
		font-size: 16px;
	}

	button:hover:not(:disabled) {
		background-color: #b41414;
	}

	button:active:not(:disabled) {
		background-color: #c73c3c;
	}

	button:disabled {
		cursor: not-allowed;
	}

	#panel {
		flex-grow: 0;
		background-color: rgba(172, 210, 235);
		border-top: 45px solid rgba(172, 210, 235, 0.845);
		border-bottom: 45px solid rgba(172, 210, 235, 0.845);
		padding: 40px;
	}
</style>