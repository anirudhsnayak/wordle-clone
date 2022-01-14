<script>
export let char;
export let l;
export let i;
function getClass(letter, index){
	let cssClass = "";
	if(letter == "G"){cssClass = "green"}
	else if(letter == "Y"){cssClass = "yellow"}
	else if(letter == "X"){cssClass = "gray"}
	return cssClass + " " + "delay" + (index+1);
}
let finalClass = "";
$: finalClass = "letterBox " + getClass(l, i);
</script>

<div class= {finalClass} style={"border-color: "+(char=="" ? "lightgray" : "darkgray")}>
	<div class="letter">
		{char}
	</div>
</div>

<style>
	.letterBox{
		display: flex;
		flex-direction: column;
		border: 2px solid lightgray;
		width: 50px;
		height: 50px;
		text-align: center;
		vertical-align: middle;
		justify-content: center;
		--flip-time: 0.55s;
		--offset-time: 0.3s;
	}
	.letter{
		font-size: 2.25rem;
		font-weight: 600;
		transform: scaleY(1.05) translateY(-1px);
	}
	.green{
		animation-name: flipIn;
		animation-fill-mode: both;
		--main-color: lightgreen;
	}
	.yellow{
		animation:  flipIn;
		animation-fill-mode: both;
		--main-color: yellow;
	}
	.gray{
		animation:  flipIn;
		animation-fill-mode: both;
		--main-color: lightgray;
	}
	.delay1{
		animation-duration: var(--flip-time);
		animation-delay: calc(var(--offset-time)*0);
	}
	.delay2{
		animation-duration: var(--flip-time);
		animation-delay: calc(var(--offset-time)*1);
	} 
	.delay3{
		animation-duration: var(--flip-time);
		animation-delay: calc(var(--offset-time)*2);
	}
	.delay4{
		animation-duration: var(--flip-time);
		animation-delay: calc(var(--offset-time)*3);
	}
	.delay5{
		animation-duration: var(--flip-time); 
		animation-delay: calc(var(--offset-time)*4);
	}
	@keyframes flipIn{
		0% {transform: rotateX(0deg); color: #000000; background: white}
		50% {transform: rotateX(90deg); border-color: darkgray; color: #000000; background: white}
		51% {transform: rotateX(90deg); border-color: var(--main-color); background: var(--main-color);}
		100% {transform: rotateX(0deg); border-color: var(--main-color); background: var(--main-color);}
	}
</style>