<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Rishitha ❤️</title>
    <script src="https://w.soundcloud.com/player/api.js"></script>
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
            background: rgba(255, 255, 255, 0.95);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 20px 50px rgba(233, 30, 99, 0.2);
            text-align: center;
            width: 320px;
            backdrop-filter: blur(10px);
            z-index: 10;
            border: 2px solid #fff;
            position: relative;
        }

        .main-heart { 
            font-size: 60px; 
            animation: pulse 0.8s infinite alternate; 
        }

        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.15); }
        }

        h1 { color: #d63384; font-size: 22px; margin: 20px 0; min-height: 80px; display: flex; align-items: center; justify-content: center; line-height: 1.4; }

        .btn-container {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            margin-top: 20px;
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

        #yes-btn { background-color: #ff4d6d; color: white; }
        #no-btn { background-color: #adb5bd; color: white; position: relative; transition: 0.1s ease; }

        #success-msg { display: none; }
        
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

        .progress {
            font-size: 12px;
            color: #ff758c;
            margin-bottom: 10px;
            text-transform: uppercase;
        }

        /* The SoundCloud player is kept invisible */
        #sc-player { display: none; }
    </style>
</head>
<body>

    <iframe id="sc-player" width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" 
        src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/837648355&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true">
    </iframe>

    <div class="card">
        <div id="quiz-box">
            <div class="progress" id="step-text">Step 1 of 6</div>
            <div class="main-heart">💖</div>
            <h1 id="question-text">Rishitha, do you believe in love?</h1>
            
            <div class="btn-container">
                <button id="yes-btn" onclick="nextQuestion()">Yes</button>
                <button id="no-btn" onmouseover="moveNo()" ontouchstart="moveNo()">No</button>
            </div>
        </div>

        <div id="success-msg">
            <div class="main-heart">🥰</div>
            <h2>Yay! ❤️</h2>
            <p>I knew you'd say yes to everything, Rishitha!</p>
            <div id="countdown">Calculating our time...</div>
        </div>
    </div>

    <script>
        const questions = [
            "Rishitha, do you believe in love?",
            "Rishitha, would you go on a Valentine’s date with me?",
            "Rishitha, do small surprises make you happy?",
            "Rishitha, is spending time together more important than gifts?",
            "Rishitha, do you think we’d make a good pair?",
            "Rishitha, will you be my Valentine?"
        ];

        let currentStep = 0;
        let musicStarted = false;
        
        // Initialize the SoundCloud widget
        const widget = SC.Widget(document.getElementById('sc-player'));

        function playMusic() {
            if (!musicStarted) {
                widget.play();
                musicStarted = true;
            }
        }

        function moveNo() {
            playMusic();
            const btn = document.getElementById('no-btn');
            btn.style.position = 'fixed';
            const maxX = window.innerWidth - btn.offsetWidth - 20;
            const maxY = window.innerHeight - btn.offsetHeight - 20;
            btn.style.left = Math.floor(Math.random() * maxX) + 'px';
            btn.style.top = Math.floor(Math.random() * maxY) + 'px';
        }

        function nextQuestion() {
            playMusic();
            currentStep++;
            if (currentStep < questions.length) {
                document.getElementById('question-text').innerText = questions[currentStep];
                document.getElementById('step-text').innerText = `Step ${currentStep + 1} of 6`;
                const noBtn = document.getElementById('no-btn');
                noBtn.style.position = 'relative';
                noBtn.style.left = '0'; noBtn.style.top = '0';
            } else {
                document.getElementById('quiz-box').style.display = 'none';
                document.getElementById('success-msg').style.display = 'block';
                startCountdown();
                setInterval(createHeart, 100);
            }
        }

        function startCountdown() {
            // Updated to Valentine's Day 2026
            const countDate = new Date("Feb 14, 2026 00:00:00").getTime();
            setInterval(() => {
                const now = new Date().getTime();
                const gap = countDate - now;
                const d = Math.floor(gap / (1000 * 60 * 60 * 24));
                const h = Math.floor((gap % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                const m = Math.floor((gap % (1000 * 60 * 60)) / (1000 * 60));
                const s = Math.floor((gap % (1000 * 60)) / 1000);
                document.getElementById("countdown").innerText = `Our date in: ${d}d ${h}h ${m}m ${s}s`;
            }, 1000);
        }

        function createHeart() {
            const heart = document.createElement('div');
            heart.className = 'falling-heart';
            heart.innerHTML = '❤️';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
            document.body.appendChild(heart);
            setTimeout(() => { heart.remove(); }, 5000);
        }
        setInterval(createHeart, 600);
    </script>
</body>
</html>
