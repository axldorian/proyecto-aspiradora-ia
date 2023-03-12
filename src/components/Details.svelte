<script lang="ts">
	export let cleaned = 0;
	export let movements = 0;
	export let crono = 0;
</script>

<div id="details">
	<div>
		<p>Basuras Limpiadas</p>
		<span>{cleaned}</span>
	</div>
	<div>
		<p>Movimientos</p>
		<span>{movements}</span>
	</div>
	<div>
		<p>Cronometro</p>
		<span>{crono}</span>
	</div>
</div>

<style>
	#details {
		width: 100%;
	}

	#details > div {
		margin-bottom: 10px;
		width: 100%;
	}

	#details > div p {
		font-size: 24px;
		text-align: center;
	}

	#details > div span {
		display: block;
		width: 100%;
		font-size: 28px;
		text-align: center;
	}
</style>
