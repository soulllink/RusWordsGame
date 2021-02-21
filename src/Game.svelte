<script>
import { onMount } from "svelte";

let data = [];
let nnumber;
let wdata = "Привет!"
let answer = { state: false };
let y = Math.floor(Math.random() * 12126);
let liststype = ["Существительное",
"Прилагательное",
"Числительное",
"Местоимение",
"Глагол",
"Наречие",
"Предлог",
"Союз",
"Частица",
"Междометие"];
let rightwrong = {right: 0, wrong: 0};
let alertinfo;


onMount(async () => {
        const res = await fetch('ruswords.json');
        data = await res.json();
});
    

async function handleClick() {
	let word = data[y]
	
    $: wdata = await word['words'];
    if(nnumber == word['stype']) { 
		answer.state = true;
        //alert("Правильно!");
        y = Math.floor(Math.random() * 12126);
        $: wdata = await data[y]['words'];
		rightwrong.right++
    } else {
		answer.state = false;
        //alert("Правильно: " + liststype[word['stype']])
		$: alertinfo = liststype[word['stype']]
		rightwrong.wrong++		
    }
}  

function clg() {
	console.log(nnumber);
}
    
</script>

<div class="material-icons mdl-badge mdl-badge--overlap" data-badge="{rightwrong.right}">done</div>
<div class="material-icons mdl-badge mdl-badge--overlap" data-badge="{rightwrong.wrong}">delete</div>


{#await wdata}
	<!-- promise is pending -->
	<p>waiting...</p>
{:then value}

	<!-- promise was fulfilled -->
	<h2>{value}</h2>

{/await}

{#if answer.state}
	<span class="mdl-chip">
    	<span class="mdl-chip__text">Правильно</span>
	</span>
{/if}
{#if !answer.state}
	<span class="mdl-chip">
    	<span class="mdl-chip__text">Неправильно</span>
	</span>
	{#if alertinfo != undefined}
		<span class="mdl-chip mdl-chip--contact">
			<span class="mdl-chip__contact mdl-color--teal mdl-color-text--white">О</span>
			<span class="mdl-chip__text">{alertinfo}</span>
		</span>
	{/if}
{/if}

<div style="display:grid">
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 0}}>Существительное</button>
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 1}}>Прилагательное</button>
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 2}}>Числительное</button>
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 3}}>Местоимение</button>
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 4}}>Глагол</button>
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 5}}>Наречие</button>
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 6}}>Предлог</button>
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 7}}>Союз</button>
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 8}}>Частица</button>
<button class="mdl-button mdl-js-button" on:click={handleClick} on:click={() => {nnumber = 9}}>Междометие</button>
</div>



