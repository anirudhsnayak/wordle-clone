<script>
	import Wordle from "./Wordle.svelte";
</script>

<h1 class="wordleTitle">amoGUESS</h1>
<div class="line"> </div>
<Wordle></Wordle>

<style>
	:global(body){
		font-family: 'Clear Sans', 'Helvetica Neue', Arial, sans-serif;
    font-size: 16px;
		padding: 0px; margin: 0px;
	}
	.wordleTitle{
		letter-spacing: 2.5px;
		font-weight: 700;
		font-size: 36px;
		
		margin-top: 6px;
		margin-bottom: 6px;
		text-align: center;
	}
	.line{
		background-color: lightgrey;
		height: 1px;
		margin-left: 50px;
		margin-right: 50px;
	}
</style>