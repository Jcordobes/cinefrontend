<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";
  import Buscar                  from "./Buscar.svelte";
  import Pelicula                from "./Pelicula.svelte";
  import Boton                   from "./Boton.svelte";
  const URL = getContext("URL");
  let busqueda = "";
  let pelicula = {};
  onMount(async () => {
    const response = await fetch(URL.peliculas);
    const data = await response.json();
    $jsonData = data;
  });
  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda 
    ? $jsonData.filter(item => regex.test(item.nombre))
    : $jsonData;
</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    flex-wrap: wrap;
  }
</style>

<h1>PELICULAS</h1>
<Buscar bind:busqueda />

<div class="container">
  <Pelicula bind:pelicula>
    <div style="text-align: right">
      <Boton documento={pelicula} tipo="insertar" coleccion="peliculas" />
    </div>
  </Pelicula>
</div>

<div class="container">
  {#each datos as pelicula}
    <Pelicula {pelicula}>
      <div style="text-align: right">
        <Boton documento={pelicula} tipo="modificar" coleccion="peliculas" />
        <Boton documento={pelicula} tipo="eliminar"  coleccion="peliculas" />
      </div>
    </Pelicula>
  {/each}
</div>
