<!doctype html>
<html lang="tr">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>Küçük Kaşif: Kayıp Ada</title>
<style>
:root{--panel:rgba(7,15,29,.94);--edge:#31496f;--text:#e8efff;--muted:#aebed9;--gold:#ffd36f;--blue:#45baff}
*{box-sizing:border-box}html,body{margin:0;width:100%;height:100%;overflow:hidden;background:#07101b;color:var(--text);font-family:Inter,system-ui,Arial,sans-serif;user-select:none;-webkit-user-select:none}
canvas{position:absolute;inset:0;width:100%;height:100%;image-rendering:pixelated;touch-action:none}
button{font:inherit;color:var(--text);background:linear-gradient(#172944,#0d1a2d);border:1px solid #405a80;border-radius:10px;padding:10px 12px;box-shadow:inset 0 1px #ffffff12;cursor:pointer}
button:active{transform:translateY(1px);filter:brightness(1.15)}
#top{position:absolute;top:12px;left:12px;right:12px;display:flex;gap:8px;align-items:flex-start;pointer-events:none}
.panel{background:var(--panel);border:1px solid var(--edge);border-radius:15px;box-shadow:0 8px 26px #0005,inset 0 1px #ffffff0a;backdrop-filter:blur(8px)}
#profile{display:flex;gap:10px;align-items:center;padding:9px 12px;width:270px;min-width:230px}
#portrait{width:52px;height:52px;border-radius:10px;display:grid;place-items:center;font-size:31px;background:linear-gradient(140deg,#344767,#17233a);border:1px solid #52698c}
.name{font-weight:800;letter-spacing:.1px}.muted{font-size:12px;color:var(--muted)}
.bar{height:8px;background:#243653;border-radius:20px;overflow:hidden}.bar>span{height:100%;display:block;background:linear-gradient(90deg,#218fe0,#4fd4ff);width:0%}
#resourceRow{display:flex;gap:7px;margin-left:auto;pointer-events:auto}
.resource{padding:11px 12px;min-width:83px;text-align:center;font-weight:750;font-size:14px}
#leftMenu{position:absolute;left:12px;top:130px;display:grid;gap:8px;width:145px}
.menuButton{text-align:left;display:flex;align-items:center;gap:9px;background:var(--panel);padding:12px 11px}
.menuButton span:first-child{font-size:23px}
#questPanel{position:absolute;right:12px;top:94px;width:245px;padding:14px}
#questPanel h3{margin:0 0 8px;font-size:16px}
.quest{padding:11px 0;border-top:1px solid #263954;font-size:12px;color:#d7e2f4}
.quest strong{display:block;color:var(--gold);font-size:13px;margin-bottom:7px}
.questLine{display:flex;justify-content:space-between;gap:8px;margin-top:5px;color:var(--muted)}
.qbar{height:5px;border-radius:8px;background:#1f304a;margin-top:8px;overflow:hidden}.qbar span{height:100%;display:block;background:linear-gradient(90deg,#2589e0,#42d2ff)}
#dialog{position:absolute;left:12px;bottom:73px;width:min(440px,calc(100vw - 24px));display:flex;gap:12px;align-items:center;padding:12px 14px}
#npcIcon{font-size:43px;width:52px;height:52px;display:grid;place-items:center;background:#182944;border-radius:12px;flex-shrink:0}
#dialogText{font-size:13px;line-height:1.5;color:#d0dcf0}#dialogText b{display:block;font-size:14px;color:#fff;margin-bottom:3px}
#hotbar{position:absolute;left:50%;bottom:12px;transform:translateX(-50%);display:flex;gap:4px;padding:5px;border-radius:13px;background:rgba(5,12,25,.94);border:1px solid #354c70;box-shadow:0 8px 24px #0006}
.slot{position:relative;width:56px;height:58px;border:1px solid #304867;border-radius:9px;background:linear-gradient(#172843,#0b172a);display:grid;place-items:center;font-size:25px}
.slot.selected{border-color:#ffce62;box-shadow:inset 0 0 0 1px #ffce6244}
.slot small{position:absolute;top:3px;left:5px;font-size:10px;color:#a8bad8}.slot b{position:absolute;right:5px;bottom:3px;font-size:11px;color:#f5f7ff}
#mapBox{position:absolute;right:12px;bottom:72px;width:160px;height:160px;padding:5px;overflow:hidden}
#mini{width:100%;height:100%;border-radius:9px;display:block}
#actionButtons{position:absolute;right:12px;bottom:245px;display:grid;gap:7px;width:150px}
#actionButtons button{background:rgba(7,18,33,.94);font-size:12px;font-weight:800}
#joystick{display:none;position:absolute;left:16px;bottom:22px;width:116px;height:116px;border-radius:50%;background:#08182c9c;border:2px solid #a8c9eb66;touch-action:none}
#knob{position:absolute;width:45px;height:45px;left:33px;top:33px;border-radius:50%;background:#a9d8f0aa;border:2px solid #e2f6ff;box-shadow:0 2px 10px #0005}
#toast{position:absolute;top:88px;left:50%;transform:translateX(-50%);max-width:90vw;padding:11px 16px;background:#071426f5;border:1px solid #65c6ef;border-radius:11px;font-size:13px;text-align:center;display:none;z-index:10}
#overlay{position:absolute;inset:0;z-index:30;background:radial-gradient(ellipse at 50% 42%,#142d3b88,#030914ed 75%);display:grid;place-items:center;padding:18px}
#intro{width:min(470px,100%);padding:28px;text-align:center;background:linear-gradient(145deg,#13233a,#091425);border:1px solid #4b7094;border-radius:22px;box-shadow:0 20px 70px #0009}
#intro .logo{font-size:53px}#intro h1{font-size:clamp(26px,6vw,38px);margin:6px 0;color:#b5f2bd;letter-spacing:1px}#intro .subtitle{color:var(--gold);font-weight:800;letter-spacing:4px;font-size:12px}
#intro p{color:#c7d6ea;font-size:14px;line-height:1.7;margin:18px 0}
#start{width:100%;padding:15px;background:linear-gradient(#b9f0bf,#7ecb92);color:#10251b;font-weight:900;border:0}
#modal{position:absolute;inset:0;z-index:25;background:#020813b9;display:grid;place-items:center;padding:18px}
#modal.hidden{display:none}#modalCard{width:min(430px,100%);max-height:80vh;overflow:auto;padding:20px;background:#0d1a2d;border:1px solid #46668b;border-radius:18px;box-shadow:0 15px 50px #0009}
#modalCard h2{margin:0 0 14px}#modalBody{line-height:1.8;font-size:14px;color:#d9e4f5}#modalBody button{margin:5px 0;width:100%}.close{width:100%;margin-top:12px}
#footerTip{position:absolute;left:12px;bottom:15px;color:#aebfda;font-size:12px;max-width:320px;pointer-events:none}
@media(max-width:700px){
 #top{top:7px;left:7px;right:7px;gap:5px}#profile{width:auto;min-width:0;flex:1;padding:6px 7px;gap:7px}#portrait{width:37px;height:37px;font-size:23px}.name{font-size:12px}.muted{font-size:10px}
 #resourceRow{gap:3px}.resource{min-width:0;padding:10px 6px;font-size:11px}
 #leftMenu{top:95px;left:7px;width:106px;gap:6px}.menuButton{padding:9px 7px;font-size:11px;gap:5px}.menuButton span:first-child{font-size:18px}
 #questPanel{top:95px;right:7px;width:166px;padding:8px}#questPanel h3{font-size:13px}.quest{padding:7px 0;font-size:10px}.quest strong{font-size:11px}
 #dialog{bottom:135px;left:7px;width:min(290px,calc(100vw - 14px));padding:8px;gap:7px}#npcIcon{width:39px;height:42px;font-size:30px}#dialogText{font-size:11px}
 #hotbar{bottom:7px;gap:2px;padding:3px}.slot{width:clamp(32px,8vw,43px);height:46px;font-size:19px}.slot small{font-size:9px}.slot b{font-size:9px}
 #mapBox{width:102px;height:102px;right:7px;bottom:7px;padding:3px}
 #actionButtons{right:7px;bottom:142px;width:112px;gap:5px}#actionButtons button{font-size:10px;padding:9px 3px}
 #joystick{display:block}#footerTip{display:none}
}
</style>
</head>
<body>
<canvas id="game"></canvas>

<div id="top">
 <div id="profile" class="panel">
  <div id="portrait">🧑🏻‍🌾</div>
  <div style="flex:1;min-width:0">
   <div class="name">Küçük Kaşif</div>
   <div style="display:flex;align-items:center;gap:8px;margin-top:5px"><span class="muted">Lv. <b id="level">1</b></span><div class="bar" style="flex:1"><span id="xpBar"></span></div></div>
   <div class="muted" style="margin-top:4px"><span id="xp">0</span> / 100 XP</div>
  </div>
 </div>
 <div id="resourceRow">
  <div class="panel resource">🪙 <span id="coins">25</span></div>
  <div class="panel resource">🪵 <span id="wood">0</span></div>
  <div class="panel resource">🪨 <span id="stone">0</span></div>
  <div class="panel resource">❤️ <span id="health">100</span></div>
 </div>
</div>

<div id="leftMenu">
 <button class="menuButton" onclick="openModal('inventory')"><span>🎒</span>Envanter</button>
 <button class="menuButton" onclick="openModal('craft')"><span>🔨</span>Üretim</button>
 <button class="menuButton" onclick="openModal('map')"><span>🗺️</span>Harita</button>
 <button class="menuButton" onclick="openModal('quests')"><span>📖</span>Görevler</button>
</div>

<div id="questPanel" class="panel">
 <h3>✿ Görevler</h3>
 <div class="quest"><strong>🟡 Daha iyi bir ev</strong>10 tahta topla<div class="qbar"><span id="qWoodBar"></span></div><div class="questLine"><span>İlerleme</span><span id="qWoodText">0 / 10</span></div></div>
 <div class="quest"><strong>◯ Aç kalma!</strong>5 meyve topla<div class="qbar"><span id="qBerryBar"></span></div><div class="questLine"><span>İlerleme</span><span id="qBerryText">0 / 5</span></div></div>
 <div class="quest"><strong>◯ Keşfet</strong>Haritanın 4 bölgesini ziyaret et<div class="qbar"><span id="qExploreBar"></span></div><div class="questLine"><span>İlerleme</span><span id="qExploreText">0 / 4</span></div></div>
</div>

<div id="dialog" class="panel">
 <div id="npcIcon">🧔🏻</div>
 <div id="dialogText"><b>Yaşlı Adam</b>Bu dünyada tek başına değilsin. Ormanı keşfet, kaynak topla ve küçük evini büyüt. Nehir kıyısında bir sürpriz olabilir!</div>
</div>

<div id="hotbar">
 <div class="slot selected" title="Balta"><small>1</small>🪓</div><div class="slot" title="Kazma"><small>2</small>⛏️</div>
 <div class="slot" title="Sulama kabı"><small>3</small>🪣</div><div class="slot" title="Balık"><small>4</small>🐟<b id="fishCount">0</b></div>
 <div class="slot" title="Odun"><small>5</small>🪵<b id="woodCount">0</b></div><div class="slot" title="Taş"><small>6</small>🪨<b id="stoneCount">0</b></div>
 <div class="slot" title="Meyve"><small>7</small>🫐<b id="berryCount">0</b></div><div class="slot" title="Meşale"><small>8</small>🏮</div>
</div>
<div id="mapBox" class="panel"><canvas id="mini"></canvas></div>
<div id="actionButtons">
 <button onclick="interact()">✋ ETKİLEŞİM [E]</button>
 <button onclick="eatBerry()">🫐 MEYVE YE [F]</button>
 <button onclick="buildHouse()">🏡 EVİ GELİŞTİR [B]</button>
</div>
<div id="joystick"><div id="knob"></div></div>
<div id="footerTip">WASD / yön tuşları: hareket · E: etkileşim · F: meyve ye · B: evi geliştir</div>
<div id="toast"></div>

<div id="modal" class="hidden" onclick="if(event.target===this)closeModal()">
 <div id="modalCard"><h2 id="modalTitle">Envanter</h2><div id="modalBody"></div><button class="close" onclick="closeModal()">Kapat</button></div>
</div>
<div id="overlay">
 <div id="intro">
  <div class="logo">🏡🌲🌊</div><h1>KÜÇÜK KAŞİF</h1><div class="subtitle">KAYIP ADA</div>
  <p>Bir kulübe, gizemli bir orman ve keşfedilmeyi bekleyen bir ada.<br><br>🌲 Kaynak topla · 🏡 Evini geliştir<br>🫐 Bahçeni hasat et · 🗺️ Yeni bölgeler keşfet<br><br><b>Bu dünyadaki hikâyeni sen yaz!</b></p>
  <button id="start" onclick="startGame()">MACERAYA BAŞLA ▶</button>
 </div>
</div>

<script>
(()=>{
'use strict';
const canvas=document.getElementById('game'),ctx=canvas.getContext('2d'),mini=document.getElementById('mini'),mctx=mini.getContext('2d');
const $=id=>document.getElementById(id);
let W=innerWidth,H=innerHeight,DPR=1,last=0,time=0,started=false;
const TILE_W=64,TILE_H=32,MW=38,MH=38;
const world=[],buildings=[],particles=[],fireflies=[];
const player={x:14,y:15,walk:0,facing:1};
const state={wood:0,stone:0,berry:0,fish:0,coins:25,hp:100,xp:0,level:1,food:100,house:1,explored:new Set(),claimed:{wood:false,berry:false,explore:false}};
let keys={},move={x:0,y:0},joyPointer=null,toastLeft=0,saveLeft=0;
const rand=(x,y,s=1)=>{const n=Math.sin(x*127.1+y*311.7+s*74.7)*43758.5453;return n-Math.floor(n)};
const clamp=(v,a,b)=>Math.max(a,Math.min(b,v));
const distance=(a,b,c,d)=>Math.hypot(a-c,b-d);
function resize(){DPR=Math.min(devicePixelRatio||1,2);W=innerWidth;H=innerHeight;canvas.width=Math.round(W*DPR);canvas.height=Math.round(H*DPR);ctx.setTransform(DPR,0,0,DPR,0,0);mini.width=Math.max(1,mini.clientWidth*DPR);mini.height=Math.max(1,mini.clientHeight*DPR);}
addEventListener('resize',resize);resize();
function waterAt(x,y){let rx=29+Math.sin(y*.24)*2.2;return Math.abs(x-rx)<1.55 && !(y>25&&y<28);}
function tileAt(x,y){if(x<0||y<0||x>=MW||y>=MH)return null;return world[Math.floor(y)*MW+Math.floor(x)]}
function generateWorld(){
 world.length=0;buildings.length=0;
 for(let y=0;y<MH;y++)for(let x=0;x<MW;x++){
  let type='grass';const r=rand(x,y);
  if(waterAt(x,y))type='water';
  else if(r>.965)type='flowers';
  else if(r>.90)type='grass2';
  if(x>26&&y>24&&y<28)type='bridge';
  if(x>8&&x<15&&y>18&&y<23)type='soil';
  world.push({x,y,type,obj:null,seed:rand(x,y,3)});
 }
 // Başlangıç açıklığı
 for(let y=8;y<22;y++)for(let x=7;x<21;x++){const t=tileAt(x,y);if(t&&t.type!=='water')t.type=(rand(x,y,8)>.7?'grass2':'grass');}
 // Bahçe yatakları
 for(let y=18;y<22;y++)for(let x=9;x<15;x++){const t=tileAt(x,y);if(t)t.type='soil';}
 // Kaynak dağılımı
 for(let y=2;y<MH-2;y++)for(let x=2;x<MW-2;x++){
  const t=tileAt(x,y);if(!t||t.type==='water'||(x>=6&&x<=21&&y>=7&&y<=22))continue;
  const r=rand(x,y,9);
  if(r>.89)t.obj={type:'tree',hp:3};
  else if(r>.83)t.obj={type:'rock',hp:3};
  else if(r>.77)t.obj={type:'berry',hp:2};
 }
 for(let y=19;y<22;y++)for(let x=10;x<14;x++){const t=tileAt(x,y);if(t)t.obj={type:'crop',hp:1};}
 // Kampın etrafında sabit binalar
 buildings.push({x:11,y:11,type:'house',level:1},{x:16,y:13,type:'table'},{x:18,y:13,type:'oven'},{x:21,y:17,type:'doghouse'},{x:15,y:16,type:'chest'});
 // Tahta köprü boyunca döşeme
 for(let x=27;x<=31;x++){const t=tileAt(x,26);if(t)t.type='bridge';}
 for(let i=0;i<32;i++)fireflies.push({x:rand(i,2)*MW,y:rand(i,9)*MH,phase:rand(i,3)*6});
}
function screenPos(x,y){
 const cx=(player.x-player.y)*TILE_W/2,cy=(player.x+player.y)*TILE_H/2;
 return {x:(x-y)*TILE_W/2-cx+W/2,y:(x+y)*TILE_H/2-cy+H*.49};
}
function polygon(points,fill,stroke=null){ctx.beginPath();points.forEach((p,i)=>i?ctx.lineTo(p[0],p[1]):ctx.moveTo(p[0],p[1]));ctx.closePath();ctx.fillStyle=fill;ctx.fill();if(stroke){ctx.strokeStyle=stroke;ctx.lineWidth=1;ctx.stroke();}}
function rect(x,y,w,h,color){ctx.fillStyle=color;ctx.fillRect(Math.round(x),Math.round(y),w,h);}
function circ(x,y,r,color){ctx.beginPath();ctx.arc(x,y,r,0,Math.PI*2);ctx.fillStyle=color;ctx.fill();}
function ellipse(x,y,rx,ry,color){ctx.beginPath();ctx.ellipse(x,y,rx,ry,0,0,Math.PI*2);ctx.fillStyle=color;ctx.fill();}
function diamond(x,y,color){polygon([[x,y-TILE_H/2],[x+TILE_W/2,y],[x,y+TILE_H/2],[x-TILE_W/2,y]],color);}
function drawGround(){
 // Distant forest vignette and terrain tiles
 rect(0,0,W,H,'#101b24');
 for(let sum=0;sum<MW+MH;sum++)for(let x=0;x<MW;x++){
  const y=sum-x;if(y<0||y>=MH)continue;const t=tileAt(x,y);if(!t)continue;
  const p=screenPos(x,y);if(p.x<-80||p.x>W+80||p.y<-50||p.y>H+80)continue;
  let col='#315f3d';
  if(t.type==='grass2')col='#386e43';
  if(t.type==='flowers')col='#3b7142';
  if(t.type==='soil')col='#71503a';
  if(t.type==='water')col='#11698b';
  if(t.type==='bridge')col='#82532f';
  diamond(p.x,p.y,col);
  if(t.type==='grass'||t.type==='grass2'){
   if(t.seed>.45){rect(p.x-13,p.y+1,2,3,'#477e46');rect(p.x+10,p.y-3,2,4,'#477e46');}
   if(t.type==='flowers'&&t.seed>.1){circ(p.x-7,p.y-1,2,'#f1b8cb');circ(p.x+5,p.y+4,2,'#e6d58b');circ(p.x+1,p.y-4,2,'#f4d8e5');}
  } else if(t.type==='soil'){
   rect(p.x-15,p.y-3,25,2,'#8e6844');rect(p.x-10,p.y+5,22,2,'#5b412f');
  } else if(t.type==='water'){
   const wave=Math.sin(time*2.2+x*.63+y*.45);
   rect(p.x-17+wave*4,p.y-3,17,2,'#36b5cc');rect(p.x+4-wave*3,p.y+5,11,2,'#2287a8');
   if((x+y)%7===0)circ(p.x+wave*8,p.y-5,1.5,'#9ce8f3');
  }else if(t.type==='bridge'){
   for(let k=-2;k<=2;k++)rect(p.x+k*10-4,p.y-8,8,16,'#a36d3e');
   rect(p.x-26,p.y-10,52,3,'#d09a59');
  }
 }
}
function drawTree(x,y){
 // cast shadow
 ellipse(x+5,y+16,24,9,'#17271f99');
 rect(x-5,y-23,10,33,'#69442c');rect(x-2,y-20,3,29,'#9a6339');
 // stacked foliage with highlights
 polygon([[x,y-78],[x+27,y-43],[x+17,y-34],[x+24,y-20],[x+10,y-12],[x-14,y-12],[x-24,y-26],[x-15,y-38],[x-26,y-45]],'#123e2b','#0b3023');
 polygon([[x,y-70],[x+20,y-43],[x+10,y-37],[x+17,y-27],[x-9,y-17],[x-19,y-31],[x-10,y-42]],'#1d5a35');
 polygon([[x,y-62],[x+13,y-43],[x+4,y-37],[x+10,y-29],[x-9,y-25],[x-15,y-38]],'#2d7541');
 polygon([[x-2,y-63],[x+6,y-49],[x-2,y-42],[x-12,y-49]],'#3c8a4c');
 rect(x-12,y-41,7,4,'#469956');rect(x+6,y-47,8,4,'#3e884a');
 if(rand(Math.round(x),Math.round(y),1)>.55){circ(x+10,y-31,2,'#f1c8d3');circ(x+13,y-28,2,'#f1c8d3');}
}
function drawRock(x,y){
 ellipse(x+3,y+8,21,7,'#17271e99');
 polygon([[x-20,y+3],[x-16,y-11],[x-5,y-20],[x+8,y-18],[x+19,y-8],[x+21,y+5],[x+6,y+13],[x-12,y+10]],'#4a5c68','#283d48');
 polygon([[x-16,y-11],[x-5,y-20],[x+5,y-10],[x-4,y-3]],'#81929a');
 polygon([[x+5,y-10],[x+19,y-8],[x+21,y+5],[x+6,y+13],[x-4,y+4]],'#5c7079');
 rect(x-8,y+1,7,3,'#a6b3b5');rect(x+8,y-4,5,2,'#748993');
}
function drawBerry(x,y){
 ellipse(x,y+5,15,6,'#17291f99');circ(x,y-3,13,'#235c37');
 circ(x-7,y-6,5,'#e34e8c');circ(x+4,y-9,5,'#f47cad');circ(x+2,y-1,5,'#c72f6a');
 rect(x-2,y-18,4,7,'#72b94e');rect(x-7,y-16,6,3,'#4f9a43');
}
function drawCrop(x,y){
 rect(x-3,y-11,5,12,'#518c3f');rect(x-11,y-8,10,4,'#60a84d');rect(x+1,y-5,10,4,'#78bc55');
 circ(x+1,y-14,3,'#dba44d');
}
function drawHouse(x,y,level=1){
 ellipse(x+3,y+34,56,14,'#15251f99');
 // walls
 polygon([[x-41,y-15],[x,y+4],[x,y+44],[x-41,y+24]],'#81502f','#4d3324');
 polygon([[x,y+4],[x+41,y-15],[x+41,y+24],[x,y+44]],'#5f3d29','#3c2c23');
 for(let i=0;i<4;i++){
  const yy=-7+i*10;
  polygon([[x-38,y+yy],[x-3,y+yy+16],[x-3,y+yy+19],[x-38,y+yy+3]],i%2?'#99653a':'#a56e40');
  polygon([[x+3,y+yy+16],[x+37,y+yy],[x+37,y+yy+3],[x+3,y+yy+19]],i%2?'#71472d':'#835330');
 }
 // roof sides
 polygon([[x-52,y-15],[x-8,y-60],[x+47,y-30],[x+5,y+5]],'#263950','#101d2b');
 polygon([[x-52,y-15],[x-8,y-60],[x-7,y-49],[x-43,y-10]],'#405875');
 polygon([[x-8,y-60],[x+47,y-30],[x+5,y+5],[x+5,y-8]],'#334967');
 // roof tile lines
 for(let i=0;i<5;i++){
  polygon([[x-43+i*8,y-16-i*7],[x-10+i*8,y-49-i*2],[x-6+i*8,y-45-i*2],[x-39+i*8,y-12-i*7]],i%2?'#4b6380':'#3d536f');
 }
 // chimney + smoke
 rect(x+14,y-56,12,22,'#69472f');rect(x+12,y-58,16,5,'#a2754e');
 for(let i=0;i<4;i++){let sy=y-65-i*8+Math.sin(time*1.4+i)*2;circ(x+20+Math.sin(time+i)*4,sy,3+i*.5,'rgba(183,197,202,'+(0.45-i*.08)+')');}
 // windows and door glow
 rect(x-31,y-3,13,14,'#ffbd55');rect(x-29,y-1,9,10,'#ffe3a0');rect(x-25,y-2,2,12,'#9b5e31');rect(x-31,y+4,13,2,'#9b5e31');
 rect(x+18,y-17,12,13,'#ffbd55');rect(x+20,y-15,8,9,'#ffe6a4');
 rect(x-13,y+9,18,34,'#3f2b24');rect(x-10,y+12,12,29,'#75492d');circ(x+1,y+27,1.8,'#ffdc8c');
 if(level>1){rect(x-1,y-54,8,15,'#80553a');rect(x+1,y-57,4,6,'#9caeb3');}
 if(level>2){rect(x-38,y+18,5,12,'#b47b44');rect(x+36,y+7,5,12,'#b47b44');}
}
function drawTable(x,y){
 ellipse(x,y+13,26,8,'#19251e88');
 polygon([[x-24,y],[x+12,y-18],[x+25,y-11],[x-12,y+8]],'#b17a43','#6a452b');
 rect(x-17,y-1,4,18,'#69432b');rect(x+12,y-15,4,18,'#69432b');
 rect(x-10,y-10,14,4,'#d5b07a');rect(x+7,y-15,5,4,'#d5b07a');
}
function drawOven(x,y){
 ellipse(x,y+20,22,8,'#17251f88');
 polygon([[x-19,y],[x-7,y-16],[x+15,y-13],[x+18,y+14],[x-18,y+27]],'#56636c','#303e47');
 polygon([[x-19,y],[x-7,y-16],[x+15,y-13],[x+1,y+2]],'#85949a');
 polygon([[x-13,y+7],[x+1,y+1],[x+1,y+20],[x-13,y+25]],'#29282c');
 circ(x-6,y+16,7,'#ff8738');circ(x-6,y+17,3.5,'#ffd16a');
 rect(x-1,y-26,10,13,'#303d46');rect(x-3,y-28,14,4,'#697981');
}
function drawDoghouse(x,y){
 ellipse(x,y+15,22,7,'#15241e88');
 polygon([[x-15,y+5],[x+13,y-7],[x+17,y+12],[x-13,y+24]],'#8b5a31');
 polygon([[x-20,y+5],[x-3,y-17],[x+20,y-6],[x+1,y+12]],'#67412b');
 polygon([[x-20,y+5],[x-3,y-17],[x-3,y-8],[x-14,y+10]],'#9b6838');
 circ(x+2,y+14,6,'#302820');
}
function drawChest(x,y){
 polygon([[x-15,y-4],[x+10,y-17],[x+18,y-11],[x-7,y+3]],'#a77843');
 polygon([[x-15,y-4],[x-7,y+3],[x-7,y+16],[x-15,y+9]],'#6d482c');
 polygon([[x-7,y+3],[x+18,y-11],[x+18,y+1],[x-7,y+16]],'#8a5a31');
 rect(x+2,y+1,4,5,'#edc86d');
}
function drawPlayer(){
 const p=screenPos(player.x,player.y),x=p.x,y=p.y;
 ellipse(x+2,y+10,15,6,'#0b171b99');
 // feet
 rect(x-8,y+3,7,10,'#4a352a');rect(x+2,y+4,7,9,'#4a352a');
 rect(x-9,y-5,18,11,'#334d75');rect(x-9,y-5,7,10,'#496a94');
 // backpack, body, arms
 rect(x-13,y-16,5,15,'#98653e');rect(x+8,y-14,5,12,'#a36b40');
 rect(x-10,y-19,20,18,'#2d7ea7');rect(x-7,y-18,5,12,'#53a9ca');
 rect(x-8,y-32,16,15,'#dca17b');rect(x-10,y-35,20,8,'#51372e');rect(x-9,y-28,4,8,'#51372e');
 rect(x-5,y-27,3,3,'#26303a');rect(x+3,y-27,3,3,'#26303a');
 rect(x+11,y-10,4,14,'#8e673f');rect(x+7,y-15,12,5,'#aebdc7');
 // tiny highlight on tool
 rect(x+11,y-14,7,2,'#d9e5e9');
}
function drawItems(){
 const items=[];
 for(const t of world)if(t.obj)items.push({x:t.x,y:t.y,obj:t.obj});
 for(const b of buildings)items.push({x:b.x,y:b.y,obj:b,building:true});
 items.sort((a,b)=>(a.x+a.y)-(b.x+b.y));
 for(const it of items){
  const p=screenPos(it.x,it.y),o=it.obj;
  if(p.x<-110||p.x>W+110||p.y<-130||p.y>H+100)continue;
  switch(o.type){
   case'tree':drawTree(p.x,p.y);break;case'rock':drawRock(p.x,p.y);break;case'berry':drawBerry(p.x,p.y);break;case'crop':drawCrop(p.x,p.y);break;
   case'house':drawHouse(p.x,p.y,o.level||1);break;case'table':drawTable(p.x,p.y);break;case'oven':drawOven(p.x,p.y);break;case'doghouse':drawDoghouse(p.x,p.y);break;case'chest':drawChest(p.x,p.y);break;
  }
 }
 // Lanterns around camp
 for(const [x0,y0] of [[7,16],[19,15],[13,7]]){
  const p=screenPos(x0,y0);rect(p.x-2,p.y-5,4,12,'#67452c');circ(p.x,p.y-10,4,'#ffc65c');circ(p.x,p.y-10,9,'rgba(255,190,70,.12)');
 }
}
function drawAtmosphere(){
 // Fireflies, soft warm lantern glows and screen vignette
 for(const f of fireflies){
  const p=screenPos(f.x,f.y),blink=(Math.sin(time*2+f.phase)+1)/2;
  if(p.x<0||p.x>W||p.y<0||p.y>H)continue;
  if(blink>.78){circ(p.x,p.y,1.4,'rgba(255,227,131,.8)');circ(p.x,p.y,5,'rgba(255,213,104,.08)');}
 }
 const v=ctx.createRadialGradient(W/2,H/2,Math.min(W,H)*.22,W/2,H/2,Math.max(W,H)*.75);
 v.addColorStop(0,'rgba(1,8,15,0)');v.addColorStop(1,'rgba(1,7,14,.42)');
 ctx.fillStyle=v;ctx.fillRect(0,0,W,H);
}
function drawParticles(){
 for(const p of particles){const s=screenPos(p.x,p.y);ctx.globalAlpha=clamp(p.life,0,1);circ(s.x,s.y,p.r,p.color);}
 ctx.globalAlpha=1;
}
function render(){
 drawGround();drawItems();drawPlayer();drawParticles();drawAtmosphere();drawMini();
}
function drawMini(){
 const w=mini.clientWidth,h=mini.clientHeight;if(!w||!h)return;
 mctx.setTransform(mini.width/w,0,0,mini.height/h,0,0);
 mctx.clearRect(0,0,w,h);mctx.fillStyle='#143a2d';mctx.fillRect(0,0,w,h);
 const cw=w/MW,ch=h/MH;
 for(const t of world){
  const x=t.x*cw,y=t.y*ch;
  if(t.type==='water'){mctx.fillStyle='#2087b1';mctx.fillRect(x,y,cw+1,ch+1);}
  else if(t.type==='bridge'){mctx.fillStyle='#a77543';mctx.fillRect(x,y,cw+1,ch+1);}
  else if(t.obj?.type==='tree'){mctx.fillStyle='#164b30';mctx.fillRect(x,y,Math.max(2,cw),Math.max(2,ch));}
  else if(t.type==='flowers'){mctx.fillStyle='#4b884d';mctx.fillRect(x,y,cw+1,ch+1);}
 }
 mctx.fillStyle='#f4d878';mctx.beginPath();mctx.arc(player.x*cw,player.y*ch,3.1,0,Math.PI*2);mctx.fill();
 mctx.fillStyle='#f8e8c0';mctx.fillRect(11*cw-2,11*ch-2,5,5);
 mctx.strokeStyle='#d3e8ff77';mctx.strokeRect(player.x*cw-12,player.y*ch-12,24,24);
}
function spawnParticles(x,y,color){
 for(let i=0;i<12;i++){const a=Math.random()*Math.PI*2,s=10+Math.random()*30;particles.push({x,y,vx:Math.cos(a)*s,vy:Math.sin(a)*s,life:1,r:1.5+Math.random()*2,color});}
}
function toast(msg){$('toast').textContent=msg;$('toast').style.display='block';toastLeft=2.5;}
function gainXP(n){state.xp+=n;while(state.xp>=100){state.xp-=100;state.level++;state.coins+=25;toast('⭐ Seviye '+state.level+'! +25 altın kazandın.');}}
function updateUI(){
 const s=state;
 for(const id of ['wood','stone','coins','health'])$(id).textContent=Math.floor(({wood:s.wood,stone:s.stone,coins:s.coins,health:s.hp})[id]);
 $('level').textContent=s.level;$('xp').textContent=s.xp;$('xpBar').style.width=s.xp+'%';
 $('woodCount').textContent=s.wood;$('stoneCount').textContent=s.stone;$('berryCount').textContent=s.berry;$('fishCount').textContent=s.fish;
 $('qWoodBar').style.width=Math.min(100,s.wood*10)+'%';$('qWoodText').textContent=Math.min(10,s.wood)+' / 10';
 $('qBerryBar').style.width=Math.min(100,s.berry*20)+'%';$('qBerryText').textContent=Math.min(5,s.berry)+' / 5';
 const regions=Math.min(4,s.explored.size);$('qExploreBar').style.width=regions*25+'%';$('qExploreText').textContent=regions+' / 4';
}
function nearest(){
 let best=null,bd=2.05;
 for(const t of world){if(!t.obj)continue;const d=distance(player.x,player.y,t.x,t.y);if(d<bd){best={x:t.x,y:t.y,obj:t.obj,tile:t};bd=d;}}
 for(const b of buildings){const d=distance(player.x,player.y,b.x,b.y);if(d<bd){best={x:b.x,y:b.y,obj:b,building:true};bd=d;}}
 return best;
}
function interact(){
 if(!started)return;
 const n=nearest();if(!n){toast('Bir ağaca, kayaya ya da yapıya yaklaşmalısın.');return;}
 const o=n.obj;
 if(n.building){
  if(o.type==='house')toast('🏡 Evin seviye '+state.house+'. Daha fazla kaynakla geliştirebilirsin!');
  else if(o.type==='table')openModal('craft');
  else if(o.type==='oven'){if(state.wood>0){state.wood--;state.food=Math.min(100,state.food+15);toast('🔥 Ocağı yaktın. Enerjin biraz arttı.');}else toast('Ocağı yakmak için odun gerekiyor.');}
  else if(o.type==='doghouse'){ $('npcIcon').textContent='🐶';$('dialogText').innerHTML='<b>Sadık Dost</b>Hav! Hav! Ada keşfinde sana eşlik edeceğim!';toast('🐶 Köpek seni sevdi!');}
  else if(o.type==='chest'){state.coins+=10;state.fish+=1;buildings.splice(buildings.indexOf(o),1);toast('🎁 Sandık açıldı: 10 altın ve 1 balık!');}
  updateUI();return;
 }
 if(o.type==='tree'){state.wood+=2;o.hp--;spawnParticles(n.x,n.y,'#d7a16a');if(o.hp<=0)n.tile.obj=null;gainXP(8);toast('🪵 +2 odun topladın!');}
 else if(o.type==='rock'){state.stone+=2;o.hp--;spawnParticles(n.x,n.y,'#b7c8d2');if(o.hp<=0)n.tile.obj=null;gainXP(8);toast('🪨 +2 taş topladın!');}
 else if(o.type==='berry'){state.berry+=2;o.hp--;spawnParticles(n.x,n.y,'#ef7ca9');if(o.hp<=0)n.tile.obj=null;gainXP(5);toast('🫐 +2 meyve topladın!');}
 else if(o.type==='crop'){state.berry++;n.tile.obj=null;gainXP(4);toast('🌱 Bahçeden ürün topladın!');}
 updateUI();checkQuestRewards();
}
function checkQuestRewards(){
 if(!state.claimed.wood&&state.wood>=10){state.claimed.wood=true;state.coins+=20;gainXP(15);toast('✅ Görev tamamlandı: Daha iyi bir ev! +20 altın');}
 if(!state.claimed.berry&&state.berry>=5){state.claimed.berry=true;state.coins+=15;gainXP(10);toast('✅ Görev tamamlandı: Aç kalma! +15 altın');}
 if(!state.claimed.explore&&state.explored.size>=4){state.claimed.explore=true;state.coins+=30;gainXP(20);toast('✅ Ada keşfedildi! +30 altın');}
}
function eatBerry(){
 if(state.berry<1){toast('Önce bahçeden ya da çalılardan meyve topla!');return;}
 if(state.food>=100){toast('Şimdilik tok ve enerjiksin.');return;}
 state.berry--;state.food=Math.min(100,state.food+30);updateUI();toast('🫐 Meyve yedin. Enerjin yenilendi!');
}
function buildHouse(){
 if(state.wood<10||state.stone<5){toast('Evi geliştirmek için 10 odun ve 5 taş gerekiyor.');return;}
 state.wood-=10;state.stone-=5;state.house++;state.coins+=10;const h=buildings.find(b=>b.type==='house');if(h)h.level=state.house;
 gainXP(20);updateUI();toast('🏡 Ev yükseltildi! Seviye '+state.house);
}
function openModal(type){
 const body=$('modalBody');$('modal').classList.remove('hidden');
 if(type==='inventory'){
  $('modalTitle').textContent='🎒 Envanter';
  body.innerHTML=`<p>🪵 Odun: <b>${state.wood}</b></p><p>🪨 Taş: <b>${state.stone}</b></p><p>🫐 Meyve: <b>${state.berry}</b></p><p>🐟 Balık: <b>${state.fish}</b></p><p>🪙 Altın: <b>${state.coins}</b></p><p>❤️ Can: <b>${Math.ceil(state.hp)}/100</b></p>`;
 }else if(type==='craft'){
  $('modalTitle').textContent='🔨 Üretim masası';
  body.innerHTML=`<p>🏡 <b>Evini geliştir</b><br>Gereken: 10 odun + 5 taş</p><button onclick="buildHouse();openModal('craft')">EVİ GELİŞTİR</button><hr><p>🪵 1 odun → 2 altın</p><button onclick="sellResource('wood');openModal('craft')">ODUN SAT</button><p>🪨 1 taş → 3 altın</p><button onclick="sellResource('stone');openModal('craft')">TAŞ SAT</button><p>🫐 3 meyve → 1 balık yemi</p><button onclick="makeBait()">YEM ÜRET</button>`;
 }else if(type==='map'){
  $('modalTitle').textContent='🗺️ Keşif haritası';
  body.innerHTML=`<p>Konumun: <b>${player.x.toFixed(1)}, ${player.y.toFixed(1)}</b></p><p>Keşfedilen bölgeler: <b>${Math.min(4,state.explored.size)}/4</b></p><p>İpucu: Adanın kuzeyindeki ormana ve doğudaki nehir kıyısına git. Ağaçlar, taşlar ve meyve çalıları kaynak sağlar.</p>`;
 }else{
  $('modalTitle').textContent='📖 Görev günlüğü';
  body.innerHTML=`<p>${state.claimed.wood?'✅':'🟡'} 10 odun topla — ${Math.min(10,state.wood)}/10</p><p>${state.claimed.berry?'✅':'◯'} 5 meyve topla — ${Math.min(5,state.berry)}/5</p><p>${state.claimed.explore?'✅':'◯'} 4 bölge keşfet — ${Math.min(4,state.explored.size)}/4</p><p>🏡 Ev seviyesi: ${state.house}</p><p>Her görevin ödülü otomatik olarak verilir.</p>`;
 }
}
function closeModal(){$('modal').classList.add('hidden');}
function sellResource(which){
 if(which==='wood'&&state.wood>0){state.wood--;state.coins+=2;toast('1 odun 2 altına satıldı.');}
 else if(which==='stone'&&state.stone>0){state.stone--;state.coins+=3;toast('1 taş 3 altına satıldı.');}
 else toast('Satacak kaynağın yok!');
 updateUI();
}
function makeBait(){if(state.berry<3){toast('Yem için 3 meyve gerekiyor.');return;}state.berry-=3;state.fish++;toast('🎣 Balık yemi hazırladın!');updateUI();}
window.openModal=openModal;window.closeModal=closeModal;window.interact=interact;window.eatBerry=eatBerry;window.buildHouse=buildHouse;window.sellResource=sellResource;window.makeBait=makeBait;
function update(dt){
 time+=dt;
 let dx=move.x,dy=move.y;
 if(keys.ArrowLeft||keys.a||keys.A)dx-=1;if(keys.ArrowRight||keys.d||keys.D)dx+=1;
 if(keys.ArrowUp||keys.w||keys.W)dy-=1;if(keys.ArrowDown||keys.s||keys.S)dy+=1;
 const mag=Math.hypot(dx,dy);if(mag>1){dx/=mag;dy/=mag;}
 const speed=3.4;
 let nx=player.x+dx*speed*dt,ny=player.y+dy*speed*dt;
 // Prevent walking through the river, map edges and solid resources
 function canMove(x,y){
  if(x<1||y<1||x>MW-2||y>MH-2||waterAt(Math.floor(x),Math.floor(y)))return false;
  const t=tileAt(x,y);if(t&&t.obj&&['tree','rock'].includes(t.obj.type))return false;
  return true;
 }
 if(dx||dy){player.walk+=dt*10;player.facing=dx<0?-1:1;}
 if(canMove(nx,player.y))player.x=nx;if(canMove(player.x,ny))player.y=ny;
 state.explored.add(Math.floor(player.x/10)+','+Math.floor(player.y/10));
 if(state.food>0)state.food-=dt*.09;else state.hp=Math.max(0,state.hp-dt*1.3);
 if(state.food>60)state.hp=Math.min(100,state.hp+dt*.15);
 if(state.hp<=0){state.hp=100;state.food=100;player.x=14;player.y=15;toast('Yoruldun ve kampında dinlenerek uyandın.');}
 for(const p of particles){p.x+=p.vx*dt*.06;p.y+=p.vy*dt*.06;p.life-=dt*1.5;}
 for(let i=particles.length-1;i>=0;i--)if(particles[i].life<=0)particles.splice(i,1);
 if(toastLeft>0){toastLeft-=dt;if(toastLeft<=0)$('toast').style.display='none';}
 saveLeft+=dt;if(saveLeft>8){saveLeft=0;saveGame();}
 updateUI();checkQuestRewards();
}
function saveGame(){
 try{localStorage.setItem('smallExplorerSave',JSON.stringify({player,state:{...state,explored:[...state.explored]},house:state.house,world:world.map(t=>t.obj?{x:t.x,y:t.y,type:t.obj.type,hp:t.obj.hp}:null)}));}catch(e){}
}
function loadGame(){
 try{
  const raw=localStorage.getItem('smallExplorerSave');if(!raw)return false;
  const s=JSON.parse(raw);if(!s||!s.player||!s.state)return false;
  player.x=clamp(Number(s.player.x)||14,1,MW-2);player.y=clamp(Number(s.player.y)||15,1,MH-2);
  Object.assign(state,s.state);state.explored=new Set(s.state.explored||[]);
  if(Array.isArray(s.world))for(const saved of s.world){if(!saved)continue;const t=tileAt(saved.x,saved.y);if(t)t.obj={type:saved.type,hp:saved.hp||1};}
  if(s.house){state.house=s.house;const h=buildings.find(b=>b.type==='house');if(h)h.level=s.house;}
  return true;
 }catch(e){return false;}
}
function startGame(){if(!world.length)generateWorld();started=true;$('overlay').style.display='none';if(loadGame())toast('🌿 Kaydın yüklendi. Macerana devam et!');else toast('🌿 Maceran başladı! Ağaçlara yaklaş ve E / ETKİLEŞİM düğmesine bas.');updateUI();}
window.startGame=startGame;
addEventListener('keydown',e=>{
 keys[e.key]=true;
 if(['ArrowUp','ArrowDown','ArrowLeft','ArrowRight',' '].includes(e.key))e.preventDefault();
 if(e.repeat)return;
 if(e.key.toLowerCase()==='e')interact();
 if(e.key.toLowerCase()==='f')eatBerry();
 if(e.key.toLowerCase()==='b')buildHouse();
 if(e.key==='Escape')closeModal();
 if('12345678'.includes(e.key)){document.querySelectorAll('.slot').forEach((s,i)=>s.classList.toggle('selected',i===Number(e.key)-1));}
});
addEventListener('keyup',e=>keys[e.key]=false);
const joy=$('joystick'),knob=$('knob');
function joystickMove(e){
 const r=joy.getBoundingClientRect();let dx=e.clientX-(r.left+r.width/2),dy=e.clientY-(r.top+r.height/2),m=Math.hypot(dx,dy),max=34;
 if(m>max){dx=dx/m*max;dy=dy/m*max;}
 knob.style.left=(34+dx)+'px';knob.style.top=(34+dy)+'px';move.x=dx/max;move.y=dy/max;
}
joy.addEventListener('pointerdown',e=>{joyPointer=e.pointerId;joy.setPointerCapture(joyPointer);joystickMove(e);});
joy.addEventListener('pointermove',e=>{if(e.pointerId===joyPointer)joystickMove(e);});
function releaseJoy(){joyPointer=null;move.x=0;move.y=0;knob.style.left='34px';knob.style.top='34px';}
joy.addEventListener('pointerup',releaseJoy);joy.addEventListener('pointercancel',releaseJoy);
document.addEventListener('visibilitychange',()=>{if(document.hidden)saveGame();});
generateWorld();updateUI();
function frame(t){const dt=Math.min((t-last)/1000||0,.04);last=t;if(started)update(dt);render();requestAnimationFrame(frame);}
requestAnimationFrame(frame);
})();
</script>
</body>
</html>
