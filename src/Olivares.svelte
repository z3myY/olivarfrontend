<script>
  import { onMount, getContext } from "svelte";
  import { jsonData } from "./store.js";
  import Buscar from "./Buscar.svelte";
  import Olivar from "./Olivar.svelte";
  import Boton from "./Boton.svelte";
  const URL = getContext("URL");
  let busqueda = "";
  let olivar = {};
  onMount(async () => {
    const response = await fetch(URL.olivares);
    const data = await response.json();
    $jsonData = data;
  });
  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda
    ? $jsonData.filter((item) => regex.test(item.variedad))
    : $jsonData;
</script>

<h1>OLIVARES</h1>
<Buscar bind:busqueda />

<div class="container">
  <Olivar bind:olivar>
    <div style="text-align: right">
      <Boton documento={olivar} tipo="insertar" coleccion="olivares" />
    </div>
  </Olivar>
</div>

<div class="container">
  {#each datos as olivar}
    <Olivar {olivar}>
      <div style="text-align: right">
        <Boton documento={olivar} tipo="modificar" coleccion="olivares" />
        <Boton documento={olivar} tipo="eliminar" coleccion="olivares" />
      </div>
    </Olivar>
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
