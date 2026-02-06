<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Rishitha ❤️</title>
    <style>
        body {
            background-color: #ffe4e1;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: 'Arial', sans-serif;
            overflow: hidden;
            cursor: pointer; /* Suggests clicking */
        }

        /* Falling Hearts */
        .heart-bg {
            position: fixed;
            top: -10vh;
            font-size: 20px;
            color: #ff4d6d;
            user-select: none;
            z-index: -1;
            animation: fall linear forwards;
        }

        @keyframes fall {
            to { transform: translateY(110vh) rotate(360deg); }
        }

        .card {
            background: rgba(255, 255, 255, 0.9);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.1);
            text-align: center;
            width: 350px;
            backdrop-filter: blur(10px);
            z-index: 10;
        }

        .main-heart { font-size: 70px; animation: pulse 1s infinite alternate; }

        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.1); }
        }

        h1 { color: #d63384; margin: 20px 0; font-size: 24px; }
        p.tap-hint { font-size: 12px; color: #999; margin-top: -10px; }

        .button-box {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
            height: 50px;
        }

        .btn {
            padding: 12px 30px;
            font-size: 18px;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        #yes-btn { background-color: #ff4d6d; color: white; transition: 0.3s; }
        #yes-btn:hover { transform: scale(1.1); background-color: #ff758c; }

        #no-btn { 
            background-color: #adb5bd; 
            color: white; 
            position: absolute; 
            transition: 0.1s; /* Quick jump */
        }

        #success-msg { display: none; }
        #success-msg h2 { color: #ff4d6d; font-size: 28px; margin-bottom: 10px; }
    </style>
</head>
<body onclick="startMusic()">

    <audio id="bgMusic" loop>
        <source src="https://www.bensound.com/bensound-music/bensound-love.mp3" type="audio/mpeg">
    </audio>

    <div class="card">
        <div id="proposal-content">
            <div class="main-heart">💖</div>
            <h1>Rishitha, will you be my Valentine?</h1>
            <p class="tap-hint">(Tap anywhere for music 🎵)</p>
            <div class="button-box">
                <button id="yes-btn" class="btn" onclick="celebrate()">Yes</button>
                <button id="no-btn" class="btn" onmouseover="moveNo()" onclick="moveNo()">No</button>
            </div>
        </div>

        <div id="success-msg">
            <div class="main-heart">🥰</div>
            <h2>Yay! ❤️</h2>
            <p>You've made me the luckiest person, Rishitha!</p>
        </div>
    </div>

    <script>
        const audio = document.getElementById("bgMusic");

        function startMusic() {
            audio.play();
        }

        // Logic for the runaway button
        function moveNo() {
            const btn = document.getElementById('no-btn');
            // Logic to keep button inside the screen area
            const x = Math.floor(Math.random() * (window.innerWidth - btn.offsetWidth - 20));
            const y = Math.floor(Math.random() * (window.innerHeight - btn.offsetHeight - 20));

            btn.style.position = 'fixed';
            btn.style.left = x + 'px';
            btn.style.top = y + 'px';
        }

        // Logic for when she says Yes
        function celebrate() {
            document.getElementById('proposal-content').style.display = 'none';
            document.getElementById('success-msg').style.display = 'block';
            
            // Increase falling heart speed for celebration
            setInterval(createHeart, 100);
        }

        // Falling heart background generator
        function createHeart() {
            const heart = document.createElement('div');
            heart.className = 'heart-bg';
            heart.innerHTML = '❤️';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
            document.body.appendChild(heart);
            setTimeout(() => { heart.remove(); }, 5000);
        }

        // Initialize slow falling hearts
        setInterval(createHeart, 500);
    </script>
</body>
</html>
