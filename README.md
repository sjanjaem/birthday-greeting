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
            background: #f0f8ff;
            overflow: hidden;
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            flex-direction: column;
        }

        h1 {
            font-size: 3em;
            color: #ff69b4;
            margin: 10px 0;
        }

        p {
            font-size: 1.5em;
            color: #6a5acd;
        }

        .balloon {
            position: absolute;
            width: 60px;
            height: 80px;
            background: red;
            border-radius: 50% 50% 45% 45%;
            box-shadow: inset -4px -4px 10px rgba(0,0,0,0.2);
            animation: float 5s infinite ease-in-out;
        }

        @keyframes float {
            0% { transform: translateY(0); }
            50% { transform: translateY(-200px); }
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
        }

        .pin-input {
            width: 50px;
            height: 50px;
            font-size: 2em;
            text-align: center;
            border: 2px solid #6a5acd;
            border-radius: 10px;
            outline: none;
        }

        img {
            max-width: 200px;
            margin: 10px 0;
        }

        .message {
            font-size: 1em;
            color: #333;
            padding: 20px;
            max-width: 600px;
            line-height: 1.5;
            text-align: left;
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <h1>🎉 Happy Birthday! 🎂</h1>
    <p>Enter your 4-digit PIN to unlock the surprise!</p>
    <div class="pin-container">
        <input type="password" maxlength="1" class="pin-input" id="pin1">
        <input type="password" maxlength="1" class="pin-input" id="pin2">
        <input type="password" maxlength="1" class="pin-input" id="pin3">
        <input type="password" maxlength="1" class="pin-input" id="pin4">
    </div>
    <div id="dogImage" class="hidden">
        <img src="/mnt/data/image.png" alt="Surprise Dog">
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
                    document.getElementById('dogImage').classList.remove('hidden');
                    setTimeout(() => {
                        document.getElementById('dogImage').classList.add('hidden');
                        const surprise = document.getElementById('surprise');
                        surprise.classList.remove('hidden');
                        surprise.innerHTML = `
                            <img src="https://via.placeholder.com/200" alt="Birthday Surprise">
                            <p>🎊 Wishing you an amazing year ahead filled with love and joy! 🎊</p>
                            <div class="message">
                                ก่อนที่มึงจะหลับตาลงในคืนนี้ กูอยากบอกมึงอีกครั้งแบบจริงจังเลยว่า… สุขสันต์วันเกิดนะเพื่อนรัก วันนี้อาจจะผ่านไปเร็ว แต่กูหวังว่าทุกวินาทีของวันเกิดปีนี้จะเต็มไปด้วยความสุข ความอบอุ่น และรอยยิ้มที่ทำให้หัวใจมึงโคตรสบายใจ<br><br>
                                ขอให้มึงได้จบวันเกิดปีนี้ด้วยความรู้สึกเต็มอิ่ม ทั้งใจและความคิด ไม่ว่ามึงจะเจอเรื่องอะไรในวันนี้ จะเป็นเรื่องใหญ่ เรื่องเล็ก หรือเรื่องไร้สาระแค่ไหน กูขอให้มึงรู้ว่ามันคือส่วนหนึ่งของความทรงจำดีๆ ที่จะอยู่กับมึงไปตลอด กูหวังว่ามึงจะจำได้ว่า มึงไม่ได้เดินผ่านวันๆ นี้คนเดียว เพราะยังมีคนที่รักมึง ห่วงใยมึง และอยู่ข้างมึงเสมอ รวมถึงกูด้วยนะเว้ย<br><br>
                                ขอให้คืนนี้มึงฝันดีที่สุดเท่าที่เคยฝันมา ฝันเห็นแต่สิ่งที่ทำให้มึงตื่นขึ้นมายิ้มได้โดยไม่ต้องพยายาม ขอให้มึงตื่นขึ้นมาในวันใหม่ด้วยความรู้สึกสดชื่น พร้อมเจอเรื่องดีๆ อีกมากมายที่กำลังรอมึงอยู่<br><br>
                                รักมึงเสมอ ไม่ว่าจะวันนี้หรือวันไหน ❤️
                            </div>
                        `;
                    }, 2000);
                }
            });
        });

        setInterval(createBalloon, 1000);
        setInterval(createFirework, 1500);
    </script>
</body>
</html>
