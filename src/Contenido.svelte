<script>
  import { Route }  from "svelte-routing";
  import Inicio     from "./Inicio.svelte";
  import Peliculas  from "./Peliculas.svelte";
  import Clientes   from "./Clientes.svelte";
</script>

<style>
  main {
    padding: 20px;
    padding-top: 50px;
  }
</style>

<main id="contenido">
  <Route path="/" component={Inicio} />
  <Route path="/peliculas" component={Peliculas} />
  <Route path="/clientes" component={Clientes} />
</main>
