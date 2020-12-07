<script>
	import AutoComplete from './AutoComplete.svelte';
	import {colors} from './color-store.js';

	let items = colors;
</script>

<AutoComplete {items}/>
