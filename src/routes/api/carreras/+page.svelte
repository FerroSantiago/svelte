<script>
	let response = undefined
	let bot = false;

	function obtenerCarreras(){
		fetch('http://localhost:4000/api/carreras',
        {method: 'GET'})
    	.then(res => res.json())
		.then(apiResponse =>{
			response = apiResponse || []
			JSON.stringify(response)
			console.log(apiResponse)
		})
	}
</script>

<h1>Prueba de carreras</h1>

<button class="btn btn-outline-success" on:click={obtenerCarreras}> Carreras </button>

<a class="btn btn-outline-success" href="/">
	Volver
</a>

{#if response && response.length > 0}
	{#each response as carreras}
    	<div>
        	<h3>
            	<strong>Carrera Numero: {carreras.idCarrera}</strong>
				<h1>Numero de vueltas de la carrera: {carreras.vueltas}</h1>
        	</h3> 
    	</div>
	{/each}
{/if}