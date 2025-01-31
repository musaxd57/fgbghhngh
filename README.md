<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Telefon Doğrulama</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f3f4f6;
        }
        .container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        input {
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
            width: 100%;
        }
        button {
            background-color: #2563eb;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .hidden { display: none; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Telefon Doğrulama</h1>
        <div id="phoneStep">
            <label for="phone">Telefon Numarası</label>
            <input type="tel" id="phone" placeholder="Telefon Numarası (5551234567)" required>
            <button onclick="sendOtp()">Kodu Gönder</button>
        </div>
        <div id="otpStep" class="hidden">
            <label for="otp">Doğrulama Kodu</label>
            <input type="number" id="otp" placeholder="Doğrulama Kodu" required>
            <p>Yeniden kod gönder: <span id="countdown">30</span>s</p>
            <button onclick="verifyOtp()">Doğrula</button>
        </div>
    </div>

    <script>
        let countdown = 30;
        let timer;

        function sendOtp() {
            const phone = document.getElementById("phone").value;
            if (phone.length === 10) {
                document.getElementById("phoneStep").classList.add("hidden");
                document.getElementById("otpStep").classList.remove("hidden");
                document.getElementById("countdown").textContent = countdown;
                alert("Doğrulama kodu gönderildi!");
                startCountdown();
            } else {
                alert("Geçerli bir telefon numarası girin!");
            }
        }

        function startCountdown() {
            clearInterval(timer);
            countdown = 30;
            timer = setInterval(() => {
                countdown--;
                document.getElementById("countdown").textContent = countdown;
                if (countdown <= 0) {
                    clearInterval(timer);
                }
            }, 1000);
        }

        function verifyOtp() {
            const otp = document.getElementById("otp").value;
            if (otp.length === 6) {
                alert("Telefon doğrulandı!");
            } else {
                alert("Geçerli bir doğrulama kodu girin!");
            }
        }
    </script>
</body>
</html>
