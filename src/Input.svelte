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
            debugger;
    		autocompletion = [];
    	}
        
        let i = 0;
        let inputTextCandidate = "";
    	
        function handleKey() {
    	    if (autocompletion.length > 0) {
    	        if (event.key == "ArrowUp") {
    		        inputTextCandidate = autocompletion[i];
    			    i -= 1;
                }
    		    else if (event.key == "ArrowDown") {
                    inputTextCandidate = autocompletion[i];
    			    i += 1;
                }
                else if (event.keyCode == 13){
                    if (inputTextCandidate != undefined && inputTextCandidate != ""){
                        inputText = inputTextCandidate;
                    }
                }
    		    return handleKey;
            }
        }
</script>

<body>
    <p>{inputTextCandidate}</p>
    <div class="container">
        <input type="text" bind:value={inputText} {placeholder}>
        <div class="sugestion">
            {#if inputText != undefined && inputText != "" && autocompletion != []}
            <ul>
                {#each autocompletion as match, i}
                <li on:click="{() => inputText = match}">{match}</li>
                {/each}
            </ul>
            {:else if autocompletion == [] && inputText != ""}
            <ul>
                <li>Not found</li>
            </ul>
            {:else}
            <p>Start Writing.</p>
            {/if}
        </div>
    </div>
    <br>
</body>

<svelte:window on:keydown={handleKey} />

<style>
    ul {
    		top: 100%;
        left: 0;
    		width: 100%;
    		background-color: #eaeaea;
    		border-color: #a5a5a5;
    		border-color: 10px;
    		border-style: solid;
    		border-radius: 10px;
    	}
      li {
        cursor: pointer;
      }
    	.container{
      	position: relative;
      }
      .sugestion{
        top: 18px;
    	z-index : 99;
      	position: absolute;
       }
</style>
