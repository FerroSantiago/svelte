<script>
    import { each } from "svelte/internal";

    let user = "";
    let pass = "";
    let response = undefined;
    let log = false;

    const handleInput = (event) => (value = event.target.value);

    $: if (log == true) {
        fetch(
            `urlDeEjemplo.com/api/auth?usuario=${user.trim()}&contraseña=${password.trim()}`
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
        
    }
</script>

<input placeholder="Usuario" {user} on:input={handleInput} />
<br>
<input type="password" placeholder="Contraseña" {pass} on:input={handleInput} />
<br>
<a href="http://127.0.0.1:5173/api/carreras">
    <button on:click={logear}> Log In </button>
</a>


    
    