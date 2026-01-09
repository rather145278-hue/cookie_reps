<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<title>Link Converter | cookiereps</title>

<link href="https://fonts.googleapis.com/css2?family=Lexend:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
*{box-sizing:border-box;font-family:'Lexend',sans-serif}

body{
  margin:0;
  background:#0b0b0b;
  color:#fff;
  min-height:100vh;
}

.logo{
  position:fixed;
  top:20px;
  left:25px;
  font-size:22px;
  font-weight:700;
}

/* 🔥 IKONY */
.top-icons{
  position:fixed;
  top:18px;
  right:25px;
  display:flex;
  gap:12px;
  z-index:10;
}

.icon{
  width:64px;
  height:64px;
  border-radius:50%;
  background:#141414;
  border:2px solid #2de2e6;
  display:flex;
  align-items:center;
  justify-content:center;
  color:#fff;
  font-size:11px;
  font-weight:600;
  cursor:pointer;
  transition:.2s;
  position:relative;
  text-align:center;
  line-height:1.1;
}

.icon:hover{
  box-shadow:0 0 16px rgba(45,226,230,.8);
  transform:scale(1.05);
}

/* TOOLTIP */
.icon[data-tip]:hover::after{
  content:attr(data-tip);
  position:absolute;
  top:70px;
  background:#fff;
  color:#000;
  padding:6px 10px;
  border-radius:8px;
  font-size:11px;
  white-space:nowrap;
  box-shadow:0 4px 14px rgba(0,0,0,.4);
}

.container{
  max-width:700px;
  margin:0 auto;
  padding:120px 20px 50px;
  text-align:center;
}

h1{font-size:40px;margin-bottom:8px}
.subtitle{color:#bbb;margin-bottom:35px}

textarea{
  width:80%;
  height:90px;
  background:#141414;
  border:1px solid #222;
  color:#fff;
  border-radius:25px;
  padding:18px 20px;
  outline:none;
  resize:none;
}

button{
  margin-top:22px;
  padding:14px 34px;
  border-radius:40px;
  background:#fff;
  color:#000;
  font-weight:600;
  cursor:pointer;
}

button:hover{
  background:#000;
  color:#fff;
  box-shadow:0 0 12px rgba(255,255,255,.5);
}

.results{
  margin-top:40px;
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(140px,1fr));
  gap:14px;
}

.result{
  background:#141414;
  padding:18px;
  border-radius:16px;
  border:1px solid #222;
}

.result:hover{
  border-color:#fff;
  box-shadow:0 0 10px rgba(255,255,255,.35);
}

.result a{
  color:#fff;
  text-decoration:none;
  font-weight:600;
}

.sheet-box{
  margin-top:45px;
  padding:22px;
  background:#111;
  border-radius:20px;
  border:1px solid #222;
}

.sheet-box a{
  color:#2de2e6;
  text-decoration:none;
  font-weight:600;
}
</style>
</head>

<body>

<div class="logo">cookiereps</div>

<!-- 🔥 KÓŁKA -->
<div class="top-icons">
  <a class="icon" data-tip="CNFans register" href="https://cnfans.com/register?ref=150969" target="_blank">CNFans</a>
  <a class="icon" data-tip="Kakobuy register" href="https://ikako.vip/r/cookie100" target="_blank">Kakobuy</a>
  <a class="icon" data-tip="USFans register" href="https://www.usfans.com/register?ref=8KXPBM" target="_blank">USFans</a>
  <a class="icon" data-tip="LitBuy register" href="https://litbuy.com/register?inviteCode=GWQAFABFI" target="_blank">LitBuy</a>
  <a class="icon" data-tip="ACBuy register" href="https://www.acbuy.com/login?loginStatus=register&code=U45G96" target="_blank">ACBuy</a>
  <a class="icon" data-tip="MuleBuy register" href="https://mulebuy.com/register?ref=200855897" target="_blank">MuleBuy</a>
  <a class="icon" data-tip="OOPBuy register" href="https://oopbuy.com/register?inviteCode=YG9049LND" target="_blank">OOPBuy</a>
</div>

<div class="container">
  <h1>Link Converter</h1>
  <div class="subtitle">Konwertuj linki do agentów jednym kliknięciem</div>

  <textarea id="input" placeholder="Wklej link produktu..."></textarea><br>
  <button onclick="convert()">Konwertuj</button>

  <div class="results" id="results"></div>

  <div class="sheet-box">
    <a target="_blank"
       href="https://docs.google.com/spreadsheets/d/10Nk0ddtukGL0hDlFWdl2NCCMVYgEqeX5Bjmyj_6mvlg/edit?gid=0#gid=0">
      📄 Przejdź do pełnego Spreadsheeta
    </a>
  </div>
</div>

<script>
function convert(){
  const input = document.getElementById("input").value.toLowerCase();
  const res = document.getElementById("results");
  res.innerHTML = "";

  const id = input.match(/\d{6,}/)?.[0];
  if(!id) return;

  // ✅ POPRAWNE WYKRYWANIE PLATFORMY
  let platform = "";

  if (input.includes("1688")) {
    platform = "ALI_1688";
  } 
  else if (
    input.includes("weidian") ||
    input.includes("wd")
  ) {
    platform = "WEIDIAN";
  } 
  else if (
    input.includes("taobao") ||
    input.includes("tmall") ||
    input.includes("tb.cn")
  ) {
    platform = "TAOBAO";
  } 
  else {
    platform = "WEIDIAN";
  }

  // ✅ SOURCE URL (KLUCZ DO KAKOBUY)
  let sourceUrl = "";
  if (platform === "WEIDIAN") {
    sourceUrl = `https://weidian.com/item.html?itemID=${id}`;
  } 
  else if (platform === "ALI_1688") {
    sourceUrl = `https://detail.1688.com/offer/${id}.html`;
  } 
  else {
    sourceUrl = `https://item.taobao.com/item.htm?id=${id}`;
  }

  const kakobuy =
    `https://www.kakobuy.com/item/details?url=${encodeURIComponent(sourceUrl)}&affcode=cookie100`;

  const links = [
    ["CNFans", `https://cnfans.com/product?id=${id}&platform=${platform}&ref=150969`],
    ["Kakobuy", kakobuy],
    ["USFans",
      platform==="ALI_1688"
        ?`https://usfans.com/product/1/${id}?ref=8KXPBM`
        :platform==="TAOBAO"
        ?`https://usfans.com/product/2/${id}?ref=8KXPBM`
        :`https://usfans.com/product/3/${id}?ref=8KXPBM`
    ],
    ["ACBuy", `https://www.acbuy.com/product?id=${id}&source=${
      platform==="ALI_1688"?"AL":platform==="TAOBAO"?"TB":"WD"
    }&code=U45G96`],
    ["MuleBuy", `https://mulebuy.com/product?id=${id}&platform=${platform}&ref=200855897`],
    ["OOPBuy",
      platform==="ALI_1688"
        ?`https://www.oopbuy.com/product/0/${id}?inviteCode=YG9049LND`
        :platform==="TAOBAO"
        ?`https://www.oopbuy.com/product/1/${id}?inviteCode=YG9049LND`
        :`https://www.oopbuy.com/product/weidian/${id}?inviteCode=YG9049LND`
    ]
  ];

  links.forEach(l=>{
    const d=document.createElement("div");
    d.className="result";
    d.innerHTML=`<a target="_blank" href="${l[1]}">${l[0]}</a>`;
    res.appendChild(d);
  });
}
</script>

</body>
</html>
