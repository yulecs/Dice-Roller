<script>
	// 2 dice, 1 round, higher number wins 

	let images = ["https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Dice-0.svg/250px-Dice-0.svg.png", "https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/Dice-1-b.svg/250px-Dice-1-b.svg.png", "https://upload.wikimedia.org/wikipedia/commons/thumb/5/5f/Dice-2-b.svg/250px-Dice-2-b.svg.png", "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b1/Dice-3-b.svg/250px-Dice-3-b.svg.png", "https://upload.wikimedia.org/wikipedia/commons/thumb/f/fd/Dice-4-b.svg/250px-Dice-4-b.svg.png", "https://upload.wikimedia.org/wikipedia/commons/thumb/0/08/Dice-5-b.svg/250px-Dice-5-b.svg.png", "https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Dice-6a-b.svg/250px-Dice-6a-b.svg.png"]

	let all_left_dice = [];
	let all_right_dice = [];

	let left_dice = 0;
	let right_dice = 0;
	
	let interval = 12.5
	let j = 0;

	let isFlashing;

	function roll() {
		
		all_left_dice.length = 0;
		all_right_dice.length = 0;

		left_dice = 0;
		right_dice = 0;

		j = 0;

		interval = 12.5

		for (let i=0; i<20; i++) {		
          all_left_dice.push(Math.floor(Math.random() * 6 + 1))
		  all_right_dice.push(Math.floor(Math.random() * 6 + 1))
		}

		function flashBackground() {
    		isFlashing = true;
    		// Reset the state after the animation duration (e.g., 500ms)
    		setTimeout(() => {
      			isFlashing = false;
    		}, 500)
		}

		function tick() {
    		left_dice = all_left_dice[j];
    		right_dice = all_right_dice[j];
    		j++;

    		if (j === 20) {
        		flashBackground();
        		return;
    		}

    		interval *= 1.2;
    		setTimeout(tick, interval);
		}

		tick();
	}

</script>

<html lang="en" class:flash={isFlashing}>
	<main class:flash={isFlashing}>
		<h1>Dice Roller</h1>
		<h2>The total is: {left_dice + right_dice}</h2>
	</main>

	<div>
		<img src={images[left_dice]} alt="Dice_1">
		<img src={images[right_dice]} alt="Dice_1">
		<div>
			<button on:click={roll}> Roll Dices! </button>
		</div>
	</div>
</html>

<style>
	html {
		background: #d8f3dc;
	}
	
	main {
		background-color: #b7e4c7;
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	div {
		text-align: center;
		padding: 1em;
	}

	button {
		background-color: #74c69d;
		font-size: 1.5em;
		cursor: pointer;
		color: #2d6a4f;
		border-radius: 0.5em;
	}

	img {
		padding: 0.5em;
	}

	h1 {
		color: #2d6a4f;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 200;
	}

	h2 {
		color: #40916c;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 200;
	}

	.flash {
		animation: flash-animation 0.5s ease-out;
	}

	@keyframes flash-animation {
    0% {
      background-color: #d8f3dc;
    }
    50% {
      background-color: #40916c; 
    }
    100% {
      background-color: #d8f3dc;
    }
  }

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>