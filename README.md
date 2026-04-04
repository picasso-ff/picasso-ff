<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Picasso FF Pro</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>
  /* Reset */
  * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Share Tech Mono', monospace; }

  body {
    background: #0f0f0f url('https://images.unsplash.com/photo-1531497865143-ec0f9a98c6a3?fit=crop&w=1400&q=80') no-repeat center center fixed;
    background-size: cover;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    color: #0f0;
  }

  /* شريط علوي */
  header {
    position: absolute;
    top: 0;
    width: 100%;
    padding: 15px 0;
    text-align: center;
    background: rgba(0,0,0,0.8);
    color: #0f0;
    font-size: 28px;
    font-weight: bold;
    letter-spacing: 2px;
    border-bottom: 2px solid #f00;
  }

  /* واجهة تسجيل الدخول */
  .login-container {
    background: rgba(0,0,0,0.85);
    padding: 40px 30px;
    border-radius: 12px;
    width: 100%;
    max-width: 400px;
    box-shadow: 0 0 20px #0f0;
    text-align: center;
  }

  .login-container h2 {
    margin-bottom: 30px;
    color: #0f0;
    text-shadow: 0 0 8px #0f0;
  }

  .input-group { margin-bottom: 20px; text-align: left; }
  .input-group label { display: block; margin-bottom: 5px; color: #0f0; text-shadow: 0 0 5px #0f0; }
  .input-group input {
    width: 100%;
    padding: 12px;
    border: 1px solid #0f0;
    border-radius: 8px;
    background: #000;
    color: #0f0;
    transition: 0.3s;
  }
  .input-group input:focus {
    border-color: #f00;
    box-shadow: 0 0 10px #f00;
    outline: none;
  }

  .btn {
    width: 100%;
    padding: 12px;
    border: none;
    border-radius: 8px;
    background: #f00;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
    transition: 0.3s;
    text-transform: uppercase;
    letter-spacing: 1px;
  }
  .btn:hover { background: #900; box-shadow: 0 0 10px #f00; }

  .footer {
    margin-top: 20px;
  }
  .footer a {
    color: #f00;
    text-decoration: none;
    font-weight: bold;
    text-shadow: 0 0 5px #f00;
  }

  @media (max-width: 480px) {
    header { font-size: 22px; }
    .login-container { padding: 30px 20px; }
  }
</style>
</head>
<body>

<header>Picasso FF Pro</header>

<div class="login-container">
  <h2>تسجيل الدخول</h2>
  <form>
    <div class="input-group">
      <label for="email">البريد الإلكتروني</label>
      <input type="email" id="email" placeholder="أدخل بريدك الإلكتروني" required>
    </div>
    <div class="input-group">
      <label for="password">كلمة المرور</label>
      <input type="password" id="password" placeholder="أدخل كلمة المرور" required>
    </div>
    <button type="submit" class="btn">دخول</button>
  </form>
  <div class="footer">
    <a href="#">إنشاء حساب</a>
  </div>
</div>

</body>
</html>
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Picasso FF Pro - المرحلة الاحترافية</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Share Tech Mono', monospace; }

  body {
    background: #0f0f0f;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    color: #0f0;
    flex-direction: column;
  }

  /* تأثير Matrix الخلفية */
  #matrix {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    pointer-events: none;
  }

  header {
    position: absolute;
    top: 0;
    width: 100%;
    padding: 15px 0;
    text-align: center;
    background: rgba(0,0,0,0.85);
    color: #0f0;
    font-size: 28px;
    font-weight: bold;
    letter-spacing: 2px;
    border-bottom: 2px solid #f00;
    z-index: 2;
  }

  .container {
    background: rgba(0,0,0,0.9);
    padding: 40px 30px;
    border-radius: 12px;
    width: 100%;
    max-width: 400px;
    box-shadow: 0 0 30px #0f0;
    text-align: center;
    z-index: 1;
    position: relative;
  }

  h2 { margin-bottom: 30px; color: #0f0; text-shadow: 0 0 12px #0f0; }

  .input-group { margin-bottom: 20px; text-align: left; }
  .input-group label { display: block; margin-bottom: 5px; color: #0f0; text-shadow: 0 0 5px #0f0; }
  .input-group input, .input-group select {
    width: 100%;
    padding: 12px;
    border: 1px solid #0f0;
    border-radius: 8px;
    background: #000;
    color: #0f0;
    transition: 0.3s;
  }
  .input-group input:focus, .input-group select:focus {
    border-color: #f00;
    box-shadow: 0 0 12px #f00;
    outline: none;
  }

  .input-group input.valid { border-color: #0ff; box-shadow: 0 0 12px #0ff; }

  .btn {
    width: 100%;
    padding: 12px;
    border: none;
    border-radius: 8px;
    background: #f00;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
    transition: 0.3s;
    text-transform: uppercase;
    letter-spacing: 1px;
  }
  .btn:hover { background: #900; box-shadow: 0 0 12px #f00; }

  .message {
    margin-top: 20px;
    font-size: 20px;
    font-weight: bold;
    text-shadow: 0 0 10px #0f0, 0 0 20px #0f0;
    animation: glow 1s infinite alternate;
    display: none;
  }

  @keyframes glow {
    0% { text-shadow: 0 0 5px #0f0, 0 0 10px #0f0; }
    50% { text-shadow: 0 0 10px #0f0, 0 0 20px #0f0; }
    100% { text-shadow: 0 0 15px #0f0, 0 0 30px #0f0; }
  }

  @media (max-width: 480px) {
    header { font-size: 22px; }
    .container { padding: 30px 20px; }
  }
</style>
</head>
<body>

<canvas id="matrix"></canvas>

<header>Picasso FF Pro</header>

<div class="container">
  <h2>المرحلة الاحترافية</h2>
  <form id="teamForm">
    <div class="input-group">
      <label for="userId">ID المستخدم</label>
      <input type="text" id="userId" placeholder="أدخل ID" required>
    </div>
    <div class="input-group">
      <label for="teamCode">Team Code</label>
      <select id="teamCode" required>
        <option value="">اختر الفريق</option>
        <option value="Alpha">Alpha</option>
        <option value="Bravo">Bravo</option>
        <option value="Charlie">Charlie</option>
        <option value="Delta">Delta</option>
        <option value="Echo">Echo</option>
        <option value="Foxtrot">Foxtrot</option>
        <option value="Golf">Golf</option>
        <option value="Hotel">Hotel</option>
        <option value="India">India</option>
        <option value="Juliet">Juliet</option>
      </select>
    </div>
    <button type="submit" class="btn">تأكيد</button>
  </form>
  <div class="message" id="successMessage">لقد تمت الرقصة 🎉</div>
</div>

<audio id="successSound" src="https://www.soundjay.com/buttons/sounds/button-3.mp3"></audio>

<script>
  // Matrix effect
  const canvas = document.getElementById('matrix');
  const ctx = canvas.getContext('2d');
  let width = canvas.width = window.innerWidth;
  let height = canvas.height = window.innerHeight;
  const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%^&*()*&^%";
  const fontSize = 16;
  const columns = Math.floor(width / fontSize);
  const drops = [];
  for (let x = 0; x < columns; x++) drops[x] = 1;
  function draw() {
    ctx.fillStyle = "rgba(0,0,0,0.05)";
    ctx.fillRect(0,0,width,height);
    ctx.fillStyle = "#0f0";
    ctx.font = fontSize + "px monospace";
    for (let i = 0; i < drops.length; i++) {
      const text = letters.charAt(Math.floor(Math.random()*letters.length));
      ctx.fillText(text, i*fontSize, drops[i]*fontSize);
      if(drops[i]*fontSize > height && Math.random() > 0.975) drops[i] = 0;
      drops[i]++;
    }
  }
  setInterval(draw, 50);
  window.addEventListener('resize', () => { width = canvas.width = window.innerWidth; height = canvas.height = window.innerHeight; });

  // Form logic
  const form = document.getElementById('teamForm');
  const message = document.getElementById('successMessage');
  const sound = document.getElementById('successSound');
  const userIdInput = document.getElementById('userId');

  // تحقق بصري عند الكتابة
  userIdInput.addEventListener('input', () => {
    if(userIdInput.value.trim() !== "") userIdInput.classList.add('valid');
    else userIdInput.classList.remove('valid');
  });

  form.addEventListener('submit', function(e) {
    e.preventDefault();
    const userId = document.getElementById('userId').value;
    const teamCode = document.getElementById('teamCode').value;
    if(userId && teamCode) {
      message.style.display = 'block';
      sound.play();
    }
  });
</script>

</body>
</html>
