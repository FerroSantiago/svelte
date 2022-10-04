<script>
    import { each } from "svelte/internal";

    let user = "";
    let pass = "";

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

                    //todo: validar respuesta antes de redirigir
                    //windos.location.replace("http://127.0.0.1:5173/api/carreras");
                });
        }else{
            res.sendStatus(409)
        }
    }

</script>

<div class="container text-center">
    <br>
    <div class="row">
      <div class="col">
        <h1>Bienvenido al sistema de carreras </h1>
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
      </div>
    </div>
  </div>