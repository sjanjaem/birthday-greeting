<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday!</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            overflow: hidden;
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            flex-direction: column;
            animation: backgroundShift 10s infinite alternate;
        }

        @keyframes backgroundShift {
            0% { background: linear-gradient(135deg, #ff9a9e, #fad0c4); }
            100% { background: linear-gradient(135deg, #a18cd1, #fbc2eb); }
        }

        h1 {
            font-size: 2.5em;
            color: #ff69b4;
            margin: 10px 0;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-15px); }
        }

        p {
            font-size: 1.2em;
            color: #6a5acd;
        }

        .balloon {
            position: absolute;
            width: 40px;
            height: 60px;
            background: red;
            border-radius: 50% 50% 45% 45%;
            box-shadow: inset -4px -4px 10px rgba(0,0,0,0.2);
            animation: float 5s infinite ease-in-out;
        }

        @keyframes float {
            0% { transform: translateY(0); }
            50% { transform: translateY(-150px); }
            100% { transform: translateY(0); }
        }

        .firework {
            position: absolute;
            width: 5px;
            height: 5px;
            background: yellow;
            border-radius: 50%;
            animation: explode 1s ease-out infinite;
        }

        @keyframes explode {
            0% { transform: scale(0); opacity: 1; }
            100% { transform: scale(5); opacity: 0; }
        }

        .pin-container {
            display: flex;
            gap: 10px;
            justify-content: center;
        }

        .pin-input {
            width: 50px;
            height: 50px;
            font-size: 2em;
            text-align: center;
            border: 2px solid #6a5acd;
            border-radius: 10px;
            outline: none;
            transition: transform 0.3s ease;
        }

        .pin-input:focus {
            transform: scale(1.1);
        }

        img {
            max-width: 90%;
            height: auto;
            margin: 10px 0;
        }

        .message {
            font-size: 1.2em;
            color: #333;
            padding: 20px;
            max-width: 90%;
            line-height: 1.8;
            text-align: center;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            animation: fadeIn 2s ease-in-out;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .hidden {
            display: none;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .highlight {
            color: #ff4500;
            font-weight: bold;
            font-size: 1.4em;
            animation: glow 1.5s infinite alternate;
        }

        @keyframes glow {
            from { text-shadow: 0 0 10px #ff4500; }
            to { text-shadow: 0 0 20px #ff6347; }
        }

        a {
            color: #6a5acd;
            text-decoration: none;
            font-weight: bold;
            transition: color 0.3s;
        }

        a:hover {
            color: #ff69b4;
        }
    </style>
</head>
<body>
    <div id="pinSection">
        <h1>🎉 Happy Birthday! 🎂</h1>
        <p>Enter your 4-digit PIN to unlock the surprise!</p>
        <div class="pin-container">
            <input type="number" maxlength="1" class="pin-input" id="pin1">
            <input type="number" maxlength="1" class="pin-input" id="pin2">
            <input type="number" maxlength="1" class="pin-input" id="pin3">
            <input type="number" maxlength="1" class="pin-input" id="pin4">
        </div>
    </div>

    <div id="surprise" class="hidden"></div>

    <script>
        function createBalloon() {
            const balloon = document.createElement('div');
            balloon.classList.add('balloon');
            balloon.style.left = Math.random() * window.innerWidth + 'px';
            balloon.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 70%)`;
            document.body.appendChild(balloon);

            setTimeout(() => {
                balloon.remove();
            }, 5000);
        }

        function createFirework() {
            const firework = document.createElement('div');
            firework.classList.add('firework');
            firework.style.left = Math.random() * window.innerWidth + 'px';
            firework.style.top = Math.random() * window.innerHeight + 'px';
            firework.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 60%)`;
            document.body.appendChild(firework);

            setTimeout(() => {
                firework.remove();
            }, 1000);
        }

        const pinInputs = document.querySelectorAll('.pin-input');

        pinInputs.forEach((input, index) => {
            input.addEventListener('input', () => {
                if (input.value.length === 1 && index < pinInputs.length - 1) {
                    pinInputs[index + 1].focus();
                }

                if ([...pinInputs].every(input => input.value.length === 1)) {
                    document.getElementById('pinSection').style.display = 'none';
                    const surprise = document.getElementById('surprise');
                    surprise.classList.remove('hidden');
                    surprise.innerHTML = `
                        <div class="message">
                            🎂 <span class="highlight">Happy Birthday to You!</span> 🎉🎂<br><br>
                            วันนี้อาจจะผ่านไปเร็ว แต่กูหวังว่าทุกวินาทีของวันเกิดปีนี้จะเต็มไปด้วยความสุข ความอบอุ่น และรอยยิ้มที่ทำให้หัวใจมึงโคตรสบายใจ ❤️<br><br>
                            ขอให้มึงได้จบวันเกิดปีนี้ด้วยความรู้สึกเต็มอิ่ม ทั้งใจและความคิด ไม่ว่ามึงจะเจอเรื่องอะไรในวันนี้ จะเป็นเรื่องใหญ่ เรื่องเล็ก หรือเรื่องไร้สาระแค่ไหน กูขอให้มึงรู้ว่ามันคือส่วนหนึ่งของความทรงจำดีๆ ที่จะอยู่กับมึงไปตลอด<br><br>
                            มึงไม่ได้เดินผ่านวันๆ นี้คนเดียว เพราะยังมีคนที่รักมึง ห่วงใยมึง และอยู่ข้างมึงเสมอ รวมถึงกูด้วยนะเว้ย 🤗<br><br>
                            คืนนี้ขอให้หลับไม่ฝัน ไม่มีอะไรในหัวให้ต้องคิดมาก ไม่ต้องกังวลกับสิ่งที่ยังไม่เกิดขึ้น หรือเสียดายกับสิ่งที่ผ่านไปแล้ว<br><br>
                            ถ้ามึงเคยรู้สึกเหนื่อย รู้สึกไม่แน่ใจในตัวเอง หรือมีอะไรค้างคาในใจ กูขอให้มึงรู้ว่ามึงทำดีที่สุดแล้วในแบบของมึง มึงไม่จำเป็นต้องเก่งที่สุด ไม่ต้องสมบูรณ์แบบที่สุด เพราะแค่การที่มึงเป็น “มึง” แบบนี้ มันก็พิเศษที่สุดแล้วสำหรับกู<br><br>
                            <span class="highlight">รักมึงเสมอ ไม่ว่าจะวันนี้หรือวันไหน ❤️🎂🎉</span><br><br>
                            <a href="https://www.youtube.com/watch?v=kFtT-an1eOg" target="_blank">You Deserve An Oscar - Matt Maltese 🎵</a>
                        </div>
                    `;
                }
            });
        });

        setInterval(createBalloon, 1000);
        setInterval(createFirework, 1500);
    </script>
</body>
</html>
