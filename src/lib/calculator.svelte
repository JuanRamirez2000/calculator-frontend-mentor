<script>
	import '../themes.css';
	let displayNumber = '0';
	let currentNumber = '0';
	let currentOperation = '+';
	let sliderTheme = 1;

	const DECIMAL = '.';
	/**
	 * @param {string} newNumber
	 */
	function setNumber(newNumber) {
		if (newNumber === DECIMAL && displayNumber.includes(DECIMAL)) {
			return;
		}
		if (displayNumber.length === 1 && displayNumber === '0') {
			displayNumber = newNumber;
			return;
		}
		displayNumber += newNumber;
	}

	function handleReset() {
		currentNumber = '0';
		displayNumber = '0';
	}

	/**
	 * @param {string} operation
	 */
	function setOperation(operation) {
		currentOperation = operation;
		currentNumber = displayNumber;
		displayNumber = '0';
	}

	// Done
	function handleDelete() {
		if (displayNumber.length === 1) {
			displayNumber = '0';
		} else {
			displayNumber = displayNumber.slice(0, displayNumber.length - 1);
		}
	}

	function handleResult() {
		let result = 0;
		if (currentOperation === '+') {
			result = Number(currentNumber) + Number(displayNumber);
		}
		if (currentOperation === '-') {
			result = Number(currentNumber) - Number(displayNumber);
		}
		if (currentOperation === 'x') {
			result = Number(currentNumber) * Number(displayNumber);
		}
		if (currentOperation === '/') {
			result = Number(currentNumber) / Number(displayNumber);
		}
		displayNumber = result.toString();
		currentNumber = '0';
	}
</script>

<div
	class="calc-container"
	class:theme1={sliderTheme === 1}
	class:theme2={sliderTheme === 2}
	class:theme3={sliderTheme === 3}
>
	<div class="calc">
		<header>
			<h2>calc</h2>
			<p>THEME</p>
			<div class="theme-selector">
				<ul class="theme-numbers">
					<li>1</li>
					<li>2</li>
					<li>3</li>
				</ul>
				<input type="range" min={1} max={3} bind:value={sliderTheme} />
			</div>
		</header>
		<main>
			<div class="calc-display">{displayNumber}</div>
			<ul class="calc-body">
				<li class="calc-numbers key"><button on:click={() => setNumber('7')}>7</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('8')}>8</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('9')}>9</button></li>
				<li class="calc-operations key"><button on:click={handleDelete}>DEL</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('4')}>4</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('5')}>5</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('6')}>6</button></li>
				<li class="calc-numbers key"><button on:click={() => setOperation('+')}>+</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('1')}>1</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('2')}>2</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('3')}>3</button></li>
				<li class="calc-numbers key"><button on:click={() => setOperation('-')}>-</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('.')}>.</button></li>
				<li class="calc-numbers key"><button on:click={() => setNumber('0')}>0</button></li>
				<li class="calc-numbers key"><button on:click={() => setOperation('/')}>/</button></li>
				<li class="calc-numbers key"><button on:click={() => setOperation('x')}>x</button></li>
				<li class="calc-operations key"><button on:click={handleReset}>RESET</button></li>
				<li class="calc-equals key"><button on:click={handleResult}>=</button></li>
			</ul>
		</main>
	</div>
</div>

<style>
	div.calc-container {
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		background-color: var(--main-background);
	}
	div.calc {
		width: 520px;
		color: var(--text-primary);
		font-size: 32px;
		display: flex;
		flex-direction: column;
		gap: 20px;
	}

	main {
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	header {
		font-size: 16px;
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 2.5rem;
		font-weight: 500;
	}

	header > h2 {
		flex-grow: 1;
		font-size: 24px;
		font-weight: 700;
	}

	input[type='range'] {
		/* removing default appearance */
		-webkit-appearance: none;
		overflow: hidden;

		/* creating a custom design */
		width: 4.5rem;
		padding: 6px;
		cursor: pointer;
		background-color: var(--toggle-background);
		border-radius: 16px;
	}

	input[type='range']::-webkit-slider-thumb {
		-webkit-appearance: none;
		height: 1rem;
		width: 1rem;
		background-color: var(--toggle-button);
		border-radius: 16px;
	}

	input[type='range']::-webkit-slider-thumb:hover,
	input[type='range']::-webkit-slider-thumb:focus {
		background-color: var(--toggle-button-hover);
	}

	.theme-selector {
		display: flex;
		flex-direction: column;
	}

	.theme-numbers {
		display: flex;
		width: 100%;
		justify-content: space-around;
		flex-direction: row;
	}

	.calc-display {
		font-size: 42px;
		color: var(--screen-text);
		background-color: var(--screen-background);
		padding: 1.5rem;
		border-radius: 0.75rem;
		text-align: right;
	}

	.calc-body {
		display: grid;
		gap: 1.5rem;
		width: 100%;
		padding: 1.75rem;
		background-color: var(--keypad-background);
		grid-template-columns: repeat(4, 1fr);
		border-radius: 0.75rem;
	}
	.calc-body > li {
		height: 100%;
		width: 100%;
		min-height: 3.5rem;
		border-radius: 0.5rem;
		font-size: 32px;
		cursor: pointer;
		text-align: center;
		font-weight: 800;
	}
	.calc-body > li:nth-last-child(-n + 2) {
		grid-column: span 2;
	}

	.key > button {
		width: 100%;
		height: 100%;
	}

	.calc-numbers {
		background-color: var(--calc-numbers-background);
		color: var(--calc-numbers-text);
		box-shadow: 0px 5px 0px var(--calc-numbers-shadow);
	}

	.calc-numbers:hover,
	.calc-operations:focus {
		background-color: var(--calc-numbers-background-hover);
	}

	.calc-operations {
		color: var(--calc-functions-text);
		background-color: var(--calc-functions-background);
		box-shadow: 0px 5px 0px var(--calc-functions-shadow);
	}

	.calc-operations:hover,
	.calc-operations:focus {
		background-color: var(--calc-functions-background-hover);
	}

	.calc-equals {
		color: var(--calc-equals-text);
		background-color: var(--calc-equals-background);
		box-shadow: 0px 5px 0px var(--calc-equals-shadow);
	}

	.calc-equals:hover,
	.calc-display:focus {
		background-color: var(--calc-equals-background-hover);
	}

	.calc-body > li.calc-operations,
	li.calc-equals {
		font-size: 22px;
		font-weight: 700;
		display: flex;
		flex-direction: column;
		height: 100%;
		justify-content: center;
	}

	@media screen and (max-width: 640px) {
		div.calc {
			width: 350px;
		}
	}
</style>
