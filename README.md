<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Metro Shop Pol1xer — Violet Ultra 4.2</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>

<style>
/* Шрифты и переменные */
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap');
:root{
  --neon:#b400ff;
  --neon-glow:0 0 25px #b400ff,0 0 50px #b400ff;
}

/* Новый градиент без фото */
body{
  margin:0;
  font-family:'Orbitron',sans-serif;
  background:linear-gradient(145deg,#222,#000);
  color:#fff;
  overflow-x:hidden;
}

/* Категории теперь сверху */
.category{
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  margin:20px 0;
  padding-top:20px;
}
.category button{
  margin:5px;
  background:transparent;
  border:2px solid var(--neon);
  color:var(--neon);
  padding:10px 18px;
  font-size:16px;
  border-radius:10px;
  cursor:pointer;
  transition:.3s;
  text-shadow:var(--neon-glow);
}
.category button:hover{
  background:var(--neon);
  color:#000;
}

/* Сетка товаров теперь 3 в ряд даже на мобилке */
.shop-grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:15px;
  padding:20px;
}
.item{
  background:#111;
  border:2px solid var(--neon);
  border-radius:12px;
  padding:12px;
  text-align:center;
  box-shadow:0 0 20px #b400ff55;
}
.item img{
  width:100%;
  border-radius:10px;
}
.btn{
  margin-top:10px;
  padding:10px 15px;
  border-radius:10px;
  background:var(--neon);
  font-weight:700;
  border:none;
  cursor:pointer;
}

/* Фиксированные кнопки */
#cartBtn,#chatBtn,#musicBtn{
  position:fixed;
  padding:10px 18px;
  border-radius:10px;
  cursor:pointer;
  border:2px solid var(--neon);
  background:#000;
  color:var(--neon);
  z-index:50;
}

#cartBtn{ right:20px; top:20px; }
#chatBtn{ right:20px; bottom:20px; background:var(--neon); color:#000; }
#musicBtn{ left:20px; bottom:20px; }

/* Модальное окно поддержки */
#chatWindow{
  position:fixed;
  top:50%; left:50%;
  transform:translate(-50%,-50%);
  background:#111;
  border:2px solid var(--neon);
  padding:25px;
  display:none;
  border-radius:12px;
  z-index:100;
}

/* Корзина */
#cartModal{
  position:fixed;
  top:50%; left:50%;
  transform:translate(-50%,-50%);
  background:#111;
  border:2px solid var(--neon);
  padding:20px;
  display:none;
  z-index:100;
  border-radius:12px;
}

.close-cart{
  position:absolute;
  top:10px; right:10px;
  background:var(--neon);
  padding:5px 10px;
  border-radius:10px;
  cursor:pointer;
}

/* Баннер стал просто затемнённой панелью */
.promo-banner{
  margin:40px 0;
  width:100%;
  min-height:180px;
  background:linear-gradient(145deg,#333,#000);
  border:2px solid var(--neon);
  display:flex;
  align-items:center;
  justify-content:center;
}

.promo-content h2{
  font-size:26px;
  color:var(--neon);
  text-shadow:var(--neon-glow);
}

/* Footer */
.footer-content{
  text-align:center;
  padding:30px;
  background:#111;
  border-top:2px solid var(--neon);
}
.footer-links a{
  color:var(--neon);
  margin:0 10px;
  text-decoration:none;
}
</style>
</head>
<body>

<!-- Кнопки категорий вместо меню -->
<div class="category">
  <button onclick="filterCategory('all')">Все</button>
  <button onclick="filterCategory('armor')">Броня</button>
  <button onclick="filterCategory('loot')">Лут</button>
  <button onclick="filterCategory('vip')">VIP</button>
</div>

<!-- Кнопки -->
<button id="cartBtn">🛒 Корзина</button>
<button id="chatBtn">💬</button>
<button id="musicBtn">🎵</button>

<!-- Окно поддержки -->
<div id="chatWindow">
  <h3>Поддержка @pol1xer</h3>
  <button onclick="openTelegramChat()">Открыть Telegram</button>
  <button class="close-cart" onclick="document.getElementById('chatWindow').style.display='none'">✖</button>
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

<!-- Товары -->
<div class="shop-grid">

  <div class="item" data-category="armor">
    <img src="0870aa5c.jpg">
    <h3>Броня Lv.6</h3>
    <p>700 ₽</p>
    <button class="btn" onclick="addToCart('Броня Lv.6',700)">Купить</button>
  </div>

  <div class="item" data-category="armor">
    <img src="13563.jpg">
    <h3>Шлем Lv.6</h3>
    <p>450 ₽</p>
    <button class="btn" onclick="addToCart('Шлем Lv.6',450)">Купить</button>
  </div>

  <div class="item" data-category="loot">
    <img src="loot1.png">
    <h3>Фиолетовый Лут</h3>
    <p>300 ₽</p>
    <button class="btn" onclick="addToCart('Фиолетовый Лут',300)">Купить</button>
  </div>

  <!-- Новый товар -->
  <div class="item" data-category="loot">
    <img src="loot2.png">
    <h3>Редкий Лут</h3>
    <p>500 ₽</p>
    <button class="btn" onclick="addToCart('Редкий Лут',500)">Купить</button>
  </div>

  <!-- Новый товар -->
  <div class="item" data-category="vip">
    <img src="vipitem.jpg">
    <h3>VIP Пак</h3>
    <p>1200 ₽</p>
    <button class="btn" onclick="addToCart('VIP Пак',1200)">Купить</button>
  </div>

</div>

<!-- Баннер -->
<section class="promo-banner">
  <div class="promo-content">
    <h2>Самые дешёвые вещи — только у POL1XER!</h2>
  </div>
</section>

<!-- Footer -->
<footer>
  <div class="footer-content">
    <div class="footer-links">
      <a href="https://t.me/pol1xer" target="_blank">Telegram @pol1xer</a>
      <a href="https://discord.com" target="_blank">Discord</a>
      <a href="https://vk.com" target="_blank">VK</a>
    </div>
  </div>
</footer>

<script>
/* Telegram */
const tg = window.Telegram.WebApp;

/* Корзина */
let cart = [];
function addToCart(name, price){
  cart.push({name, price});
  updateCart();
}
function updateCart(){
  const b=document.getElementById('cartItems');
  b.innerHTML='';
  let total=0;
  cart.forEach((item,i)=>{
    b.innerHTML+=`<div>${item.name} — ${item.price} ₽</div>`;
    total+=item.price;
  });
  document.getElementById('cartTotal').innerText=total;
}
document.getElementById('cartBtn').onclick=()=>{document.getElementById('cartModal').style.display='block';}
function closeCart(){document.getElementById('cartModal').style.display='none';}

/* Категории */
function filterCategory(cat){
  document.querySelectorAll('.item').forEach(i=>{
    i.style.display = (cat==='all'||i.dataset.category===cat)?'block':'none';
  });
}

/* Поддержка */
document.getElementById('chatBtn').onclick=()=>{
  document.getElementById('chatWindow').style.display='block';
};
function openTelegramChat(){
  tg.openLink('https://t.me/pol1xer');
}

/* Музыка */
document.getElementById('musicBtn').onclick=()=>{
  alert("Музыка отключена в этой версии.");
};
</script>

</body>
</html>
