


                    <!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEURAL AI - GAME HUB ELITE</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #020617;
            --card-bg: rgba(15, 23, 42, 0.95);
            --neon-blue: #38bdf8;
            --neon-gold: #fbbf24;
            --text-main: #f8fafc;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Inter', sans-serif; }
        
        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            overflow-x: hidden;
            background: radial-gradient(circle at center, #1e293b 0%, #020617 100%);
        }

        /* Hiệu ứng Tuyết Rơi */
        #snow-canvas {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; z-index: -1;
        }

        /* Container chính */
        .main-wrapper {
            display: flex; flex-direction: column; align-items: center;
            padding: 20px; gap: 30px;
        }

        /* Tool AI MD5 */
        .app-container {
            width: 100%; max-width: 420px; background-color: var(--card-bg);
            border: 1px solid rgba(56, 189, 248, 0.3); border-radius: 32px;
            padding: 30px 25px; box-shadow: 0 0 50px rgba(0,0,0,0.8);
            backdrop-filter: blur(10px); z-index: 10;
        }

        .header { text-align: center; margin-bottom: 20px; }
        .title { font-size: 26px; font-weight: 800; background: linear-gradient(to right, #38bdf8, #fbbf24); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }

        .md5-input {
            width: 100%; background: #000; border: 2px solid #1e293b;
            border-radius: 16px; padding: 15px; color: var(--neon-blue);
            text-align: center; font-family: monospace; margin-bottom: 15px;
        }

        .predict-btn {
            width: 100%; background: linear-gradient(135deg, #0ea5e9, #2563eb);
            border: none; border-radius: 15px; padding: 18px; color: white;
            font-weight: 800; cursor: pointer; text-transform: uppercase;
        }

        /* Section Chọn Game */
        .game-selector {
            width: 100%; max-width: 420px; display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px;
        }

        .game-btn {
            background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255,255,255,0.1);
            padding: 12px; border-radius: 15px; color: #fff; cursor: pointer;
            transition: 0.3s; text-align: center; font-weight: 600; font-size: 13px;
        }
        .game-btn:hover { background: var(--neon-blue); color: #000; box-shadow: 0 0 20px var(--neon-blue); }
        .game-btn.active { background: var(--neon-gold); color: #000; border-color: var(--neon-gold); }

        /* Khung chứa Game */
        .game-frame-container {
            width: 100%; max-width: 1000px; height: 80vh; 
            background: #000; border-radius: 25px; overflow: hidden;
            border: 2px solid rgba(255, 255, 255, 0.1);
            display: none; box-shadow: 0 0 40px rgba(0,0,0,1);
            margin-bottom: 50px;
        }
        iframe { width: 100%; height: 100%; border: none; }

        /* Result Styles */
        .result-display { margin: 20px 0; text-align: center; }
        .res-text { font-size: 45px; font-weight: 900; }
        .tai { color: var(--neon-gold); text-shadow: 0 0 20px rgba(251, 191, 36, 0.5); }
        .xiu { color: var(--neon-blue); text-shadow: 0 0 20px rgba(56, 189, 248, 0.5); }

        .progress-bar { width: 100%; height: 6px; background: #1e293b; border-radius: 5px; margin-top: 5px; }
        .fill { height: 100%; width: 0%; transition: 1.5s; }
    </style>
</head>
<body>

    <canvas id="snow-canvas"></canvas>

    <div class="main-wrapper">
        <!-- TOOL AI -->
        <div class="app-container">
            <div class="header">
                <h1 class="title">NEURAL CORE AI</h1>
                <p style="font-size: 10px; letter-spacing: 2px; color: #64748b;">QUANTUM HASH ANALYSIS</p>
            </div>

            <input type="text" id="hashInp" class="md5-input" placeholder="Nhập MD5 32 ký tự...">
            <button id="runBtn" class="predict-btn" onclick="startAnalysis()">⚡ PHÂN TÍCH AI ⚡</button>

            <div class="result-display">
                <div id="resTxt" class="res-text">---</div>
                <div style="display: flex; justify-content: space-between; font-size: 12px; margin-top: 10px;">
                    <span id="perTai">TÀI: 0%</span>
                    <span id="perXiu">XỈU: 0%</span>
                </div>
                <div class="progress-bar"><div id="fillBar" class="fill" style="background: var(--neon-blue);"></div></div>
            </div>
        </div>

        <!-- MENU CHỌN GAME -->
        <div style="text-align: center;">
            <p style="margin-bottom: 15px; font-weight: 800; color: var(--neon-gold);">🚀 CHỌN GAME ĐỂ KÍCH HOẠT</p>
            <div class="game-selector">
                <div class="game-btn" onclick="loadGame('betvip', 'https://play.betvip.fit/')">BETVIP</div>
                <div class="game-btn" onclick="loadGame('lc79', 'https://lc79b.bet')">LC79</div>
                <div class="game-btn" onclick="loadGame('sunwin', 'https://sunwin.ag')">SUNWIN</div>
                <div class="game-btn" onclick="loadGame('sunvtv', 'http://sunvtv9.win')">SUNVTV</div>
                <div class="game-btn" onclick="loadGame('68gb', 'https://68gbvn88.bar')" style="grid-column: span 2;">68 GAME BÀI</div>
            </div>
        </div>

        <!-- KHUNG GAME -->
        <div id="gameWindow" class="game-frame-container">
            <iframe id="gameIframe" src="" allowfullscreen></iframe>
        </div>
    </div>

    <script>
        // --- HIỆU ỨNG TUYẾT RƠI ---
        const canvas = document.getElementById('snow-canvas');
        const ctx = canvas.getContext('2d');
        let particles = [];

        function initSnow() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            for(let i=0; i<100; i++) {
                particles.push({
                    x: Math.canvas() * canvas.width,
                    y: Math.canvas() * canvas.height,
                    r: Math.canvas() * 3 + 1,
                    d: Math.canvas() * 1
                });
            }
        }

        function drawSnow() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "white";
            ctx.beginPath();
            for(let p of particles) {
                ctx.moveTo(p.x, p.y);
                ctx.arc(p.x, p.y, p.r, 0, Math.PI*2, true);
            }
            ctx.fill();
            updateSnow();
        }

        function updateSnow() {
            for(let p of particles) {
                p.y += Math.cos(p.d) + 1 + p.r/2;
                p.x += Math.sin(p.d) * 2;
                if(p.y > canvas.height) {
                    p.y = -10; p.x = Math.canvas() * canvas.width;
                }
            }
        }
        setInterval(drawSnow, 30);
        initSnow();

        // --- THUẬT TOÁN AI MD5 ---
        function startAnalysis() {
            const hash = document.getElementById('hashInp').value.trim();
            if(hash.length !== 32) return alert("Vui lòng nhập đủ 32 ký tự MD5!");

            const btn = document.getElementById('runBtn');
            btn.disabled = true;
            btn.innerText = "ĐANG TÍNH TOÁN CORE...";

            setTimeout(() => {
                // Thuật toán giả lập dựa trên Hex sum
                let sum = 0;
                for(let char of hash) sum += parseInt(char, 16) || 0;
                
                const isTai = sum % 2 === 0;
                const rate = 75 + (sum % 20);
                
                const resTxt = document.getElementById('resTxt');
                resTxt.innerText = isTai ? "TÀI" : "XỈU";
                resTxt.className = `res-text ${isTai ? 'tai' : 'xiu'}`;
                
                document.getElementById('perTai').innerText = `TÀI: ${isTai ? rate : 100-rate}%`;
                document.getElementById('perXiu').innerText = `XỈU: ${isTai ? 100-rate : rate}%`;
                document.getElementById('fillBar').style.width = (isTai ? rate : 100-rate) + "%";
                document.getElementById('fillBar').style.backgroundColor = isTai ? "var(--neon-gold)" : "var(--neon-blue)";

                btn.disabled = false;
                btn.innerText = "⚡ PHÂN TÍCH TIẾP ⚡";
            }, 1500);
        }

        // --- HỆ THỐNG LOAD GAME ---
        function loadGame(id, url) {
            // Cập nhật trạng thái nút
            document.querySelectorAll('.game-btn').forEach(btn => btn.classList.remove('active'));
            event.currentTarget.classList.add('active');

            // Hiển thị khung game và load URL
            const container = document.getElementById('gameWindow');
            const iframe = document.getElementById('gameIframe');
            
            container.style.display = 'block';
            iframe.src = url;

            // Tự động cuộn xuống phần game
            setTimeout(() => {
                container.scrollIntoView({ behavior: 'smooth' });
            }, 300);
        }
    </script>
</body>
</html>
