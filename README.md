<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gioco: Indovina il Numero - 20 Livelli</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f4;
        }
        .game-container {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        input[type="number"] {
            padding: 10px;
            margin: 10px 0;
            width: 50%;
            font-size: 16px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
        }
        button:hover {
            background-color: #45a049;
        }
        .message {
            font-size: 18px;
            margin-top: 15px;
        }
        .level {
            font-size: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="game-container">
    <h1>Indovina il Numero - 20 Livelli</h1>
    <p id="levelText" class="level">Livello 1: Indovina un numero tra 1 e 10.</p>
    <input type="number" id="userGuess" min="1" placeholder="Inserisci il numero">
    <br>
    <button onclick="checkGuess()">Indovina!</button>
    <div class="message" id="message"></div>
</div>

<script>
    let currentLevel = 1; // Livello corrente
    let maxLevel = 20;    // Numero massimo di livelli
    let secretNumber;     // Numero segreto
    let attempts = 0;     // Tentativi fatti

    // Funzione per inizializzare un nuovo livello
    function startLevel(level) {
        const maxNumber = level * 5; // Aumenta il range dei numeri a seconda del livello
        secretNumber = Math.floor(Math.random() * maxNumber) + 1;
        document.getElementById("levelText").textContent = `Livello ${level}: Indovina un numero tra 1 e ${maxNumber}.`;
        document.getElementById("message").textContent = "";
        document.getElementById("userGuess").value = "";
    }

    // Funzione per controllare la risposta dell'utente
    function checkGuess() {
        const userGuess = parseInt(document.getElementById("userGuess").value);
        const messageDiv = document.getElementById("message");
        attempts++;

        if (userGuess === secretNumber) {
            messageDiv.textContent = `Corretto! Hai completato il livello ${currentLevel} in ${attempts} tentativi.`;
            messageDiv.style.color = "green";

            setTimeout(function() {
                if (currentLevel < maxLevel) {
                    currentLevel++;
                    attempts = 0;
                    startLevel(currentLevel);
                } else {
                    messageDiv.textContent = `Complimenti! Hai completato tutti i 20 livelli in ${attempts} tentativi!`;
                    messageDiv.style.color = "blue";
                }
            }, 2000); // Passa al prossimo livello dopo 2 secondi
        } else if (userGuess < secretNumber) {
            messageDiv.textContent = `Il numero segreto è più grande. Riprova!`;
            messageDiv.style.color = "orange";
        } else if (userGuess > secretNumber) {
            messageDiv.textContent = `Il numero segreto è più piccolo. Riprova!`;
            messageDiv.style.color = "orange";
        } else {
            messageDiv.textContent = "Per favore, inserisci un numero valido!";
            messageDiv.style.color = "red";
        }
    }

    // Inizializza il gioco al primo livello
    startLevel(currentLevel);
</script>

</body>
</html>
