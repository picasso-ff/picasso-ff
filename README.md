# Write the complete HTML file directlywith open('/mnt/agents/output/koora_ef.html', 'w', encoding='utf-8') as f:
    f.write('''<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KOORA EF - eFootball Formation Evaluator</title>
    <link href="https://fonts.googleapis.com/css2?family=Teko:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600;700;800&family=Noto+Sans+Arabic:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #00ff88;
            --primary-dark: #00cc6a;
            --primary-glow: rgba(0, 255, 136, 0.4);
            --secondary: #00d4ff;
            --secondary-glow: rgba(0, 212, 255, 0.4);
            --accent: #ffd700;
            --accent-glow: rgba(255, 215, 0, 0.4);
            --danger: #ff4757;
            --warning: #ffa502;
            --bg-dark: #050810;
            --bg-darker: #020408;
            --bg-card: rgba(12, 18, 35, 0.92);
            --bg-glass: rgba(255, 255, 255, 0.04);
            --text-primary: #ffffff;
            --text-secondary: #8b95a8;
            --border: rgba(255, 255, 255, 0.08);
            --border-hover: rgba(0, 255, 136, 0.25);
            --card-bg: linear-gradient(145deg, rgba(20, 28, 50, 0.95), rgba(12, 18, 35, 0.98));
            --transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.3);
            --shadow-md: 0 8px 32px rgba(0, 0, 0, 0.4);
            --shadow-lg: 0 20px 60px rgba(0, 0, 0, 0.5);
            --shadow-glow: 0 0 40px rgba(0, 255, 136, 0.15);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            background: var(--bg-dark);
            color: var(--text-primary);
            overflow-x: hidden;
            min-height: 100vh;
            line-height: 1.6;
        }

        .bg-stadium {
            position: fixed; inset: 0;
            background: 
                radial-gradient(ellipse at 50% 0%, rgba(0, 255, 136, 0.08) 0%, transparent 50%),
                radial-gradient(ellipse at 80% 50%, rgba(0, 212, 255, 0.05) 0%, transparent 40%),
                linear-gradient(180deg, var(--bg-darker) 0%, var(--bg-dark) 50%, var(--bg-darker) 100%);
            z-index: -3;
        }

        .bg-noise {
            position: fixed; inset: 0; opacity: 0.03;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
            z-index: -2; pointer-events: none;
        }

        .bg-grid {
            position: fixed; inset: 0;
            background-image: 
                linear-gradient(rgba(0, 255, 136, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 255, 136, 0.03) 1px, transparent 1px);
            background-size: 60px 60px; z-index: -1;
            mask-image: radial-gradient(ellipse at center, black 0%, transparent 70%);
        }

        .particles {
            position: fixed; inset: 0; z-index: 0;
            pointer-events: none; overflow: hidden;
        }

        .particle {
            position: absolute; border-radius: 50%; opacity: 0;
            animation: floatParticle 20s infinite linear;
        }

        @keyframes floatParticle {
            0% { opacity: 0; transform: translateY(100vh) scale(0) rotate(0deg); }
            10% { opacity: 0.6; }
            90% { opacity: 0.6; }
            100% { opacity: 0; transform: translateY(-20vh) scale(1.5) rotate(720deg); }
        }

        header {
            position: fixed; top: 0; width: 100%; z-index: 1000;
            background: rgba(5, 8, 16, 0.85);
            backdrop-filter: blur(24px) saturate(1.2);
            border-bottom: 1px solid var(--border);
            transition: var(--transition);
        }

        header.scrolled {
            background: rgba(5, 8, 16, 0.95);
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.5);
        }

        .header-container {
            max-width: 1440px; margin: 0 auto;
            padding: 0.875rem 2rem;
            display: flex; justify-content: space-between; align-items: center;
        }

        .logo {
            display: flex; align-items: center; gap: 0.875rem;
            text-decoration: none; position: relative;
        }

        .logo-icon {
            width: 44px; height: 44px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border-radius: 14px;
            display: flex; align-items: center; justify-content: center;
            font-size: 1.35rem; color: var(--bg-dark);
            box-shadow: 0 0 20px var(--primary-glow), inset 0 1px 0 rgba(255,255,255,0.3);
            position: relative; overflow: hidden;
        }

        .logo-icon::after {
            content: ''; position: absolute; inset: 0;
            background: linear-gradient(135deg, transparent 40%, rgba(255,255,255,0.3) 100%);
        }

        .logo-text {
            font-family: 'Teko', sans-serif;
            font-size: 2.4rem; font-weight: 700;
            color: var(--text-primary); letter-spacing: 3px;
            line-height: 1; text-transform: uppercase;
        }

        .logo-text span {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            background-clip: text;
            filter: drop-shadow(0 0 8px var(--primary-glow));
        }

        .nav-controls { display: flex; gap: 0.75rem; align-items: center; }

        .control-btn {
            background: var(--bg-glass); border: 1px solid var(--border);
            color: var(--text-secondary); padding: 0.625rem 1.25rem;
            border-radius: 12px; cursor: pointer;
            font-family: 'Inter', sans-serif; font-size: 0.875rem; font-weight: 600;
            transition: var(--transition);
            display: flex; align-items: center; gap: 0.5rem;
            backdrop-filter: blur(10px); position: relative; overflow: hidden;
        }

        .control-btn::before {
            content: ''; position: absolute; inset: 0;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            opacity: 0; transition: var(--transition);
        }

        .control-btn:hover {
            border-color: var(--primary); color: var(--primary);
            transform: translateY(-2px); box-shadow: 0 4px 20px var(--primary-glow);
        }

        .control-btn:hover::before { opacity: 0.1; }
        .control-btn i { font-size: 0.9rem; position: relative; z-index: 1; }
        .control-btn span { position: relative; z-index: 1; }

        .hero {
            margin-top: 76px; padding: 5rem 2rem 4rem;
            text-align: center; position: relative; overflow: hidden;
        }

        .hero-badge {
            display: inline-flex; align-items: center; gap: 0.625rem;
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.1), rgba(0, 212, 255, 0.1));
            border: 1px solid rgba(0, 255, 136, 0.2);
            padding: 0.625rem 1.5rem; border-radius: 100px;
            font-size: 0.875rem; font-weight: 600; color: var(--primary);
            margin-bottom: 2rem; animation: fadeInUp 0.8s ease;
            backdrop-filter: blur(10px);
        }

        .hero-badge i { font-size: 1rem; }

        .hero h1 {
            font-family: 'Teko', sans-serif;
            font-size: clamp(3.5rem, 10vw, 7rem); font-weight: 700;
            line-height: 0.95; margin-bottom: 1.25rem;
            background: linear-gradient(180deg, #fff 0%, #c0c8d8 50%, var(--primary) 100%);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            background-clip: text; animation: fadeInUp 0.8s ease 0.15s both;
            letter-spacing: 2px;
        }

        .hero p {
            font-size: 1.25rem; color: var(--text-secondary);
            max-width: 560px; margin: 0 auto 2.5rem;
            animation: fadeInUp 0.8s ease 0.3s both;
            font-weight: 400; line-height: 1.7;
        }

        .hero-cta {
            display: inline-flex; align-items: center; gap: 0.75rem;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: var(--bg-dark); padding: 1rem 2.5rem;
            border-radius: 14px; font-weight: 700; font-size: 1.1rem;
            text-decoration: none; transition: var(--transition);
            box-shadow: 0 4px 30px var(--primary-glow);
            animation: fadeInUp 0.8s ease 0.45s both;
            border: none; cursor: pointer; text-transform: uppercase;
            letter-spacing: 1px; position: relative; overflow: hidden;
        }

        .hero-cta::before {
            content: ''; position: absolute; inset: 0;
            background: linear-gradient(135deg, transparent, rgba(255,255,255,0.3));
            opacity: 0; transition: var(--transition);
        }

        .hero-cta:hover { transform: translateY(-3px); box-shadow: 0 8px 40px var(--primary-glow); }
        .hero-cta:hover::before { opacity: 1; }

        .hero-stats {
            display: flex; justify-content: center; gap: 4rem;
            margin-top: 4rem; animation: fadeInUp 0.8s ease 0.6s both;
        }

        .stat-item { text-align: center; position: relative; }

        .stat-item:not(:last-child)::after {
            content: ''; position: absolute; right: -2rem; top: 50%;
            transform: translateY(-50%); height: 40px; width: 1px;
            background: var(--border);
        }

        .stat-value {
            font-family: 'Teko', sans-serif; font-size: 3.5rem; font-weight: 700;
            line-height: 1;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .stat-label {
            font-size: 0.8rem; color: var(--text-secondary);
            text-transform: uppercase; letter-spacing: 2px;
            font-weight: 600; margin-top: 0.25rem;
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(40px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .container { max-width: 1440px; margin: 0 auto; padding: 0 2rem; }

        .section { margin-bottom: 6rem; position: relative; }

        .section-header { text-align: center; margin-bottom: 3.5rem; }

        .section-label {
            display: inline-block; font-size: 0.8rem; font-weight: 700;
            text-transform: uppercase; letter-spacing: 3px;
            color: var(--primary); margin-bottom: 0.75rem;
        }

        .section-title {
            font-family: 'Teko', sans-serif; font-size: 3.5rem; font-weight: 600;
            line-height: 1; margin-bottom: 0.75rem;
            display: flex; align-items: center; justify-content: center; gap: 1rem;
        }

        .section-title i { color: var(--primary); font-size: 2rem; filter: drop-shadow(0 0 10px var(--primary-glow)); }
        .section-subtitle { color: var(--text-secondary); font-size: 1.1rem; max-width: 500px; margin: 0 auto; }

        .panel {
            background: var(--card-bg); border: 1px solid var(--border);
            border-radius: 24px; padding: 2rem; backdrop-filter: blur(20px);
            transition: var(--transition); position: relative; overflow: hidden;
        }

        .panel::before {
            content: ''; position: absolute; top: 0; left: 0; right: 0;
            height: 1px;
            background: linear-gradient(90deg, transparent, var(--primary), transparent);
            opacity: 0; transition: var(--transition);
        }

        .panel:hover {
            border-color: var(--border-hover);
            box-shadow: var(--shadow-glow), var(--shadow-lg);
            transform: translateY(-4px);
        }

        .panel:hover::before { opacity: 1; }

        .panel-title {
            font-family: 'Teko', sans-serif; font-size: 1.75rem;
            margin-bottom: 1.5rem; display: flex; align-items: center; gap: 0.75rem;
            color: var(--text-primary); letter-spacing: 1px;
        }

        .panel-title i { color: var(--primary); font-size: 1.25rem; }

        .formation-select {
            width: 100%; padding: 1rem 1.25rem;
            background: var(--bg-glass); border: 1px solid var(--border);
            border-radius: 14px; color: var(--text-primary);
            font-size: 1rem; font-family: 'Inter', sans-serif;
            cursor: pointer; transition: var(--transition);
            margin-bottom: 1.5rem; appearance: none;
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='20' height='20' viewBox='0 0 24 24' fill='none' stroke='%2300ff88' stroke-width='2.5' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
            background-repeat: no-repeat; background-position: right 1rem center;
            font-weight: 600;
        }

        .formation-select:focus {
            outline: none; border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(0, 255, 136, 0.1), 0 0 20px var(--primary-glow);
        }

        .formation-select option { background: var(--bg-dark); color: var(--text-primary); }

        .player-slots {
            display: flex; flex-direction: column; gap: 0.625rem;
            max-height: 640px; overflow-y: auto; padding-right: 0.5rem;
        }

        .player-slots::-webkit-scrollbar { width: 5px; }
        .player-slots::-webkit-scrollbar-track { background: transparent; }
        .player-slots::-webkit-scrollbar-thumb { background: var(--primary); border-radius: 10px; }

        .player-slot {
            background: var(--bg-glass); border: 1px solid var(--border);
            border-radius: 14px; padding: 0.875rem 1rem; cursor: pointer;
            transition: var(--transition); display: flex; align-items: center;
            gap: 1rem; position: relative; overflow: hidden;
        }

        .player-slot::before {
            content: ''; position: absolute; left: 0; top: 0;
            height: 100%; width: 3px;
            background: linear-gradient(180deg, var(--primary), var(--secondary));
            opacity: 0; transition: var(--transition);
        }

        .player-slot:hover {
            background: rgba(0, 255, 136, 0.04);
            border-color: rgba(0, 255, 136, 0.2);
            transform: translateX(6px);
        }

        .player-slot:hover::before { opacity: 1; }

        .player-slot.selected {
            background: linear-gradient(90deg, rgba(0, 255, 136, 0.08), rgba(0, 212, 255, 0.04));
            border-color: var(--primary);
        }

        .player-slot.selected::before { opacity: 1; }

        .slot-position {
            width: 42px; height: 42px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border-radius: 12px; display: flex; align-items: center; justify-content: center;
            font-family: 'Teko', sans-serif; font-size: 1.3rem; font-weight: 700;
            color: var(--bg-dark); flex-shrink: 0;
            box-shadow: 0 2px 10px var(--primary-glow);
            position: relative; overflow: hidden;
        }

        .slot-position::after {
            content: ''; position: absolute; inset: 0;
            background: linear-gradient(135deg, transparent 50%, rgba(255,255,255,0.3) 100%);
        }

        .slot-info { flex: 1; min-width: 0; }
        .slot-name { font-weight: 700; font-size: 0.95rem; margin-bottom: 0.125rem; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .slot-role { font-size: 0.8rem; color: var(--text-secondary); font-weight: 500; }
        .slot-rating { font-family: 'Teko', sans-serif; font-size: 1.75rem; font-weight: 700; color: var(--accent); line-height: 1; }

        .pitch-container {
            position: relative; aspect-ratio: 3/4;
            background: 
                linear-gradient(180deg, rgba(0, 60, 30, 0.3) 0%, rgba(0, 40, 20, 0.4) 100%),
                repeating-linear-gradient(0deg, rgba(0, 255, 136, 0.03) 0px, rgba(0, 255, 136, 0.03) 1px, transparent 1px, transparent 20px);
            border: 2px solid rgba(0, 255, 136, 0.2);
            border-radius: 24px; overflow: hidden;
            box-shadow: inset 0 0 100px rgba(0, 255, 136, 0.05), 0 0 60px rgba(0, 255, 136, 0.08);
        }

        .pitch-lines {
            position: absolute; inset: 1.5rem;
            border: 2px solid rgba(255, 255, 255, 0.15); border-radius: 12px;
        }

        .pitch-lines::before {
            content: ''; position: absolute; top: 50%; left: 0; right: 0;
            height: 2px; background: rgba(255, 255, 255, 0.15);
        }

        .pitch-lines::after {
            content: ''; position: absolute; top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            width: 100px; height: 100px;
            border: 2px solid rgba(255, 255, 255, 0.15); border-radius: 50%;
        }

        .pitch-player {
            position: absolute; transform: translate(-50%, -50%);
            cursor: pointer; transition: var(--transition); z-index: 10;
        }

        .pitch-player:hover { transform: translate(-50%, -50%) scale(1.15); z-index: 20; }

        .pitch-player-dot {
            width: 52px; height: 52px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border-radius: 50%; display: flex; align-items: center; justify-content: center;
            font-family: 'Teko', sans-serif; font-size: 1.4rem; font-weight: 700;
            color: var(--bg-dark);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4), 0 0 20px var(--primary-glow);
            border: 3px solid rgba(255, 255, 255, 0.4);
            position: relative; overflow: hidden;
        }

        .pitch-player-dot::after {
            content: ''; position: absolute; inset: 0;
            background: linear-gradient(135deg, transparent 40%, rgba(255,255,255,0.4) 100%);
        }

        .pitch-player.empty .pitch-player-dot {
            background: var(--bg-glass); border-color: var(--border);
            color: var(--text-secondary); box-shadow: none; font-size: 1rem;
        }

        .pitch-player.empty .pitch-player-dot::after { display: none; }

        .pitch-player-label {
            position: absolute; bottom: -22px; left: 50%;
            transform: translateX(-50%); font-size: 0.7rem; font-weight: 700;
            color: var(--text-primary); white-space: nowrap;
            text-shadow: 0 2px 8px rgba(0,0,0,0.9); letter-spacing: 0.5px;
            background: rgba(0,0,0,0.6); padding: 2px 8px;
            border-radius: 6px; backdrop-filter: blur(4px);
        }

        .rating-display { text-align: center; margin-bottom: 2rem; }

        .rating-circle {
            width: 180px; height: 180px;
            margin: 0 auto 1.5rem; position: relative;
        }

        .rating-circle svg {
            transform: rotate(-90deg); width: 100%; height: 100%;
            filter: drop-shadow(0 0 10px var(--primary-glow));
        }

        .rating-circle-bg { fill: none; stroke: rgba(255, 255, 255, 0.05); stroke-width: 10; }

        .rating-circle-progress {
            fill: none; stroke: url(#ratingGradient); stroke-width: 10;
            stroke-linecap: round; stroke-dasharray: 502; stroke-dashoffset: 502;
            transition: stroke-dashoffset 2s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .rating-value { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); text-align: center; }
        .rating-number { font-family: 'Teko', sans-serif; font-size: 4.5rem; font-weight: 700; line-height: 1; background: linear-gradient(180deg, #fff, var(--primary)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
        .rating-label { font-size: 0.85rem; color: var(--text-secondary); text-transform: uppercase; letter-spacing: 3px; font-weight: 700; }

        .rating-breakdown {
            display: grid; grid-template-columns: 1fr 1fr; gap: 0.875rem;
            margin-bottom: 1.5rem;
        }

        .breakdown-item {
            background: var(--bg-glass); padding: 1.125rem;
            border-radius: 16px; text-align: center;
            border: 1px solid var(--border); transition: var(--transition);
            position: relative; overflow: hidden;
        }

        .breakdown-item::before {
            content: ''; position: absolute; top: 0; left: 0; right: 0;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--primary), transparent);
            opacity: 0; transition: var(--transition);
        }

        .breakdown-item:hover { border-color: var(--border-hover); transform: translateY(-4px); box-shadow: var(--shadow-sm); }
        .breakdown-item:hover::before { opacity: 1; }

        .breakdown-value { font-family: 'Teko', sans-serif; font-size: 2.25rem; font-weight: 700; line-height: 1; margin-bottom: 0.25rem; }
        .breakdown-item:nth-child(1) .breakdown-value { color: var(--danger); }
        .breakdown-item:nth-child(2) .breakdown-value { color: var(--secondary); }
        .breakdown-item:nth-child(3) .breakdown-value { color: var(--primary); }
        .breakdown-item:nth-child(4) .breakdown-value { color: var(--accent); }
        .breakdown-label { font-size: 0.75rem; color: var(--text-secondary); text-transform: uppercase; letter-spacing: 1.5px; font-weight: 600; }

        .estimated-value {
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.06), rgba(0, 212, 255, 0.06));
            border: 1px solid rgba(0, 255, 136, 0.15); border-radius: 20px;
            padding: 1.75rem; text-align: center; margin-bottom: 1.5rem;
            position: relative; overflow: hidden;
        }

        .estimated-value::before {
            content: ''; position: absolute; top: -50%; left: -50%;
            width: 200%; height: 200%;
            background: radial-gradient(circle, rgba(0, 255, 136, 0.1) 0%, transparent 60%);
            animation: rotate 10s linear infinite;
        }

        @keyframes rotate { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }

        .value-label { font-size: 0.8rem; color: var(--text-secondary); text-transform: uppercase; letter-spacing: 3px; font-weight: 700; margin-bottom: 0.5rem; position: relative; z-index: 1; }
        .value-amount { font-family: 'Teko', sans-serif; font-size: 3.5rem; font-weight: 700; color: var(--accent); line-height: 1; text-shadow: 0 0 30px var(--accent-glow); position: relative; z-index: 1; }
        .value-currency { font-size: 1rem; color: var(--text-secondary); font-weight: 600; position: relative; z-index: 1; }

        .btn-primary {
            width: 100%; padding: 1.125rem 2rem;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border: none; border-radius: 14px; color: var(--bg-dark);
            font-family: 'Inter', sans-serif; font-size: 1.1rem; font-weight: 800;
            cursor: pointer; transition: var(--transition); text-transform: uppercase;
            letter-spacing: 1.5px; position: relative; overflow: hidden;
            display: flex; align-items: center; justify-content: center; gap: 0.75rem;
        }

        .btn-primary::before { content: ''; position: absolute; inset: 0; background: linear-gradient(135deg, transparent, rgba(255,255,255,0.4)); opacity: 0; transition: var(--transition); }
        .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 10px 40px var(--primary-glow); }
        .btn-primary:hover::before { opacity: 1; }
        .btn-primary:active { transform: translateY(-1px); }

        .btn-secondary {
            width: 100%; padding: 0.875rem 1.5rem;
            background: var(--bg-glass); border: 1px solid var(--border);
            border-radius: 12px; color: var(--text-primary);
            font-family: 'Inter', sans-serif; font-size: 0.95rem; font-weight: 600;
            cursor: pointer; transition: var(--transition);
            display: flex; align-items: center; justify-content: center; gap: 0.5rem;
        }

        .btn-secondary:hover { background: rgba(0, 255, 136, 0.08); border-color: var(--primary); color: var(--primary); }

        .upload-zone {
            border: 2px dashed var(--border); border-radius: 20px;
            padding: 2.5rem; text-align: center; cursor: pointer;
            transition: var(--transition); background: var(--bg-glass);
            position: relative; overflow: hidden;
        }

        .upload-zone:hover, .upload-zone.dragover {
            border-color: var(--primary); background: rgba(0, 255, 136, 0.04);
            box-shadow: 0 0 30px var(--primary-glow);
        }

        .upload-zone i { font-size: 3rem; color: var(--primary); margin-bottom: 1rem; display: block; }
        .upload-zone-text { font-size: 1.1rem; font-weight: 600; color: var(--text-primary); margin-bottom: 0.5rem; }
        .upload-zone-hint { font-size: 0.875rem; color: var(--text-secondary); }

        .upload-preview {
            margin-top: 1.5rem; border-radius: 16px; overflow: hidden;
            border: 1px solid var(--border); display: none; position: relative;
        }

        .upload-preview img { width: 100%; display: block; }
        .upload-preview.active { display: block; }

        .upload-remove {
            position: absolute; top: 0.75rem; right: 0.75rem;
            width: 36px; height: 36px; background: rgba(255, 71, 87, 0.9);
            border: none; border-radius: 10px; color: white; cursor: pointer;
            display: flex; align-items: center; justify-content: center;
            transition: var(--transition); font-size: 1rem;
        }

        .upload-remove:hover { transform: scale(1.1); background: var(--danger); }

        .player-card {
            background: linear-gradient(145deg, #1a1f35, #0f1425);
            border: 1px solid var(--border); border-radius: 20px;
            padding: 1.25rem; text-align: center; cursor: pointer;
            transition: var(--transition); position: relative; overflow: hidden;
            box-shadow: var(--shadow-sm);
        }

        .player-card::before {
            content: ''; position: absolute; top: 0; left: 0; right: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            opacity: 0; transition: var(--transition);
        }

        .player-card:hover {
            transform: translateY(-8px) scale(1.02);
            border-color: var(--primary);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4), 0 0 30px var(--primary-glow);
        }

        .player-card:hover::before { opacity: 1; }

        .player-card.selected {
            border-color: var(--primary);
            background: linear-gradient(145deg, rgba(0, 255, 136, 0.1), rgba(0, 212, 255, 0.05));
            box-shadow: 0 0 30px var(--primary-glow);
        }

        .player-card.selected::before { opacity: 1; }

        .player-card-img {
            width: 80px; height: 80px; border-radius: 50%;
            margin: 0 auto 1rem; object-fit: cover;
            border: 3px solid var(--primary);
            box-shadow: 0 0 20px var(--primary-glow);
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            display: flex; align-items: center; justify-content: center;
            font-family: 'Teko', sans-serif; font-size: 2rem;
            color: var(--bg-dark); position: relative; overflow: hidden;
        }

        .player-card-img img { width: 100%; height: 100%; object-fit: cover; border-radius: 50%; }

        .player-card-rating-badge {
            position: absolute; top: -5px; right: -5px;
            width: 32px; height: 32px;
            background: linear-gradient(135deg, var(--accent), #ff9500);
            border-radius: 50%; display: flex; align-items: center; justify-content: center;
            font-family: 'Teko', sans-serif; font-size: 1.1rem; font-weight: 700;
            color: var(--bg-dark); box-shadow: 0 2px 10px var(--accent-glow);
            border: 2px solid var(--bg-dark);
        }

        .player-card-name { font-weight: 700; font-size: 0.95rem; margin-bottom: 0.375rem; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .player-card-position { display: inline-block; background: var(--bg-glass); padding: 0.25rem 0.75rem; border-radius: 50px; font-size: 0.75rem; font-weight: 700; color: var(--primary); text-transform: uppercase; letter-spacing: 1px; border: 1px solid var(--border); }
        .player-card-stats { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0.5rem; margin-top: 0.875rem; padding-top: 0.875rem; border-top: 1px solid var(--border); }
        .player-stat { text-align: center; }
        .player-stat-value { font-family: 'Teko', sans-serif; font-size: 1.5rem; font-weight: 700; line-height: 1; color: var(--text-primary); }
        .player-stat-label { font-size: 0.65rem; color: var(--text-secondary); text-transform: uppercase; letter-spacing: 0.5px; font-weight: 600; }

        .suggestions-list { display: flex; flex-direction: column; gap: 1rem; }

        .suggestion-card {
            background: var(--card-bg); border: 1px solid var(--border);
            border-radius: 20px; padding: 1.75rem; transition: var(--transition);
            cursor: pointer; position: relative; overflow: hidden;
        }

        .suggestion-card::before {
            content: ''; position: absolute; top: 0; left: 0;
            width: 4px; height: 100%;
            background: linear-gradient(180deg, var(--secondary), var(--primary));
            opacity: 0; transition: var(--transition);
        }

        .suggestion-card:hover { border-color: var(--secondary); transform: translateX(12px); box-shadow: var(--shadow-md); }
        .suggestion-card:hover::before { opacity: 1; }

        .suggestion-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 0.875rem; }
        .suggestion-title { font-weight: 800; font-size: 1.15rem; display: flex; align-items: center; gap: 0.625rem; }
        .suggestion-title i { color: var(--secondary); font-size: 1.1rem; }
        .suggestion-rating { font-family: 'Teko', sans-serif; font-size: 1.75rem; color: var(--secondary); font-weight: 700; background: rgba(0, 212, 255, 0.1); padding: 0.25rem 0.875rem; border-radius: 10px; }
        .suggestion-desc { color: var(--text-secondary); font-size: 0.95rem; line-height: 1.7; margin-bottom: 1rem; }
        .suggestion-tags { display: flex; gap: 0.5rem; flex-wrap: wrap; }
        .tag { background: rgba(0, 212, 255, 0.08); color: var(--secondary); padding: 0.375rem 0.875rem; border-radius: 50px; font-size: 0.8rem; font-weight: 700; border: 1px solid rgba(0, 212, 255, 0.2); text-transform: uppercase; letter-spacing: 0.5px; }

        .converter-box {
            background: var(--card-bg); border: 1px solid var(--border);
            border-radius: 24px; padding: 2.5rem; max-width: 640px;
            margin: 0 auto; backdrop-filter: blur(20px); box-shadow: var(--shadow-md);
        }

        .converter-inputs { display: grid; grid-template-columns: 1fr auto 1fr; gap: 1.25rem; align-items: end; margin-bottom: 1.5rem; }
        @media (max-width: 640px) { .converter-inputs { grid-template-columns: 1fr; } .swap-btn { margin: 0 auto; } }

        .input-group { display: flex; flex-direction: column; gap: 0.5rem; }
        .input-group label { font-size: 0.8rem; color: var(--text-secondary); text-transform: uppercase; letter-spacing: 2px; font-weight: 700; }
        .input-group input, .input-group select { padding: 1rem 1.25rem; background: var(--bg-glass); border: 1px solid var(--border); border-radius: 14px; color: var(--text-primary); font-size: 1.05rem; font-family: 'Inter', sans-serif; transition: var(--transition); font-weight: 600; }
        .input-group input:focus, .input-group select:focus { outline: none; border-color: var(--primary); box-shadow: 0 0 0 3px rgba(0, 255, 136, 0.1), 0 0 20px var(--primary-glow); }

        .swap-btn {
            background: var(--bg-glass); border: 1px solid var(--border);
            color: var(--primary); width: 52px; height: 52px;
            border-radius: 14px; display: flex; align-items: center; justify-content: center;
            cursor: pointer; transition: var(--transition); font-size: 1.25rem; margin-bottom: 0;
        }

        .swap-btn:hover { background: rgba(0, 255, 136, 0.1); border-color: var(--primary); transform: rotate(180deg); box-shadow: 0 0 20px var(--primary-glow); }

        .converter-result { text-align: center; padding: 2rem; background: linear-gradient(135deg, rgba(0, 255, 136, 0.05), rgba(0, 212, 255, 0.05)); border-radius: 16px; border: 1px solid rgba(0, 255, 136, 0.15); position: relative; overflow: hidden; }
        .result-value { font-family: 'Teko', sans-serif; font-size: 3rem; font-weight: 700; color: var(--primary); line-height: 1; text-shadow: 0 0 20px var(--primary-glow); }
        .result-label { color: var(--text-secondary); font-size: 1rem; font-weight: 600; margin-top: 0.5rem; }

        footer {
            background: rgba(5, 8, 16, 0.95); border-top: 1px solid var(--border);
            padding: 4rem 2rem 2rem; margin-top: 8rem; text-align: center; position: relative;
        }

        footer::before { content: ''; position: absolute; top: 0; left: 50%; transform: translateX(-50%); width: 200px; height: 2px; background: linear-gradient(90deg, transparent, var(--primary), transparent); }
        .footer-logo { font-family: 'Teko', sans-serif; font-size: 3rem; font-weight: 700; margin-bottom: 1rem; letter-spacing: 3px; }
        .footer-logo span { background: linear-gradient(135deg, var(--primary), var(--secondary)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
        .footer-text { color: var(--text-secondary); margin-bottom: 2rem; font-size: 1.05rem; }
        .footer-links { display: flex; justify-content: center; gap: 2.5rem; margin-bottom: 2.5rem; }
        .footer-links a { color: var(--text-secondary); text-decoration: none; transition: var(--transition); font-weight: 600; font-size: 0.95rem; position: relative; }
        .footer-links a::after { content: ''; position: absolute; bottom: -4px; left: 0; width: 0; height: 2px; background: var(--primary); transition: var(--transition); }
        .footer-links a:hover { color: var(--primary); }
        .footer-links a:hover::after { width: 100%; }
        .social-links { display: flex; justify-content: center; gap: 1rem; margin-bottom: 2.5rem; }
        .social-links a { width: 48px; height: 48px; background: var(--bg-glass); border: 1px solid var(--border); border-radius: 14px; display: flex; align-items: center; justify-content: center; color: var(--text-secondary); text-decoration: none; transition: var(--transition); font-size: 1.25rem; }
        .social-links a:hover { background: rgba(0, 255, 136, 0.1); border-color: var(--primary); color: var(--primary); transform: translateY(-4px); box-shadow: 0 10px 20px var(--primary-glow); }
        .copyright { color: var(--text-secondary); font-size: 0.9rem; padding-top: 2rem; border-top: 1px solid var(--border); font-weight: 500; }

        .modal-overlay {
            position: fixed; inset: 0; background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(12px); z-index: 2000;
            display: none; align-items: center; justify-content: center;
            padding: 2rem; opacity: 0; transition: opacity 0.3s ease;
        }

        .modal-overlay.active { display: flex; opacity: 1; }

        .modal {
            background: var(--card-bg); border: 1px solid var(--border);
            border-radius: 28px; padding: 2rem; max-width: 900px;
            width: 100%; max-height: 85vh; overflow-y: auto;
            position: relative;
            transform: translateY(30px) scale(0.95);
            transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
            box-shadow: var(--shadow-lg);
        }

        .modal-overlay.active .modal { transform: translateY(0) scale(1); }

        .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem; padding-bottom: 1rem; border-bottom: 1px solid var(--border); }
        .modal-title { font-family: 'Teko', sans-serif; font-size: 2.25rem; color: var(--text-primary); letter-spacing: 1px; }
        .modal-close { background: var(--bg-glass); border: 1px solid var(--border); color: var(--text-secondary); font-size: 1.25rem; cursor: pointer; width: 44px; height: 44px; display: flex; align-items: center; justify-content: center; border-radius: 12px; transition: var(--transition); }
        .modal-close:hover { background: rgba(255, 71, 87, 0.2); border-color: var(--danger); color: var(--danger); transform: rotate(90deg); }
        .player-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 1rem; }

        @media (max-width: 1200px) { .builder-grid { grid-template-columns: 1fr !important; } .pitch-container { max-width: 500px; margin: 0 auto; } }
        @media (max-width: 768px) {
            .header-container { padding: 0.75rem 1rem; }
            .logo-text { font-size: 1.75rem; }
            .hero { padding: 3rem 1rem; }
            .hero-stats { gap: 2rem; flex-wrap: wrap; }
            .stat-item:not(:last-child)::after { display: none; }
            .stat-value { font-size: 2.5rem; }
            .section-title { font-size: 2.5rem; }
            .panel { padding: 1.5rem; }
            .rating-circle { width: 140px; height: 140px; }
            .rating-number { font-size: 3.5rem; }
            .converter-box { padding: 1.5rem; }
            .footer-links { gap: 1.5rem; flex-wrap: wrap; }
        }

        .fade-in { opacity: 0; transform: translateY(40px); transition: opacity 0.7s ease, transform 0.7s ease; }
        .fade-in.visible { opacity: 1; transform: translateY(0); }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--bg-dark); }
        ::-webkit-scrollbar-thumb { background: linear-gradient(180deg, var(--primary), var(--secondary)); border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--primary); }

        [dir="rtl"] .player-slot:hover { transform: translateX(-6px); }
        [dir="rtl"] .suggestion-card:hover { transform: translateX(-12px); }
        [dir="rtl"] .logo-text { letter-spacing: 0; }

        .builder-grid { display: grid; grid-template-columns: 1fr 1.3fr 1fr; gap: 2rem; align-items: start; }

        .tactic-badges { display: flex; gap: 0.5rem; flex-wrap: wrap; margin-top: 1rem; }
        .tactic-badge { background: var(--bg-glass); border: 1px solid var(--border); padding: 0.5rem 1rem; border-radius: 10px; font-size: 0.85rem; font-weight: 600; color: var(--text-secondary); transition: var(--transition); cursor: pointer; }
        .tactic-badge:hover { border-color: var(--primary); color: var(--primary); background: rgba(0, 255, 136, 0.05); }
        .tactic-badge.active { background: linear-gradient(135deg, var(--primary), var(--secondary)); color: var(--bg-dark); border-color: transparent; }

        .loading-overlay {
            position: fixed; inset: 0; background: var(--bg-dark);
            z-index: 9999; display: flex; align-items: center; justify-content: center;
            flex-direction: column; gap: 1.5rem;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        .loading-overlay.hidden { opacity: 0; visibility: hidden; }
        .loading-spinner { width: 60px; height: 60px; border: 3px solid var(--bg-glass); border-top-color: var(--primary); border-radius: 50%; animation: spin 1s linear infinite; box-shadow: 0 0 20px var(--primary-glow); }
        .loading-text { font-family: 'Teko', sans-serif; font-size: 1.5rem; letter-spacing: 4px; color: var(--text-secondary); }
        @keyframes spin { to { transform: rotate(360deg); } }
    </style>
</head>
<body>
    <div class="loading-overlay" id="loadingScreen">
        <div class="loading-spinner"></div>
        <div class="loading-text">KOORA EF</div>
    </div>

    <div class="bg-stadium"></div>
    <div class="bg-noise"></div>
    <div class="bg-grid"></div>
    <div class="particles" id="particles"></div>

    <svg width="0" height="0" style="position:absolute">
        <defs>
            <linearGradient id="ratingGradient" x1="0%" y1="0%" x2="100%" y2="0%">
                <stop offset="0%" style="stop-color:#00ff88"/>
                <stop offset="100%" style="stop-color:#00d4ff"/>
            </linearGradient>
        </defs>
    </svg>

    <header id="mainHeader">
        <div class="header-container">
            <a href="#" class="logo">
                <div class="logo-icon"><i class="fas fa-futbol"></i></div>
                <div class="logo-text">KOORA <span>EF</span></div>
            </a>
            <div class="nav-controls">
                <button class="control-btn" onclick="toggleLanguage()">
                    <i class="fas fa-globe"></i><span id="langLabel">EN</span>
                </button>
                <button class="control-btn" onclick="toggleCurrency()">
                    <i class="fas fa-coins"></i><span id="currLabel">USD</span>
                </button>
            </div>
        </div>
    </header>

    <section class="hero">
        <div class="hero-badge">
            <i class="fas fa-bolt"></i>
            <span data-i18n="badge">Next-Gen Formation Analyzer</span>
        </div>
        <h1 data-i18n="heroTitle">DOMINATE THE PITCH</h1>
        <p data-i18n="heroDesc">Build, evaluate, and optimize your eFootball formations with AI-powered analysis and real-time market valuations.</p>
        <button class="hero-cta" onclick="scrollToBuilder()">
            <span data-i18n="startNow">Start Building</span>
            <i class="fas fa-arrow-right"></i>
        </button>
        <div class="hero-stats">
            <div class="stat-item">
                <div class="stat-value">50+</div>
                <div class="stat-label" data-i18n="statFormations">Formations</div>
            </div>
            <div class="stat-item">
                <div class="stat-value">10K+</div>
                <div class="stat-label" data-i18n="statPlayers">Players</div>
            </div>
            <div class="stat-item">
                <div class="stat-value">99%</div>
                <div class="stat-label" data-i18n="statAccuracy">Accuracy</div>
            </div>
        </div>
    </section>

    <div class="container">
        <section class="section fade-in" id="builderSection">
            <div class="section-header">
                <div class="section-label" data-i18n="builderLabel">Tactical Center</div>
                <h2 class="section-title">
                    <i class="fas fa-chess-board"></i>
                    <span data-i18n="builderTitle">Formation Builder</span>
                </h2>
                <p class="section-subtitle" data-i18n="builderDesc">Select your formation and players to get instant analysis</p>
            </div>

            <div class="builder-grid">
                <div class="panel fade-in">
                    <div class="panel-title">
                        <i class="fas fa-users"></i>
                        <span data-i18n="squad">Squad</span>
                    </div>
                    <select class="formation-select" id="formationSelect" onchange="changeFormation()">
                        <option value="433">4-3-3 Attack</option>
                        <option value="442">4-4-2 Balanced</option>
                        <option value="352">3-5-2 Control</option>
                        <option value="4231">4-2-3-1 Meta</option>
                        <option value="343">3-4-3 Ultra Attack</option>
                        <option value="451">4-5-1 Defensive</option>
                        <option value="532">5-3-2 Park the Bus</option>
                    </select>
                    
                    <div class="tactic-badges" id="tacticBadges">
                        <div class="tactic-badge active" data-tactic="possession" onclick="setTactic(this)">Possession</div>
                        <div class="tactic-badge" data-tactic="counter" onclick="setTactic(this)">Counter Attack</div>
                        <div class="tactic-badge" data-tactic="wide" onclick="setTactic(this)">Wide Play</div>
                        <div class="tactic-badge" data-tactic="tiki" onclick="setTactic(this)">Tiki-Taka</div>
                    </div>
                    
                    <div class="player-slots" id="playerSlots" style="margin-top: 1.5rem;"></div>
                </div>

                <div class="panel fade-in" style="padding: 1.25rem;">
                    <div class="pitch-container" id="pitchContainer">
                        <div class="pitch-lines"></div>
                        <div id="pitchPlayers"></div>
                    </div>
                    
                    <div class="upload-zone" id="uploadZone" onclick="document.getElementById('formationUpload').click()">
                        <input type="file" id="formationUpload" accept="image/*" style="display:none" onchange="handleImageUpload(event)">
                        <i class="fas fa-cloud-upload-alt"></i>
                        <div class="upload-zone-text" data-i18n="uploadTitle">Upload Formation Image</div>
                        <div class="upload-zone-hint" data-i18n="uploadHint">Drag & drop or click to upload your tactical setup</div>
                    </div>
                    
                    <div class="upload-preview" id="uploadPreview">
                        <img id="previewImg" src="" alt="Formation Preview">
                        <button class="upload-remove" onclick="removeUpload(event)">
                            <i class="fas fa-times"></i>
                        </button>
                    </div>
                </div>

                <div class="panel fade-in">
                    <div class="panel-title">
                        <i class="fas fa-chart-line"></i>
                        <span data-i18n="analysis">Analysis</span>
                    </div>
                    
                    <div class="rating-display">
                        <div class="rating-circle">
                            <svg viewBox="0 0 200 200">
                                <circle class="rating-circle-bg" cx="100" cy="100" r="80"/>
                                <circle class="rating-circle-progress" id="ratingCircle" cx="100" cy="100" r="80"/>
                            </svg>
                            <div class="rating-value">
                                <div class="rating-number" id="ratingNumber">0</div>
                                <div class="rating-label" data-i18n="overall">Overall</div>
                            </div>
                        </div>
                    </div>

                    <div class="rating-breakdown">
                        <div class="breakdown-item">
                            <div class="breakdown-value" id="attackScore">0</div>
                            <div class="breakdown-label" data-i18n="attack">Attack</div>
                        </div>
                        <div class="breakdown-item">
                            <div class="breakdown-value" id="midfieldScore">0</div>
                            <div class="breakdown-label" data-i18n="midfield">Midfield</div>
                        </div>
                        <div class="breakdown-item">
                            <div class="breakdown-value" id="defenseScore">0</div>
                            <div class="breakdown-label" data-i18n="defense">Defense</div>
                        </div>
                        <div class="breakdown-item">
                            <div class="breakdown-value" id="chemistryScore">0</div>
                            <div class="breakdown-label" data-i18n="chemistry">Chemistry</div>
                        </div>
                    </div>

                    <div class="estimated-value">
                        <div class="value-label" data-i18n="estValue">Estimated Value</div>
                        <div class="value-amount" id="valueAmount">0</div>
                        <div class="value-currency" id="valueCurrency">USD</div>
                    </div>

                    <button class="btn-primary" onclick="analyzeFormation()">
                        <i class="fas fa-microchip"></i>
                        <span data-i18n="analyzeBtn">Analyze Formation</span>
                    </button>
                </div>
            </div>
        </section>

        <section class="section fade-in">
            <div class="section-header">
                <div class="section-label" data-i18n="suggestionsLabel">AI Coach</div>
                <h2 class="section-title">
                    <i class="fas fa-lightbulb"></i>
                    <span data-i18n="suggestionsTitle">AI Suggestions</span>
                </h2>
                <p class="section-subtitle" data-i18n="suggestionsDesc">Smart recommendations to improve your team</p>
            </div>
            <div class="suggestions-list" id="suggestionsList"></div>
        </section>

        <section class="section fade-in">
            <div class="section-header">
                <div class="section-label" data-i18n="converterLabel">Finance</div>
                <h2 class="section-title">
                    <i class="fas fa-exchange-alt"></i>
                    <span data-i18n="converterTitle">Currency Converter</span>
                </h2>
                <p class="section-subtitle" data-i18n="converterDesc">Convert player values across currencies</p>
            </div>
            <div class="converter-box">
                <div class="converter-inputs">
                    <div class="input-group">
                        <label data-i18n="amount">Amount</label>
                        <input type="number" id="convAmount" value="1000000" oninput="convertCurrency()">
                    </div>
                    <button class="swap-btn" onclick="swapCurrency()">
                        <i class="fas fa-exchange-alt"></i>
                    </button>
                    <div class="input-group">
                        <label data-i18n="from">From</label>
                        <select id="convFrom" onchange="convertCurrency()">
                            <option value="USD">USD ($)</option>
                            <option value="EUR">EUR (€)</option>
                            <option value="EGP">EGP (£)</option>
                            <option value="MAD">MAD (DH)</option>
                            <option value="GBP">GBP (£)</option>
                            <option value="JPY">JPY (¥)</option>
                        </select>
                    </div>
                </div>
                <div class="input-group" style="margin-bottom: 1.5rem;">
                    <label data-i18n="to">To</label>
                    <select id="convTo" onchange="convertCurrency()">
                        <option value="EUR">EUR (€)</option>
                        <option value="USD">USD ($)</option>
                        <option value="EGP">EGP (£)</option>
                        <option value="MAD">MAD (DH)</option>
                        <option value="GBP">GBP (£)</option>
                        <option value="JPY">JPY (¥)</option>
                    </select>
                </div>
                <div class="converter-result">
                    <div class="result-value" id="convResult">920,000</div>
                    <div class="result-label" id="convLabel">EUR (€)</div>
                </div>
            </div>
        </section>
    </div>

    <footer>
        <div class="footer-logo">KOORA <span>EF</span></div>
        <p class="footer-text" data-i18n="footerText">The ultimate eFootball formation analyzer and squad builder</p>
        <div class="footer-links">
            <a href="#" data-i18n="privacy">Privacy</a>
            <a href="#" data-i18n="terms">Terms</a>
            <a href="#" data-i18n="contact">Contact</a>
        </div>
        <div class="social-links">
            <a href="#"><i class="fab fa-twitter"></i></a>
            <a href="#"><i class="fab fa-discord"></i></a>
            <a href="#"><i class="fab fa-youtube"></i></a>
            <a href="#"><i class="fab fa-instagram"></i></a>
        </div>
        <div class="copyright">© 2026 KOORA EF. <span data-i18n="rights">All rights reserved.</span></div>
    </footer>

    <div class="modal-overlay" id="playerModal">
        <div class="modal">
            <div class="modal-header">
                <h3 class="modal-title" data-i18n="selectPlayer">Select Player</h3>
                <button class="modal-close" onclick="closeModal()">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="player-grid" id="playerGrid"></div>
        </div>
    </div>
''')

print("Part 1 written successfully")
