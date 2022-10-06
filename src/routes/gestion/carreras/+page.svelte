<script>
	import Cronometro from "../../../componentes/Tiempos/Cronometro.svelte"
	let response = undefined
	let responseEquipos = undefined
	let v = undefined

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

	function recolectarEquipos(carrera, vueltas){
		v = vueltas
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
	<br>
	<div class="botonera">
		<button class="btn btn-primary w-100" on:click={obtenerCarreras}> Obtener</button>
		<a class="btn btn-outline-primary w-100" href="/">
			Volver
		</a>
	</div>
	
	<div class="botonera">
		{#if response && response.length > 0}
			{#each response as carreras}
				<div>
					<br>
					<button class="btn btn-primary w-100" on:click={recolectarEquipos(carreras.idCarrera, carreras.vueltas)}> Carrera numero: {carreras.idCarrera} "{carreras.nombre}" </button>
				</div>
			{/each}
		{/if}
	</div>

	{#if responseEquipos && responseEquipos.length > 0}
		<br>
		<h1 class="vueltas">Vueltas de la carrera: <strong>{v}</strong></h1>
		<br>
		<Cronometro></Cronometro>
		<br>
		<h2>Equipos de la carrera:</h2>
		<br>
		<div class="linea">
			{#each responseEquipos as Equipos}
				<h5>
				Equipo {Equipos.idEquipo}
				<button class="btn btn-success w-50"> Marcar vuelta </button>
				</h5>
			{/each}
		</div>
		<br><br><br><br>
	{/if}
	
</body>

<style>
	*{
	  margin: 0;
	  padding: 0;
	  box-sizing: border-box;
  	}	
	body{
	  display: flex;
	  align-items: center;
	  justify-content:flex-start;
	  background: #e8f2fc;
  	}
	.botonera{
		width: 300px;
		align-items: center;
	  	justify-content: center;
	}
	.linea{
		display: inline-flex;
	}
	.vueltas{
		color: darkslategrey;
	}
</style>





