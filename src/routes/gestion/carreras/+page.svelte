<script>
	import Controls from "../../../componentes/Tiempos/Controls.svelte";
	import Cronometro from "../../../componentes/Tiempos/Cronometro.svelte"
	let response = undefined
	let responseEquipos = undefined

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

	function marcarTiempos(carrera){
		fetch(`http://localhost:4000/api/carreraEquipos/${carrera}`,
        {method: 'GET',
		headers: {'authorization': `Bearer ${localStorage.getItem("token")}`}
		})
    	.then(res => res.json())
		.then(apiResponse =>{
			responseEquipos = apiResponse || []
			JSON.stringify(responseEquipos)
			console.log(apiResponse)
		})
	}
</script>

<head>
	<title>ListaCarreras</title>
</head>

<body>
	<br>
	<h1>Lista de carreras para gestionar</h1>

	<button class="btn btn-outline-success w-auto" on:click={obtenerCarreras}> Carreras </button>

	<a class="btn btn-outline-success w-auto" href="/">
	Volver
	</a>

	{#if response && response.length > 0}
		{#each response as carreras}
    		<div>
				<br>
				<button class="btn btn-outline-success" on:click={marcarTiempos(carreras.idCarrera)}> Carrera numero: {carreras.idCarrera} "{carreras.nombre}" </button>
				<br>
    		</div>
		{/each}
	{/if}

	{#if responseEquipos && responseEquipos.length > 0}
		<h1>Equipos de la carrera:</h1>
		<Cronometro></Cronometro>
		{#each responseEquipos as Equipos}
			<div>
				<br>
				<h3>Equipo: {Equipos.idEquipo} </h3>
				<br>
			</div>
		{/each}
	{/if}
</body>





