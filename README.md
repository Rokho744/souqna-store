# souqna-store
Souqna - Moroccan online store for various products
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>سوقنا | SOUQNA</title>
<style>
body{font-family:Arial;background:#f6f8f5;margin:0;color:#183629}
header{background:#176b4b;color:white;padding:22px;text-align:center}
.hero{text-align:center;padding:35px 15px;background:#e5f1e9}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:15px;padding:20px}
.card{background:white;padding:20px;border-radius:15px;text-align:center}
.emoji{font-size:55px}
.price{color:#176b4b;font-weight:bold}
button{background:#176b4b;color:white;border:0;padding:12px 18px;border-radius:9px;cursor:pointer}
#cart{padding:20px;background:white;margin:20px;border-radius:12px}
</style>
</head>
<body>
<header>
<h1>🛍️ سوقنا SOUQNA</h1>
<p>كل ما تحتاجه في مكان واحد</p>
</header>
<section class="hero">
<h2>مرحباً بك في متجر سوقنا</h2>
<p>اكتشف منتجاتنا المتنوعة بأثمنة مناسبة</p>
</section>
<h2 style="text-align:center">منتجاتنا</h2>
<div class="grid" id="products"></div>
<div id="cart">
<h2>🛒 سلة المشتريات</h2>
<div id="items">السلة فارغة</div>
<h3 id="total">المجموع: 0 درهم</h3>
<input id="name" placeholder="الاسم الكامل">
<br><br>
<input id="phone" placeholder="رقم الهاتف">
<br><br>
<input id="address" placeholder="عنوان التوصيل">
<br><br>
<button onclick="order()">اطلب الآن - الدفع عند الاستلام</button>
</div>
<script>
const whatsapp="212696374968";
const products=[
["حامل هاتف للسيارة",59,"🚗"],
["منظم المنزل",59,"👜"],
["جهاز عرض النجوم",169,"🌌"],
["قطاعة الخضروات",119,"🥕"],
["رف التوابل",159,"🧂"],
["مصباح LED",59,"🔦"],
["منظم مستحضرات التجميل",109,"💄"],
["منظم الحقائب",59,"🎒"]
];
let cart={};
function display(){
document.getElementById("products").innerHTML=products.map((p,i)=>`
<div class="card">
<div class="emoji">${p[2]}</div>
<h3>${p[0]}</h3>
<p class="price">${p[1]} درهم</p>
<button onclick="add(${i})">أضف إلى السلة</button>
</div>`).join("");
}
function add(i){cart[i]=(cart[i]||0)+1;showCart();}
function showCart(){
let total=0;
let html="";
for(let i in cart){
let p=products[i],sum=p[1]*cart[i];total+=sum;
html+=`<p>${p[0]} × ${cart[i]} = ${sum} درهم</p>`;
}
document.getElementById("items").innerHTML=html||"السلة فارغة";
document.getElementById("total").innerText="المجموع: "+total+" درهم";
}
function order(){
let name=document.getElementById("name").value;
let phone=document.getElementById("phone").value;
let address=document.getElementById("address").value;
if(!name||!phone||!address||Object.keys(cart).length===0){
alert("يرجى إدخال معلوماتك واختيار منتج");return;
}
let msg="طلب جديد من سوقنا\nالاسم: "+name+"\nالهاتف: "+phone+"\nالعنوان: "+address+"\n";
let total=0;
for(let i in cart){
msg+=products[i][0]+" × "+cart[i]+"\n";
total+=products[i][1]*cart[i];
}
msg+="المجموع: "+total+" درهم\nالدفع عند الاستلام";
window.open("https://wa.me/"+whatsapp+"?text="+encodeURIComponent(msg),"_blank");
}
display();
</script>
</body>
</html>
