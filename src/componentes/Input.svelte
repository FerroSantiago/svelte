<script>
    import { each } from "svelte/internal";

    let user = "";
    let pass = "";
    let response = undefined;
    let log = false;

    const handleInput = (event) => (value = event.target.value);

    $: if (log == true) {
        fetch(
            `sexo.com`
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
<input placeholder="Contraseña" {pass} on:input={handleInput} />
<br>
<button on:click={logear}> Buscar </button>

