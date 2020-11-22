<script>
	import Input from "./Input.svelte"
	
	export let nameToSearch = [];
	export let addressToSearch = [];
	
	let storesData = [["Apple", "Apple Park, 95014 Cupertino, CA, USA", "IDk"],["Nike", "Cool Street, NYC, NY, USA"], ["Amazon", "Online (amazon.com)"], ["Disney World", "Wonderland, USA"], ["Tesla", "Store addres, Passadena, CA, USA", "dsfsfsdf", "sdfadf"]];
	
	$: if (storesData != undefined){
		nameToSearch = [];
		addressToSearch = [];
		for (i = 0; i < storesData.length; i++) {
  		if (storesData[i][0]){
				nameToSearch = [...nameToSearch, storesData[i][0]];
			}
		}
		for (i = 0; i < storesData.length; i++) {
  		if (storesData[i][1]){
				addressToSearch = [...addressToSearch, storesData[i][1]];
			}
		}
		console.log(nameToSearch);
		console.log(addressToSearch);
	}
	
</script>

<main>
	<div>
			<Input arrayToSearch={nameToSearch} placeholder="Store's name"/>
			<hr>
			<Input arrayToSearch={addressToSearch} placeholder="Store's address"/>
	</div>
</main>


<style>
</style>