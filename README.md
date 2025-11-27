<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Metro Shop Pol1xer — Violet Ultra 4.2</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap');
:root{
  --neon:#b400ff;
  --neon-glow:0 0 25px #b400ff,0 0 50px #b400ff;
  --neon-accent:#ff33ff;
}
body{margin:0;font-family:'Orbitron',sans-serif;background:#000;color:#fff;overflow-x:hidden;}
.gradient-bg{position:fixed;inset:0;background:linear-gradient(160deg,#555,#000);z-index:-10;transition:all 0.5s;}
.smoke{position:fixed;inset:0;background:url('https://i.imgur.com/8O6xE8H.png');opacity:.18;background-size:cover;animation:smokeMove 50s linear infinite;z-index:-9;}
@keyframes smokeMove{from{transform:translateX(-12%);} to{transform:translateX(12%);}}
.light-lines{position:fixed;inset:0;pointer-events:none;z-index:-8;}
.light-lines div{position:absolute;width:2px;height:100%;background:var(--neon-accent);opacity:.08;animation:lineMove 20s linear infinite;}
@keyframes lineMove{0%{transform:translateX(0);}100%{transform:translateX(100vw);}}
.overlay{position:fixed;inset:0;background:rgba(0,0,0,.4);z-index:-7}
header{text-align:center;padding:25px 0;position:relative;}
header h1{margin:0;font-size:55px;color:var(--neon);text-shadow:var(--neon-glow);animation:glitchHeader 3s infinite;}
@keyframes glitchHeader{
  0%{text-shadow:0 0 25px #b400ff,0 0 50px #b400ff;}
  20%{text-shadow:0 0 25px #ff00ff,0 0 50px #ff00ff;}
  40%{text-shadow:0 0 20px #b400ff,0 0 40px #b400ff;}
  60%{text-shadow:0 0 30px #ff33ff,0 0 60px #ff33ff;}
  80%{text-shadow:0 0 25px #b400ff,0 0 50px #b400ff;}
  100%{text-shadow:0 0 25px #b400ff,0 0 50px #b400ff;}
}
.menu{margin-top:15px;padding:12px;border-radius:12px;background:rgba(255,255,255,.05);border:1px solid var(--neon);backdrop-filter:blur(10px);}
.menu button{background:transparent;border:2px solid var(--neon);color:var(--neon);padding:10px 20px;margin:5px;border-radius:8px;cursor:pointer;transition:.3s;text-shadow:var(--neon-glow);}
.menu button:hover{background:var(--neon);color:#000;}
.category{display:flex;justify-content:center;flex-wrap:wrap;margin:15px 0;}
.category button{margin:5px;background:transparent;border:2px solid var(--neon);color:var(--neon);padding:8px 16px;border-radius:8px;cursor:pointer;transition:.3s;text-shadow:var(--neon-glow);}
.category button:hover{background:var(--neon);color:#000;}
.shop-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;padding:20px;}
.item{background:rgba(0,0,0,.55);border:2px solid var(--neon);border-radius:12px;padding:15px;text-align:center;box-shadow:0 0 20px #b400ff55;transition:.3s;animation:itemShow .7s ease,floatItem 4s ease-in-out infinite alternate;position:relative;overflow:hidden;transform-style:preserve-3d;}
@keyframes itemShow{from{opacity:0;transform:translateY(20px);} to{opacity:1;transform:translateY(0);}}
@keyframes floatItem{0%{transform: translateY(0px) rotate(0deg);}25%{transform: translateY(-10px) rotate(-1deg);}50%{transform: translateY(7px) rotate(1deg);}75%{transform: translateY(-5px) rotate(-0.5deg);}100%{transform: translateY(0px) rotate(0deg);}}
.item:hover{transform:scale(1.08) translateZ(5px);box-shadow:0 0 40px #b400ffaa;}
.item img{width:100%;border-radius:10px;margin-bottom:10px;transition:transform .3s, box-shadow .3s;}
.item img:hover{animation:glitch 0.4s;transform:scale(1.08);box-shadow:0 0 45px var(--neon);}
@keyframes glitch{0%{transform:translate(0,0);}25%{transform:translate(-2px,2px);}50%{transform:translate(2px,-2px);}75%{transform:translate(-1px,1px);}100%{transform:translate(0,0);}}
.sale,.vip-tag{position:absolute;top:10px;left:10px;background:var(--neon);color:#000;padding:5px 10px;font-weight:bold;transform:rotate(-15deg);animation:badgeGlow 2s infinite;}
.vip-tag{left:auto;right:10px;transform:rotate(10deg);}
@keyframes badgeGlow{0%,100%{box-shadow:0 0 20px var(--neon);}50%{box-shadow:0 0 45px var(--neon);}}
.btn{display:inline-block;padding:12px 18px;border-radius:8px;color:#000;background:var(--neon);text-decoration:none;font-weight:700;cursor:pointer;position:relative;overflow:hidden;transition:.3s;box-shadow:var(--neon-glow);}
.btn::before{content:"";position:absolute;inset:0;background:var(--neon);filter:blur(15px);opacity:.5;animation:pulse 2.5s infinite ease-in-out;}
@keyframes pulse{0%{opacity:0.3;}50%{opacity:1;}100%{opacity:0.3;}}
.btn:hover{transform:scale(1.08);box-shadow:0 0 55px var(--neon);}
.btn:hover::after{content:"";position:absolute;left:0;top:0;width:100%;height:100%;background:linear-gradient(90deg,transparent,#fff 30%,transparent);animation:glitchBtn 0.4s linear;}
@keyframes glitchBtn{from{transform:translateX(-100%);} to{transform:translateX(100%);}}
#cartBtn,#vipBtn,#chatBtn,#musicBtn{position:fixed;padding:10px 18px;border-radius:10px;cursor:pointer;border:2px solid var(--neon);background:rgba(0,0,0,.7);color:var(--neon);z-index:50;text-shadow:var(--neon-glow);}
#cartBtn{right:20px;top:20px;} #vipBtn{left:20px;top:20px;color:#ffd700;border-color:#ffd700;} #chatBtn{right:20px;bottom:20px;background:var(--neon);color:#000;} #musicBtn{left:20px;bottom:20px;}
#cartModal,#chatWindow{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);background:rgba(0,0,0,.85);border:2px solid var(--neon);border-radius:12px;padding:25px;display:none;z-index:100;min-width:300px;max-width:90%;}
#cartModal .cart-box,#chatWindow{position:relative;}
.cart-item{display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--neon);}
.cart-item button{border:none;background:var(--neon);color:#000;padding:3px 8px;border-radius:5px;cursor:pointer;transition:.3s;}
.cart-item button:hover{transform:scale(1.1);box-shadow:0 0 25px var(--neon);}
.close-cart{position:absolute;top:10px;right:10px;padding:6px 12px;background:var(--neon);color:#000;border:none;border-radius:8px;font-weight:bold;cursor:pointer;transition:.3s;}
.close-cart:hover{transform:scale(1.1);box-shadow:0 0 30px var(--neon);}
.pay-btn{margin-top:15px;padding:10px 20px;background:#00ff99;color:#000;font-weight:bold;border:none;border-radius:8px;cursor:pointer;transition:.3s;box-shadow:0 0 25px #00ff99;}
.pay-btn:hover{transform:scale(1.05);box-shadow:0 0 40px #00ff99;}
.promo-banner {position: relative;margin: 40px 0;width: 100%;min-height: 220px;background: url('https://i.imgur.com/8O6xE8H.png') center center / cover no-repeat;display: flex;justify-content: center;align-items: center;overflow: hidden;border: 2px solid var(--neon);box-shadow: 0 0 40px var(--neon);}
.promo-banner::after{content:"";position:absolute;inset:0;background:rgba(0,0,0,.55);}
.promo-content{position:relative;padding:20px 30px;text-align:center;z-index:1;}
.promo-content h2{font-size:32px;color:var(--neon);text-shadow:var(--neon-glow);font-weight:700;letter-spacing:1.5px;animation:glowText 2s infinite alternate;}
@keyframes glowText{0%{text-shadow:0 0 20px #b400ff,0 0 40px #b400ff;}50%{text-shadow:0 0 35px #ff33ff,0 0 70px #ff33ff;}100%{text-shadow:0 0 25px #b400ff,0 0 50px #b400ff;}}
footer{position:relative;margin-top:50px;padding:50px 20px 20px;background:#111;border-top:2px solid var(--neon);overflow:hidden;}
.footer-bg{position:absolute;inset:0;background:linear-gradient(to top,#000,#222);z-index:-2;}
.footer-content{display:flex;flex-direction:column;align-items:center;text-align:center;color:#fff;font-family:'Orbitron',sans-serif;}
.footer-links a{color:var(--neon);margin:0 10px;text-decoration:none;font-weight:700;text-shadow:var(--neon-glow);transition:.3s;}
.footer-links a:hover{text-shadow:0 0 35px #b400ff,0 0 60px #b400ff;text-decoration:underline;}
.ticker{margin:15px 0;width:100%;overflow:hidden;white-space:nowrap;box-sizing:border-box;border-top:1px solid var(--neon);border-bottom:1px solid var(--neon);padding:10px 0;color:var(--neon);font-weight:700;text-shadow:var(--neon-glow);animation:scrollText 15s linear infinite;}
@keyframes scrollText{0%{transform:translateX(100%);}100%{transform:translateX(-100%);}}
.footer-stats{margin-top:10px;font-size:14px;color:#fff;text-shadow:0 0 15px #b400ff33;}
</style>
</head>
<body>

<div class="gradient-bg"></div>
<div class="smoke"></div>
<div class="light-lines"><div></div><div></div><div></div><div></div><div></div></div>
<div class="overlay"></div>

<header>
<h1>МЕТРО ШОП POL1XER</h1>
<div class="menu">
<button>Главная</button>
<button>Каталог</button>
<button>Популярное</button>
<button>Контакты</button>
<button>Поддержка</button>
</div>
</header>

<div class="category">
<button onclick="filterCategory('all')">Все</button>
<button onclick="filterCategory('armor')">Броня</button>
<button onclick="filterCategory('loot')">Лут</button>
<button onclick="filterCategory('vip')">VIP</button>
</div>

<button id="cartBtn">🛒 Корзина</button>
<button id="vipBtn">👑 VIP</button>
<button id="chatBtn">💬</button>
<button id="musicBtn">🎵</button>

<div id="chatWindow">
<h3>Поддержка</h3>
<button onclick="openTelegramChat()">Открыть Telegram</button>
<button class="close-cart" onclick="document.getElementById('chatWindow').style.display='none'">Закрыть</button>
</div>

<div id="cartModal">
<div class="cart-box">
<h2>Корзина</h2>
<div id="cartItems"></div>
<h3>Итого: <span id="cartTotal">0</span> ₽</h3>
<button class="pay-btn" onclick="payCart()">Оплатить</button>
<button class="close-cart" onclick="closeCart()">Закрыть</button>
</div>
</div>

<div class="shop-grid">
<div class="item" data-category="armor"><div class="sale">SALE</div><img src="0870aa5c571f4c1199380020ceca6dd5_1000027912.image.jpg"><h3>Броня Lv.6</h3><p>700 ₽</p><button class="btn" onclick="addToCart('Броня Lv.6',700)">Купить</button></div>
<div class="item" data-category="armor"><img src="13563520000b454d9bbf91528b161665_1000027913.preview.jpg"><h3>Шлем Lv.6</h3><p>450 ₽</p><button class="btn" onclick="addToCart('Шлем Lv.6',450)">Купить</button></div>
<div class="item" data-category="loot"><div class="sale">SALE</div><img src="c24e36c968bb47aa968c5ad34326918d_1000027917.image.png"><h3>Фиолетовый Лут</h3><p>300 ₽</p><button class="btn" onclick="addToCart('Фиолетовый Лут',300)">Купить</button></div>
<div class="item" data-category="vip"><div class="vip-tag">VIP</div><img src="7c4bbfd998cac612d13670027269beae.preview.jpg"><h3>МК14 ВЫШКА</h3><p>900 ₽</p><button class="btn" onclick="addToCart('Золотой Лут',900)">Купить</button></div>
</div>

<section class="promo-banner">
  <canvas id="bannerParticles"></canvas>
  <div class="promo-content">
    <h2>Самые дешёвые вещи — только в этом магазине!</h2>
  </div>
</section>

<audio id="music" loop><source src="https://files.catbox.moe/3j2d0q.mp3"></audio>

<footer>
<div class="footer-bg"></div>
<div class="footer-content">
<div class="footer-links">
<a href="https://t.me" target="_blank">Telegram</a>
<a href="https://discord.com" target="_blank">Discord</a>
<a href="https://vk.com" target="_blank">VK</a>
<a href="mailto:support@metroshop.com">Email</a>
</div>
<div class="ticker">
🔥 Скидки на броню Lv.6! VIP лут только сегодня! 🛒 Не пропусти!
</div>
<div class="footer-stats">
Онлайн: <span id="onlineCount">27</span> игроков | Продано сегодня: <span id="soldCount">13</span> предметов
</div>
</div>
</footer>

<script>
// Telegram WebApp
const tg = window.Telegram.WebApp;
tg.expand();

// Корзина
let cart = [];
function addToCart(name, price) { cart.push({name, price}); updateCart(); }
function updateCart() {
    const b = document.getElementById('cartItems'); b.innerHTML = '';
    let total = 0;
    cart.forEach((item,i)=>{b.innerHTML+=`<div class="cart-item"><span>${item.name}</span> <span>${item.price} ₽</span> <button onclick="removeItem(${i})">X</button></div>`; total+=item.price;});
    document.getElementById('cartTotal').innerText = total;
}
function removeItem(index){cart.splice(index,1);updateCart();}
document.getElementById('cartBtn').onclick=()=>{document.getElementById('cartModal').style.display='block';}
function closeCart(){document.getElementById('cartModal').style.display='none';}
function payCart(){tg.sendData(JSON.stringify({type:'payment',items:cart}));alert('Оплата через Telegram ещё не настроена!');}

// Категории
function filterCategory(cat){document.querySelectorAll('.item').forEach(i=>{i.style.display=(cat==='all'||i.dataset.category===cat)?'block':'none';});}

// Поддержка
document.getElementById('chatBtn').onclick=()=>{document.getElementById('chatWindow').style.display='block';}
function openTelegramChat(){tg.openLink('https://t.me/YOUR_SUPPORT_USERNAME');}

// VIP
let vip=false;
document.getElementById('vipBtn').onclick=()=>{vip=!vip;document.body.classList.toggle('vip-enabled');document.getElementById('vipBtn').innerText=vip?'👑 VIP ON':'👑 VIP';}

// Музыка
document.getElementById('musicBtn').onclick=()=>{const m=document.getElementById('music');if(m.paused){m.play();document.getElementById('musicBtn').innerText='🔇';}else{m.pause();document.getElementById('musicBtn').innerText='🎵';}}

// Онлайн счётчик (динамический эффект)
setInterval(()=>{document.getElementById('onlineCount').innerText=20+Math.floor(Math.random()*10);document.getElementById('soldCount').innerText=10+Math.floor(Math.random()*10);},5000);

// Частицы на баннере
const canvas=document.getElementById('bannerParticles');canvas.width=canvas.offsetWidth;canvas.height=canvas.offsetHeight;
const ctx=canvas.getContext('2d');let particles=[];
for(let i=0;i<70;i++){particles.push({x:Math.random()*canvas.width,y:Math.random()*canvas.height,r:Math.random()*3+1,dx:(Math.random()-0.5)*1.5,dy:(Math.random()-0.5)*1.5});}
function animateParticles(){ctx.clearRect(0,0,canvas.width,canvas.height);particles.forEach(p=>{ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);ctx.fillStyle='rgba(255,0,255,0.6)';ctx.fill();p.x+=p.dx;p.y+=p.dy;if(p.x<0||p.x>canvas.width)p.dx*=-1;if(p.y<0||p.y>canvas.height)p.dy*=-1;});requestAnimationFrame(animateParticles);}
animateParticles();
window.addEventListener('resize',()=>{canvas.width=canvas.offsetWidth;canvas.height=canvas.offsetHeight;});
</script>

</body>
</html>
