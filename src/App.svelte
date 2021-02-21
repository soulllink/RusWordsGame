<script>
  export let name;
  import Game from "./Game.svelte";
  export let title;
  document.title = title;


  let stypetip = { show: false };

	function toggle() {
		stypetip.show = !stypetip.show;
	}
</script>

<style>
  
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff0000;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
  .mdl-grid.center-items {
  justify-content: center;
  }

</style>

<svelte:head>
  <link rel="stylesheet" href="material.min.css">
  <script src="material.min.js"></script>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</svelte:head>

<main>

  <h1>Части речи</h1>
  

  {#if stypetip.show}
  <button class="mdl-button mdl-js-button mdl-button--fab mdl-button--mini-fab" on:click={toggle}>
    <i class="material-icons">clear</i>
  </button>
  <div class="mdl-grid center-items">

    <table class="mdl-data-table mdl-js-data-table mdl-shadow--2dp">
    <tbody>
    <tr>
      <td class="mdl-data-table__cell--non-numeric">Кто? Что?</td>
      <td>существительное или местоимение</td>
      
    </tr>
    <tr>
      <td class="mdl-data-table__cell--non-numeric">Какой? Какая? Какое? Какие?</td>
      <td>прилагательное</td>
      
    </tr>
    <tr>
      <td class="mdl-data-table__cell--non-numeric">Что делать? Что сделать? Что делает(ют)?</td>
      <td>глагол</td>
      
    </tr>
    <tr>
      <td class="mdl-data-table__cell--non-numeric">Как? Куда? Когда? Почему? Зачем?</td>
      <td>наречие</td>
      
    </tr>
    <tr>
      <td class="mdl-data-table__cell--non-numeric">Какой? Что делающий? Что сделавший?</td>
      <td>причастие</td>
      
    </tr>
    <tr>
      <td class="mdl-data-table__cell--non-numeric">Как? Что делая? Что сделав?</td>
      <td>деепричастие</td>
      
    </tr>
    
    </tbody>
    </table>
  </div>
  
{/if}

{#if !stypetip.show}
	<button class="mdl-button mdl-js-button mdl-button--fab mdl-button--mini-fab" on:click={toggle}>
		<i class="material-icons">add</i>
	</button>
{/if}


<div class="mdl-grid">
    <div class="mdl-layout-spacer"></div>
    <div class="mdl-cell mdl-cell--4-col">
    
    
    <Game/>
    
    
    </div>
    <div class="mdl-layout-spacer"></div>
</div>
  
 
</main>
