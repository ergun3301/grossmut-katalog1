<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Grossmut Katalog</title>

<style>
*{box-sizing:border-box}

body{
  margin:0;
  padding:20px;
  font-family:Arial;
  background:#eef1f4;
}

.panel{
  background:#fff;
  padding:15px;
  border-radius:12px;
  margin-bottom:15px;
}

input{
  padding:10px;
  border:1px solid #ccc;
  border-radius:6px;
  margin:5px;
}

button{
  padding:10px;
  border:none;
  border-radius:6px;
  font-weight:bold;
  cursor:pointer;
}

.yesil{background:green;color:#fff}
.turuncu{background:orange;color:#fff}
.gri{background:#666;color:#fff}

.poster{
  background:#fff;
  max-width:1100px;
  margin:auto;
}

.ust{
  display:flex;
  justify-content:space-between;
  padding:15px;
}

.logo{
  font-size:40px;
  font-weight:bold;
}
.logo span:first-child{color:green}
.logo span:last-child{color:orange}

.baslik{
  font-size:22px;
  font-weight:bold;
}

.tarih{
  background:green;
  color:#fff;
  padding:10px;
  border-radius:10px;
  text-align:center;
}

.qr img{
  width:100px;
}

.grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
}

.kart{
  border:1px solid #ddd;
  padding:10px;
  text-align:center;
  height:420px;
  display:flex;
  flex-direction:column;
}

.resim{
  height:200px;
}
.resim img{
  width:100%;
  height:100%;
  object-fit:contain;
}

.ad{
  font-size:22px;
  font-weight:bold;
}

.aciklama{
  font-size:13px;
  color:#666;
}

.eski{
  text-decoration:line-through;
  color:red;
}

.yeni{
  font-size:40px;
  color:green;
  font-weight:bold;
}

.alt{
  background:goldenrod;
  font-weight:bold;
  padding:5px;
  margin-top:auto;
}

@media print{
  .panel{display:none}
}
</style>
</head>

<body>

<div class="panel">
  <input id="baslikInput" placeholder="Başlık">
  <input id="tarihInput" placeholder="Tarih">
  <button class="yesil" onclick="guncelle()">Güncelle</button>

  <br>

  <input id="ad" placeholder="Ürün adı">
  <input id="aciklama" placeholder="Açıklama">
  <input id="eski" placeholder="Eski fiyat">
  <input id="yeni" placeholder="Yeni fiyat">
  <input id="resim" placeholder="Resim linki">

  <button class="turuncu" onclick="ekle()">Ürün ekle</button>
  <button class="gri" onclick="window.print()">PDF</button>
</div>

<div class="poster">

  <div class="ust">
    <div>
      <div class="logo"><span>GROSS</span> <span>MUT</span></div>
      <div class="baslik" id="baslik">Haftanın Yıldızları</div>
    </div>

    <div class="tarih" id="tarih">16-23 NİSAN</div>

    <div class="qr">
      <img src="https://api.qrserver.com/v1/create-qr-code/?size=120x120&data=https://www.instagram.com/grossmut33">
    </div>
  </div>

  <div class="grid" id="grid"></div>

</div>

<script>
let urunler=[]

function guncelle(){
  document.getElementById("baslik").innerText=document.getElementById("baslikInput").value
  document.getElementById("tarih").innerText=document.getElementById("tarihInput").value
}

function ekle(){
  if(urunler.length>=12){
    alert("Max 12 ürün")
    return
  }

  urunler.push({
    ad:ad.value,
    aciklama:aciklama.value,
    eski:eski.value,
    yeni:yeni.value,
    resim:resim.value
  })

  ciz()
}

function ciz(){
  let html=""

  for(let i=0;i<12;i++){
    let u=urunler[i]

    html+=`
    <div class="kart">
      <div class="resim">${u?`<img src="${u.resim}">`:""}</div>
      <div class="ad">${u?u.ad:""}</div>
      <div class="aciklama">${u?u.aciklama:""}</div>
      <div class="eski">${u?u.eski+" TL":""}</div>
      <div class="yeni">${u?u.yeni:""}</div>
      <div class="alt">İNDİRİM ŞOKU</div>
    </div>`
  }

  grid.innerHTML=html
}

ciz()
</script>

</body>
</html>
