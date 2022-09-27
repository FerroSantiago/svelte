<h1>Prueba de carreras</h1>

<script>
        fetch('http://localhost:3050/api/carreras', {
        method: 'GET', 
        })
        .then(res => res.json())
        .then(apiResponse =>{
            response = apiResponse.data.results || []
            bool = false
            console.log(response)
        },)
        .catch((error) => {
            console.error('Error:', error);
        });
</script>