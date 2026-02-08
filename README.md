<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VoxelShop</title>

<style>
body{
  margin:0;
  font-family:Arial, sans-serif;
  background:#111;
  color:white;
}

header{
  background:#1b1b1b;
  padding:15px 30px;
  display:flex;
  justify-content:space-between;
  align-items:center;
}

.logo{
  font-size:22px;
  font-weight:bold;
  color:#00ffcc;
}

nav a{
  margin-left:20px;
  text-decoration:none;
  color:white;
  font-weight:bold;
}

nav a:hover{
  color:#00ffcc;
}

section{
  padding:50px 20px;
  max-width:900px;
  margin:auto;
}

.products{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
  gap:20px;
}

.card{
  background:#1c1c1c;
  padding:20px;
  border-radius:10px;
  box-shadow:0 0 10px rgba(0,0,0,0.5);
}

button{
  background:#00ffcc;
  border:none;
  padding:10px 15px;
  border-radius:6px;
  cursor:pointer;
  font-weight:bold;
}

button:hover{
  background:#00ccaa;
}

form{
  display:none;
  background:#1c1c1c;
  padding:20px;
  border-radius:10px;
  margin-top:20px;
}

input, textarea{
  width:100%;
  padding:10px;
  margin-top:10px;
  border-radius:6px;
  border:none;
}

footer{
  background:#1b1b1b;
  text-align:center;
  padding:30px;
  margin-top:40px;
}
</style>
</head>

<body>

<header>
  <div class="logo">VoxelShop</div>
  <nav>
    <a href="#about">Über uns</a>
    <a href="#products">Produkte</a>
    <a href="#contact">Kontakt</a>
  </nav>
</header>

<section id="about">
  <h2>Über uns</h2>
  <p>
    VoxelShop wir sind eine kleine Gruppe aus Designern, Programmierer und Beats Ersteller.
    Wir wollen unsere Produkte billig verkaufen.
  </p>
</section>

<section id="products">
  <h2>Unsere Produkte</h2>

  <div class="products">

    <div class="card">
      <h3>Eigene Roblox Scripts</h3>
      <p>Preis: 10€</p>
      <button onclick="openForm('Roblox Script')">Kaufen</button>
    </div>

    <div class="card">
      <h3>Eigene Bilder</h3>
      <p>Preis: 5€</p>
      <button onclick="openForm('Bild')">Kaufen</button>
    </div>

    <div class="card">
      <h3>Eigene Beats</h3>
      <p>Preis: 5€</p>
      <button onclick="openForm('Beat')">Kaufen</button>
    </div>

  </div>

  <form id="orderForm">
    <h3>Produkt Infos</h3>
    <p id="productName"></p>

    <label>Beschreibung: Wie soll dein Produkt aussehen / können?</label>
    <textarea id="beschreibung" required></textarea>

    <label>Email:</label>
    <input type="email" id="email" required>

    <button type="submit">Absenden</button>
  </form>
</section>

<section id="contact">
  <h2>Kontakt</h2>
  <p>Discord:</p>
  <a href="https://discord.gg/u2X7hZKZbQ" target="_blank" style="color:#00ffcc;">
    https://discord.gg/u2X7hZKZbQ
  </a>
</section>

<footer>
  © 2026 VoxelShop
</footer>

<script>
let selectedProduct = "";

function openForm(product){
  selectedProduct = product;
  document.getElementById("orderForm").style.display = "block";
  document.getElementById("productName").innerText = "Produkt: " + product;
}

document.getElementById("orderForm").addEventListener("submit", function(e){
  e.preventDefault();

  const beschreibung = document.getElementById("beschreibung").value;
  const email = document.getElementById("email").value;

  fetch("https://discord.com/api/webhooks/1469853218958741504/YdvphiXBfz0-SctC9aEz751dZsS_7AfnkXOltBs2xkkF2TiGpCneKl1eMcQTtHgqRypW", {
    method:"POST",
    headers:{"Content-Type":"application/json"},
    body:JSON.stringify({
      content:
      "**Neue Bestellung**\n" +
      "Produkt: " + selectedProduct + "\n" +
      "Beschreibung: " + beschreibung + "\n" +
      "Email: " + email
    })
  });

  alert("Bestellung gesendet!");
  document.getElementById("orderForm").reset();
  document.getElementById("orderForm").style.display = "none";
});
</script>

</body>
</html>
