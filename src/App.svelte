<script>
import Input from "./Input.svelte";
let inputText = ""
let storeName=["Apple", "Amazon", "Google", "Facebook", "Lederek", "Microsoft", "Zeferino"];
</script>

<Input arrayToSearch={storeName} {inputText}/>

