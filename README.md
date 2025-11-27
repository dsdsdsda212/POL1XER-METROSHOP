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
body{
  margin:0;
  font-family:'Orbitron',sans-serif;
  background:#000;
  color:#fff;
  overflow-x:hidden;
}
.gradient-bg{
  position:fixed; inset:0;
  background:linear-gradient(160deg,#555,#000);
  z-index:-10; transition:all 0.5s;
}
header{
  text-align:center;
  padding:25px 0;
}
header h1{
  margin:0;
  font-size:55px;
  color:var(--neon);
  text-shadow:var(--neon-glow);
}
.category{
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  margin:15px 0;
}
.category button{
  margin:5px;
  background:transparent;
  border:2px solid var(--neon);
  color:var(--neon);
  padding:8px 16px;
  border-radius:8px;
  cursor:pointer;
  transition:.3s;
  text-shadow:var(--neon-glow);
}
.category button:hover{
  background:var(--neon);
  color:#000;
}
.shop-grid{
  display:grid;
  grid-template-columns:repeat(3, 1fr);
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
  transition:.3s;
}
.item:hover{
  transform:scale(1.08);
  box-shadow:0 0 40px #b400ffaa;
}
.item img{
  width:100%;
  border-radius:10px;
  margin-bottom:10px;
}
.btn{
  display:inline-block;
  padding:12px 18px;
  border-radius:8px;
  color:#000;
  background:var(--neon);
  text-decoration:none;
  font-weight:700;
  cursor:pointer;
  position:relative;
  overflow:hidden;
  transition:.3s;
}
.btn:hover{
  transform:scale(1.08);
  box-shadow:0 0 55px var(--neon);
}
#cartBtn{
  position:fixed; right:20px; top:20px; padding:10px 18px;
  border-radius:10px; cursor:pointer; border:2px solid var(--neon);
  background:rgba(0,0,0,.7); color:var(--neon); z-index:50;
  text-shadow:var(--neon-glow);
}
#cartModal{
  position:fixed; top:50%; left:50%; transform:translate(-50%,-50%);
  background:rgba(0,0,0,.85); border:2px solid var(--neon); border-radius:12px;
  padding:25px; display:none; z-index:100; min-width:300px; max-width:90%;
}
.cart-item{
  display:flex; justify-content:space-between; padding:5px 0;
  border-bottom:1px solid var(--neon);
}
.cart-item button{
  border:none; background:var(--neon); color:#000;
  padding:3px 8px; border-radius:5px; cursor:pointer; transition:.3s;
}
.cart-item button:hover{
  transform:scale(1.1); box-shadow:0 0 25px var(--neon);
}
.close-cart{
  position:absolute; top:10px; right:10px;
  padding:6px 12px; background:var(--neon); color:#000;
  border:none; border-radius:8px; font-weight:bold; cursor:pointer; transition:.3s;
}
.close-cart:hover{
  transform:scale(1.1); box-shadow:0 0 30px var(--neon);
}
.pay-btn{
  margin-top:15px; padding:10px 20px;
  background:#00ff99; color:#000; font-weight:bold; border:none; border-radius:8px; cursor:pointer;
  transition:.3s; box-shadow:0 0 25px #00ff99;
}
.pay-btn:hover{
  transform:scale(1.05); box-shadow:0 0 40px #00ff99;
}
.promo-banner{
  position: relative;
  margin: 40px 0;
  width: 100%;
  min-height: 220px;
  display:flex; justify-content:center; align-items:center;
  overflow:hidden;
  border:2px solid var(--neon);
  background: linear-gradient(160deg,#555,#000);
}
.promo-content{
  position:relative; padding:20px 30px; text-align:center; z-index:1;
}
.promo-content h2{
  font-size:32px;
  color:var(--neon);
  text-shadow:var(--neon-glow);
  font-weight:700;
}
footer{
  padding:50px 20px 20px;
  background:#111; border-top:2px solid var(--neon);
  text-align:center;
}
footer a{
  color:var(--neon); margin:0 10px; text-decoration:none; font-weight:700; text-shadow:var(--neon-glow);
}
footer a:hover{text-decoration:underline;}
</style>
</head>
<body>

<div class="gradient-bg"></div>

<header>
  <h1>МЕТРО ШОП POL1XER</h1>
</header>

<div class="category">
  <button onclick="filterCategory('all')">Все</button>
  <button onclick="filterCategory('armor')">Броня</button>
  <button onclick="filterCategory('loot')">Лут</button>
  <button onclick="filterCategory('vip')">VIP</button>
</div>

<button id="cartBtn">🛒 Корзина</button>

<div id="cartModal">
  <h2>Корзина</h2>
  <div id="cartItems"></div>
  <h3>Итого: <span id="cartTotal">0</span> ₽</h3>
  <button class="pay-btn">Оплатить</button>
  <button class="close-cart" onclick="document.getElementById('cartModal').style.display='none'">Закрыть</button>
</div>

<div class="shop-grid">
  <div class="item" data-category="armor">
    <h3>Броня Lv.6</h3>
    <p>700 ₽</p>
    <button class="btn" onclick="addToCart('Броня Lv.6',700)">Купить</button>
  </div>
  <div class="item" data-category="armor">
    <h3>Шлем Lv.6</h3>
    <p>450 ₽</p>
    <button class="btn" onclick="addToCart('Шлем Lv.6',450)">Купить</button>
  </div>
  <div class="item" data-category="loot">
    <h3>Фиолетовый Лут</h3>
    <p>300 ₽</p>
    <button class="btn" onclick="addToCart('Фиолетовый Лут',300)">Купить</button>
  </div>
  <div class="item" data-category="vip">
    <h3>МК14 ВЫШКА</h3>
    <p>900 ₽</p>
    <button class="btn" onclick="addToCart('МК14 ВЫШКА',900)">Купить</button>
  </div>
  <div class="item" data-category="loot">
    <h3>Новый Лут 1</h3>
    <p>350 ₽</p>
    <button class="btn" onclick="addToCart('Новый Лут 1',350)">Купить</button>
  </div>
  <div class="item" data-category="armor">
    <h3>Новая Броня 2</h3>
    <p>800 ₽</p>
    <button class="btn" onclick="addToCart('Новая Броня 2',800)">Купить</button>
  </div>
</div>

<section class="promo-banner">
  <div class="promo-content">
    <h2>Самые дешёвые вещи — только в этом магазине!</h2>
  </div>
</section>

<footer>
  <a href="https://t.me/pol1xer" target="_blank">@pol1xer</a>
  <a href="https://discord.com" target="_blank">Discord</a>
  <a href="https://vk.com" target="_blank">VK</a>
  <a href="mailto:support@metroshop.com">Email</a>
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
    b.innerHTML+=`<div class="cart-item"><span>${item.name}</span><span>${item.price} ₽</span><button onclick="removeItem(${i})">X</button></div>`;
    total+=item.price;
  });
  document.getElementById('cartTotal').innerText = total;
}
function removeItem(index){
  cart.splice(index,1);
  updateCart();
}
document.getElementById('cartBtn').onclick=()=>{document.getElementById('cartModal').style.display='block';}

// Категории
function filterCategory(cat){
  document.querySelectorAll('.item').forEach(i=>{
    i.style.display=(cat==='all'||i.dataset.category===cat)?'block':'none';
  });
}
</script>

</body>
</html>
