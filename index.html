<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no, viewport-fit=cover">
<title>Süper Macera</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;-webkit-user-select:none;user-select:none}
html,body{width:100%;height:100%;overflow:hidden;background:#07131a;touch-action:none}
body{font-family:Arial,Helvetica,sans-serif;display:flex;justify-content:center}
#game{position:relative;width:100vw;height:100vh;overflow:hidden;background:#75c8ed}
canvas{position:absolute;inset:0;width:100%;height:100%;display:block}
.ui{position:absolute;inset:0;pointer-events:none}
.screen{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:24px;background:linear-gradient(180deg,rgba(4,18,27,.30),rgba(4,12,18,.88));color:white;pointer-events:auto}
.screen.hidden{display:none}
.logo{font-size:clamp(42px,13vw,76px);font-weight:1000;letter-spacing:2px;color:#fff;text-shadow:0 5px 0 #172b31,0 8px 20px #0009;margin-bottom:12px}
.subtitle{font-size:16px;opacity:.9;margin-bottom:28px}
.menuButton,.resultButton{width:min(270px,80vw);padding:16px 22px;margin:7px;border:0;border-radius:16px;font-size:21px;font-weight:900;letter-spacing:.5px;color:#132018;background:#f4c934;box-shadow:0 5px 0 #8b6812,0 10px 22px #0006}
.menuButton:active,.resultButton:active{transform:translateY(4px);box-shadow:0 1px 0 #8b6812}
#settings{background:#59656a;color:#fff;box-shadow:0 5px 0 #333;position:relative}
.notice{position:absolute;bottom:13%;left:50%;transform:translateX(-50%) translateY(10px);background:#121b20ee;border:1px solid #ffffff33;padding:13px 18px;border-radius:14px;font-weight:800;opacity:0;transition:.18s;white-space:nowrap;pointer-events:none}
.notice.show{opacity:1;transform:translateX(-50%) translateY(0)}
#hud{position:absolute;top:max(10px,env(safe-area-inset-top));left:0;right:0;display:flex;justify-content:space-between;padding:8px 13px;color:#fff;font-weight:900;font-size:16px;text-shadow:2px 2px 4px #000;pointer-events:none}
#hud .title{position:absolute;left:50%;transform:translateX(-50%);top:5px;font-size:18px;letter-spacing:1px}
#hud.hidden{display:none}
#controls{position:absolute;left:0;right:0;bottom:max(70px,env(safe-area-inset-bottom));display:flex;justify-content:space-between;align-items:end;padding:0 16px;pointer-events:none}
#controls.hidden{display:none}
.controlGroup{display:flex;gap:10px}
.control{width:67px;height:67px;border-radius:21px;border:2px solid #ffffff77;background:#12212acc;color:#fff;display:flex;align-items:center;justify-content:center;font-size:30px;font-weight:900;box-shadow:0 6px 14px #0007;pointer-events:auto;touch-action:none}
#jump{width:78px;height:78px;border-radius:50%;background:#1767a8cc}
.control.down{transform:translateY(3px);background:#ffffff44}
#levelScreen h2{font-size:34px;margin-bottom:12px}
.levelGrid{display:grid;grid-template-columns:repeat(4,64px);gap:11px;margin:12px 0 20px}
.level{height:64px;border:0;border-radius:16px;font-size:20px;font-weight:1000;background:#33464e;color:#fff;box-shadow:0 4px 0 #17242a}
.level.unlocked{background:#36a965}
.level:active{transform:translateY(3px);box-shadow:0 1px 0 #17242a}
.level.locked{opacity:.5}
#result h2{font-size:clamp(30px,9vw,52px);margin-bottom:8px;text-shadow:0 4px 0 #183026}
#result p{font-size:17px;line-height:1.5;margin-bottom:15px}
.small{font-size:13px;opacity:.72;margin-top:5px}
</style>
</head>
<body>
<div id="game">
<canvas id="canvas"></canvas>

<div id="hud" class="hidden">
  <span id="coinHud">🪙 0</span>
  <span class="title">SÜPER MACERA</span>
  <span id="lifeHud">❤️ 3</span>
</div>

<div id="controls" class="hidden">
  <div class="controlGroup">
    <div class="control" id="left">◀</div>
    <div class="control" id="right">▶</div>
  </div>
  <div class="control" id="jump">▲</div>
</div>

<div id="mainMenu" class="screen">
  <div class="logo">SÜPER MACERA</div>
  <div class="subtitle">Kısa, kolay ve macera dolu ilk bölüm</div>
  <button class="menuButton" id="startBtn">BAŞLA</button>
  <button class="menuButton" id="settings">AYARLAR</button>
  <div class="notice" id="notice">Bu özellik gelecek güncellemede eklenecek.</div>
</div>

<div id="levelScreen" class="screen hidden">
  <div class="logo" style="font-size:42px">BÖLÜMLER</div>
  <div class="subtitle">Toplam 8 bölüm</div>
  <div class="levelGrid" id="levelGrid"></div>
  <button class="menuButton" id="levelBack">ANA MENÜ</button>
</div>

<div id="result" class="screen hidden">
  <h2>🎉 TEBRİKLER!</h2>
  <p>Bölümü tamamladınız!<br><b>Asansör güvenle kapandı.</b></p>
  <button class="resultButton" id="replay">YENİDEN OYNA</button>
  <button class="resultButton" id="next">SIRADAKİ BÖLÜM</button>
  <button class="resultButton" id="toMenu">ANA MENÜ</button>
  <div class="small">2. bölüm henüz hazırlanmadı.</div>
</div>

<div id="gameOver" class="screen hidden">
  <h2>💥 OYUN BİTTİ</h2>
  <p>Yaratığa çarptın veya parkurdan düştün.</p>
  <button class="resultButton" id="retry">YENİDEN OYNA</button>
  <button class="resultButton" id="overMenu">ANA MENÜ</button>
</div>
</div>

<script>
(() => {
'use strict';

const canvas=document.getElementById('canvas');
const ctx=canvas.getContext('2d');
let W=innerWidth,H=innerHeight,dpr=Math.min(devicePixelRatio||1,2);
function resize(){
  W=innerWidth; H=innerHeight;
  canvas.width=Math.floor(W*dpr); canvas.height=Math.floor(H*dpr);
  canvas.style.width=W+'px'; canvas.style.height=H+'px';
  ctx.setTransform(dpr,0,0,dpr,0,0);
}
addEventListener('resize',resize,{passive:true}); resize();

const mainMenu=document.getElementById('mainMenu');
const levelScreen=document.getElementById('levelScreen');
const result=document.getElementById('result');
const gameOver=document.getElementById('gameOver');
const hud=document.getElementById('hud');
const controls=document.getElementById('controls');
const notice=document.getElementById('notice');
const coinHud=document.getElementById('coinHud');
const lifeHud=document.getElementById('lifeHud');

let running=false, level=1, cameraX=0, coins=0, lives=3, last=0;
let player, platforms=[], enemies=[], gold=[], clouds=[], trees=[], elevator, particles=[];
const input={left:false,right:false};

function hideScreens(){
  mainMenu.classList.add('hidden'); levelScreen.classList.add('hidden');
  result.classList.add('hidden'); gameOver.classList.add('hidden');
}
function openMenu(){
  running=false; hideScreens(); mainMenu.classList.remove('hidden');
  hud.classList.add('hidden'); controls.classList.add('hidden');
}
function openLevels(){
  running=false; hideScreens(); levelScreen.classList.remove('hidden');
  hud.classList.add('hidden'); controls.classList.add('hidden');
}
function showNotice(){
  notice.classList.add('show');
  clearTimeout(showNotice.timer);
  showNotice.timer=setTimeout(()=>notice.classList.remove('show'),1500);
}

document.getElementById('settings').addEventListener('click',e=>{e.preventDefault();showNotice()});
document.getElementById('startBtn').addEventListener('click',()=>openLevels());
document.getElementById('levelBack').addEventListener('click',openMenu);

const grid=document.getElementById('levelGrid');
for(let i=1;i<=8;i++){
  const b=document.createElement('button');
  b.className='level '+(i===1?'unlocked':'locked');
  b.textContent=i+(i===1?'':' 🔒');
  if(i===1)b.addEventListener('click',()=>startLevel(1));
  else b.addEventListener('click',showNotice);
  grid.appendChild(b);
}

function startLevel(n){
  level=n; coins=0; lives=3; cameraX=0; particles=[];
  buildLevel();
  hideScreens(); hud.classList.remove('hidden'); controls.classList.remove('hidden');
  running=true; updateHud();
}

function buildLevel(){
  platforms=[
    {x:-100,y:610,w:610,h:220},
    {x:650,y:545,w:190,h:285},
    {x:890,y:600,w:300,h:230},
    {x:1260,y:505,w:190,h:325},
    {x:1500,y:585,w:260,h:245},
    {x:1810,y:525,w:180,h:305},
    {x:2050,y:610,w:430,h:220},
    {x:2540,y:550,w:230,h:280},
    {x:2830,y:610,w:480,h:220},
    {x:3370,y:500,w:190,h:330},
    {x:3620,y:585,w:270,h:245},
    {x:3960,y:610,w:500,h:220}
  ];

  enemies=[
    {x:990,y:552,w:43,h:48,min:910,max:1135,v:0.9,type:0},
    {x:1580,y:537,w:45,h:48,min:1510,max:1715,v:-0.8,type:1},
    {x:2150,y:562,w:46,h:48,min:2070,max:2380,v:1.0,type:2},
    {x:2910,y:562,w:45,h:48,min:2850,max:3240,v:-0.85,type:0},
    {x:3680,y:537,w:46,h:48,min:3630,max:3850,v:0.9,type:1}
  ];

  gold=[];
  const addCoins=(x,y,count,spacing=50)=>{
    for(let i=0;i<count;i++)gold.push({x:x+i*spacing,y:y-(i%2)*15,r:10,taken:false,phase:Math.random()*6.28});
  };
  addCoins(250,550,4);
  addCoins(680,485,2);
  addCoins(930,545,3);
  addCoins(1285,445,2);
  addCoins(1530,530,3);
  addCoins(2070,555,5);
  addCoins(2570,500,3);
  addCoins(2870,555,4);
  addCoins(3400,440,2);
  addCoins(3650,530,3);
  addCoins(4010,555,5);

  elevator={x:4380,y:480,w:82,h:160,closed:0,inside:false,done:false};
  player={x:70,y:530,w:34,h:58,vx:0,vy:0,onGround:false,inv:0,face:1};

  clouds=Array.from({length:14},(_,i)=>({x:i*360+Math.random()*100,y:55+Math.random()*150,s:.7+Math.random()*.7}));
  trees=Array.from({length:32},(_,i)=>({x:i*145+Math.random()*80,y:500+Math.random()*20,s:.65+Math.random()*.55}));
}

function updateHud(){
  coinHud.textContent='🪙 '+coins;
  lifeHud.textContent='❤️ '+lives;
}

function overlap(a,b){
  return a.x<b.x+b.w && a.x+a.w>b.x && a.y<b.y+b.h && a.y+a.h>b.y;
}

function stompOrDie(e){
  const wasAbove=player.y+player.h-player.vy <= e.y+10;
  if(player.vy>0 && wasAbove){
    player.y=e.y-player.h; player.vy=-8.5;
    e.dead=true; coins+=2; burst(e.x+e.w/2,e.y+20,12);
  }else if(player.inv<=0){
    loseLife();
  }
}

function loseLife(){
  lives--; updateHud(); burst(player.x+17,player.y+25,18);
  if(lives<=0){running=false;controls.classList.add('hidden');gameOver.classList.remove('hidden');return}
  player.x=Math.max(40,player.x-220); player.y=400; player.vy=0; player.inv=90;
}

function update(dt){
  if(!running)return;

  const accel=0.7, maxSpeed=4.4;
  if(input.left)player.vx-=accel*dt;
  if(input.right)player.vx+=accel*dt;
  if(!input.left&&!input.right)player.vx*=Math.pow(.78,dt);
  player.vx=Math.max(-maxSpeed,Math.min(maxSpeed,player.vx));
  if(player.vx!==0)player.face=player.vx>0?1:-1;

  const oldBottom=player.y+player.h;
  player.vy+=0.62*dt;
  player.x+=player.vx*dt;
  player.y+=player.vy*dt;
  player.onGround=false;

  for(const p of platforms){
    if(player.x+player.w>p.x && player.x<p.x+p.w &&
       oldBottom<=p.y+7 && player.y+player.h>=p.y && player.vy>=0){
      player.y=p.y-player.h; player.vy=0; player.onGround=true;
    }
  }

  if(player.inv>0)player.inv-=dt;

  for(const e of enemies){
    if(e.dead)continue;
    e.x+=e.v*dt;
    if(e.x<e.min||e.x>e.max)e.v*=-1;
    if(overlap(player,e))stompOrDie(e);
  }
  enemies=enemies.filter(e=>!e.dead);

  for(const g of gold){
    if(g.taken)continue;
    const gy=g.y+Math.sin(performance.now()/300+g.phase)*4;
    if(Math.hypot(player.x+17-g.x,player.y+27-gy)<31){
      g.taken=true;coins++;burst(g.x,gy,7);updateHud();
    }
  }

  if(player.x+player.w>elevator.x+8 && player.x<elevator.x+elevator.w-8 &&
     player.y+player.h>elevator.y && player.y<elevator.y+elevator.h && !elevator.inside){
      elevator.inside=true;
  }
  if(elevator.inside && !elevator.done){
    elevator.closed=Math.min(1,elevator.closed+dt/30);
    if(elevator.closed>=1){
      elevator.done=true; running=false;
      controls.classList.add('hidden');
      result.classList.remove('hidden');
    }
  }

  if(player.y>H+140)loseLife();

  const target=player.x-W*.38;
  cameraX+=(target-cameraX)*.11;
  cameraX=Math.max(0,Math.min(cameraX,4100));

  for(const p of particles){
    p.x+=p.vx*dt;p.y+=p.vy*dt;p.vy+=.13*dt;p.life-=dt;
  }
  particles=particles.filter(p=>p.life>0);
}

function burst(x,y,n){
  for(let i=0;i<n;i++)particles.push({x,y,vx:(Math.random()-.5)*4,vy:-Math.random()*4-1,life:35+Math.random()*25});
}

function draw(){
  ctx.clearRect(0,0,W,H);

  const sky=ctx.createLinearGradient(0,0,0,H);
  sky.addColorStop(0,'#55b9eb');sky.addColorStop(.58,'#bde9e5');sky.addColorStop(1,'#eef4cf');
  ctx.fillStyle=sky;ctx.fillRect(0,0,W,H);

  ctx.fillStyle='#fff4a6';ctx.beginPath();ctx.arc(W*.78,100,42,0,Math.PI*2);ctx.fill();
  ctx.fillStyle='#79ad83';ctx.beginPath();
  for(let x=-700;x<7000;x+=480){
    const sx=x-cameraX*.25;
    ctx.moveTo(sx,H*.63);ctx.quadraticCurveTo(sx+240,H*.43,sx+480,H*.63);
  }
  ctx.lineTo(7000,H);ctx.lineTo(-700,H);ctx.fill();

  ctx.save();
  for(const c of clouds){
    const x=c.x-cameraX*.18;
    drawCloud(x,c.y,c.s);
  }

  ctx.translate(-cameraX,0);
  for(const t of trees)drawTree(t.x,t.y,t.s);
  for(const p of platforms)drawPlatform(p);
  for(const g of gold)if(!g.taken)drawGold(g);
  for(const e of enemies)if(!e.dead)drawEnemy(e);
  drawElevator();
  drawPlayer();

  for(const p of particles){
    ctx.globalAlpha=Math.max(0,p.life/45);
    ctx.fillStyle='#fff3a0';ctx.fillRect(p.x,p.y,5,5);
    ctx.globalAlpha=1;
  }
  ctx.restore();

  if(player && player.x>3900 && !elevator.inside){
    ctx.fillStyle='#fff';ctx.font='900 17px Arial';ctx.textAlign='center';
    ctx.fillText('ASANSÖR →',W*.72,105);ctx.textAlign='left';
  }
}

function drawCloud(x,y,s){
  ctx.fillStyle='#ffffffbb';ctx.beginPath();
  ctx.arc(x,y,22*s,0,Math.PI*2);ctx.arc(x+24*s,y-13*s,29*s,0,Math.PI*2);
  ctx.arc(x+54*s,y,23*s,0,Math.PI*2);ctx.fill();
}

function drawTree(x,y,s){
  ctx.fillStyle='#664329';ctx.fillRect(x-9*s,y,18*s,115*s);
  ctx.fillStyle='#2d7541';ctx.beginPath();
  ctx.arc(x,y,43*s,0,Math.PI*2);ctx.arc(x-30*s,y+22*s,29*s,0,Math.PI*2);
  ctx.arc(x+30*s,y+23*s,31*s,0,Math.PI*2);ctx.fill();
  ctx.fillStyle='#5bb05c';ctx.beginPath();ctx.arc(x-13*s,y-17*s,24*s,0,Math.PI*2);ctx.fill();
}

function drawPlatform(p){
  ctx.fillStyle='#6a4529';ctx.fillRect(p.x,p.y,p.w,p.h);
  ctx.fillStyle='#38a449';ctx.fillRect(p.x,p.y,p.w,17);
  ctx.fillStyle='#63c75e';
  for(let x=p.x;x<p.x+p.w;x+=13){
    ctx.beginPath();ctx.moveTo(x,p.y+2);ctx.lineTo(x+4,p.y-8);ctx.lineTo(x+6,p.y+2);ctx.fill();
  }
  ctx.fillStyle='#8b5a35';
  for(let x=p.x+12;x<p.x+p.w;x+=45){
    ctx.beginPath();ctx.arc(x,p.y+45,5,0,Math.PI*2);ctx.fill();
  }
}

function drawGold(g){
  const y=g.y+Math.sin(performance.now()/300+g.phase)*4;
  ctx.fillStyle='#f7c928';ctx.beginPath();ctx.arc(g.x,y,11,0,Math.PI*2);ctx.fill();
  ctx.strokeStyle='#a06e00';ctx.lineWidth=2;ctx.stroke();
  ctx.fillStyle='#fff6a8';ctx.beginPath();ctx.arc(g.x-3,y-3,3,0,Math.PI*2);ctx.fill();
}

function drawEnemy(e){
  const colors=['#7343a9','#c34c38','#287f78'];
  ctx.fillStyle=colors[e.type];
  ctx.beginPath();ctx.ellipse(e.x+22,e.y+28,23,22,0,0,Math.PI*2);ctx.fill();
  ctx.fillStyle=colors[e.type];
  ctx.beginPath();ctx.moveTo(e.x+5,e.y+13);ctx.lineTo(e.x+12,e.y-3);ctx.lineTo(e.x+19,e.y+14);ctx.fill();
  ctx.beginPath();ctx.moveTo(e.x+25,e.y+14);ctx.lineTo(e.x+34,e.y-3);ctx.lineTo(e.x+40,e.y+15);ctx.fill();
  ctx.fillStyle='#fff';ctx.beginPath();ctx.arc(e.x+14,e.y+23,7,0,Math.PI*2);ctx.arc(e.x+31,e.y+23,7,0,Math.PI*2);ctx.fill();
  ctx.fillStyle='#171717';ctx.beginPath();ctx.arc(e.x+14,e.y+23,3,0,Math.PI*2);ctx.arc(e.x+31,e.y+23,3,0,Math.PI*2);ctx.fill();
  ctx.fillStyle='#222';ctx.fillRect(e.x+7,e.y+46,11,5);ctx.fillRect(e.x+28,e.y+46,11,5);
}

function drawPlayer(){
  if(!player)return;
  if(player.inv>0 && Math.floor(player.inv/7)%2===0)return;

  ctx.fillStyle='#158c45';ctx.fillRect(player.x+4,player.y+2,27,14);
  ctx.fillStyle='#0c6330';ctx.fillRect(player.x+1,player.y+12,34,6);
  ctx.fillStyle='#ffd0a1';ctx.fillRect(player.x+8,player.y+17,21,22);
  ctx.fillStyle='#3b2419';ctx.fillRect(player.x+8,player.y+17,21,6);
  ctx.fillStyle='#111';ctx.fillRect(player.x+(player.face>0?24:8),player.y+27,3,3);
  ctx.fillStyle='#158c45';ctx.fillRect(player.x+5,player.y+38,25,17);
  ctx.fillStyle='#0b5d30';ctx.fillRect(player.x+1,player.y+53,14,7);ctx.fillRect(player.x+22,player.y+53,14,7);
  ctx.fillStyle='#f2d63b';ctx.fillRect(player.x+10,player.y+40,4,4);ctx.fillRect(player.x+22,player.y+40,4,4);
}

function drawElevator(){
  const e=elevator;
  ctx.fillStyle='#38434a';ctx.fillRect(e.x,e.y,e.w,e.h);
  ctx.fillStyle='#8e9aa0';ctx.fillRect(e.x+5,e.y+5,e.w-10,e.h-10);
  ctx.fillStyle='#202a30';ctx.fillRect(e.x+10,e.y+15,e.w-20,e.h-20);
  const gap=(e.w-20)/2*(1-e.closed);
  ctx.fillStyle='#aeb8bd';
  ctx.fillRect(e.x+10,e.y+15,gap,e.h-20);
  ctx.fillRect(e.x+e.w-10-gap,e.y+15,gap,e.h-20);
  ctx.fillStyle='#ffd43b';ctx.fillRect(e.x+e.w/2-4,e.y+25,8,10);
  ctx.fillStyle='#dff7ff';ctx.fillRect(e.x+e.w/2-3,e.y+7,6,4);
}

function jump(){
  if(running && player.onGround){player.vy=-12.5;player.onGround=false;burst(player.x+17,player.y+57,4)}
}

function bindHold(id,key){
  const el=document.getElementById(id);
  const press=e=>{e.preventDefault();input[key]=true;el.classList.add('down');try{el.setPointerCapture(e.pointerId)}catch(_){}};
  const release=e=>{e.preventDefault();input[key]=false;el.classList.remove('down')};
  el.addEventListener('pointerdown',press,{passive:false});
  el.addEventListener('pointerup',release,{passive:false});
  el.addEventListener('pointercancel',release,{passive:false});
  el.addEventListener('lostpointercapture',release,{passive:false});
}
bindHold('left','left');bindHold('right','right');

const jumpEl=document.getElementById('jump');
jumpEl.addEventListener('pointerdown',e=>{e.preventDefault();jump();jumpEl.classList.add('down');try{jumpEl.setPointerCapture(e.pointerId)}catch(_){}},{passive:false});
['pointerup','pointercancel','lostpointercapture'].forEach(ev=>jumpEl.addEventListener(ev,e=>{e.preventDefault();jumpEl.classList.remove('down')},{passive:false}));

addEventListener('keydown',e=>{
  if(e.key==='ArrowLeft'||e.key.toLowerCase()==='a')input.left=true;
  if(e.key==='ArrowRight'||e.key.toLowerCase()==='d')input.right=true;
  if(e.key==='ArrowUp'||e.key===' '||e.key.toLowerCase()==='w'){e.preventDefault();jump()}
});
addEventListener('keyup',e=>{
  if(e.key==='ArrowLeft'||e.key.toLowerCase()==='a')input.left=false;
  if(e.key==='ArrowRight'||e.key.toLowerCase()==='d')input.right=false;
});

document.getElementById('replay').addEventListener('click',()=>startLevel(1));
document.getElementById('retry').addEventListener('click',()=>startLevel(1));
document.getElementById('toMenu').addEventListener('click',openMenu);
document.getElementById('overMenu').addEventListener('click',openMenu);
document.getElementById('next').addEventListener('click',showNotice);

function frame(t){
  const dt=Math.min(2,(t-last)/16.666||1);last=t;
  update(dt);draw();requestAnimationFrame(frame);
}
buildLevel();requestAnimationFrame(frame);
})();
</script>
</body>
</html>
