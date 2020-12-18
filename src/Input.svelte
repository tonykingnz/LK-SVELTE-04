<script>
	export let placeholder = "Write here";

	let autocompletion = [];
	export let inputText = "";
	export let arrayToSearch = [];
	
	$: hidden = inputText ? false:true;
	
	let timer;
	function debounce (v) {
		hidden = false;
		clearTimeout(timer);
		timer = setTimeout(() => {
			if (v != undefined && v != "") {
				autocompletion = [];
				arrayToSearch.forEach(checkAndAdd);
				function checkAndAdd(item) {
					if (item.toUpperCase().includes(v.toUpperCase())) {
						autocompletion = [...autocompletion, item];
						
					}
				}
			} else {
				autocompletion = [];
			}
		}, 500);
	}
	
	let i = 0;
	let inputTextCandidate = autocompletion[0];
	function handleKey() {
		/*console.log(event.key);*/
		
		if (autocompletion.length > 0) {
			if (event.key == "ArrowUp" && inputTextCandidate != autocompletion[0])  {
				inputTextCandidate = autocompletion[i];
				i -= 1;
			}
			else if (event.key == "ArrowDown" && inputTextCandidate != autocompletion[autocompletion.length - 1]) {
				inputTextCandidate = autocompletion[i];
				i += 1;
			}
			else if (event.key == "Enter"){
				if (inputTextCandidate != undefined && inputTextCandidate != ""){
					inputText = inputTextCandidate;
				}
			}
			else if (event.key == "Escape"){
				hidden = true
			}
			return handleKey;
		}
	}
	$: console.log(hidden);
	let attenction = "NotClicked";
	
	const clicked = event => filteredItems = [event];
	
	function clickedOut(event) {
		hidden = true
	}
</script>

<main on:click|stopPropagation={clickedOut}>
    <div class="container">

        <input type="text" bind:value={inputText} {placeholder} on:input={({ target: {value} }) => debounce(value)} />

        <div class="sugestion" class:sugestion-hidden="{hidden}">
            {#if inputText.length > 0 && autocompletion.length < 1}
                 <ul>
                     <p>Not found</p>
                </ul>
            {:else if inputText != "" && autocompletion != []}
                <ul>
										<br>
                    {#each autocompletion as match, i}
                        <li class:selected="{match == inputTextCandidate}" on:click="{() => inputText = match}">{match}</li>
                    {/each}
                </ul>
            {:else}
                <h5>Start Writing.</h5>
            {/if}
        </div> 
    </div>
    <br>
</main>

<svelte:window on:keydown={handleKey}/>

<style>
	main {
		padding: 0;
		margin: 0;
	}
	ul {
		background-color: #eaeaea;
		border-color: #a5a5a5;
		border: 2.5px;
		border-style: solid;
		border-radius: 10px;
		width: 180px;
		height: 120px;
		overflow-x: hidden;
		overflow-y: auto;
		text-align: left;
		list-style-type: none;
		
	}
	
	li {
		background-color: #cccccc;
		cursor: pointer;
		margin: 0;
		position: relative;
		left: -30px;
	}
	
	.selected {
		background-color: #aaaaaa;
		cursor: pointer;
	}
	
	p {
		text-align: left;
		border: none;
		color: #567987;
	}
	
	.container{
		position: relative;
	}
	.sugestion{
		top: 18px;
		z-index : 99;
		position: absolute;
	}
	.sugestion-hidden {
		display: none;
	}

</style>
