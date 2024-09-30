<script>
    let computerInput = '';
    let userInput = '';
    let resultComp = '';
	let resultUser = ''
    let computerAleatorios = [];
    let userAleatorios = [];
    let quantidadeRandomizados = 0;
    let btnSubmitDisabled = true;

    function randomizeNumber(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function limparcomDelay(time) {
        setTimeout(() => {
            userInput = '';
        }, time);
    }

    function startGame() {
        userInput = '';
        computerInput = '';
        computerAleatorios = [];
        userAleatorios = [];
        resultComp = '';
		resultUser = '';
        quantidadeRandomizados++;

        for (let i = 0; i < quantidadeRandomizados; i++) {
            computerAleatorios.push(randomizeNumber(1, 100));
        }

        let index = 0;
        const mostrarNumeros = setInterval(() => {
            if (index < computerAleatorios.length) {
                computerInput = computerAleatorios[index].toString();
                index++;
            } else {
                clearInterval(mostrarNumeros);
                setTimeout(() => {
                    computerInput = ''; // Limpa o campo após a sequência
                }, 1000); // Limpa após 1 segundo
                btnSubmitDisabled = false;
            }
        }, 1000);
    }

    function submit() {
        userAleatorios.push(userInput);
        userInput = '';
        limparcomDelay(1000);

        if (userAleatorios.length === computerAleatorios.length) {
            resultComp = `Computador: ${computerAleatorios.join(', ')}`;
			resultUser = `Usuário: ${userAleatorios.join(', ')}`;
        }
    }

    function resetGame() {
        userInput = '';
        computerInput = '';
        computerAleatorios = [];
        userAleatorios = [];
        btnSubmitDisabled = true;
        quantidadeRandomizados = 0;
        result = '';
    }
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        background-color: #ff6347;
        font-family: Arial, Helvetica, sans-serif;
        text-align: center;
        display: flex;
        align-items: center;
        justify-content: space-evenly;
        height: 100vh;
    }

    #rules {
        width: 700px;
        text-align: start;
    }

    h1 {
        font-size: 2rem;
        margin-bottom: 70px;
        color: white;
    }

    #resultComp, #resultUser {
        font-size: 1.5rem;
        margin: 20px;
        color: white;
    }

    h3 {
        margin-bottom: 20px;
    
    }

    #main {
        background-color: white;
        width: 500px;
        padding-bottom: 20px;
        border-radius: 5px;
        display: flex;
        margin-bottom: 50px;
        justify-content: center;
        align-items: center;
    }

    input {
        width: 200px;
        height: 200px;
        margin: 20px;
        border: 5px solid tomato;
        font-size: 4rem;
        text-align: center;
    }

    .btn {
        width: 120px;
        height: 30px;
        border-radius: 3px;
        margin-top: 20px;
        font-size: 1rem;
        border: none;
        color: white;
        cursor: pointer;
        transition: background-color 0.3s ease, transform 0.2s ease;
    }

    #btn-start {
        background-color: green;
    }

    #btn-start:active {
        background-color: rgba(0, 128, 0, 0.875);
        transform: scale(0.95);
    }

    #btn-stop {
        background-color: blue;
    }

    #btn-stop:active {
        background-color: rgba(0, 0, 255, 0.557);
        transform: scale(0.95);
    }

    #btn-submit {
        background-color: purple;
    }

    #btn-submit:active {
        background-color: purple;
        transform: scale(0.95);
    }

    #result {
        margin-top: 20px;
    }
</style>
<body>
<div id="rules">
    <h1>Regras</h1>
    <h3>Digite à direita os valores que aparecem à esquerda na mesma sequência.</h3>
    <h3>Compare-os e veja quantos acertou.</h3>
    <h3>A cada jogada a sequência de números aumenta.</h3>
    <h3>Recomece quando desejar.</h3>
</div>

<div>
    <h1>Jogo da Memória</h1>
    <div id="main">
        <div class="data" id="computer">
            <input type="text" bind:value={computerInput} readonly /><br />
            <button class="btn" id="btn-start" on:click={startGame}>Jogar</button>
        </div>
        <div class="data">
            <input type="text" bind:value={userInput} /><br />
            <button class="btn" id="btn-submit" on:click={submit} disabled={btnSubmitDisabled}>Enviar</button>
        </div>
    </div>
    <div id="btn">
        <button class="btn" id="btn-stop" on:click={resetGame}>Recomeçar</button>
    </div>
    <div id="resultComp">{resultComp}</div>
	<div id="resultUser">{resultUser}</div>
</div>
</body>