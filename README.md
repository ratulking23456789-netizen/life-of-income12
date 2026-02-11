<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Secure Demo Verification</title>
<style>
body{
  font-family: 'Poppins', sans-serif;
  background: linear-gradient(135deg,#f093fb,#f5576c,#4facfe,#00f2fe);
  background-size: 400% 400%;
  animation: gradientBG 15s ease infinite;
  display:flex;
  justify-content:center;
  align-items:center;
  height:100vh;
  margin:0;
}
@keyframes gradientBG{
  0%{background-position:0% 50%}
  50%{background-position:100% 50%}
  100%{background-position:0% 50%}
}
.container{
  background: rgba(255,255,255,0.95);
  padding:30px;
  border-radius:20px;
  width:380px;
  text-align:center;
  box-shadow:0 15px 30px rgba(0,0,0,0.3);
}
h2{
  margin-bottom:15px;
  color:#333;
}
button{
  background: linear-gradient(90deg,#f093fb,#f5576c);
  color:white;
  border:none;
  padding:12px 25px;
  border-radius:12px;
  cursor:pointer;
  margin-top:10px;
  font-weight:bold;
  font-size:16px;
  transition: transform 0.2s;
}
button:hover{
  transform: scale(1.05);
}
input{
  width:90%;
  padding:10px;
  margin:10px 0;
  border-radius:10px;
  border:2px solid #f093fb;
  text-align:center;
  font-size:16px;
}
#otpBox{
  display:none;
  margin-top:20px;
}
#numberBox{
  margin-top:15px;
  font-weight:bold;
  font-size:18px;
  color:#f5576c;
}
.success{
  color:#4facfe;
  font-weight:bold;
  font-size:18px;
}
.tabs{
  display:flex;
  justify-content:space-around;
  margin-bottom:20px;
}
.tab{
  padding:10px 18px;
  border-radius:15px;
  cursor:pointer;
  font-weight:bold;
  background: linear-gradient(90deg,#43e97b,#38f9d7);
  color:white;
  transition: transform 0.2s;
}
.tab:hover{
  transform: scale(1.05);
}
.tab.active{
  background: linear-gradient(90deg,#f093fb,#f5576c);
}
</style>
</head>
<body>

<div class="container">
  <h2>🌟 Secure Demo App 🌟</h2>
  
  <div class="tabs">
    <div class="tab active" onclick="switchTab('gmail')">Gmail</div>
    <div class="tab" onclick="switchTab('telegram')">Telegram</div>
    <div class="tab" onclick="switchTab('whatsapp')">WhatsApp</div>
  </div>
  
  <button onclick="startApp()">Start</button>

  <div id="numberBox"></div>

  <div id="securityBox" style="display:none;">
    <input type="password" id="code" placeholder="Enter Security Code">
    <button onclick="checkCode()">Verify</button>
  </div>

  <div id="otpBox">
    <p class="success">🎉 New OTP Generated:</p>
    <h3 id="otp"></h3>
  </div>
</div>

<script>
let currentTab = 'gmail';

// ডেমো নাম্বার
const numbers = {
  gmail: "01935827159",
  telegram: "01876432519",
  whatsapp: "01723456890"
};

// ডেমো সিকিউরিটি কোড
const codes = {
  gmail: "58281",
  telegram: "82645",
  whatsapp: "37282"
};

// ডেমো OTP
const otps = {
  gmail: "373616",
  telegram: "3583",
  whatsapp: "123456"
};

function switchTab(tab){
  currentTab = tab;
  document.querySelectorAll('.tab').forEach(el=>el.classList.remove('active'));
  document.querySelector(.tab[onclick="switchTab('${tab}')"]).classList.add('active');
  document.getElementById("securityBox").style.display="none";
  document.getElementById("otpBox").style.display="none";
  document.getElementById("numberBox").innerText = "";
}

function startApp(){
  document.getElementById("securityBox").style.display="block";
  document.getElementById("otpBox").style.display="none";
  document.getElementById("numberBox").innerText = "📱 New Number: " + numbers[currentTab];
}

function checkCode(){
  let code = document.getElementById("code").value;
  if(code === codes[currentTab]){
    document.getElementById("otp").innerText = otps[currentTab];
    document.getElementById("otpBox").style.display="block";
  }else{
    alert("❌ Wrong Code!");
  }
}
</script>

</body>
</html>
