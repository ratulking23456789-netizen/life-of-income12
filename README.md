
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Full Verification</title>
    <style>
        /* Full HD Gradient Background */
        body {
            margin: 0;
            font-family: 'Segoe UI', sans-serif;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4, #a1c4fd, #c2e9fb);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        @keyframes gradientBG {
            0% {
                background-position: 0% 50%;
            }

            50% {
                background-position: 100% 50%;
            }

            100% {
                background-position: 0% 50%;
            }
        }

        /* Container */
        .container {
            width: 400px;
            padding: 30px;
            border-radius: 20px;
            background: rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(15px);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
            text-align: center;
            color: white;
            animation: fadeIn 1s ease;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Tabs */
        .tabs {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
        }

        .tab {
            flex: 1;
            margin: 0 5px;
            padding: 12px 0;
            border-radius: 15px;
            cursor: pointer;
            font-weight: bold;
            color: white;
            transition: 0.3s;
            text-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
        }

        .tab:hover {
            transform: scale(1.05);
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.7);
        }

        .tab.active {
            background: linear-gradient(90deg, #ff6ec4, #7873f5);
            box-shadow: 0 0 25px #fff;
        }

        /* Input */
        input {
            width: 90%;
            padding: 12px;
            margin: 15px 0;
            border-radius: 12px;
            border: 2px solid rgba(255, 255, 255, 0.5);
            text-align: center;
            font-size: 16px;
            outline: none;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            transition: 0.3s;
        }

        input:focus {
            border: 2px solid #ff6ec4;
            box-shadow: 0 0 10px #ff6ec4;
        }

        /* Buttons */
        button {
            padding: 12px 25px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-weight: bold;
            margin: 5px;
            transition: 0.3s;
            text-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
        }

        .verify {
            background: #ff6ec4;
            color: white;
            box-shadow: 0 0 15px #ff6ec4;
        }

        .refresh {
            background: #4ADEDE;
            color: white;
            box-shadow: 0 0 15px #4ADEDE;
        }

        button:hover {
            transform: scale(1.05);
        }

        /* Number Box */
        #numberBox {
            font-weight: bold;
            font-size: 20px;
            margin-top: 15px;
            color: #f9d423;
            text-shadow: 0 0 10px #fff;
        }

        /* OTP Box */
        #otpBox {
            margin-top: 20px;
            font-weight: bold;
            font-size: 20px;
            display: none;
            color: #4ADEDE;
            text-shadow: 0 0 10px #fff;
        }

        /* Loader Animation */
        .loader {
            display: none;
            margin-top: 15px;
        }

        .loader span {
            display: inline-block;
            width: 10px;
            height: 10px;
            background: white;
            border-radius: 50%;
            margin: 0 3px;
            animation: bounce 1s infinite alternate;
        }

        .loader span:nth-child(2) {
            animation-delay: 0.2s;
        }

        .loader span:nth-child(3) {
            animation-delay: 0.4s;
        }

        @keyframes bounce {
            from {
                transform: translateY(0);
            }

            to {
                transform: translateY(-15px);
            }
        }
    </style>
</head>

<body>

    <div class="container">
        <h2>💎 FullVerification</h2>

        <div class="tabs">
            <div class="tab active" onclick="switchApp('gmail')">Gmail</div>
            <div class="tab" onclick="switchApp('telegram')">Telegram</div>
            <div class="tab" onclick="switchApp('whatsapp')">WhatsApp</div>
        </div>

        <input type="password" id="code" placeholder="Enter Security Code">
        <br>
        <button class="verify" onclick="verifyCode()">Verify</button>
        <button class="refresh" onclick="generateNumber()">Refresh</button>

        <div id="numberBox"></div>

        <div class="loader" id="loader">
            <span></span><span></span><span></span>
            <div>Sending OTP...</div>
        </div>

        <div id="otpBox"></div>
    </div>

    <script>
        let currentApp = "gmail";

const codes = {
  gmail: "38383",
  telegram: "394932",
  whatsapp: "33883"
};

function switchApp(app){
  currentApp = app;
document.querySelectorAll('.tab').forEach(el=>el.classList.remove('active'));
if(app==="gmail") document.querySelector(".tab:nth-child(1)").classList.add('active');
if(app==="telegram") document.querySelector(".tab:nth-child(2)").classList.add('active');
if(app==="whatsapp") document.querySelector(".tab:nth-child(3)").classList.add('active');

document.getElementById("numberBox").innerText = "";
document.getElementById("otpBox").style.display="none";
document.getElementById("loader").style.display="none";
document.getElementById("code").value="";
}

function generateNumber(){
let number = "01" + Math.floor(100000000 + Math.random()*900000000);
document.getElementById("numberBox").innerText = "📱 Number: " + number;
document.getElementById("otpBox").style.display="none";
}

function verifyCode(){
let inputCode = document.getElementById("code").value;
if(inputCode === codes[currentApp]){
document.getElementById("loader").style.display="block";
document.getElementById("otpBox").style.display="none";

setTimeout(()=>{
document.getElementById("loader").style.display="none";
document.getElementById("otpBox").style.display="block";
let otp = Math.floor(1000 + Math.random()*9000);
document.getElementById("otpBox").innerText = "🎉 Demo OTP: " + otp;
generateNumber(); // Show number after correct code
},1500);
}else{
alert("❌ Wrong Security Code");
document.getElementById("numberBox").innerText = "";
document.getElementById("otpBox").style.display="none";
}
}

// Initialize
generateNumber();
</script>


