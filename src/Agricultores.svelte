<script>
    import { onMount, getContext } from "svelte";
    import { jsonData } from "./store.js";
    import Buscar from "./Buscar.svelte";
    import Agricultor from "./Agricultor.svelte";
    import Boton from "./Boton.svelte";
    const URL = getContext("URL");
    let busqueda = "";
    let agricultor = {};
    onMount(async () => {
        const response = await fetch(URL.agricultores);
        const data = await response.json();
        $jsonData = data;
    });
    $: regex = new RegExp(busqueda, "i");
    $: datos = busqueda
        ? $jsonData.filter((item) => regex.test(item.nombre))
        : $jsonData;
</script>

<h1>AGRICULTORES</h1>
<Buscar bind:busqueda />

<div class="container">
    <Agricultor bind:agricultor>
        <div style="text-align: right">
            <Boton documento={agricultor} tipo="insertar" coleccion="agricultores" />
        </div>
    </Agricultor>
</div>

<div class="container">
    {#each datos as agricultor}
        <Agricultor {agricultor}>
            <div style="text-align: right">
                <Boton
                    documento={agricultor}
                    tipo="modificar"
                    coleccion="agricultores"
                />
                <Boton
                    documento={agricultor}
                    tipo="eliminar"
                    coleccion="agricultores"
                />
            </div>
        </Agricultor>
    {/each}
</div>

<style>
    .container {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: left;
        flex-wrap: wrap;
    }
</style>
