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

body{
  margin:0;
  font-family:'Orbitron',sans-serif;
  background:linear-gradient(160deg,#444,#000);
  color:#fff;
  overflow-x:hidden;
}

/* Удалён фон-дым, оставлен чистый прозрачный эффект */
.gradient-bg{display:none;}
.smoke{display:none;}
.light-lines{display:none;}
.overlay{display:none;}

header{
  text-align:center;
  padding:25px 0;
  position:relative;
}

header h1{
  margin:0;
  font-size:55px;
  color:var(--neon);
  text-shadow:var(--neon-glow);
  animation:glowHeader 3s infinite;
}

@keyframes glowHeader{
  0%{text-shadow:0 0 25px #b400ff;}
  50%{text-shadow:0 0 50px #ff33ff;}
  100%{text-shadow:0 0 25px #b400ff;}
}

/* Новое меню (Категории сверху) */
.category{
  margin-top:15px;
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  gap:10px;
}

.category button{
  background:transparent;
  border:2px solid var(--neon);
  color:var(--neon);
  padding:10px 22px;
  border-radius:10px;
  cursor:pointer;
  font-size:17px;
  transition:.3s;
  text-shadow:var(--neon-glow);
}

.category button:hover{
  background:var(--neon);
  color:#000;
}

/* Товары 3-в-ряд */
.shop-grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:20px;
  padding:20px;
}

.item{
  background:rgba(0,0,0,.55);
  border:2px solid var(--neon);
  border-radius:12px;
  padding:15px;
  text-align:center;
  box-shadow:0 0 20px #b400ff55;
  transition:0.3s;
  position:relative;
  overflow:hidden;
}

.item:hover{
  transform:scale(1.07);
  box-shadow:0 0 40px #b400ffaa;
}

.item img{
  width:100%;
  border-radius:10px;
  margin-bottom:10px;
}

/* Бейджи */
.sale,.vip-tag{
  position:absolute;
  top:10px;
  left:10px;
  background:var(--neon);
  color:#000;
  padding:5px 10px;
  font-weight:bold;
  transform:rotate(-15deg);
  animation:badgeGlow 2s infinite;
}

.vip-tag{
  right:10px;
  left:auto;
  transform:rotate(10deg);
}

@keyframes badgeGlow{
  0%,100%{box-shadow:0 0 20px var(--neon);}
  50%{box-shadow:0 0 40px var(--neon);}
}

/* Кнопки купить */
.btn{
  background:var(--neon);
  color:#000;
  padding:12px 18px;
  border-radius:10px;
  font-weight:700;
  cursor:pointer;
  border:none;
  box-shadow:var(--neon-glow);
  transition:.3s;
}

.btn:hover{
  transform:scale(1.1);
}

/* Кнопки функционала */
#cartBtn,#chatBtn,#musicBtn{
  position:fixed;
  padding:10px 18px;
  border-radius:10px;
  cursor:pointer;
  border:2px solid var(--neon);
  background:rgba(0,0,0,.7);
  color:var(--neon);
  z-index:50;
}

#cartBtn{right:20px;top:20px;}
#chatBtn{right:20px;bottom:20px;background:var(--neon);color:#000;}
#musicBtn{left:20px;bottom:20px;}

/* Модальные окна */
#cartModal,#chatWindow{
  position:fixed;
  top:50%;left:50%;
  transform:translate(-50%,-50%);
  background:rgba(0,0,0,.85);
  border:2px solid var(--neon);
  border-radius:12px;
  padding:25px;
  display:none;
  z-index:100;
  min-width:300px;
  max-width:90%;
}

.close-cart{
  position:absolute;
  top:10px;right:10px;
  padding:7px 12px;
  background:var(--neon);
  border:none;
  border-radius:10px;
  color:#000;
  font-weight:bold;
  cursor:pointer;
}

</style>
</head>
<body>

<header>
<h1>МЕТРО ШОП POL1XER</h1>
</header>

<!-- Категории – теперь вместо меню -->
<div class="category">
<button onclick="filterCategory('all')">Все</button>
<button onclick="filterCategory('armor')">Броня</button>
<button onclick="filterCategory('loot')">Лут</button>
<button onclick="filterCategory('vip')">VIP</button>
</div>

<button id="cartBtn">🛒 Корзина</button>
<button id="chatBtn">💬</button>
<button id="musicBtn">🎵</button>

<!-- Окно поддержки -->
<div id="chatWindow">
<h3>Поддержка</h3>
<button onclick="tg.openLink('https://t.me/pol1xer')">Написать @pol1xer</button>
<button class="close-cart" onclick="document.getElementById('chatWindow').style.display='none'">Закрыть</button>
</div>

<!-- Корзина -->
<div id="cartModal">
<div class="cart-box">
<h2>Корзина</h2>
<div id="cartItems"></div>
<h3>Итого: <span id="cartTotal">0</span> ₽</h3>
<button class="close-cart" onclick="closeCart()">Закрыть</button>
</div>
</div>

<!-- ⚡ ТОВАРЫ 3-в-ряд -->
<div class="shop-grid">

<div class="item" data-category="armor">
<div class="sale">SALE</div>
<img src="0870aa5c571f4c1199380020ceca6dd5_1000027912.image.jpg">
<h3>Броня Lv.6</h3>
<p>700 ₽</p>
<button class="btn" onclick="addToCart('Броня Lv.6',700)">Купить</button>
</div>

<div class="item" data-category="armor">
<img src="13563520000b454d9bbf91528b161665_1000027913.preview.jpg">
<h3>Шлем Lv.6</h3>
<p>450 ₽</p>
<button class="btn" onclick="addToCart('Шлем Lv.6',450)">Купить</button>
</div>

<div class="item" data-category="loot">
<div class="sale">SALE</div>
<img src="c24e36c968bb47aa968c5ad34326918d_1000027917.image.png">
<h3>Фиолетовый Лут</h3>
<p>300 ₽</p>
<button class="btn" onclick="addToCart('Фиолетовый Лут',300)">Купить</button>
</div>

<div class="item" data-category="vip">
<div class="vip-tag">VIP</div>
<img src="7c4bbfd998cac612d13670027269beae.preview.jpg">
<h3>МК14 ВЫШКА</h3>
<p>900 ₽</p>
<button class="btn" onclick="addToCart('МК14 Вышка',900)">Купить</button>
</div>

<!-- Новый товар 1 -->
<div class="item" data-category="loot">
<img src="https://i.imgur.com/YvYIYdL.png">
<h3>Эпический Лут</h3>
<p>550 ₽</p>
<button class="btn" onclick="addToCart('Эпический Лут',550)">Купить</button>
</div>

<!-- Новый товар 2 -->
<div class="item" data-category="armor">
<img src="https://i.imgur.com/ljQ0v9N.png">
<h3>Броник Тактик</h3>
<p>650 ₽</p>
<button class="btn" onclick="addToCart('Броник Тактик',650)">Купить</button>
</div>
<!-- Футер -->
<footer>
  <div style="position:absolute;inset:0;background:linear-gradient(to top,#000,#222);z-index:-2;"></div>
  <div style="display:flex;flex-direction:column;align-items:center;text-align:center;color:#fff;font-family:'Orbitron',sans-serif;">
    <div style="margin:0 0 10px 0;">
      <a href="https://t.me/pol1xer" target="_blank" style="color:var(--neon);margin:0 10px;text-decoration:none;font-weight:700;text-shadow:var(--neon-glow);">@pol1xer</a>
      <a href="https://discord.com" target="_blank" style="color:var(--neon);margin:0 10px;text-decoration:none;font-weight:700;text-shadow:var(--neon-glow);">Discord</a>
      <a href="https://vk.com" target="_blank" style="color:var(--neon);margin:0 10px;text-decoration:none;font-weight:700;text-shadow:var(--neon-glow);">VK</a>
      <a href="mailto:support@metroshop.com" style="color:var(--neon);margin:0 10px;text-decoration:none;font-weight:700;text-shadow:var(--neon-glow);">Email</a>
    </div>
    <div style="margin:15px 0;width:100%;overflow:hidden;white-space:nowrap;box-sizing:border-box;border-top:1px solid var(--neon);border-bottom:1px solid var(--neon);padding:10px 0;color:var(--neon);font-weight:700;text-shadow:var(--neon-glow);animation:scrollText 15s linear infinite;">
      🔥 Скидки на броню Lv.6! VIP лут только сегодня! 🛒 Не пропусти!
    </div>
    <div style="margin-top:10px;font-size:14px;color:#fff;text-shadow:0 0 15px #b400ff33;">
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
function addToCart(name, price) {
  cart.push({name, price});
  updateCart();
}
function updateCart() {
  const b = document.getElementById('cartItems');
  b.innerHTML = '';
  let total = 0;
  cart.forEach((item,i)=>{
    b.innerHTML+=`<div style="display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--neon);"><span>${item.name}</span><span>${item.price} ₽</span><button onclick="removeItem(${i})" style="border:none;background:var(--neon);color:#000;padding:3px 8px;border-radius:5px;cursor:pointer;transition:.3s;">X</button></div>`;
    total+=item.price;
  });
  document.getElementById('cartTotal').innerText = total;
}
function removeItem(index){
  cart.splice(index,1);
  updateCart();
}
document.getElementById('cartBtn').onclick=()=>{document.getElementById('cartModal').style.display='block';}
function closeCart(){document.getElementById('cartModal').style.display='none';}

// Категории
function filterCategory(cat){
  document.querySelectorAll('.item').forEach(i=>{
    i.style.display=(cat==='all'||i.dataset.category===cat)?'block':'none';
  });
}

// Поддержка
document.getElementById('chatBtn').onclick=()=>{
  tg.openLink('https://t.me/pol1xer');
}

// Музыка
document.getElementById('musicBtn').onclick=()=>{
  const m=document.getElementById('music');
  if(m.paused){
    m.play();
    document.getElementById('musicBtn').innerText='🔇';
  }else{
    m.pause();
    document.getElementById('musicBtn').innerText='🎵';
  }
}

// Онлайн счётчик (динамический эффект)
setInterval(()=>{
  document.getElementById('onlineCount').innerText=20+Math.floor(Math.random()*10);
  document.getElementById('soldCount').innerText=10+Math.floor(Math.random()*10);
},5000);
</script>

<audio id="music" loop>
  <source src="https://files.catbox.moe/3j2d0q.mp3">
</audio>

</body>
</html>


</div>
