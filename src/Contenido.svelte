<script>
    import { Route }  from "svelte-routing";
    import Inicio     from "./Inicio.svelte";
    import Olivares  from "./Olivares.svelte";
    import Agricultores   from "./Agricultores.svelte";
  </script>
  
  <style>
    main {
      padding: 20px;
      padding-top: 50px;
    }
  </style>
  
  <main id="contenido">
    <Route path="/" component={Inicio} />
    <Route path="/olivares" component={Olivares} />
    <Route path="/agricultores" component={Agricultores} />
  </main>