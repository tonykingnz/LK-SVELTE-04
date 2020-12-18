<script>
import Input from "./Input.svelte";
let inputText = ""
let storeName=["Apple", "Amazon", "Google", "Facebook", "Lederek", "Microsoft", "Zeferino"];
</script>

<Input arrayToSearch={storeName} {inputText}/>
<p>Some text</p>
<p>Another text</p>
<Input arrayToSearch={storeName} {inputText}/>
<p>More!</p>
<Input arrayToSearch={storeName} {inputText}/>
<p>Random?</p>
<br>


