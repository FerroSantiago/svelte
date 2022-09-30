<script>
    import { each } from "svelte/internal";

    let user = "";
    let pass = "";
    let response = undefined;
    let log = false;

    const handleInput = (event) => (value = event.target.value);

    $: if (log == true) {

        
    }
    function logear() {
        log = true;
        console.log({user});
        console.log({pass});
        if(user != "" && pass != ""){
            fetch(
                `urlDeEjemplo.com/api/auth?usuario=${user.trim()}&contraseña=${pass.trim()}`,
                {method:'POST',
                 body: {user: user,
                       pass: pass}
                }
            )
                .then((res) => res.json())
                .then((json) => {
                    response = json.data.results || [];
                    log = false;
                    console.log(response);
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
        <h1>Bienvenido al sistema de careras </h1>
      </div>
      <div class="col">
        <div class="mb-3">
            <input class="form-control" placeholder="Usuario" bind:value={user} on:input={handleInput} />
            <br>
            <input class="form-control" type="password" placeholder="Contraseña" bind:value={pass} on:input={handleInput} />
            <br>
            <button class="btn btn-outline-success" on:click={logear}> Log In </button>
            <a class="btn btn-outline-success" href="/">
                Volver
            </a>
        </div>
      </div>
    </div>
  </div>

    
    
    