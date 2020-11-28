<script>
    export let placeholder = "Write here";
    	
    	let autocompletion = [];
    	export let inputText = "";
    	export let arrayToSearch = [];
    	
        setInterval(function() {
            if (inputText != undefined && inputText != "") {
                autocompletion = [];

                arrayToSearch.forEach(checkAndAdd);
                function checkAndAdd(item) {
                    if (item.toUpperCase().includes(inputText.toUpperCase())) {
                        autocompletion = [...autocompletion, item];
                    }
                }
            } else {
                autocompletion = [];
            }
        }, 500);
        
        let i = 0;
    	let inputTextCandidate = autocompletion[0];
        
        function handleKey() {
    	    if (autocompletion.length > 0) {
                if (event.key == "ArrowUp" && inputTextCandidate != autocompletion[0])  {
    		        inputTextCandidate = autocompletion[i];
    			    i -= 1;
                }
    		    else if (event.key == "ArrowDown" && inputTextCandidate != autocompletion[autocompletion.length - 1]) {
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
    <div class="container">
        <input type="text" bind:value={inputText} {placeholder}>
        <div class="sugestion">
            {#if inputText.length > 0 && autocompletion.length < 1}
                 <ul>
                     <p>Not found</p>
                </ul>
            {:else if inputText != "" && autocompletion != []}
                <ul>
                    {#if inputTextCandidate != undefined}
                        <p>Press enter to select: {inputTextCandidate}</p>
                    {:else}
                        <p>Use the arrows keys to find in the sugestions.</p>
                    {/if}
                    {#each autocompletion as match, i}
                        <li on:click="{() => inputText = match}">{match}</li>
                    {/each}
                </ul>
            {:else}
                <h5>Start Writing.</h5>
            {/if}
        </div> 
    </div>
    <br>
</body>

<svelte:window on:keydown={handleKey} />

<style>
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
    }
    p {
        text-align: left;
        border: none;
        color: #567987;
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
