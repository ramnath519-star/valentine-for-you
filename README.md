<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Special Surprise for Rishitha ❤️</title>
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

        /* Falling Hearts/Glitters Background */
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
            width: 350px;
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

        h1 { color: #d63384; font-size: 22px; margin: 20px 0; min-height: 80px; display: flex; align-items: center; justify-content: center; }

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

        #yes-btn { background-color: #ff4d6d; color: white; transition: 0.2s; }
        
        #no-btn { 
            background-color: #adb5bd; 
            color: white; 
            position: relative; 
            transition: 0.1s ease; 
        }

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
            letter-spacing: 1px;
        }
    </style>
</head>
<body onclick="playMusic()">

    <audio id="bgMusic" loop>
        <source src="https://files.catbox.moe/39k013.mp3" type="audio/mpeg">
    </audio>

    <div class="card">
        <div id="quiz-box">
            <div class="progress" id="step-text">Step 1 of 6</div>
            <div class="main-heart">💖</div>
            <h1 id="question-text">Do you believe in love?</h1>
            
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
            "Do you believe in love?",
            "Would you go on a Valentine’s date with me?",
            "Do small surprises make you happy?",
            "Is spending time together more important than gifts?",
            "Do you think we’d make a good pair?",
            "Rishitha, will you be my Valentine?"
        ];

        let currentStep = 0;
        const music = document.getElementById("bgMusic");

        function playMusic() { 
            music.play().catch(() => {
                console.log("Interact with page to play audio");
            }); 
        }

        // Runaway Button Logic
        function moveNo() {
            playMusic();
            const btn = document.getElementById('no-btn');
            btn.style.position = 'fixed';
            
            // Randomly move button within the window bounds
            const maxX = window.innerWidth - btn.offsetWidth - 20;
            const maxY = window.innerHeight - btn.offsetHeight - 20;
            
            const randomX = Math.floor(Math.random() * maxX);
            const randomY = Math.floor(Math.random() * maxY);
            
            btn.style.left = randomX + 'px';
            btn.style.top = randomY + 'px';
        }

        function nextQuestion() {
            playMusic();
            currentStep++;

            if (currentStep < questions.length) {
                // Update text to next question
                document.getElementById('question-text').innerText = questions[currentStep];
                document.getElementById('step-text').innerText = `Step ${currentStep + 1} of 6`;
                
                // Return No button to card momentarily for the new question
                const noBtn = document.getElementById('no-btn');
                noBtn.style.position = 'relative';
                noBtn.style.left = '0';
                noBtn.style.top = '0';
            } else {
                showFinal();
            }
        }

        function showFinal() {
            document.getElementById('quiz-box').style.display = 'none';
            document.getElementById('success-msg').style.display = 'block';
            startCountdown();
            setInterval(createHeart, 100); // Massive heart/glitter shower
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
                document.getElementById("countdown").innerText = `Our date in: ${d}d ${h}h ${m}m ${s}s`;
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

        // Continuous slow background hearts
        setInterval(createHeart, 600);
    </script>
</body>
</html>
