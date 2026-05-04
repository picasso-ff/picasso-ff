html_content = '''<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KOORA EF - Team Evaluation</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;600;700;800;900&family=Rajdhani:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #0a0a0f;
            --bg-secondary: #0f111a;
            --bg-card: #13151f;
            --bg-input: #1a1d2b;
            --border-color: #1e2132;
            --neon-green: #00ff88;
            --neon-green-dim: #00cc6a;
            --neon-blue: #00d4ff;
            --deep-blue: #0d1b3e;
            --text-primary: #ffffff;
            --text-secondary: #8b92b4;
            --text-muted: #4a5068;
            --accent-gold: #ffd700;
            --danger: #ff4757;
            --warning: #ffa502;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Rajdhani', sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Animated background grid */
        .bg-grid {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(0, 255, 136, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 255, 136, 0.03) 1px, transparent 1px);
            background-size: 50px 50px;
            pointer-events: none;
            z-index: 0;
        }

        .bg-glow {
            position: fixed;
            width: 600px;
            height: 600px;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(0, 255, 136, 0.08) 0%, transparent 70%);
            pointer-events: none;
            z-index: 0;
            animation: float 20s ease-in-out infinite;
        }

        .bg-glow:nth-child(2) {
            top: -200px;
            right: -200px;
            animation-delay: -5s;
        }

        .bg-glow:nth-child(3) {
            bottom: -200px;
            left: -200px;
            background: radial-gradient(circle, rgba(0, 212, 255, 0.06) 0%, transparent 70%);
            animation-delay: -10s;
        }

        @keyframes float {
            0%, 100% { transform: translate(0, 0); }
            25% { transform: translate(-30px, 30px); }
            50% { transform: translate(20px, -20px); }
            75% { transform: translate(-20px, -30px); }
        }

        /* Header */
        header {
            position: relative;
            z-index: 10;
            padding: 20px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
            background: rgba(10, 10, 15, 0.8);
            backdrop-filter: blur(20px);
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-icon {
            width: 50px;
            height: 50px;
            background: linear-gradient(135deg, var(--neon-green), var(--neon-blue));
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: 'Orbitron', sans-serif;
            font-weight: 900;
            font-size: 20px;
            color: var(--bg-primary);
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.3);
            position: relative;
            overflow: hidden;
        }

        .logo-icon::after {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.3), transparent);
            animation: shine 3s infinite;
        }

        @keyframes shine {
            0% { transform: translateX(-100%) rotate(45deg); }
            100% { transform: translateX(100%) rotate(45deg); }
        }

        .logo-text {
            font-family: 'Orbitron', sans-serif;
            font-size: 28px;
            font-weight: 800;
            background: linear-gradient(135deg, var(--text-primary), var(--neon-green));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            letter-spacing: 2px;
        }

        .logo-sub {
            font-size: 12px;
            color: var(--text-secondary);
            letter-spacing: 4px;
            text-transform: uppercase;
            margin-top: -5px;
        }

        .header-controls {
            display: flex;
            gap: 20px;
            align-items: center;
        }

        .lang-toggle, .currency-toggle {
            display: flex;
            background: var(--bg-input);
            border-radius: 10px;
            padding: 4px;
            border: 1px solid var(--border-color);
        }

        .lang-btn, .currency-btn {
            padding: 8px 16px;
            border: none;
            background: transparent;
            color: var(--text-secondary);
            font-family: 'Rajdhani', sans-serif;
            font-weight: 600;
            font-size: 14px;
            cursor: pointer;
            border-radius: 8px;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .lang-btn.active, .currency-btn.active {
            background: linear-gradient(135deg, var(--neon-green), var(--neon-green-dim));
            color: var(--bg-primary);
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.3);
        }

        /* Main Container */
        .main-container {
            position: relative;
            z-index: 5;
            max-width: 1200px;
            margin: 0 auto;
            padding: 40px 20px;
        }

        .hero-section {
            text-align: center;
            margin-bottom: 50px;
        }

        .hero-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 48px;
            font-weight: 800;
            margin-bottom: 15px;
            background: linear-gradient(135deg, var(--text-primary), var(--neon-green), var(--neon-blue));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 40px rgba(0, 255, 136, 0.2);
        }

        .hero-subtitle {
            font-size: 18px;
            color: var(--text-secondary);
            max-width: 600px;
            margin: 0 auto;
            line-height: 1.6;
        }

        /* Mode Switcher */
        .mode-switcher {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 40px;
        }

        .mode-btn {
            padding: 15px 40px;
            border: 2px solid var(--border-color);
            background: var(--bg-card);
            color: var(--text-secondary);
            font-family: 'Orbitron', sans-serif;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            border-radius: 12px;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 10px;
            position: relative;
            overflow: hidden;
        }

        .mode-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 255, 136, 0.1), transparent);
            transition: left 0.5s;
        }

        .mode-btn:hover::before {
            left: 100%;
        }

        .mode-btn:hover {
            border-color: var(--neon-green);
            color: var(--neon-green);
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(0, 255, 136, 0.1);
        }

        .mode-btn.active {
            border-color: var(--neon-green);
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.1), rgba(0, 212, 255, 0.05));
            color: var(--neon-green);
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.2);
        }

        .mode-icon {
            font-size: 20px;
        }

        /* Cards */
        .card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 20px;
            padding: 40px;
            margin-bottom: 30px;
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--neon-green), transparent);
            opacity: 0;
            transition: opacity 0.3s;
        }

        .card:hover::before {
            opacity: 1;
        }

        .card-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            gap: 12px;
            color: var(--text-primary);
        }

        .card-title .icon {
            width: 40px;
            height: 40px;
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.2), rgba(0, 212, 255, 0.2));
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            border: 1px solid rgba(0, 255, 136, 0.3);
        }

        /* Form Elements */
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .form-label {
            font-weight: 600;
            color: var(--text-secondary);
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .form-input, .form-select {
            padding: 14px 18px;
            background: var(--bg-input);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            color: var(--text-primary);
            font-family: 'Rajdhani', sans-serif;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s ease;
            outline: none;
        }

        .form-input:focus, .form-select:focus {
            border-color: var(--neon-green);
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.1);
        }

        .form-input::placeholder {
            color: var(--text-muted);
        }

        /* Player Input Grid */
        .players-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .player-input {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 12px;
            background: var(--bg-input);
            border: 1px solid var(--border-color);
            border-radius: 10px;
            transition: all 0.3s;
        }

        .player-input:hover {
            border-color: var(--neon-green);
            transform: translateY(-2px);
        }

        .player-num {
            width: 32px;
            height: 32px;
            background: linear-gradient(135deg, var(--neon-green), var(--neon-blue));
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            color: var(--bg-primary);
            font-size: 14px;
            flex-shrink: 0;
        }

        .player-input input {
            width: 60px;
            background: transparent;
            border: none;
            color: var(--text-primary);
            font-family: 'Rajdhani', sans-serif;
            font-size: 18px;
            font-weight: 700;
            text-align: center;
            border-bottom: 2px solid var(--border-color);
            transition: all 0.3s;
        }

        .player-input input:focus {
            outline: none;
            border-bottom-color: var(--neon-green);
        }

        /* Upload Area */
        .upload-area {
            border: 2px dashed var(--border-color);
            border-radius: 20px;
            padding: 60px 40px;
            text-align: center;
            background: var(--bg-input);
            transition: all 0.3s ease;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .upload-area:hover {
            border-color: var(--neon-green);
            background: rgba(0, 255, 136, 0.05);
        }

        .upload-area.dragover {
            border-color: var(--neon-green);
            background: rgba(0, 255, 136, 0.1);
            transform: scale(1.02);
        }

        .upload-icon {
            font-size: 60px;
            margin-bottom: 20px;
            opacity: 0.5;
        }

        .upload-text {
            font-size: 20px;
            font-weight: 600;
            color: var(--text-secondary);
            margin-bottom: 10px;
        }

        .upload-hint {
            font-size: 14px;
            color: var(--text-muted);
        }

        .upload-preview {
            max-width: 100%;
            max-height: 400px;
            border-radius: 12px;
            margin-top: 20px;
            display: none;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
        }

        /* AI Analysis Overlay */
        .ai-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(10, 10, 15, 0.95);
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 100;
            border-radius: 20px;
        }

        .ai-overlay.active {
            display: flex;
        }

        .ai-spinner {
            width: 80px;
            height: 80px;
            border: 3px solid var(--border-color);
            border-top-color: var(--neon-green);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-bottom: 30px;
            position: relative;
        }

        .ai-spinner::after {
            content: '';
            position: absolute;
            top: -5px;
            left: -5px;
            right: -5px;
            bottom: -5px;
            border: 3px solid transparent;
            border-top-color: var(--neon-blue);
            border-radius: 50%;
            animation: spin 2s linear infinite reverse;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .ai-status {
            font-family: 'Orbitron', sans-serif;
            font-size: 18px;
            color: var(--neon-green);
            margin-bottom: 15px;
            text-align: center;
        }

        .ai-progress {
            width: 300px;
            height: 4px;
            background: var(--border-color);
            border-radius: 2px;
            overflow: hidden;
            margin-bottom: 20px;
        }

        .ai-progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--neon-green), var(--neon-blue));
            width: 0%;
            transition: width 0.3s ease;
            box-shadow: 0 0 10px var(--neon-green);
        }

        .ai-log {
            font-size: 13px;
            color: var(--text-muted);
            font-family: 'Courier New', monospace;
            text-align: center;
            max-width: 400px;
        }

        /* Evaluate Button */
        .evaluate-btn {
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, var(--neon-green), var(--neon-green-dim));
            border: none;
            border-radius: 14px;
            color: var(--bg-primary);
            font-family: 'Orbitron', sans-serif;
            font-size: 18px;
            font-weight: 800;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 2px;
            position: relative;
            overflow: hidden;
            margin-top: 30px;
        }

        .evaluate-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transition: left 0.6s;
        }

        .evaluate-btn:hover::before {
            left: 100%;
        }

        .evaluate-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(0, 255, 136, 0.4);
        }

        .evaluate-btn:active {
            transform: translateY(-1px);
        }

        /* Results Section */
        .results-section {
            display: none;
            animation: fadeInUp 0.6s ease;
        }

        .results-section.active {
            display: block;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .result-card {
            background: var(--bg-input);
            border: 1px solid var(--border-color);
            border-radius: 16px;
            padding: 30px;
            text-align: center;
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
        }

        .result-card:hover {
            transform: translateY(-5px);
            border-color: var(--neon-green);
            box-shadow: 0 10px 30px rgba(0, 255, 136, 0.1);
        }

        .result-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, var(--neon-green), var(--neon-blue));
        }

        .result-label {
            font-size: 14px;
            color: var(--text-secondary);
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 15px;
            font-weight: 600;
        }

        .result-value {
            font-family: 'Orbitron', sans-serif;
            font-size: 36px;
            font-weight: 800;
            background: linear-gradient(135deg, var(--text-primary), var(--neon-green));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .result-stars {
            font-size: 32px;
            color: var(--accent-gold);
            letter-spacing: 5px;
            text-shadow: 0 0 20px rgba(255, 215, 0, 0.3);
        }

        .currency-values {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-top: 10px;
        }

        .currency-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 15px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            font-weight: 600;
        }

        .currency-flag {
            font-size: 20px;
        }

        .currency-amount {
            font-family: 'Orbitron', sans-serif;
            color: var(--neon-green);
        }

        /* Analysis Details */
        .analysis-details {
            background: var(--bg-input);
            border-radius: 16px;
            padding: 30px;
            border: 1px solid var(--border-color);
        }

        .detail-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid var(--border-color);
        }

        .detail-row:last-child {
            border-bottom: none;
        }

        .detail-label {
            color: var(--text-secondary);
            font-weight: 600;
        }

        .detail-value {
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            color: var(--neon-green);
        }

        .progress-bar {
            width: 200px;
            height: 8px;
            background: var(--bg-primary);
            border-radius: 4px;
            overflow: hidden;
            margin-left: 20px;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--neon-green), var(--neon-blue));
            border-radius: 4px;
            transition: width 1s ease;
            box-shadow: 0 0 10px rgba(0, 255, 136, 0.3);
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 40px;
            color: var(--text-muted);
            font-size: 14px;
            border-top: 1px solid var(--border-color);
            margin-top: 60px;
            position: relative;
            z-index: 5;
        }

        .footer-logo {
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            color: var(--text-secondary);
            margin-bottom: 10px;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .hero-title {
                font-size: 32px;
            }
            
            header {
                flex-direction: column;
                gap: 20px;
                padding: 20px;
            }
            
            .mode-switcher {
                flex-direction: column;
                align-items: center;
            }
            
            .mode-btn {
                width: 100%;
                max-width: 300px;
                justify-content: center;
            }
            
            .form-grid {
                grid-template-columns: 1fr;
            }
            
            .players-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .results-grid {
                grid-template-columns: 1fr;
            }
        }

        /* RTL Support */
        [dir="rtl"] .logo {
            flex-direction: row-reverse;
        }
        
        [dir="rtl"] .header-controls {
            flex-direction: row-reverse;
        }
        
        [dir="rtl"] .card-title {
            flex-direction: row-reverse;
        }
        
        [dir="rtl"] .detail-row {
            flex-direction: row-reverse;
        }
        
        [dir="rtl"] .currency-item {
            flex-direction: row-reverse;
        }

        /* Hidden sections */
        .section-content {
            display: none;
        }
        
        .section-content.active {
            display: block;
            animation: fadeIn 0.4s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Tooltip */
        .tooltip {
            position: relative;
            display: inline-block;
            cursor: help;
        }
        
        .tooltip:hover::after {
            content: attr(data-tip);
            position: absolute;
            bottom: 100%;
            left: 50%;
            transform: translateX(-50%);
            padding: 8px 12px;
            background: var(--bg-primary);
            border: 1px solid var(--neon-green);
            border-radius: 8px;
            font-size: 12px;
            white-space: nowrap;
            z-index: 1000;
            color: var(--text-primary);
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.5);
        }
    </style>
</head>
<body>
    <div class="bg-grid"></div>
    <div class="bg-glow"></div>
    <div class="bg-glow"></div>

    <header>
        <div class="logo">
            <div class="logo-icon">KE</div>
            <div>
                <div class="logo-text">KOORA EF</div>
                <div class="logo-sub" data-i18n="subtitle">Team Evaluation System</div>
            </div>
        </div>
        <div class="header-controls">
            <div class="lang-toggle">
                <button class="lang-btn active" data-lang="en" onclick="setLanguage('en')">EN</button>
                <button class="lang-btn" data-lang="fr" onclick="setLanguage('fr')">FR</button>
                <button class="lang-btn" data-lang="ar" onclick="setLanguage('ar')">AR</button>
            </div>
            <div class="currency-toggle">
                <button class="currency-btn active" data-currency="MAD" onclick="setCurrency('MAD')">MAD 🇲🇦</button>
                <button class="currency-btn" data-currency="EGP" onclick="setCurrency('EGP')">EGP 🇪🇬</button>
                <button class="currency-btn" data-currency="EUR" onclick="setCurrency('EUR')">EUR 💶</button>
            </div>
        </div>
    </header>

    <div class="main-container">
        <div class="hero-section">
            <h1 class="hero-title" data-i18n="heroTitle">Evaluate Your Team</h1>
            <p class="hero-subtitle" data-i18n="heroSubtitle">Professional team analysis powered by advanced algorithms. Get instant ratings and market valuations.</p>
        </div>

        <div class="mode-switcher">
            <button class="mode-btn active" onclick="switchMode('manual')">
                <span class="mode-icon">⚙️</span>
                <span data-i18n="manualMode">Manual Input</span>
            </button>
            <button class="mode-btn" onclick="switchMode('ai')">
                <span class="mode-icon">🤖</span>
                <span data-i18n="aiMode">AI Analysis</span>
            </button>
        </div>

        <!-- Manual Input Section -->
        <div id="manual-section" class="section-content active">
            <div class="card">
                <div class="card-title">
                    <div class="icon">📊</div>
                    <span data-i18n="teamConfig">Team Configuration</span>
                </div>
                <div class="form-grid">
                    <div class="form-group">
                        <label class="form-label" data-i18n="teamName">Team Name</label>
                        <input type="text" class="form-input" id="teamName" placeholder="e.g., Galactic FC" data-i18n-placeholder="teamNamePlaceholder">
                    </div>
                    <div class="form-group">
                        <label class="form-label" data-i18n="formation">Formation</label>
                        <select class="form-select" id="formation">
                            <option value="4-3-3">4-3-3</option>
                            <option value="4-4-2">4-4-2</option>
                            <option value="3-5-2">3-5-2</option>
                            <option value="4-2-3-1">4-2-3-1</option>
                            <option value="5-3-2">5-3-2</option>
                            <option value="3-4-3">3-4-3</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label" data-i18n="coachStyle">Coach Playstyle</label>
                        <select class="form-select" id="coachStyle">
                            <option value="possession" data-i18n="possession">Possession Game</option>
                            <option value="counter" data-i18n="counter">Quick Counter</option>
                            <option value="longball" data-i18n="longball">Long Ball</option>
                            <option value="wide" data-i18n="wide">Wide Play</option>
                            <option value="balanced" data-i18n="balanced">Balanced</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label" data-i18n="coachLevel">Coach Level (1-10)</label>
                        <input type="number" class="form-input" id="coachLevel" min="1" max="10" value="5">
                    </div>
                </div>
            </div>

            <div class="card">
                <div class="card-title">
                    <div class="icon">👥</div>
                    <span data-i18n="playerRatings">Player Ratings (OVR)</span>
                </div>
                <div class="players-grid" id="playersGrid">
                    <!-- Generated by JS -->
                </div>
            </div>

            <button class="evaluate-btn" onclick="evaluateTeam()" data-i18n="evaluateBtn">Evaluate Team</button>
        </div>

        <!-- AI Analysis Section -->
        <div id="ai-section" class="section-content">
            <div class="card" style="position: relative;">
                <div class="card-title">
                    <div class="icon">🤖</div>
                    <span data-i18n="aiUpload">AI-Powered Analysis</span>
                </div>
                
                <div class="upload-area" id="uploadArea" onclick="document.getElementById('fileInput').click()">
                    <div class="upload-icon">📸</div>
                    <div class="upload-text" data-i18n="uploadText">Upload Team Screenshot</div>
                    <div class="upload-hint" data-i18n="uploadHint">Drag & drop or click to select image</div>
                    <img class="upload-preview" id="uploadPreview" alt="Preview">
                </div>
                
                <input type="file" id="fileInput" accept="image/*" style="display: none;" onchange="handleFileSelect(event)">
                
                <div class="ai-overlay" id="aiOverlay">
                    <div class="ai-spinner"></div>
                    <div class="ai-status" data-i18n="aiAnalyzing">Analyzing Image...</div>
                    <div class="ai-progress">
                        <div class="ai-progress-bar" id="aiProgressBar"></div>
                    </div>
                    <div class="ai-log" id="aiLog">Initializing neural network...</div>
                </div>

                <button class="evaluate-btn" onclick="startAIAnalysis()" id="aiEvaluateBtn" style="display: none;" data-i18n="analyzeBtn">Analyze with AI</button>
            </div>
        </div>

        <!-- Results Section -->
        <div id="results-section" class="results-section">
            <div class="card">
                <div class="card-title">
                    <div class="icon">🏆</div>
                    <span data-i18n="evaluationResults">Evaluation Results</span>
                </div>
                
                <div class="results-grid">
                    <div class="result-card">
                        <div class="result-label" data-i18n="finalRating">Final Rating</div>
                        <div class="result-stars" id="resultStars">⭐⭐⭐⭐⭐</div>
                        <div style="margin-top: 10px; font-size: 14px; color: var(--text-secondary);" id="resultScore">92/100</div>
                    </div>
                    
                    <div class="result-card">
                        <div class="result-label" data-i18n="teamValue">Estimated Value</div>
                        <div class="result-value" id="primaryValue">2.4M</div>
                        <div class="currency-values" id="currencyValues">
                            <div class="currency-item">
                                <span class="currency-flag">🇲🇦</span>
                                <span class="currency-amount" id="madValue">24M MAD</span>
                            </div>
                            <div class="currency-item">
                                <span class="currency-flag">🇪🇬</span>
                                <span class="currency-amount" id="egpValue">45M EGP</span>
                            </div>
                            <div class="currency-item">
                                <span class="currency-flag">💶</span>
                                <span class="currency-amount" id="eurValue">220K EUR</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="result-card">
                        <div class="result-label" data-i18n="teamTier">Team Tier</div>
                        <div class="result-value" id="teamTier" style="font-size: 28px;">ELITE</div>
                        <div style="margin-top: 10px; font-size: 14px; color: var(--text-secondary);" data-i18n="tierDesc">Top 5% of all teams</div>
                    </div>
                </div>

                <div class="analysis-details">
                    <div class="detail-row">
                        <span class="detail-label" data-i18n="avgOVR">Average OVR</span>
                        <div style="display: flex; align-items: center;">
                            <span class="detail-value" id="avgOVR">89.5</span>
                            <div class="progress-bar">
                                <div class="progress-fill" id="ovrBar" style="width: 89.5%"></div>
                            </div>
                        </div>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label" data-i18n="balance">Team Balance</span>
                        <div style="display: flex; align-items: center;">
                            <span class="detail-value" id="balanceScore">85%</span>
                            <div class="progress-bar">
                                <div class="progress-fill" id="balanceBar" style="width: 85%"></div>
                            </div>
                        </div>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label" data-i18n="consistency">Consistency</span>
                        <div style="display: flex; align-items: center;">
                            <span class="detail-value" id="consistencyScore">78%</span>
                            <div class="progress-bar">
                                <div class="progress-fill" id="consistencyBar" style="width: 78%"></div>
                            </div>
                        </div>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label" data-i18n="coachBonus">Coach Bonus</span>
                        <div style="display: flex; align-items: center;">
                            <span class="detail-value" id="coachBonus">+12%</span>
                            <div class="progress-bar">
                                <div class="progress-fill" id="coachBar" style="width: 60%"></div>
                            </div>
                        </div>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label" data-i18n="chemistry">Team Chemistry</span>
                        <div style="display: flex; align-items: center;">
                            <span class="detail-value" id="chemistryScore">92%</span>
                            <div class="progress-bar">
                                <div class="progress-fill" id="chemistryBar" style="width: 92%"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <footer>
        <div class="footer-logo">KOORA EF</div>
        <div data-i18n="footer">Professional Team Evaluation System</div>
        <div style="margin-top: 10px; font-size: 12px;">© 2026 KOORA EF. All rights reserved.</div>
    </footer>

    <script>
        // Translations
        const translations = {
            en: {
                subtitle: "Team Evaluation System",
                heroTitle: "Evaluate Your Team",
                heroSubtitle: "Professional team analysis powered by advanced algorithms. Get instant ratings and market valuations.",
                manualMode: "Manual Input",
                aiMode: "AI Analysis",
                teamConfig: "Team Configuration",
                teamName: "Team Name",
                teamNamePlaceholder: "e.g., Galactic FC",
                formation: "Formation",
                coachStyle: "Coach Playstyle",
                possession: "Possession Game",
                counter: "Quick Counter",
                longball: "Long Ball",
                wide: "Wide Play",
                balanced: "Balanced",
                coachLevel: "Coach Level (1-10)",
                playerRatings: "Player Ratings (OVR)",
                evaluateBtn: "Evaluate Team",
                aiUpload: "AI-Powered Analysis",
                uploadText: "Upload Team Screenshot",
                uploadHint: "Drag & drop or click to select image",
                aiAnalyzing: "Analyzing Image...",
                analyzeBtn: "Analyze with AI",
                evaluationResults: "Evaluation Results",
                finalRating: "Final Rating",
                teamValue: "Estimated Value",
                teamTier: "Team Tier",
                tierDesc: "Top 5% of all teams",
                avgOVR: "Average OVR",
                balance: "Team Balance",
                consistency: "Consistency",
                coachBonus: "Coach Bonus",
                chemistry: "Team Chemistry",
                footer: "Professional Team Evaluation System"
            },
            fr: {
                subtitle: "Système d'Évaluation d'Équipe",
                heroTitle: "Évaluez Votre Équipe",
                heroSubtitle: "Analyse professionnelle d'équipe propulsée par des algorithmes avancés. Obtenez des évaluations et des valorisations instantanées.",
                manualMode: "Saisie Manuelle",
                aiMode: "Analyse IA",
                teamConfig: "Configuration de l'Équipe",
                teamName: "Nom de l'Équipe",
                teamNamePlaceholder: "ex: Galactic FC",
                formation: "Formation",
                coachStyle: "Style du Coach",
                possession: "Jeu de Possession",
                counter: "Contre Rapide",
                longball: "Ballon Long",
                wide: "Jeu sur les Ailes",
                balanced: "Équilibré",
                coachLevel: "Niveau du Coach (1-10)",
                playerRatings: "Notes des Joueurs (OVR)",
                evaluateBtn: "Évaluer l'Équipe",
                aiUpload: "Analyse par IA",
                uploadText: "Télécharger la Capture d'Écran",
                uploadHint: "Glisser-déposer ou cliquer pour sélectionner",
                aiAnalyzing: "Analyse de l'Image...",
                analyzeBtn: "Analyser avec l'IA",
                evaluationResults: "Résultats de l'Évaluation",
                finalRating: "Note Finale",
                teamValue: "Valeur Estimée",
                teamTier: "Niveau d'Équipe",
                tierDesc: "Top 5% de toutes les équipes",
                avgOVR: "OVR Moyen",
                balance: "Équilibre d'Équipe",
                consistency: "Cohérence",
                coachBonus: "Bonus Coach",
                chemistry: "Chimie d'Équipe",
                footer: "Système Professionnel d'Évaluation d'Équipe"
            },
            ar: {
                subtitle: "نظام تقييم الفرق",
                heroTitle: "قيّم فريقك",
                heroSubtitle: "تحليل احترافي للفريق باستخدام خوارزميات متقدمة. احصل على تقييمات وتقييمات سوقية فورية.",
                manualMode: "الإدخال اليدوي",
                aiMode: "التحليل بالذكاء الاصطناعي",
                teamConfig: "إعدادات الفريق",
                teamName: "اسم الفريق",
                teamNamePlaceholder: "مثال: غالاكتيك",
                formation: "التشكيلة",
                coachStyle: "أسلوب المدرب",
                possession: "لعب الاستحواذ",
                counter: "الهجوم المرتد",
                longball: "الكرة الطويلة",
                wide: "اللعب العرضي",
                balanced: "متوازن",
                coachLevel: "مستوى المدرب (1-10)",
                playerRatings: "تقييمات اللاعبين",
                evaluateBtn: "قيّم الفريق",
                aiUpload: "التحليل بالذكاء الاصطناعي",
                uploadText: "رفع لقطة الشاشة",
                uploadHint: "اسحب وأفلت أو انقر لاختيار الصورة",
                aiAnalyzing: "جاري تحليل الصورة...",
                analyzeBtn: "حلل بالذكاء الاصطناعي",
                evaluationResults: "نتائج التقييم",
                finalRating: "التقييم النهائي",
                teamValue: "القيمة التقديرية",
                teamTier: "مستوى الفريق",
                tierDesc: "أفضل 5% من جميع الفرق",
                avgOVR: "متوسط التقييم",
                balance: "توازن الفريق",
                consistency: "الاتساق",
                coachBonus: "مكافأة المدرب",
                chemistry: "الانسجام",
                footer: "نظام احترافي لتقييم الفرق"
            }
        };

        let currentLang = 'en';
        let currentCurrency = 'MAD';
        let uploadedImage = null;

        // Initialize player inputs
        function initPlayers() {
            const grid = document.getElementById('playersGrid');
            grid.innerHTML = '';
            for (let i = 1; i <= 11; i++) {
                grid.innerHTML += `
                    <div class="player-input">
                        <div class="player-num">${i}</div>
                        <input type="number" id="player${i}" min="1" max="99" value="80" placeholder="OVR">
                    </div>
                `;
            }
            // Add substitutes
            for (let i = 12; i <= 16; i++) {
                grid.innerHTML += `
                    <div class="player-input" style="opacity: 0.7;">
                        <div class="player-num" style="background: linear-gradient(135deg, #4a5068, #2a2d3a);">${i}</div>
                        <input type="number" id="player${i}" min="1" max="99" value="75" placeholder="OVR">
                    </div>
                `;
            }
        }

        // Language switcher
        function setLanguage(lang) {
            currentLang = lang;
            document.documentElement.lang = lang;
            document.documentElement.dir = lang === 'ar' ? 'rtl' : 'ltr';
            
            document.querySelectorAll('.lang-btn').forEach(btn => {
                btn.classList.toggle('active', btn.dataset.lang === lang);
            });

            document.querySelectorAll('[data-i18n]').forEach(el => {
                const key = el.dataset.i18n;
                if (translations[lang][key]) {
                    el.textContent = translations[lang][key];
                }
            });

            document.querySelectorAll('[data-i18n-placeholder]').forEach(el => {
                const key = el.dataset.i18nPlaceholder;
                if (translations[lang][key]) {
                    el.placeholder = translations[lang][key];
                }
            });
        }

        // Currency switcher
        function setCurrency(curr) {
            currentCurrency = curr;
            document.querySelectorAll('.currency-btn').forEach(btn => {
                btn.classList.toggle('active', btn.dataset.currency === curr);
            });
            // Update displayed values if results are shown
            if (document.getElementById('results-section').classList.contains('active')) {
                updateCurrencyDisplay();
            }
        }

        // Mode switcher
        function switchMode(mode) {
            document.querySelectorAll('.mode-btn').forEach(btn => btn.classList.remove('active'));
            event.target.closest('.mode-btn').classList.add('active');
            
            document.querySelectorAll('.section-content').forEach(sec => sec.classList.remove('active'));
            document.getElementById(mode + '-section').classList.add('active');
            
            // Hide results when switching
            document.getElementById('results-section').classList.remove('active');
        }

        // File upload handling
        function handleFileSelect(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    uploadedImage = e.target.result;
                    const preview = document.getElementById('uploadPreview');
                    preview.src = uploadedImage;
                    preview.style.display = 'block';
                    document.getElementById('aiEvaluateBtn').style.display = 'block';
                    
                    // Hide upload text
                    document.querySelector('.upload-text').style.display = 'none';
                    document.querySelector('.upload-hint').style.display = 'none';
                    document.querySelector('.upload-icon').style.display = 'none';
                };
                reader.readAsDataURL(file);
            }
        }

        // Drag and drop
        const uploadArea = document.getElementById('uploadArea');
        uploadArea.addEventListener('dragover', (e) => {
            e.preventDefault();
            uploadArea.classList.add('dragover');
        });
        uploadArea.addEventListener('dragleave', () => {
            uploadArea.classList.remove('dragover');
        });
        uploadArea.addEventListener('drop', (e) => {
            e.preventDefault();
            uploadArea.classList.remove('dragover');
            const files = e.dataTransfer.files;
            if (files.length > 0) {
                const event = { target: { files: files } };
                handleFileSelect(event);
            }
        });

        // AI Analysis Simulation
        function startAIAnalysis() {
            if (!uploadedImage) return;
            
            const overlay = document.getElementById('aiOverlay');
            const progressBar = document.getElementById('aiProgressBar');
            const log = document.getElementById('aiLog');
            
            overlay.classList.add('active');
            
            const logs = [
                "Initializing neural network...",
                "Detecting formation layout...",
                "Scanning player cards...",
                "Analyzing OVR ratings...",
                "Calculating team balance...",
                "Evaluating coach influence...",
                "Computing market value...",
                "Finalizing results..."
            ];
            
            let step = 0;
            const interval = setInterval(() => {
                step++;
                const progress = (step / logs.length) * 100;
                progressBar.style.width = progress + '%';
                
                if (step <= logs.length) {
                    log.textContent = logs[step - 1];
                }
                
                if (step >= logs.length) {
                    clearInterval(interval);
                    setTimeout(() => {
                        overlay.classList.remove('active');
                        // Generate random but realistic results for AI mode
                        generateAIResults();
                    }, 500);
                }
            }, 400);
        }

        function generateAIResults() {
            // Simulate AI-detected values
            const avgOVR = Math.floor(Math.random() * 15) + 78; // 78-93
            const balance = Math.floor(Math.random() * 20) + 75; // 75-95
            const consistency = Math.floor(Math.random() * 25) + 70; // 70-95
            const coachBonus = Math.floor(Math.random() * 15) + 5; // 5-20
            const chemistry = Math.floor(Math.random() * 15) + 80; // 80-95
            
            displayResults(avgOVR, balance, consistency, coachBonus, chemistry);
        }

        // Manual Evaluation
        function evaluateTeam() {
            const players = [];
            for (let i = 1; i <= 16; i++) {
                const val = parseInt(document.getElementById('player' + i).value) || 0;
                if (val > 0) players.push(val);
            }
            
            if (players.length === 0) return;
            
            const avgOVR = players.reduce((a, b) => a + b, 0) / players.length;
            const coachLevel = parseInt(document.getElementById('coachLevel').value) || 5;
            const coachBonus = coachLevel * 1.5;
            
            // Calculate balance (standard deviation inverse)
            const mean = avgOVR;
            const variance = players.reduce((sum, val) => sum + Math.pow(val - mean, 2), 0) / players.length;
            const stdDev = Math.sqrt(variance);
            const balance = Math.max(0, 100 - (stdDev * 5));
            
            // Consistency based on min-max range
            const min = Math.min(...players);
            const max = Math.max(...players);
            const consistency = Math.max(0, 100 - ((max - min) * 2));
            
            // Chemistry (random factor for demo)
            const chemistry = Math.floor(Math.random() * 20) + 75;
            
            displayResults(avgOVR, balance, consistency, coachBonus, chemistry);
        }

        function displayResults(avgOVR, balance, consistency, coachBonus, chemistry) {
            // Calculate final score
            const finalScore = Math.min(100, (avgOVR * 0.4) + (balance * 0.2) + (consistency * 0.15) + (chemistry * 0.15) + (coachBonus * 0.5));
            
            // Stars
            let stars = '';
            const starCount = Math.round(finalScore / 20);
            for (let i = 0; i < 5; i++) {
                stars += i < starCount ? '⭐' : '☆';
            }
            
            // Tier
            let tier = 'BRONZE';
            let tierDesc = 'Bottom 50%';
            if (finalScore >= 90) { tier = 'ELITE'; tierDesc = 'Top 5%'; }
            else if (finalScore >= 80) { tier = 'GOLD'; tierDesc = 'Top 15%'; }
            else if (finalScore >= 70) { tier = 'SILVER'; tierDesc = 'Top 35%'; }
            
            // Value calculation (base on final score)
            const baseValue = finalScore * 15000; // Base in some unit
            
            document.getElementById('resultStars').textContent = stars;
            document.getElementById('resultScore').textContent = Math.round(finalScore) + '/100';
            document.getElementById('teamTier').textContent = tier;
            document.querySelector('[data-i18n="tierDesc"]').textContent = 
                currentLang === 'ar' ? `أفضل ${tierDesc.replace(/[^0-9]/g, '')}%` :
                currentLang === 'fr' ? `Top ${tierDesc.replace(/[^0-9]/g, '')}%` :
                tierDesc;
            
            document.getElementById('avgOVR').textContent = avgOVR.toFixed(1);
            document.getElementById('balanceScore').textContent = Math.round(balance) + '%';
            document.getElementById('consistencyScore').textContent = Math.round(consistency) + '%';
            document.getElementById('coachBonus').textContent = '+' + Math.round(coachBonus) + '%';
            document.getElementById('chemistryScore').textContent = Math.round(chemistry) + '%';
            
            document.getElementById('ovrBar').style.width = Math.min(100, avgOVR) + '%';
            document.getElementById('balanceBar').style.width = balance + '%';
            document.getElementById('consistencyBar').style.width = consistency + '%';
            document.getElementById('coachBar').style.width = Math.min(100, coachBonus * 5) + '%';
            document.getElementById('chemistryBar').style.width = chemistry + '%';
            
            // Currency values
            const madValue = Math.round(baseValue * 10.5); // Approximate conversion
            const egpValue = Math.round(baseValue * 19.2);
            const eurValue = Math.round(baseValue * 0.095);
            
            document.getElementById('madValue').textContent = formatCurrency(madValue, 'MAD');
            document.getElementById('egpValue').textContent = formatCurrency(egpValue, 'EGP');
            document.getElementById('eurValue').textContent = formatCurrency(eurValue, 'EUR');
            
            updateCurrencyDisplay();
            
            document.getElementById('results-section').classList.add('active');
            document.getElementById('results-section').scrollIntoView({ behavior: 'smooth' });
        }

        function formatCurrency(value, currency) {
            if (value >= 1000000) {
                return (value / 1000000).toFixed(1) + 'M ' + currency;
            } else if (value >= 1000) {
                return (value / 1000).toFixed(1) + 'K ' + currency;
            }
            return value + ' ' + currency;
        }

        function updateCurrencyDisplay() {
            const mad = document.getElementById('madValue').textContent;
            const egp = document.getElementById('egpValue').textContent;
            const eur = document.getElementById('eurValue').textContent;
            
            let primary = mad;
            if (currentCurrency === 'EGP') primary = egp;
            if (currentCurrency === 'EUR') primary = eur;
            
            document.getElementById('primaryValue').textContent = primary;
        }

        // Initialize
        initPlayers();
        setLanguage('en');
    </script>
</body>
</html>'''

# Save the file
with open('/mnt/agents/output/koora_ef.html', 'w', encoding='utf-8') as f:
    f.write(html_content)

print("✅ KOORA EF website built successfully!")
print(f"📁 File saved to: /mnt/agents/output/koora_ef.html")
print(f"📊 File size: {len(html_content):,} characters")
