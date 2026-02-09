<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Be My Valentine? 💕</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            font-family: 'Arial', sans-serif;
            overflow: hidden;
        }

        .container {
            text-align: center;
            background: white;
            padding: 60px 40px;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            max-width: 500px;
            animation: slideUp 0.8s ease-out;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        h1 {
            color: #ff4458;
            font-size: 2.5em;
            margin-bottom: 20px;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-20px);
            }
        }

        .heart-animation {
            font-size: 4em;
            display: inline-block;
            margin: 20px 0;
            animation: heartbeat 1.2s infinite;
        }

        @keyframes heartbeat {
            0%, 100% {
                transform: scale(1);
            }
            25% {
                transform: scale(1.2);
            }
            50% {
                transform: scale(1);
            }
        }

        p {
            color: #333;
            font-size: 1.2em;
            margin: 20px 0;
            line-height: 1.6;
        }

        .button-container {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin-top: 40px;
            flex-wrap: wrap;
        }

        button {
            padding: 15px 40px;
            font-size: 1.1em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
        }

        .yes-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .yes-btn:hover {
            transform: scale(1.1);
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
        }

        .no-btn {
            background: #e0e0e0;
            color: #666;
        }

        .no-btn:hover {
            background: #d0d0d0;
            transform: translateX(20px);
        }

        .floating-hearts {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            pointer-events: none;
            z-index: -1;
        }

        .heart {
            position: absolute;
            color: rgba(255, 68, 88, 0.6);
            font-size: 2em;
            animation: float 3s infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(0) translateX(0);
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) translateX(50px);
                opacity: 0;
            }
        }

        .success-message {
            display: none;
            text-align: center;
            animation: slideUp 0.6s ease-out;
        }

        .success-message h2 {
            color: #ff4458;
            font-size: 2em;
            margin: 20px 0;
        }

        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background: #ff4458;
            animation: confetti-fall 3s ease-in forwards;
        }

        /* Panda and Gorilla Hug Animation */
        .hug-container {
            position: relative;
            height: 200px;
            margin: 40px 0;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .panda {
            font-size: 80px;
            position: absolute;
            animation: pandaHug 1.5s ease-in-out forwards;
            left: 20px;
            z-index: 2;
        }

        .gorilla {
            font-size: 80px;
            position: absolute;
            animation: gorillaHug 1.5s ease-in-out forwards;
            right: 20px;
            z-index: 1;
        }

        @keyframes pandaHug {
            0% {
                left: -100px;
                opacity: 0;
            }
            50% {
                opacity: 1;
            }
            100% {
                left: 30px;
                transform: scaleX(-1);
                opacity: 1;
            }
        }

        @keyframes gorillaHug {
            0% {
                right: -100px;
                opacity: 0;
            }
            50% {
                opacity: 1;
            }
            100% {
                right: 30px;
                opacity: 1;
            }
        }

        .hug-hearts {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 3em;
            animation: hugHeartbeat 1.2s ease-in-out 0.8s infinite;
            z-index: 3;
        }

        @keyframes hugHeartbeat {
            0%, 100% {
                transform: translate(-50%, -50%) scale(1);
                opacity: 1;
            }
            50% {
                transform: translate(-50%, -50%) scale(1.3);
                opacity: 1;
            }
        }
    </style>
</head>
<body>
    <div class="floating-hearts" id="floatingHearts"></div>

    <div class="container">
        <div id="question">
            <h1>Will You Be My Valentine? 💕</h1>
            <div class="heart-animation">❤️</div>
            <p>I'd love to spend this special day with you!</p>
            <div class="button-container">
                <button class="yes-btn" onclick="handleYes()">Yes! ❤️</button>
                <button class="no-btn" onclick="handleNo()">No</button>
            </div>
        </div>

        <div id="successMessage" class="success-message">
            <h2>🎉 You Just Made Me The Happiest Person! 🎉</h2>
            
            <div class="hug-container">
                <div class="panda">🐼</div>
                <div class="gorilla">🦍</div>
                <div class="hug-hearts">💕</div>
            </div>

            <p>I can't wait to celebrate with you!</p>
        </div>
    </div>

    <script>
        // Create floating hearts
        function createFloatingHearts() {
            const container = document.getElementById('floatingHearts');
            for (let i = 0; i < 20; i++) {
                const heart = document.createElement('div');
                heart.className = 'heart';
                heart.textContent = '❤️';
                heart.style.left = Math.random() * 100 + '%';
                heart.style.top = Math.random() * 100 + '%';
                heart.style.animationDelay = Math.random() * 2 + 's';
                heart.style.animationDuration = (3 + Math.random() * 2) + 's';
                container.appendChild(heart);
            }
        }

        function handleYes() {
            const question = document.getElementById('question');
            const success = document.getElementById('successMessage');
            question.style.display = 'none';
            success.style.display = 'block';
            createConfetti();
        }

        function handleNo() {
            const noBtn = document.querySelector('.no-btn');
            noBtn.style.position = 'fixed';
            noBtn.style.top = Math.random() * 80 + '%';
            noBtn.style.left = Math.random() * 80 + '%';
        }

        function createConfetti() {
            for (let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + '%';
                confetti.style.background = ['#ff4458', '#667eea', '#ffd700', '#ff69b4'][Math.floor(Math.random() * 4)];
                confetti.style.animationDelay = Math.random() * 0.5 + 's';
                confetti.style.animationDuration = (2 + Math.random() * 1) + 's';
                document.body.appendChild(confetti);
                setTimeout(() => confetti.remove(), 3000);
            }
        }

        // Initialize floating hearts on page load
        window.addEventListener('load', createFloatingHearts);
    </script>
</body>
</html>
