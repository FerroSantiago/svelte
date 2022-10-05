<script>

    let user = "";
    let pass = "";
    let fail = undefined;

    function logear() {
        if(user != "" && pass != ""){
            fetch(
                `http://localhost:4000/api/login/signin`,
                { 
                  method:'POST',
                  headers: {'Content-Type': 'application/json'},
                  body: JSON.stringify({ usuario: user,
                      contraseña: pass})
                })
                .then(res => res.json())
                .then(apiResponse => {
                  console.log(apiResponse)
                  localStorage.setItem("token", apiResponse.token);
                  if(apiResponse.token) {fail = undefined; location.href = "http://127.0.0.1:5173/gestion/carreras"} 
                  else{fail = apiResponse
                    JSON.stringify(fail)}
                })
        }else{
            res.sendStatus(409)
        }
    }

</script>

<div class="container text-center">
    <br>
    <div class="row">
      <div class="col">
        <h1>Ingresar usuario y contraseña</h1>
      </div>
      <div class="col">
        <div class="mb-3">
            <input style="width: auto" class="form-control" placeholder="Usuario" bind:value={user} />
            <br>
            <input style="width: auto" class="form-control" type="password" placeholder="Contraseña" bind:value={pass} />
            <br>
            <button class="btn btn-outline-success" on:click={logear}> Log In </button>
            <a class="btn btn-outline-success" href="/">
                Volver
            </a>
        </div>
        {#if fail}
                  <h3>
                      <strong>{fail.message}</strong>
                  </h3> 
        {/if}
      </div>
    </div>
  </div>