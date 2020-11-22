<script>
	export let placeholder = "Write here";
	
	let autocompletion = [];
	export let inputText = "";
	export let arrayToSearch = [];
	
	$: if (inputText != undefined && inputText != ""){
		autocompletion = [];
		
		arrayToSearch.forEach(checkAndAdd);
		function checkAndAdd(item){
			if (item.toUpperCase().includes(inputText.toUpperCase())){
				autocompletion = [...autocompletion, item];
			}
		}
	}else {
		autocompletion = [];
	}
	
</script>

<input type="text" bind:value={inputText} {placeholder}> 
<ul>
	{#each autocompletion as match, i}
 		<li on:click="{() => inputText = match}">{match}</li>
	{/each}
</ul>

<style>
	ul {
		top: 100%;
    left: 0;
		width: 100%;
	}
  li {
    cursor: pointer;
  }
</style>