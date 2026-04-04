<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بوت الرقصات واللايكات</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            padding: 40px;
            max-width: 500px;
            width: 100%;
            text-align: center;
        }

        h1 {
            color: #333;
            margin-bottom: 30px;
            font-size: 2.2em;
        }

        .login-form {
            margin-bottom: 30px;
        }

        .input-group {
            margin-bottom: 20px;
            text-align: right;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #555;
            font-weight: 500;
        }

        input {
            width: 100%;
            padding: 15px;
            border: 2px solid #e1e5e9;
            border-radius: 12px;
            font-size: 16px;
            transition: all 0.3s ease;
            text-align: right;
        }

        input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 10px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
        }

        .btn-success {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        }

        .btn-warning {
            background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
        }

        .dashboard {
            display: none;
        }

        .bot-section {
            margin-top: 30px;
            padding: 25px;
            background: #f8f9ff;
            border-radius: 15px;
            border: 2px solid #e3e8ff;
        }

        .bot-title {
            color: #333;
            margin-bottom: 20px;
            font-size: 1.4em;
        }

        .options {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .option-btn {
            padding: 15px 20px;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }

        .dance-btn { background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%); color: #333; }
        .like-btn { background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%); color: #333; }
        .scene-btn { background: linear-gradient(135deg, #d299c2 0%, #fef9d7 100%); color: #333; }

        .option-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
        }

        .form-hidden {
            display: none;
        }

        .active-form {
            margin-top: 20px;
            padding: 25px;
            background: white;
            border-radius: 15px;
            border: 2px solid #667eea;
        }

        .team-code-group {
            margin-top: 15px;
        }

        @media (max-width: 480px) {
            .container {
                padding: 25px 20px;
            }
            
            h1 {
                font-size: 1.8em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- شاشة تسجيل الدخول -->
        <div id="loginScreen">
            <h1>🎵 بوت الرقصات واللايكات 🎵</h1>
            <div class="login-form">
                <div class="input-group">
                    <label>اسم المستخدم</label>
                    <input type="text" id="username" placeholder="أدخل اسمك">
                </div>
                <div class="input-group">
                    <label>كلمة المرور</label>
                    <input type="password" id="password" placeholder="أدخل كلمة المرور">
                </div>
                <button class="btn" onclick="login()">دخول</button>
            </div>
        </div>

        <!-- لوحة التحكم -->
        <div id="dashboard" class="dashboard">
            <h1>مرحباً بك! 👋</h1>
            <p>اختر البوت الذي تريده:</p>
            
            <div class="bot-section">
                <div class="bot-title">🤖 بوت الرقصات</div>
                <div class="options">
                    <button class="option-btn dance-btn" onclick="showDanceForm()">تشغيل بوت الرقصات</button>
                </div>
            </div>

            <div class="bot-section">
                <div class="bot-title">❤️ بوت اللايكات</div>
                <div class="options">
                    <button class="option-btn like-btn" onclick="showLikeForm()">تشغيل بوت اللايكات</button>
                </div>
            </div>

            <div class="bot-section">
                <div class="bot-title">🎬 بوت المشاهدات</div>
                <div class="options">
                    <button class="option-btn scene-btn" onclick="showSceneForm()">تشغيل بوت المشاهدات</button>
                </div>
            </div>

            <!-- نموذج بوت الرقصات -->
            <div id="danceForm" class="form-hidden active-form">
                <h3>⚡ بوت الرقصات</h3>
                <div class="input-group">
                    <label>ID الفيديو</label>
                    <input type="text" id="danceId" placeholder="أدخل ID الفيديو">
                </div>
                <div class="team-code-group input-group">
                    <label>كود الفريق (اختياري)</label>
                    <input type="text" id="teamCode" placeholder="أدخل كود الفريق">
                </div>
                <button class="btn btn-success" onclick="startDanceBot()">بدء البوت</button>
                <button class="btn btn-secondary" onclick="hideForms()">رجوع</button>
            </div>

            <!-- نموذج بوت اللايكات -->
            <div id="likeForm" class="form-hidden">
                <h3>❤️ بوت اللايكات</h3>
                <div class="input-group">
                    <label>ID الفيديو</label>
                    <input type="text" id="likeId" placeholder="أدخل ID الفيديو">
                </div>
                <button class="btn btn-success" onclick="startLikeBot()">بدء البوت</button>
                <button class="btn btn-secondary" onclick="hideForms()">رجوع</button>
            </div>

            <!-- نموذج بوت المشاهدات -->
            <div id="sceneForm" class="form-hidden">
                <h3>🎬 بوت المشاهدات</h3>
                <div class="input-group">
                    <label>ID الفيديو</label>
                    <input type="text" id="sceneId" placeholder="أدخل ID الفيديو">
                </div>
                <button class="btn btn-success" onclick="startSceneBot()">بدء البوت</button>
                <button class="btn btn-secondary" onclick="hideForms()">رجوع</button>
            </div>
        </div>
    </div>

    <script>
        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            if (username && password) {
                document.getElementById('loginScreen').style.display = 'none';
                document.getElementById('dashboard').style.display = 'block';
            } else {
                alert('يرجى إدخال اسم المستخدم وكلمة المرور');
            }
        }

        function showDanceForm() {
            hideForms();
            document.getElementById('danceForm').style.display = 'block';
        }

        function showLikeForm() {
            hideForms();
            document.getElementById('likeForm').style.display = 'block';
        }

        function showSceneForm() {
            hideForms();
            document.getElementById('sceneForm').style.display = 'block';
        }

        function hideForms() {
            document.getElementById('danceForm').style.display = 'none';
            document.getElementById('likeForm').style.display = 'none';
            document.getElementById('sceneForm').style.display = 'none';
        }

        function startDanceBot() {
            const id = document.getElementById('danceId').value;
            const teamCode = document.getElementById('teamCode').value;
            
            if (!id) {
                alert('يرجى إدخال ID الفيديو');
                return;
            }
            
            alert(`🚀 تم تشغيل بوت الرقصات!\nID: ${id}\nكود الفريق: ${teamCode || 'غير محدد'}\n\nالبوت يعمل الآن...`);
            // هنا تضع رابط API الخاص بك
        }

        function startLikeBot() {
            const id = document.getElementById('likeId').value;
            
            if (!id) {
                alert('يرجى إدخال ID الفيديو');
                return;
            }
            
            alert(`❤️ تم تشغيل بوت اللايكات!\nID: ${id}\n\nالبوت يعمل الآن...`);
        }

        function startSceneBot() {
            const id = document.getElementById('sceneId').value;
            
            if (!id) {
                alert('يرجى إدخال ID الفيديو');
                return;
            }
            
            alert(`🎬 تم تشغيل بوت المشاهدات!\nID: ${id}\n\nالبوت يعمل الآن...`);
        }

        // السماح بالدخول بـ Enter
        document.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                if (document.getElementById('loginScreen').style.display !== 'none') {
                    login();
                }
            }
        });
    </script>
</body>
</html>
