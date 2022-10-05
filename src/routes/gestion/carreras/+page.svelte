<script>
	import Controls from "../../../componentes/Tiempos/Controls.svelte";
import Cronometro from "../../../componentes/Tiempos/Cronometro.svelte"
	let response = undefined

	function obtenerCarreras(){
		fetch('http://localhost:4000/api/carreras',
        {method: 'GET',
		headers: {'authorization': `Bearer ${localStorage.getItem("token")}`}
		})
    	.then(res => res.json())
		.then(apiResponse =>{
			response = apiResponse || []
			JSON.stringify(response)
			console.log(apiResponse)
		})
	}
</script>

<body>
	<title>ListaCarreras</title>
</body>
<br>
<h1>Lista de carreras para gestionar</h1>

<button class="btn btn-outline-success" on:click={obtenerCarreras}> Carreras </button>

<a class="btn btn-outline-success" href="/">
	Volver
</a>

{#if response && response.length > 0}
	{#each response as carreras}
    	<div>
			<br>
			<button class="btn btn-outline-success"> Carrera numero: {carreras.idCarrera} "{carreras.nombre}" </button>
			<br>
    	</div>
	{/each}
{/if}

<Cronometro></Cronometro>