<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RK Studios - Game Opening</title>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700;900&family=Playfair+Display:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #050505;
            overflow: hidden;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Cinzel', serif;
            cursor: none;
        }

        /* Cinematic Black Bars */
        .black-bar {
            position: fixed;
            left: 0;
            width: 100%;
            height: 12vh;
            background: #000;
            z-index: 1000;
            transition: height 2s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .black-bar.top { top: 0; }
        .black-bar.bottom { bottom: 0; }

        /* Main Stage */
        .stage {
            position: relative;
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: radial-gradient(ellipse at center, #0a0a0a 0%, #000000 100%);
        }

        /* Dramatic Spotlight */
        .spotlight {
            position: absolute;
            width: 600px;
            height: 600px;
            background: radial-gradient(circle, rgba(255,255,255,0.03) 0%, transparent 70%);
            border-radius: 50%;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            animation: spotlightPulse 4s ease-in-out infinite;
        }

        @keyframes spotlightPulse {
            0%, 100% { transform: translate(-50%, -50%) scale(1); opacity: 0.5; }
            50% { transform: translate(-50%, -50%) scale(1.1); opacity: 0.8; }
        }

        /* Dust Particles */
        .dust-container {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
        }

        .dust {
            position: absolute;
            width: 2px;
            height: 2px;
            background: rgba(255,255,255,0.3);
            border-radius: 50%;
            animation: dustFloat 15s linear infinite;
        }

        @keyframes dustFloat {
            0% { transform: translateY(100vh) translateX(0); opacity: 0; }
            10% { opacity: 0.6; }
            90% { opacity: 0.6; }
            100% { transform: translateY(-100vh) translateX(50px); opacity: 0; }
        }

        /* Vignette */
        .vignette {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(ellipse at center, transparent 40%, rgba(0,0,0,0.9) 100%);
            pointer-events: none;
            z-index: 50;
        }

        /* Film Grain Overlay */
        .grain {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 200;
            opacity: 0.04;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
        }

        /* Logo Container */
        .logo-wrapper {
            position: relative;
            text-align: center;
            opacity: 0;
            animation: logoReveal 1.5s cubic-bezier(0.22, 1, 0.36, 1) 1s forwards;
        }

        @keyframes logoReveal {
            0% { 
                opacity: 0; 
                transform: scale(1.3) translateY(30px);
                filter: blur(20px);
            }
            100% { 
                opacity: 1; 
                transform: scale(1) translateY(0);
                filter: blur(0);
            }
        }

        /* RK Monogram */
        .rk-monogram {
            font-size: 180px;
            font-weight: 900;
            letter-spacing: -8px;
            color: #e8e8e8;
            line-height: 1;
            position: relative;
            text-shadow: 
                0 1px 1px rgba(0,0,0,0.8),
                0 2px 30px rgba(255,255,255,0.1);
        }

        .rk-monogram .r { display: inline-block; animation: letterSlide 1.2s cubic-bezier(0.22, 1, 0.36, 1) 1.2s both; }
        .rk-monogram .k { display: inline-block; animation: letterSlide 1.2s cubic-bezier(0.22, 1, 0.36, 1) 1.4s both; }

        @keyframes letterSlide {
            0% { 
                opacity: 0; 
                transform: translateX(-60px) scale(0.8);
                filter: blur(10px);
            }
            100% { 
                opacity: 1; 
                transform: translateX(0) scale(1);
                filter: blur(0);
            }
        }

        /* Elegant Divider Line */
        .divider {
            width: 0;
            height: 1px;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
            margin: 25px auto;
            animation: lineExpand 1.5s cubic-bezier(0.22, 1, 0.36, 1) 2s forwards;
        }

        @keyframes lineExpand {
            0% { width: 0; opacity: 0; }
            100% { width: 200px; opacity: 1; }
        }

        /* Studio Name */
        .studio-name {
            font-family: 'Playfair Display', serif;
            font-size: 18px;
            font-weight: 400;
            font-style: italic;
            letter-spacing: 12px;
            color: rgba(255,255,255,0.5);
            text-transform: uppercase;
            opacity: 0;
            animation: textFadeUp 1.2s cubic-bezier(0.22, 1, 0.36, 1) 2.5s forwards;
        }

        /* Creator Credit */
        .creator-credit {
            margin-top: 15px;
            font-family: 'Cinzel', serif;
            font-size: 11px;
            font-weight: 400;
            letter-spacing: 6px;
            color: rgba(255,255,255,0.3);
            text-transform: uppercase;
            opacity: 0;
            animation: textFadeUp 1.2s cubic-bezier(0.22, 1, 0.36, 1) 3s forwards;
        }

        @keyframes textFadeUp {
            0% { 
                opacity: 0; 
                transform: translateY(20px);
                filter: blur(5px);
            }
            100% { 
                opacity: 1; 
                transform: translateY(0);
                filter: blur(0);
            }
        }

        /* Subtle Glow behind logo */
        .logo-glow {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, rgba(200,180,140,0.03) 0%, transparent 70%);
            border-radius: 50%;
            pointer-events: none;
            animation: glowBreathe 4s ease-in-out infinite;
        }

        @keyframes glowBreathe {
            0%, 100% { transform: translate(-50%, -50%) scale(1); opacity: 0.5; }
            50% { transform: translate(-50%, -50%) scale(1.2); opacity: 0.8; }
        }

        /* Loading Progress (subtle) */
        .progress-container {
            position: fixed;
            bottom: 15vh;
            left: 50%;
            transform: translateX(-50%);
            width: 150px;
            height: 1px;
            background: rgba(255,255,255,0.05);
            opacity: 0;
            animation: textFadeUp 1s ease 3.5s forwards;
        }

        .progress-bar {
            height: 100%;
            width: 0%;
            background: rgba(255,255,255,0.3);
            animation: progressFill 2.5s cubic-bezier(0.4, 0, 0.2, 1) 3.5s forwards;
        }

        @keyframes progressFill {
            0% { width: 0%; }
            100% { width: 100%; }
        }

        /* Fade to Black Transition */
        .fade-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            opacity: 0;
            pointer-events: none;
            z-index: 500;
            animation: fadeToBlack 1.5s ease-in 6.5s forwards;
        }

        @keyframes fadeToBlack {
            0% { opacity: 0; }
            100% { opacity: 1; }
        }

        /* Skip hint */
        .skip-hint {
            position: fixed;
            bottom: 20px;
            right: 30px;
            font-family: 'Cinzel', serif;
            font-size: 10px;
            letter-spacing: 3px;
            color: rgba(255,255,255,0.15);
            text-transform: uppercase;
            opacity: 0;
            animation: textFadeUp 1s ease 4s forwards;
            cursor: pointer;
            transition: color 0.3s;
        }
        .skip-hint:hover { color: rgba(255,255,255,0.4); }

        /* Responsive */
        @media (max-width: 768px) {
            .rk-monogram { font-size: 100px; letter-spacing: -4px; }
            .studio-name { font-size: 14px; letter-spacing: 8px; }
            .creator-credit { font-size: 9px; letter-spacing: 4px; }
        }
    </style>
