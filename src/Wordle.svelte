<script>
	import WordleLetter from "./WordleLetter.svelte"
	import SolutionWordBank from "./SolutionWordBank.js"
	let currentWordID = 0;
	SolutionWordBank.createList();
	let answerWord = SolutionWordBank.getRandom();
	console.log(answerWord);
	let highlightStringList = ["_____"];
	document.addEventListener("keydown", onKeyPress);
	let currentWordList = [""];
	function replaceAt(string, index, replacement) {
    return string.substr(0, index) + replacement+ string.substr(index + replacement.length);
	}
	function onKeyPress(e){
		if(currentWordID>=6){
			return;
		}
		highlightStringList[currentWordID] = "_____";
		let currentWord = currentWordList[currentWordID];
		if(currentWord.length != 0 && e.key == "Backspace"){
			currentWordList[currentWordID] = currentWord.slice(0, -1);
		}
		if(currentWord.length == 5){
			if(e.key == "Enter"){
				checkWord();
			} 
			return;
		}
		if((/^[A-Za-z]+$/).test(e.key)){
			if(e.key.length==1){
				currentWordList[currentWordID] += e.key;
			}
		}
	}
function checkWord(){
	let highlightString = 'XXXXX';
	let word = answerWord;
	let testWord = currentWordList[currentWordID];
	for (let i = 0; i < word.length; i+=1){
		if(word[i] == testWord[i]){
			highlightString = replaceAt(highlightString, i, "G");
			word = replaceAt(word, i, "_");
			testWord = replaceAt(testWord, i, "_");
		} 
	}
	for (let i = 0; i < testWord.length; i+=1){
		if(highlightString[i]!="X"){
			continue;
		}
		for (let j = 0; j < word.length; j+=1){
			if(word[j] != "_" && word[j]==testWord[i]){
				highlightString = replaceAt(highlightString, i, "Y");
				word = replaceAt(word, j, "_");
			}
		}
	}
	highlightStringList[currentWordID] = highlightString;
	currentWordList.push("");
	currentWordID += 1;
}
</script>

<div class="center">
<div class="wordleGame">
	{#each currentWordList as currentWord, i}
		{#each currentWord as letter, j}
			<WordleLetter char={letter} l={highlightStringList[i][j]} i={j}></WordleLetter>
		{/each}
	{/each}
	{#each {length: 30-(currentWordList[currentWordID].length + 5*currentWordID)} as _, i}
		<WordleLetter char="" l="" i=""></WordleLetter>
	{/each}
</div>
</div>

<style>
	.wordleGame{
		margin-top: 15px;
		flex: 0 1 auto;
		display: grid;
		grid-template-columns: 60px 60px 60px 60px 60px;
		grid-template-rows: 60px 60px 60px 60px 60px;
		
	}
	.center{
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>