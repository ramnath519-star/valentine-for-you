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
            font-family: 'Segoe UI', Tahoma, sans-serif;
            overflow: hidden;
            touch-action: none;
        }

        /* Falling Hearts/Glitters */
        .falling-heart {
            position: fixed;
            top: -10vh;
            color: #ff4d6d;
            font-size: 20px;
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
            box-shadow: 0 20px 50px rgba(233, 30, 99, 0.2);
            text-align: center;
            width: 340px;
            backdrop-filter: blur(10px);
            z-index: 10;
            border: 2px solid #fff;
            position: relative; /* Keep buttons relative to card initially */
        }

        .main-heart { 
            font-size: 70px; 
            animation: pulse 0.8s infinite alternate; 
        }

        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.15); }
        }

        h1 { color: #d63384; font-size: 24px; margin: 20px 0; }

        .btn-container {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            margin-top: 30px;
            min-height: 60px;
        }

        button {
            padding: 12px 30px;
            font-size: 18px;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            z-index: 20;
        }

        #yes-btn { 
            background-color: #ff4d6d; 
            color: white; 
        }

        #no-btn { 
            background-color: #adb5bd; 
            color: white; 
            transition: 0.1s ease;
            position: relative; /* Starts visible inside the container */
        }

        #success-msg { display: none; }
        #success-msg h2 { color: #d63384; font-size: 28px; }
        
        #countdown {
            margin-top: 20px;
            font-weight: bold;
            color: #ff4d6d;
            font-size: 1.1rem;
            background: #fff0f3;
            padding: 15px;
            border-radius: 15px;
            border: 1px dashed #ff4d6d;
        }
    </style>
</head>
<body onclick="playMusic()">

    <audio id="bgMusic" loop>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg">
    </audio>

    <div class="card">
        <div id="proposal-box">
            <div class="main-heart">💖</div>
            <h1>Rishitha, will you be my Valentine?</h1>
            
            <div class="btn-container">
                <button id="yes-btn" onclick="sayYes()">Yes</button>
                <button id="no-btn" onmouseover="moveNo()" ontouchstart="moveNo()">No</button>
            </div>
        </div>

        <div id="success-msg">
            <div class="main-heart">🥰</div>
            <h2>Yay! ❤️</h2>
            <p>I knew you'd say yes, Rishitha!</p>
            <div id="countdown">Calculating...</div>
        </div>
    </div>

    <script>
        const music = document.getElementById("bgMusic");

        function playMusic() { 
            music.play().catch(() => {}); 
        }

        function moveNo() {
            playMusic();
            const btn = document.getElementById('no-btn');
            
            // Switch to fixed positioning so it can jump ANYWHERE on the screen
            btn.style.position = 'fixed';
            
            const x = Math.random() * (window.innerWidth - btn.offsetWidth - 20);
            const y = Math.random() * (window.innerHeight - btn.offsetHeight - 20);
            
            btn.style.left = `${x}px`;
            btn.style.top = `${y}px`;
        }

        function sayYes() {
            playMusic();
            document.getElementById('proposal-box').style.display = 'none';
            document.getElementById('success-msg').style.display = 'block';
            startCountdown();
            setInterval(createHeart, 100);
        }

        function startCountdown() {
            const countDate = new Date("Feb 14, 2026 00:00:00").getTime();
            setInterval(() => {
                const now = new Date().getTime();
                const gap = countDate - now;
                const d = Math.floor(gap / (1000 * 60 * 60 * 24));
                const h = Math.floor((gap % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                const m = Math.floor((gap % (1000 * 60 * 60)) / (1000 * 60));
                const s = Math.floor((gap % (1000 * 60)) / 1000);
                document.getElementById("countdown").innerText = `See you in: ${d}d ${h}h ${m}m ${s}s`;
            }, 1000);
        }

        function createHeart() {
            const heart = document.createElement('div');
            heart.className = 'falling-heart';
            heart.innerHTML = Math.random() > 0.5 ? '❤️' : '✨';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
            document.body.appendChild(heart);
            setTimeout(() => { heart.remove(); }, 5000);
        }

        setInterval(createHeart, 600);
    </script>
</body>
</html>
