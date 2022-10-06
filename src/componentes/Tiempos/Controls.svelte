<script>
    // dispatch start/stop/pause/lap events following a click on the button
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    let contador = 0;

    // following a click on the buttons dispatch the matching events
    function start() {
        dispatch("start");
    }
    function stop() {
        contador = 0;
        dispatch("stop");
    }

    function lap() {
        contador = contador + 1;
    }
   
    // consider the booleans passed down from App.svelte
    export let subscription;
</script>
<style>
    /* display the button(s) in a row */
    div {
        display: flex;
        border: 1px solid hsl(0, 0%, 25%);
        border-radius: 100px;
    }
    div button {
        font-size: 1.0rem;
        color: hsl(0, 0%, 10%);
        font-family: inherit;
        padding: 0.6rem;
        flex-grow: 1;
        width: 100px;
        border: none;
        background: none;
        border-radius: inherit;
        margin: 0; /* by default svelte applies a margin to the bottom of the button*/
        transition: background 0.2s ease-out;
    }
    /* include a border on all button but the first, to avoid a border when only one element exist */
    div button:not(:first-of-type) {
        border-left: 1px solid hsl(0, 0%, 25%);
        border-top-left-radius: 5;
        border-bottom-left-radius: 5;
    }

    .controls:focus {
        outline-color: hsl(0, 0%, 0%);
    }
    .controls:hover {
        background: hsla(140, 100%, 22%, 0.616);
    }

    .reset:focus{
        outline-color: rgb(0, 0, 0);
    }
    .reset:hover{
        background-color: rgba(155, 0, 0, 0.623);
    }

</style>

<!-- depending on the value of subscription and lapsed display different controls
subscription -> Lap & pause
    otherwise, lapsed -> Reset & continue
        otherwiose -> Start
-->


    {#if subscription}
    <div class="reset">
        <button on:click="{stop}">Terminar carrera</button>
    </div>
    {:else}
    <div class="controls">
    <button on:click="{start}">Iniciar carrera</button>
    </div>
    {/if}






