<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>System Node</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #050505;
            color: #00ff66;
            font-family: 'Courier New', Courier, monospace;
            overflow: hidden;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            opacity: 0.15;
        }

        .container {
            position: relative;
            z-index: 2;
            text-align: center;
            padding: 2rem;
            border: 1px solid rgba(0, 255, 102, 0.2);
            background: rgba(10, 10, 10, 0.85);
            box-shadow: 0 0 30px rgba(0, 255, 102, 0.15);
            backdrop-filter: blur(5px);
            max-width: 90%;
            border-radius: 8px;
        }

        .hud-header {
            font-size: 0.75rem;
            color: #008833;
            letter-spacing: 2px;
            margin-bottom: 1.5rem;
            text-transform: uppercase;
        }

        .message-box {
            position: relative;
            margin: 20px 0;
        }

        .main-text {
            font-size: 2.2rem;
            font-weight: bold;
            color: #00ff66;
            text-shadow: 0 0 10px rgba(0, 255, 102, 0.7),
                         0 0 20px rgba(0, 255, 102, 0.4);
            letter-spacing: 1px;
            position: relative;
            display: inline-block;
        }

        /* Glitch Effect */
        .glitch {
            position: relative;
        }
        .glitch::before, .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            clip: rect(0, 0, 0, 0);
        }
        .glitch::before {
            left: -2px;
            text-shadow: 2px 0 #ff0055;
            animation: glitch-anim-1 2s infinite linear alternate-reverse;
        }
        .glitch::after {
            left: 2px;
            text-shadow: -2px 0 #00e5ff;
            animation: glitch-anim-2 3s infinite linear alternate-reverse;
        }

        @keyframes glitch-anim-1 {
            0% { clip: rect(20px, 9999px, 15px, 0); }
            20% { clip: rect(50px, 9999px, 80px, 0); }
            40% { clip: rect(10px, 9999px, 40px, 0); }
            60% { clip: rect(70px, 9999px, 20px, 0); }
            80% { clip: rect(30px, 9999px, 60px, 0); }
            100% { clip: rect(90px, 9999px, 10px, 0); }
        }

        @keyframes glitch-anim-2 {
            0% { clip: rect(10px, 9999px, 60px, 0); }
            20% { clip: rect(80px, 9999px, 10px, 0); }
            40% { clip: rect(30px, 9999px, 90px, 0); }
            60% { clip: rect(50px, 9999px, 30px, 0); }
            80% { clip: rect(20px, 9999px, 70px, 0); }
            100% { clip: rect(60px, 9999px, 40px, 0); }
        }

        .hud-footer {
            margin-top: 1.5rem;
            font-size: 0.7rem;
            color: #008833;
            display: flex;
            justify-content: space-between;
            border-top: 1px solid rgba(0, 255, 102, 0.1);
            padding-top: 0.8rem;
        }

        @media (max-width: 600px) {
            .main-text {
                font-size: 1.5rem;
            }
        }
    </style>
</head>
<body>

    <canvas id="matrix"></canvas>

    <div class="container">
        <div class="hud-header">
            [ SYS_EXEC // PROTOCOL_0x3F9 ]
        </div>

        <div class="message-box">
            <div class="main-text glitch" data-text="اللعنة عليك يا فراس">
                اللعنة عليك يا فراس
            </div>
        </div>

        <div class="hud-footer">
            <span>STATUS: ACTIVE</span>
            <span>0x88F2A</span>
        </div>
    </div>

    <script>
        // Matrix Rain Background Effect
        const canvas = document.getElementById('matrix');
        const ctx = canvas.getContext('2d');

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);

        const chars = '0123456789ABCDEFHIJKLMNOPQRSTUVWXYZ<>/{}[]*&^%$#@!';
        const fontSize = 14;
        const columns = Math.floor(canvas.width / fontSize);
        const drops = Array(columns).fill(1);

        function drawMatrix() {
            ctx.fillStyle = 'rgba(5, 5, 5, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            ctx.fillStyle = '#00ff66';
            ctx.font = fontSize + 'px monospace';

            for (let i = 0; i < drops.length; i++) {
                const text = chars.charAt(Math.floor(Math.random() * chars.length));
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);

                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                drops[i]++;
            }
        }

        setInterval(drawMatrix, 33);
    </script>
</body>
</html>

