<script>
  import Card from "./lib/card.svelte";
  let caracteres=[]
  let pagina =1;
  async function loadcharacter() {
    const response = await fetch('https://rickandmortyapi.com/api/character?page='+pagina)
    const data = await response.json()
    console.log(data)
    caracteres= data.results;
  }
  loadcharacter()
  function siguiente(){
    pagina++;
    loadcharacter()
  }
  function anterior(){
    pagina--;
    loadcharacter()
  }
</script>
<h1 class="title">rick and morty</h1>
<h2 class="title">pagina: {pagina}</h2>
<div class="contenedor">
  <div class="botones">
    <button class="boton" on:click={anterior} disabled={pagina===1}>anterior</button>
    <button class="boton" on:click={siguiente}>siguiente</button>
  </div>
  <div class="grid">
    {#each caracteres as caracter }
    <Card {caracter}/>
    {/each}
  </div>
</div>
