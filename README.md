# Grambanglar-Traditional-Food
<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Grambanglar Full Marketplace</title>

<style>
body{font-family:Arial;margin:0;background:#f5f5f5;}

header{
  background:#1b5e20;
  color:white;
  padding:15px;
  text-align:center;
}

.container{padding:10px;}

.grid{
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:10px;
}

.card{
  background:white;
  padding:10px;
  border-radius:10px;
}

button{
  width:100%;
  padding:8px;
  background:#2e7d32;
  color:white;
  border:none;
  margin-top:5px;
}

.section{
  background:white;
  margin:10px;
  padding:10px;
  border-radius:10px;
}

input{
  width:100%;
  padding:8px;
  margin:5px 0;
}

footer{
  text-align:center;
  background:#1b5e20;
  color:white;
  padding:10px;
}
</style>
</head>

<body>

<header>
🌾 Grambanglar Traditional Food - FULL MARKET
</header>

<div class="section">
🛒 Cart: <span id="cartCount">0</span> | 💰 Total: ৳ <span id="cartTotal">0</span>
</div>

<div class="container">

<h3>🛍️ Products</h3>
<div class="grid" id="productList"></div>

<h3>➕ Admin Add Product</h3>
<div class="section">
<input id="pname" placeholder="Product Name">
<input id="pprice" placeholder="Price">
<button onclick="addProduct()">Add Product</button>
</div>

<h3>🧾 Checkout</h3>
<div class="section">
<input id="name" placeholder="Name">
<input id="phone" placeholder="Phone">
<input id="address" placeholder="Address">

<select id="payment">
<option>Cash on Delivery</option>
<option>bKash</option>
<option>Bank Transfer</option>
</select>

<button onclick="placeOrder()">Place Order</button>
</div>

</div>

<footer>
🚚 24H Delivery Dhaka | COD | bKash | Bank
</footer>

<script>

// load products
let products = JSON.parse(localStorage.getItem("products")) || [
  {name:"খাঁটি ঘি", price:650},
  {name:"আতপ চাল", price:420},
  {name:"মধু", price:550},
  {name:"আচার", price:250}
];

let cart = [];

function render(){
  let list = document.getElementById("productList");
  list.innerHTML = "";

  products.forEach((p,i)=>{
    list.innerHTML += `
      <div class="card">
        <h4>${p.name}</h4>
        <p>৳ ${p.price}</p>
        <button onclick="addCart(${i})">Add to Cart</button>
      </div>
    `;
  });
}

function addCart(i){
  cart.push(products[i]);
  updateCart();
}

function updateCart(){
  let total = 0;
  cart.forEach(c => total += parseInt(c.price));

  document.getElementById("cartCount").innerText = cart.length;
  document.getElementById("cartTotal").innerText = total;
}

function addProduct(){
  let name = document.getElementById("pname").value;
  let price = document.getElementById("pprice").value;

  if(name && price){
    products.push({name,price});
    localStorage.setItem("products", JSON.stringify(products));
    render();
    alert("Product Added!");
  }
}

function placeOrder(){
  let name = document.getElementById("name").value;
  let phone = document.getElementById("phone").value;
  let address = document.getElementById("address").value;

  if(cart.length==0){
    alert("Cart empty!");
    return;
  }

  alert("Order Placed Successfully!\nThank you 🌾");

  cart = [];
  updateCart();
}

render();

</script>

</body>
</html>
