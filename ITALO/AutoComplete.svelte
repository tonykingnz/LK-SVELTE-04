<script>
	export let items = [];
	let color = "";
	let inputValue = "";
	$: if (!inputValue)  {
		filteredItems = [];
	}
	export let filteredItems = [];
	let preSelected = -1;

	const filterItems = () => {
		let tempArr = [];
		if (inputValue) {
			items.forEach(item => {
			if (item.toLowerCase().includes(inputValue.toLowerCase())) {
				tempArr = [...tempArr, makeMatchBold(item)];
			}
		});
	}
	filteredItems = tempArr;
}

	const makeMatchBold = (str) => {
		let auxStr = str.toLowerCase().indexOf(inputValue);
		let matched = str.substring(auxStr, (auxStr + inputValue.length));
		let makeBold = `<strong>${matched}</strong>`;
		let boldedMatch = str.replace(matched, makeBold);
		return boldedMatch;
	}
	
	const removeBold = (str) => {
		return str.replace(/<(.)*?>/g, "");
	}
	const setInputValue = (item) => {
		inputValue = removeBold(item);
	}
	
	$: colorCheck = color;
	
	const handleClick = () => {
		let checkInput = items.includes(inputValue)
		if (checkInput) {
			color = inputValue;
		};
		inputValue = "";
		preSelected = -1;
		
	};
	function handleKey() {
			if (filteredItems.length > 0) {
				if (event.key == "ArrowUp") {
					setInputValue(filteredItems[preSelected-1]);
					preSelected--;
				}
				else if (event.key == "ArrowDown") {
					setInputValue(filteredItems[preSelected+1]);
					preSelected++;
				}	
				else if (event.key == "Enter") {
					return handleClick();
				}
			return handleKey;
		}
	}
</script>

<main>

	<div class="form">	
		<input type="text" bind:value={inputValue} on:input={filterItems} placeholder="Selet Color"/>
		<button on:click|preventDefault= {handleClick}>Add</button>	
	</div >
	
	<div class="circle" style="--theme-color: {color}"></div>

		{#if filteredItems.length > 0 && inputValue.length > 2}
			<div class="container">
				{#each filteredItems as item, i}
					<div class="items" class:items-active={i == preSelected} on:mouseover={() => preSelected = i} on:click={() => setInputValue(item)}>{@html item}</div>
				{/each}
			</div>
		{:else if inputValue.length > 2}
			<div class="container items">No match found</div>
		{/if}
	<div class="xxx"></div>	
</main>

<svelte:window on:keydown={handleKey} />
<style>
	main {
		padding : 0px;
		padding-top : 1rem;
		margin : 0px;
		font-family : serat;
	}
	.form {
		position : relative;
		height : 2.5rem;
		width : 23.1rem;
	}
	input {
  border : 1px solid transparent;
  background-color : #676778;
  padding : 10px;
  font-size : 16px;
	width : 20rem;

}
	::placeholder {
  	color : #ffffff;
		font-weight : bold;
		text-transform : capitalize;
		opacity : 85%;
		font-size : 20px;
		padding-left : 0.5rem;
	}
	button {
		border : 1px solid transparent;
		border-radius : 25%;
		height : 40px;	
		background-color : #1c6ea4;
		color : #ffffff;
		font-weight : bold;
	}
	.container {
		position : absolute;
		z-index : 99;
		width : 20rem;
		max-height : 20rem;
		overflow : auto;
		top : 4rem;
		background-color : #e7e7e9;

		
	}
	.items {
	font-size : 16px;
	text-align : left;
	padding : 0.18rem;
	padding-left : 0.5rem;
	}
	
	.items-active{
		background-color :  #ababab !important;
	}
	.circle {
		width : 4rem;
		height : 4rem;
		border : 2px solid black;
		border-radius : 50%;
		position : relative;
		left : 23.5rem;
		bottom : 3.5rem;
		background-color : var(--theme-color);
	}
	.xxx {
		position : fixed;
		width : 500px;
		height : 200px;
		background-color : black;
	}
</style>
