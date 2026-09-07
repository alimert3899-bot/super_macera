<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Süper Macera - Mario</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            user-select: none;
            -webkit-user-select: none;
        }
        body {
            background-color: #111;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        #game-container {
            position: relative;
            width: 100vw;
            max-width: 420px;
            height: 100vh;
            max-height: 750px;
            background: linear-gradient(to bottom, #3a7bd5, #3a6073);
            box-shadow: 0 0 25px rgba(0,0,0,0.9);
            overflow: hidden;
        }
        canvas {
            width: 100%;
            height: 100%;
            display: block;
        }

        /* OYUN İÇİ ARAYÜZ (HUD) */
        .hud {
            position: absolute;
            top: 15px;
            left: 15px;
            color: #fff;
            font-size: 18px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
            z-index: 10;
            display: none;
        }
        .controls {
            position: absolute;
            bottom: 20px;
            width: 100%;
            padding: 0 20px;
            display: none;
            justify-content: space-between;
            align-items: center;
            z-index: 10;
        }
        .d-pad {
            display: flex;
            gap: 15px;
        }
        .btn {
            width: 65px;
            height: 65px;
            background: rgba(255, 255, 255, 0.25);
            border: 2px solid rgba(255, 255, 255, 0.5);
            border-radius: 50%;
            color: white;
            font-size: 24px;
            font-weight: bold;
            display: flex;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(5px);
            touch-action: manipulation;
            cursor: pointer;
        }
        .btn:active {
            background: rgba(255, 255, 255, 0.5);
            transform: scale(0.95);
        }
        .btn-jump {
            width: 75px;
            height: 75px;
            background: rgba(231, 76, 60, 0.6);
            border-color: rgba(255, 255, 255, 0.7);
        }

        /* EKRAN MODALLARI & MENÜLER */
        .screen {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.95);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: white;
            z-index: 30;
            text-align: center;
            padding: 20px;
        }
        .screen h1 {
            font-size: 36px;
            margin-bottom: 25px;
            color: #f1c40f;
            text-shadow: 0 4px 10px rgba(241, 196, 15, 0.4);
            letter-spacing: 1px;
        }

        .btn-main {
            width: 220px;
            padding: 15px;
            margin: 10px 0;
            font-size: 18px;
            font-weight: bold;
            color: white;
            background: #2ecc71;
            border: none;
            border-radius: 30px;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(46, 204, 113, 0.4);
            transition: all 0.2s;
        }
        .btn-main:active {
            transform: scale(0.96);
        }
        .btn-disabled {
            background: #475569 !important;
            color: #94a3b8 !important;
            box-shadow: none !important;
            cursor: not-allowed;
            opacity: 0.7;
        }

        /* BÖLÜM SEÇME GRID */
        .level-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
            width: 100%;
            max-width: 320px;
            margin-bottom: 25px;
        }
        .level-btn {
            aspect-ratio: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 18px;
            font-weight: bold;
            border-radius: 12px;
            border: 2px solid transparent;
            cursor: pointer;
        }
        .level-active {
            background: #e67e22;
            color: white;
            border-color: #f39c12;
            box-shadow: 0 0 15px rgba(230, 126, 34, 0.6);
        }
        .level-locked {
            background: #1e293b;
            color: #475569;
            border-color: #334155;
            cursor: not-allowed;
        }

        /* UYARI BİLDİRİMİ (TOAST) */
        #toast {
            position: absolute;
            bottom: 30px;
            background: #e74c3c;
            color: white;
            padding: 12px 20px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(0,0,0,0.5);
            display: none;
            z-index: 50;
            animation: fadeIn 0.3s ease;
        }

        .stars { font-size: 38px; margin: 10px 0; color: #f1c40f; }
    </style>
</head>
<body>

<div id="game-container">
    <div class="hud" id="hud">Altın: <span id="coin-count">0</span> / <span id="max-coins">0</span></div>
    <canvas id="canvas"></canvas>
    
    <!-- Ekran Üstü Kontroller -->
    <div class="controls" id="controls">
        <div class="d-pad">
            <div class="btn" id="btn-left">◄</div>
            <div class="btn" id="btn-right">►</div>
        </div>
        <div class="btn btn-jump" id="btn-jump">▲</div>
    </div>

    <!-- 1. ANA MENÜ -->
    <div id="main-menu" class="screen">
        <h1>SÜPER MACERA</h1>
        <button class="btn-main" onclick="openLevelSelect()">BAŞLA</button>
        <button class="btn-main btn-disabled" onclick="showToast('Ayarlar gelecek güncellemede eklenecektir!')">AYARLAR</button>
    </div>

    <!-- 2. BÖLÜM SEÇME MENÜSÜ -->
    <div id="level-menu" class="screen" style="display: none;">
        <h2 style="margin-bottom: 20px; color: #38bdf8;">Bölüm Seç</h2>
        <div class="level-grid" id="level-grid"></div>
        <button class="btn-main" style="width: 150px; background: #64748b;" onclick="openMainMenu()">Geri</button>
    </div>

    <!-- 3. GAME OVER EKRANI -->
    <div id="game-over" class="screen" style="display: none;">
        <h1 style="color: #e74c3c;">ÖLDÜN!</h1>
        <p style="margin-bottom: 20px; color: #cbd5e1;">Düştün veya Yaratığa Çarptın!</p>
        <button class="btn-main" onclick="restartGame()">Tekrar Oyna</button>
        <button class="btn-main" style="background: #64748b;" onclick="openMainMenu()">Ana Menü</button>
    </div>

    <!-- 4. KAZANMA EKRANI -->
    <div id="win-screen" class="screen" style="display: none;">
        <h1 style="color: #2ecc71;">TEBRİKLER!</h1>
        <p>Bölüm 1 Tamamlandı!</p>
        <div class="stars" id="star-rating">☆☆☆</div>
        <p id="coin-result-text" style="font-size: 14px; color: #cbd5e1; margin-bottom: 20px;"></p>
        
        <button class="btn-main" onclick="restartGame()">Tekrar Oyna</button>
        <button class="btn-main btn-disabled" onclick="showToast('Sıradaki bölüm gelecek güncellemede gelecek!')">Sıradaki Bölüm</button>
        <button class="btn-main" style="background: #64748b;" onclick="openMainMenu()">Ana Menü</button>
    </div>

    <!-- Bildirim Balonu -->
    <div id="toast"></div>
</div>

<script>
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');

// UI Elemanları
const hud = document.getElementById('hud');
const controls = document.getElementById('controls');
const mainMenu = document.getElementById('main-menu');
const levelMenu = document.getElementById('level-menu');
const gameOverScreen = document.getElementById('game-over');
const winScreen = document.getElementById('win-screen');
const levelGrid = document.getElementById('level-grid');
const coinDisplay = document.getElementById('coin-count');
const maxCoinsDisplay = document.getElementById('max-coins');
const starRating = document.getElementById('star-rating');
const coinResultText = document.getElementById('coin-result-text');
const toast = document.getElementById('toast');

canvas.width = 420;
canvas.height = 750;

let coins = 0;
let isGameOver = false;
let isGameWon = false;
let isPlaying = false;
let gameTime = 0;
let cameraX = 0;

const keys = { left: false, right: false, jump: false };
const gravity = 0.55;

// Karakter Fizikleri
const player = {
    x: 50, y: 500,
    width: 30, height: 46,
    vx: 0, vy: 0,
    speed: 2.8, jumpPower: -11.8,
    grounded: false
};

// --- HARİTA TASARIMI (Bölüm 1) ---
const platforms = [
    { x: 0, y: 640, width: 800, height: 110 },
    { x: 880, y: 640, width: 700, height: 110 },
    { x: 1640, y: 640, width: 600, height: 110 }
];

const movingPlatforms = [
    { x: 810, y: 550, width: 120, height: 20, startX: 810, endX: 860, vx: 0.6 }
];

const blocks = [
    { x: 300, y: 500, width: 40, height: 40, hit: false, bounce: 0 },
    { x: 500, y: 500, width: 40, height: 40, hit: false, bounce: 0 },
    { x: 1100, y: 500, width: 40, height: 40, hit: false, bounce: 0 }
];

let enemies = [
    { x: 1150, y: 605, width: 35, height: 35, vx: -0.8, minX: 950, maxX: 1350, alive: true }
];

const elevator = {
    x: 1950, y: 500, width: 70, height: 140,
    doorProgress: 0, isTriggered: false, timer: 0
};

let particles = [];
let grassBlades = [];

for (let i = 0; i < 2300; i += 4) {
    grassBlades.push({
        x: i,
        height: 12 + Math.random() * 10,
        speed: 0.05 + Math.random() * 0.05
    });
}

maxCoinsDisplay.innerText = blocks.length;

// --- MENÜ VE NAVİGASYON FONKSİYONLARI ---

function openMainMenu() {
    isPlaying = false;
    mainMenu.style.display = 'flex';
    levelMenu.style.display = 'none';
    gameOverScreen.style.display = 'none';
    winScreen.style.display = 'none';
    hud.style.display = 'none';
    controls.style.display = 'none';
}

function openLevelSelect() {
    mainMenu.style.display = 'none';
    levelMenu.style.display = 'flex';
    renderLevelGrid();
}

function renderLevelGrid() {
    levelGrid.innerHTML = '';
    for (let i = 1; i <= 15; i++) {
        const btn = document.createElement('div');
        btn.classList.add('level-btn');
        btn.innerText = i;
        
        if (i === 1) {
            btn.classList.add('level-active');
            btn.onclick = () => startLevel(1);
        } else {
            btn.classList.add('level-locked');
            btn.onclick = () => showToast('Bu bölüm gelecek güncellemede açılacaktır!');
        }
        levelGrid.appendChild(btn);
    }
}

function startLevel(levelNum) {
    levelMenu.style.display = 'none';
    hud.style.display = 'block';
    controls.style.display = 'flex';
    restartGame();
    isPlaying = true;
}

function showToast(msg) {
    toast.innerText = msg;
    toast.style.display = 'block';
    setTimeout(() => {
        toast.style.display = 'none';
    }, 2500);
}

// --- ÇİZİM VE OYUN MANTIĞI ---

function drawSun() {
    ctx.save();
    let gradient = ctx.createRadialGradient(340, 70, 10, 340, 70, 80);
    gradient.addColorStop(0, 'rgba(255, 255, 220, 1)');
    gradient.addColorStop(0.2, 'rgba(255, 220, 100, 0.8)');
    gradient.addColorStop(1, 'rgba(255, 200, 50, 0)');
    ctx.fillStyle = gradient;
    ctx.beginPath();
    ctx.arc(340, 70, 80, 0, Math.PI * 2);
    ctx.fill();
    ctx.restore();
}

function drawClouds() {
    ctx.fillStyle = 'rgba(255, 255, 255, 0.85)';
    [
        { x: 100, y: 80, scale: 0.9 },
        { x: 600, y: 120, scale: 1.1 },
        { x: 1200, y: 70, scale: 0.8 },
        { x: 1700, y: 110, scale: 1.0 }
    ].forEach(c => {
        let drawX = c.x - cameraX * 0.2;
        ctx.save();
        ctx.beginPath();
        ctx.arc(drawX, c.y, 20 * c.scale, 0, Math.PI * 2);
        ctx.arc(drawX + 25 * c.scale, c.y - 10 * c.scale, 25 * c.scale, 0, Math.PI * 2);
        ctx.arc(drawX + 50 * c.scale, c.y, 20 * c.scale, 0, Math.PI * 2);
        ctx.fill();
        ctx.restore();
    });
}

function drawPlatforms() {
    platforms.forEach(p => {
        let drawX = p.x - cameraX;
        let earthGrad = ctx.createLinearGradient(0, p.y, 0, p.y + p.height);
        earthGrad.addColorStop(0, '#5d4037');
        earthGrad.addColorStop(1, '#2d1b14');
        ctx.fillStyle = earthGrad;
        ctx.fillRect(drawX, p.y, p.width, p.height);

        ctx.fillStyle = '#2e7d32';
        ctx.fillRect(drawX, p.y - 4, p.width, 6);

        ctx.lineWidth = 2;
        grassBlades.forEach(blade => {
            if (blade.x >= p.x && blade.x <= p.x + p.width) {
                let bladeDrawX = blade.x - cameraX;
                let wind = Math.sin(gameTime * blade.speed + blade.x) * 4;
                let tipX = bladeDrawX + wind;
                let tipY = p.y - blade.height;

                let grad = ctx.createLinearGradient(bladeDrawX, p.y, tipX, tipY);
                grad.addColorStop(0, '#1b5e20');
                grad.addColorStop(1, '#76ff03');

                ctx.strokeStyle = grad;
                ctx.beginPath();
                ctx.moveTo(bladeDrawX, p.y);
                ctx.quadraticCurveTo(bladeDrawX, p.y - blade.height / 2, tipX, tipY);
                ctx.stroke();
            }
        });
    });

    movingPlatforms.forEach(mp => {
        let drawX = mp.x - cameraX;
        ctx.fillStyle = '#8e44ad';
        ctx.fillRect(drawX, mp.y, mp.width, mp.height);
        ctx.strokeStyle = '#9b59b6';
        ctx.lineWidth = 3;
        ctx.strokeRect(drawX, mp.y, mp.width, mp.height);
    });
}

function drawPlayer() {
    let drawX = player.x - cameraX;
    ctx.save();
    
    if (player.grounded) {
        ctx.fillStyle = 'rgba(0,0,0,0.3)';
        ctx.beginPath();
        ctx.ellipse(drawX + player.width/2, player.y + player.height, player.width/2, 4, 0, 0, Math.PI * 2);
        ctx.fill();
    }

    let bodyGrad = ctx.createLinearGradient(drawX, player.y, drawX + player.width, player.y + player.height);
    bodyGrad.addColorStop(0, '#00c6ff');
    bodyGrad.addColorStop(1, '#0072ff');
    ctx.fillStyle = bodyGrad;
    ctx.fillRect(drawX + 4, player.y + 16, player.width - 8, player.height - 16);

    let headGrad = ctx.createLinearGradient(drawX, player.y, drawX, player.y + 16);
    headGrad.addColorStop(0, '#11998e');
    headGrad.addColorStop(1, '#38ef7d');
    ctx.fillStyle = headGrad;
    ctx.beginPath();
    ctx.arc(drawX + player.width/2, player.y + 12, 12, 0, Math.PI * 2);
    ctx.fill();

    ctx.fillStyle = '#fff';
    ctx.fillRect(drawX + 18, player.y + 8, 4, 4);
    ctx.restore();
}

function drawBlocks() {
    blocks.forEach(b => {
        let drawX = b.x - cameraX;
        let drawY = b.y + b.bounce;

        ctx.save();
        if (b.hit) {
            ctx.fillStyle = '#7f8c8d';
            ctx.fillRect(drawX, drawY, b.width, b.height);
        } else {
            let grad = ctx.createLinearGradient(drawX, drawY, drawX + b.width, drawY + b.height);
            grad.addColorStop(0, '#f1c40f');
            grad.addColorStop(1, '#f39c12');
            ctx.fillStyle = grad;
            ctx.fillRect(drawX, drawY, b.width, b.height);

            ctx.fillStyle = '#fff';
            ctx.font = 'bold 22px Arial';
            ctx.fillText('?', drawX + 14, drawY + 28);
        }

        ctx.strokeStyle = 'rgba(0,0,0,0.3)';
        ctx.lineWidth = 3;
        ctx.strokeRect(drawX, drawY, b.width, b.height);
        ctx.restore();

        if (b.bounce < 0) b.bounce += 1;
    });
}

function drawEnemies() {
    enemies.forEach(e => {
        if (!e.alive) return;
        let drawX = e.x - cameraX;

        ctx.save();
        let grad = ctx.createRadialGradient(
            drawX + 15, e.y + 15, 5,
            drawX + 15, e.y + 15, 20
        );
        grad.addColorStop(0, '#ff4e50');
        grad.addColorStop(1, '#f9d423');

        ctx.fillStyle = grad;
        ctx.beginPath();
        ctx.arc(drawX + e.width/2, e.y + e.height/2, e.width/2, 0, Math.PI * 2);
        ctx.fill();

        ctx.fillStyle = '#000';
        ctx.fillRect(drawX + 8, e.y + 10, 5, 5);
        ctx.fillRect(drawX + 20, e.y + 10, 5, 5);
        ctx.restore();
    });
}

function drawElevator() {
    let drawX = elevator.x - cameraX;
    ctx.save();
    ctx.fillStyle = '#34495e';
    ctx.fillRect(drawX, elevator.y, elevator.width, elevator.height);
    
    ctx.fillStyle = '#111';
    ctx.fillRect(drawX + 5, elevator.y + 10, elevator.width - 10, elevator.height - 10);

    let doorWidth = (elevator.width - 10) / 2 * elevator.doorProgress;
    ctx.fillStyle = '#7f8c8d';
    ctx.fillRect(drawX + 5, elevator.y + 10, doorWidth, elevator.height - 10);
    ctx.fillRect(drawX + elevator.width - 5 - doorWidth, elevator.y + 10, doorWidth, elevator.height - 10);

    ctx.strokeStyle = '#ecf0f1';
    ctx.lineWidth = 4;
    ctx.strokeRect(drawX, elevator.y, elevator.width, elevator.height);
    ctx.restore();
}

function drawParticles() {
    particles.forEach((p, index) => {
        p.x += p.vx;
        p.y += p.vy;
        p.alpha -= 0.02;

        ctx.fillStyle = `rgba(${p.color || '241, 196, 15'}, ${p.alpha})`;
        ctx.beginPath();
        ctx.arc(p.x - cameraX, p.y, p.size, 0, Math.PI * 2);
        ctx.fill();

        if (p.alpha <= 0) particles.splice(index, 1);
    });
}

function update() {
    if (!isPlaying || isGameOver || isGameWon) return;

    gameTime += 0.05;

    if (keys.left) player.vx = -player.speed;
    else if (keys.right) player.vx = player.speed;
    else player.vx *= 0.65;

    player.vy += gravity;
    player.x += player.vx;
    player.y += player.vy;

    if (player.x - cameraX > 200) {
        cameraX = player.x - 200;
    } else if (player.x - cameraX < 80 && cameraX > 0) {
        cameraX = player.x - 80;
    }

    if (player.y > canvas.height + 100) {
        triggerGameOver();
    }

    movingPlatforms.forEach(mp => {
        mp.x += mp.vx;
        if (mp.x <= mp.startX || mp.x >= mp.endX) mp.vx *= -1;

        if (
            player.x + player.width > mp.x &&
            player.x < mp.x + mp.width &&
            player.y + player.height >= mp.y &&
            player.y + player.height <= mp.y + 10 &&
            player.vy >= 0
        ) {
            player.y = mp.y - player.height;
            player.vy = 0;
            player.grounded = true;
            player.x += mp.vx;
        }
    });

    player.grounded = false;
    platforms.forEach(p => {
        if (
            player.x + player.width > p.x &&
            player.x < p.x + p.width &&
            player.y + player.height >= p.y &&
            player.y + player.height <= p.y + 15 &&
            player.vy >= 0
        ) {
            player.y = p.y - player.height;
            player.vy = 0;
            player.grounded = true;
        }
    });

    if (keys.jump && player.grounded) {
        player.vy = player.jumpPower;
        player.grounded = false;
    }

    blocks.forEach(b => {
        if (
            player.x < b.x + b.width &&
            player.x + player.width > b.x &&
            player.y < b.y + b.height &&
            player.y + player.height > b.y
        ) {
            if (player.vy < 0 && player.y > b.y + b.height - 12) {
                player.vy = 2;
                if (!b.hit) {
                    b.hit = true;
                    b.bounce = -8;
                    coins++;
                    coinDisplay.innerText = coins;
                    spawnParticles(b.x + b.width/2, b.y, '241, 196, 15');
                }
            } else if (player.vy > 0 && player.y + player.height - player.vy <= b.y) {
                player.y = b.y - player.height;
                player.v
