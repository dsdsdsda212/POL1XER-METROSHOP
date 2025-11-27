<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Metro Shop Pol1xer — Mini App</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap');

:root{
  --neon:#b400ff;
  --neon-glow:0 0 15px #b400ff,0 0 30px #b400ff;
}

body{
  margin:0;
  font-family:'Orbitron',sans-serif;
  background:linear-gradient(160deg,#555,#000);
  color:#fff;
  overflow-x:hidden;
  -webkit-tap-highlight-color: transparent;
}

header{
  text-align:center;
  padding:15px 10px;
}
header h1{
  margin:0;
  font-size:28px;
  color:var(--neon);
  text-shadow:var(--neon-glow);
}

.category{
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  margin:10px 0;
}
.category button{
  margin:5px;
  flex:1 1 40%;
  min-width:100px;
  background:transparent;
  border:2px solid var(--neon);
  color:var(--neon);
  padding:10px 0;
  border-radius:8px;
  font-size:14px;
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
  grid-template-columns:repeat(auto-fit,minmax(140px,1fr));
  gap:10px;
  padding:10px;
}
.item{
  background:rgba(0,0,0,.55);
  border:2px solid var(--neon);
  border-radius:10px;
  padding:10px;
  text-align:center;
  font-size:14px;
}
.item:hover{
  transform:scale(1.05);
}
.item img{
  width:100%;
  border-radius:8px;
  margin-bottom:5px;
}

.btn{
  display:block;
  width:100%;
  margin-top:5px;
  padding:8px 0;
  border-radius:6px;
  color:#000;
  background:var(--neon);
  font-weight:700;
  text-decoration:none;
  cursor:pointer;
  transition:.3s;
}
.btn:hover{
  transform:scale(1.05);
  box-shadow:0 0 20px var(--neon);
}

/* Корзина */
#cartBtn{
  position:fixed; right:10px; bottom:10px; 
  padding:10px 14px; border-radius:50%; 
  border:2px solid var(--neon);
  background:rgba(0,0,0,0.7); color:var(--neon);
  z-index:50;
}

#cartModal{
  position:fixed;
  top:50%;
  left:50%;
  transform:translate(-50%,-50%);
  background:rgba(0,0,0,.9);
  border:2px solid var(--neon);
  border-radius:12px;
  padding:15px;
  display:none;
  z-index:100;
  width:90%;
  max-width:350px;
}

.cart-item{
  display:flex; justify-content:space-between; padding:5px 0;
  border-bottom:1px solid var(--neon);
}
.cart-item button{
  border:none; background:var(--neon); color:#000;
  padding:3px 6px; border-radius:5px; cursor:pointer; font-size:12px;
}
.close-cart{
  margin-top:10px;
  width:100%;
  padding:8px 0;
  background:var(--neon); color:#000;
  border:none; border-radius:8px;
  font-weight:bold; cursor:pointer;
}

.promo-banner{
  margin:15px 10px;
  width:calc(100% - 20px);
  min-height:120px;
  display:flex;
  justify-content:center;
  align-items:center;
  overflow:hidden;
  border:2px solid var(--neon);
}
.promo-content h2{
  font-size:16px;
  color:var(--neon);
  text-align:center;
  font-weight:700;
}
footer{
  padding:15px 5px;
  text-align:center;
  font-size:12px;
}
footer a{
  color:var(--neon); margin:0 5px; text-decoration:none; font-weight:700;
}
footer a:hover{text-decoration:underline;}
</style>
</head>
<body>

<header>
  <h1>МЕТРО ШОП POL1XER</h1>
</header>

<div class="category">
  <button onclick="filterCategory('all')">Все</button>
  <button onclick="filterCategory('armor')">Броня</button>
  <button onclick="filterCategory('loot')">Лут</button>
  <button onclick="filterCategory('vip')">VIP</button>
</div>

<div class="shop-grid">
  <div class="item" data-category="armor"><h3>Броня Lv.6</h3><p>700 ₽</p><button class="btn" onclick="addToCart('Броня Lv.6',700)">Купить</button></div>
  <div class="item" data-category="armor"><h3>Шлем Lv.6</h3><p>450 ₽</p><button class="btn" onclick="addToCart('Шлем Lv.6',450)">Купить</button></div>
  <div class="item" data-category="loot"><h3>Фиолетовый Лут</h3><p>300 ₽</p><button class="btn" onclick="addToCart('Фиолетовый Лут',300)">Купить</button></div>
  <div class="item" data-category="vip"><h3>МК14 ВЫШКА</h3><p>900 ₽</p><button class="btn" onclick="addToCart('МК14 ВЫШКА',900)">Купить</button></div>
  <div class="item" data-category="loot"><h3>Новый Лут 1</h3><p>350 ₽</p><button class="btn" onclick="addToCart('Новый Лут 1',350)">Купить</button></div>
  <div class="item" data-category="armor"><h3>Новая Броня 2</h3><p>800 ₽</p><button class="btn" onclick="addToCart('Новая Броня 2',800)">Купить</button></div>
</div>

<section class="promo-banner">
  <div class="promo-content">
    <h2>Самые дешёвые вещи — только в этом магазине!</h2>
  </div>
</section>

<button id="cartBtn">🛒</button>

<div id="cartModal">
  <h2>Корзина</h2>
  <div id="cartItems"></div>
  <h3>Итого: <span id="cartTotal">0</span> ₽</h3>
  <button class="close-cart" onclick="document.getElementById('cartModal').style.display='none'">Закрыть</button>
</div>

<footer>
  <a href="https://t.me/pol1xer" target="_blank">@pol1xer</a>
  <a href="https://discord.com" target="_blank">Discord</a>
  <a href="https://vk.com" target="_blank">VK</a>
  <a href="mailto:support@metroshop.com">Email</a>
</footer>

<script>
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
