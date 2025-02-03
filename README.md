<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
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
            min-height: 100vh;
            text-align: center;
            flex-direction: column;
            animation: backgroundShift 10s infinite alternate;
        }

        @keyframes backgroundShift {
            0% { background: linear-gradient(135deg, #ff9a9e, #fad0c4); }
            100% { background: linear-gradient(135deg, #a18cd1, #fbc2eb); }
        }

        h1 {
            font-size: 2em;
            color: #ff69b4;
            margin: 10px 0;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-15px); }
        }

        p {
            font-size: 1em;
            color: #6a5acd;
        }

        .pin-container {
            display: flex;
            gap: 10px;
            justify-content: center;
        }

        .pin-input {
            width: 40px;
            height: 40px;
            font-size: 1.5em;
            text-align: center;
            border: 2px solid #6a5acd;
            border-radius: 10px;
            outline: none;
            transition: transform 0.3s ease;
        }

        .pin-input:focus {
            transform: scale(1.1);
        }

        .message {
            font-size: 1em;
            color: #333;
            padding: 10px;
            width: 90%;
            line-height: 1.5;
            text-align: center;
            animation: fadeIn 2s ease-in-out;
        }

        .hidden {
            display: none;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
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
                            🎂 Happy Birthday to You! 🎉🎂<br><br>
                            วันนี้อาจจะผ่านไปเร็ว แต่กูหวังว่าทุกวินาทีของวันเกิดปีนี้จะเต็มไปด้วยความสุข ความอบอุ่น และรอยยิ้มที่ทำให้หัวใจมึงโคตรสบายใจ ❤️<br><br>
                            ขอให้มึงได้จบวันเกิดปีนี้ด้วยความรู้สึกเต็มอิ่ม ทั้งใจและความคิด ไม่ว่ามึงจะเจอเรื่องอะไรในวันนี้ จะเป็นเรื่องใหญ่ เรื่องเล็ก หรือเรื่องไร้สาระแค่ไหน กูขอให้มึงรู้ว่ามันคือส่วนหนึ่งของความทรงจำดีๆ ที่จะอยู่กับมึงไปตลอด<br><br>
                            มึงไม่ได้เดินผ่านวันๆ นี้คนเดียว เพราะยังมีคนที่รักมึง ห่วงใยมึง และอยู่ข้างมึงเสมอ รวมถึงกูด้วยนะเว้ย 🤗<br><br>
                            คืนนี้ขอให้หลับไม่ฝัน ไม่มีอะไรในหัวให้ต้องคิดมาก ไม่ต้องกังวลกับสิ่งที่ยังไม่เกิดขึ้น หรือเสียดายกับสิ่งที่ผ่านไปแล้ว<br><br>
                            ถ้ามึงเคยรู้สึกเหนื่อย รู้สึกไม่แน่ใจในตัวเอง หรือมีอะไรค้างคาในใจ กูขอให้มึงรู้ว่ามึงทำดีที่สุดแล้วในแบบของมึง มึงไม่จำเป็นต้องเก่งที่สุด ไม่ต้องสมบูรณ์แบบที่สุด เพราะแค่การที่มึงเป็น “มึง” แบบนี้ มันก็พิเศษที่สุดแล้วสำหรับกู<br><br>
                            รักมึงเสมอ ไม่ว่าจะวันนี้หรือวันไหน ❤️🎂🎉<br><br>
                            <a href="https://www.youtube.com/watch?v=kFtT-an1eOg" target="_blank">You Deserve An Oscar - Matt Maltese 🎵</a>
                        </div>
                    `;
                }
            });
        });
    </script>
</body>
</html>
