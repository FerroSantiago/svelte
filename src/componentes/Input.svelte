<script>
    import { each } from "svelte/internal";

    let user = "";
    let pass = "";
    let response = undefined;
    let log = false;

    const handleInput = (event) => (value = event.target.value);

    $: if (log == true) {
        fetch(
            `urlDeEjemplo.com/api/auth?usuario=${user.trim()}&contraseña=${pass.trim()}`
        )
            .then((res) => res.json())
            .then((json) => {
                response = json.data.results || [];
                log = false;
                console.log(response);
            });
        
    }
    function logear() {
        log = true;
        console.log({user});
        console.log({pass});
    }
</script>

<input placeholder="Usuario" bind:value={user} on:input={handleInput} />
<br>
<input type="password" placeholder="Contraseña" bind:value={pass} on:input={handleInput} />
<br>
<!--><a href="http://127.0.0.1:5173/api/carreras"><-->
    <button on:click={logear}> Log In </button>
<!--></a><-->


    
    