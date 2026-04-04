<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>PICASSO FF PRO</title>

<style>
body {
  margin: 0;
  font-family: Arial;
  background: linear-gradient(180deg, #000000, #1a0000);
  color: white;
  text-align: center;
}

/* 😈 PROFILE */
.profile {
  margin-top: 20px;
}
.profile img {
  width: 120px;
  border-radius: 50%;
  border: 3px solid red;
  box-shadow: 0 0 20px red;
}

h2 {
  color: red;
  text-shadow: 0 0 10px red;
}

/* 🔐 LOGIN */
.container {
  margin-top: 30px;
}

input {
  padding: 12px;
  margin: 10px;
  border-radius: 10px;
  border: none;
  width: 220px;
  background: #111;
  color: white;
}

button {
  padding: 12px 25px;
  background: red;
  border: none;
  border-radius: 12px;
  color: white;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  background: darkred;
  transform: scale(1.1);
}

/* 🤖 PANEL */
.panel {
  display: none;
}

.box {
  background: #111;
  margin: 20px;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 0 15px red;
}
</style>
</head>

<body>

<!-- 😈 PROFILE -->
<div class="profile">
  <img src="https://i.imgur.com/6VBx3io.png">
  <h2>PICASSO FF PRO 😈</h2>
</div>

<!-- 🔐 LOGIN -->
<div class="container" id="loginBox">
  <h3>Login / Sign Up</h3>
  <input type="text" placeholder="Username"><br>
  <input type="password" placeholder="Password"><br>
  <button onclick="login()">Enter</button>
</div>

<!-- 🤖 PANEL -->
<div class="panel" id="panel">

  <!-- MENU -->
  <div class="box">
    <h3>Choose Bot</h3>
    <button onclick="show('dance')">💃 Dance Bot</button>
    <button onclick="show('like')">❤️ Like Bot</button>
    <button onclick="show('view')">👁 View Bot</button>
  </div>

  <!-- 💃 DANCE -->
  <div class="box" id="dance" style="display:none;">
    <h3>Dance Bot</h3>
    <input placeholder="Player ID"><br>
    <input placeholder="Team Code"><br>
    <button onclick="alert('💃 Dance Sent!')">Send</button>
  </div>

  <!-- ❤️ LIKE -->
  <div class="box" id="like" style="display:none;">
    <h3>Like Bot</h3>
    <input placeholder="Player ID"><br>
    <button onclick="alert('❤️ Likes Sent!')">Send</button>
  </div>

  <!-- 👁 VIEW -->
  <div class="box" id="view" style="display:none;">
    <h3>View Bot</h3>
    <input placeholder="Player ID"><br>
    <button onclick="alert('👁 Views Sent!')">Send</button>
  </div>

</div>

<script>
function login(){
  document.getElementById("loginBox").style.display = "none";
  document.getElementById("panel").style.display = "block";
}

function show(bot){
  document.getElementById("dance").style.display = "none";
  document.getElementById("like").style.display = "none";
  document.getElementById("view").style.display = "none";

  document.getElementById(bot).style.display = "block";
}
</script>

</body>
</html>
