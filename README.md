<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI in K-12 Education Game</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500&display=swap');
        
        body {
            font-family: 'Orbitron', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #0a1a33;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-image: url('science-blue-background.jpg'); /* Replace with a science/AI themed image */
            background-size: cover;
            background-position: center;
        }
        .container {
            text-align: center;
            background: rgba(0, 0, 0, 0.8);
            padding: 50px;
            border-radius: 15px;
            box-shadow: 0 4px 8px rgba(0, 100, 255, 0.5);
        }
        h1 {
            color: #00ccff;
            font-size: 3rem;
            text-shadow: 0px 0px 15px #00ccff;
        }
        p {
            color: #bbb;
            font-size: 1.3rem;
            margin-top: 20px;
        }
        .button {
            display: inline-block;
            margin-top: 40px;
            padding: 15px 30px;
            background-color: #008CFF;
            color: #fff;
            font-size: 1.2rem;
            border-radius: 30px;
            text-decoration: none;
            box-shadow: 0 4px 10px rgba(0, 100, 255, 0.7);
            transition: background-color 0.3s ease, box-shadow 0.3s ease;
            cursor: pointer;
        }
        .button:hover {
            background-color: #006bb3;
            box-shadow: 0 6px 12px rgba(0, 150, 255, 0.9);
        }
        .input-field {
            margin-top: 20px;
            padding: 10px;
            width: 80%;
            max-width: 300px;
            border-radius: 5px;
            border: 1px solid #00ccff;
            background-color: #0a1a33;
            color: white;
            font-size: 1rem;
        }
        #username-page, #game-page, #ranking-page, #mode-selection-page {
            display: none;
        }
    </style>
    <script>
        let score = 0;
        let startTime;

        function showUsernamePage() {
            document.getElementById('start-page').style.display = 'none';
            document.getElementById('username-page').style.display = 'block';
        }

        function saveUsername() {
            const username = document.getElementById('username-input').value;
            if (!username) {
                alert('Please enter a username');
                return;
            }
            localStorage.setItem('playerUsername', username);
            localStorage.setItem('startTime', new Date().getTime());  // Save start time
            showModeSelectionPage();  // Show mode selection page
        }

        function showModeSelectionPage() {
            document.getElementById('username-page').style.display = 'none';
            document.getElementById('mode-selection-page').style.display = 'block';
        }

        function chooseSinglePlayer() {
            // For now, direct to the game page for single-player
            showGamePage();
        }

        function chooseMultiplayer() {
            // Implement multiplayer logic later
            alert('Multiplayer mode coming soon!');
        }

        function showGamePage() {
            document.getElementById('mode-selection-page').style.display = 'none';
            document.getElementById('game-page').style.display = 'block';
            startTime = new Date().getTime();
            document.getElementById('username-display').innerText = 'Welcome, ' + localStorage.getItem('playerUsername');
        }

        function increaseScore() {
            score += 10;  // Simulate score increase
            document.getElementById('score-display').innerText = 'Score: ' + score;
        }

        function finishGame() {
            const endTime = new Date().getTime();
            const timeTaken = Math.floor((endTime - startTime) / 1000); // Time in seconds
            localStorage.setItem('playerScore', score);
            localStorage.setItem('timeTaken', timeTaken);
            showRankingPage();  // Show the ranking page
        }

        function showRankingPage() {
            document.getElementById('game-page').style.display = 'none';
            document.getElementById('ranking-page').style.display = 'block';

            const username = localStorage.getItem('playerUsername');
            const score = localStorage.getItem('playerScore');
            const timeTaken = localStorage.getItem('timeTaken');

            document.getElementById('ranking-list').innerHTML = `
                <tr>
                    <td>${username}</td>
                    <td>${score}</td>
                    <td>${timeTaken} seconds</td>
                </tr>
            `;
        }
    </script>
</head>
<body>

    <!-- Start Page Section -->
    <div class="container" id="start-page">
        <h1>AI in K-12 Education</h1>
        <p>Discover how AI transforms classrooms and unlocks new learning potential!</p>
        <button class="button" onclick="showUsernamePage()">Start the Game</button>
    </div>

    <!-- Username Input Page Section -->
    <div class="container" id="username-page">
        <h1>Enter Your Username</h1>
        <input type="text" id="username-input" class="input-field" placeholder="Enter your username" required>
        <button class="button" onclick="saveUsername()">Submit</button>
    </div>

    <!-- Mode Selection Page Section -->
    <div class="container" id="mode-selection-page">
        <h1>Choose Game Mode</h1>
        <p>Select the mode you want to play.</p>
        <button class="button" onclick="chooseSinglePlayer()">Single-Player Mode</button>
        <br><br>
        <button class="button" onclick="chooseMultiplayer()">Multiplayer Mode</button>
    </div>

    <!-- Game Page Section -->
    <div class="container" id="game-page">
        <h1 id="username-display"></h1>
        <p id="score-display">Score: 0</p>
        <button class="button" onclick="increaseScore()">Increase Score</button>
        <br><br>
        <button class="button" onclick="finishGame()">Finish Game</button>
    </div>

    <!-- Ranking Page Section -->
    <div class="container" id="ranking-page">
        <h1>Game Rankings</h1>
        <table>
            <thead>
                <tr>
                    <th>Username</th>
                    <th>Score</th>
                    <th>Time Taken</th>
                </tr>
            </thead>
            <tbody id="ranking-list">
                <!-- Rankings will be injected here -->
            </tbody>
        </table>
    </div>

</body>
</html>
