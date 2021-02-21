<script>
import { onMount } from "svelte";

let data = [];

let wdata = "Привет!"
let answer = { state: false };
let y = Math.floor(Math.random() * 10820);
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
    

async function handleClick(click) {
	let word = data[y]
	
    $: wdata = await word['words'];
    if(word['stype'] == click) { 
		answer.state = true;
        //alert("Правильно!");
		$: alertinfo = word['words'] + " - " + liststype[word['stype']]
        y = Math.floor(Math.random() * 10820);
        $: wdata = await data[y]['words'];
		rightwrong.right++
    } else {
		answer.state = false;
        //alert("Правильно: " + liststype[word['stype']])
		$: alertinfo = word['words'] + " - " + liststype[word['stype']]
		rightwrong.wrong++		
    }
}  
    
</script>

<div class="material-icons mdl-badge mdl-badge--overlap" data-badge="{rightwrong.right}">done</div>
<div class="material-icons mdl-badge mdl-badge--overlap" data-badge="{rightwrong.wrong}">clear</div>

{#if answer.state}
	<span class="mdl-chip">
    	<span class="mdl-chip__text">Правильно</span>
	</span>
	{#if alertinfo != undefined}
		<span class="mdl-chip mdl-chip--contact">
			<span class="mdl-chip__contact mdl-color--teal mdl-color-text--white"><i class="material-icons">done</i></span>
			<span class="mdl-chip__text">{alertinfo}</span>
		</span>
	{/if}
{/if}
{#if !answer.state}
	<span class="mdl-chip">
    	<span class="mdl-chip__text">Неправильно</span>
	</span>
	{#if alertinfo != undefined}
		<span class="mdl-chip mdl-chip--contact">
			<span class="mdl-chip__contact mdl-color--teal mdl-color-text--white"><i class="material-icons">clear</i></span>
			<span class="mdl-chip__text">{alertinfo}</span>
		</span>
	{/if}
{/if}


{#await wdata}
	<!-- promise is pending -->
	<p>waiting...</p>
{:then value}

	<!-- promise was fulfilled -->
	<h2>{value}</h2>

{/await}



<div style="display:grid">
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(0)}>Существительное</button>
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(1)}>Прилагательное</button>
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(2)}>Числительное</button>
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(3)}>Местоимение</button>
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(4)}>Глагол</button>
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(5)}>Наречие</button>
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(6)}>Предлог</button>
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(7)}>Союз</button>
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(8)}>Частица</button>
<button class="mdl-button mdl-js-button" on:click={ () => handleClick(9)}>Междометие</button>
</div>



