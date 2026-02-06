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
        }

        /* Floating Hearts Background */
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
            background: white;
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.1);
            text-align: center;
            width: 350px;
            position: relative;
            z-index: 10;
        }

        .main-heart {
            font-size: 80px;
            animation: pulse 1s infinite alternate;
        }

        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.1); }
        }

        h1 { color: #d63384; margin: 20px 0; font-size: 24px; }

        .button-box {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
            height: 60px; /* Buffer for buttons */
        }

        .btn {
            padding: 15px 35px;
            font-size: 18px;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.2s ease;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }

        #yes-btn {
            background-color: #ff4d6d;
            color: white;
        }

        #no-btn {
            background-color: #adb5bd;
            color: white;
            position: absolute; /* Allows freedom of movement */
        }

        #success-msg {
            display: none;
        }

        #success-msg h2 { color: #ff4d6d; font-size: 28px; }
    </style>
</head>
<body>

    <div class="card" id="main-card">
        <div id="proposal-content">
            <div class="main-heart">💖</div>
            <h1>Rishitha, will you be my Valentine?</h1>
            <div class="button-box">
                <button id="yes-btn" class="btn" onclick="celebrate()">Yes</button>
                <button id="no-btn" class="btn" onmouseover="moveNo()" onclick="moveNo()">No</button>
            </div>
        </div>

        <div id="success-msg">
            <div class="main-heart">🥰</div>
            <h2>I knew it! ❤️</h2>
            <p>See you soon, Rishitha!</p>
        </div>
    </div>

    <script>
        // Function to move the "No" button randomly
        function moveNo() {
            const btn = document.getElementById('no-btn');
            
            // Generate random X and Y coordinates within the viewport
            // We subtract button size to keep it within view
            const x = Math.floor(Math.random() * (window.innerWidth - btn.offsetWidth));
            const y = Math.floor(Math.random() * (window.innerHeight - btn.offsetHeight));

            btn.style.position = 'fixed'; // Keeps it relative to the screen
            btn.style.left = x + 'px';
            btn.style.top = y + 'px';
        }

        // Function when she clicks "Yes"
        function celebrate() {
            document.getElementById('proposal-content').style.display = 'none';
            document.getElementById('success-msg').style.display = 'block';
            
            // Trigger extra heart burst
            for(let i=0; i<50; i++) {
                setTimeout(createHeart, i * 50);
            }
        }

        // Create falling hearts background
        function createHeart() {
            const heart = document.createElement('div');
            heart.className = 'heart-bg';
            heart.innerHTML = '❤️';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
            heart.style.opacity = Math.random();
            document.body.appendChild(heart);

            setTimeout(() => { heart.remove(); }, 5000);
        }

        // Start background hearts
        setInterval(createHeart, 400);
    </script>
</body>
</html>