<base target="_blank">
</head>
<body>
    <!-- Cinematic Black Bars -->
    <div class="black-bar top" id="barTop"></div>
    <div class="black-bar bottom" id="barBottom"></div>

    <!-- Film Grain -->
    <div class="grain"></div>

    <!-- Vignette -->
    <div class="vignette"></div>

    <!-- Dust Particles -->
    <div class="dust-container" id="dustContainer"></div>

    <!-- Main Stage -->
    <div class="stage">
        <div class="spotlight"></div>
        <div class="logo-glow"></div>

        <div class="logo-wrapper">
            <div class="rk-monogram">
                <span class="r">R</span><span class="k">K</span>
            </div>
            <div class="divider"></div>
            <div class="studio-name">Studios</div>
            <div class="creator-credit">Created by Rajib Mohammad</div>
        </div>
    </div>

    <!-- Progress Bar -->
    <div class="progress-container">
        <div class="progress-bar"></div>
    </div>

    <!-- Fade Overlay -->
    <div class="fade-overlay"></div>

    <!-- Skip -->
    <div class="skip-hint" onclick="skipAnimation()">Click to Skip</div>

    <script>
        // Generate dust particles
        const dustContainer = document.getElementById('dustContainer');
        for (let i = 0; i < 30; i++) {
            const dust = document.createElement('div');
            dust.className = 'dust';
            dust.style.left = Math.random() * 100 + '%';
            dust.style.animationDelay = Math.random() * 15 + 's';
            dust.style.animationDuration = (Math.random() * 10 + 10) + 's';
            dust.style.width = (Math.random() * 2 + 1) + 'px';
            dust.style.height = dust.style.width;
            dustContainer.appendChild(dust);
        }

        // Animate black bars (cinematic open)
        setTimeout(() => {
            document.getElementById('barTop').style.height = '0vh';
            document.getElementById('barBottom').style.height = '0vh';
        }, 500);

        // Auto redirect
        let redirectTimer = setTimeout(() => {
            window.location.href = 'https://ducklings.io';
        }, 8000);

        // Skip function
        function skipAnimation() {
            clearTimeout(redirectTimer);
            document.querySelector('.fade-overlay').style.animation = 'none';
            document.querySelector('.fade-overlay').style.opacity = '1';
            setTimeout(() => {
                window.location.href = 'https://ducklings.io';
            }, 500);
        }

        // Keyboard skip (Space or Enter)
        document.addEventListener('keydown', (e) => {
            if (e.code === 'Space' || e.code === 'Enter') {
                skipAnimation();
            }
        });
    </script>
</body>
</html>
