# birthday-surprise
index.html.

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Happy Birthday Bestie 💗</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;text-align:center;font-family:Arial,sans-serif;
 color:#713d59;background:linear-gradient(135deg,#ffe4ef,#eee6ff);
}
header{padding:35px 15px}
h1{font-size:clamp(35px,8vw,55px);color:#d74483}
h2{color:#c13d79}
p{line-height:1.7}
.card{
 background:#ffffffdf;margin:20px auto;padding:25px 18px;
 width:92%;max-width:650px;border-radius:25px;
 box-shadow:0 8px 30px #bb7b9b25;
}
button{
 border:0;border-radius:25px;padding:13px 20px;
 background:#ed6da1;color:white;font-size:16px;
 margin:7px;cursor:pointer;
}
button:hover{transform:scale(1.04)}
#gift{font-size:100px;cursor:pointer;animation:bounce 1.5s infinite}
@keyframes bounce{50%{transform:translateY(-10px)}}
.hidden{display:none}
.letter{
 background:#fff7e8;padding:20px;border-radius:15px;
 line-height:1.9;white-space:pre-line;text-align:left
}
.gallery{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.gallery img{width:100%;aspect-ratio:1;object-fit:cover;border-radius:12px}
.heart{position:fixed;bottom:-30px;animation:up 4s linear forwards;pointer-events:none}
@keyframes up{to{transform:translateY(-110vh);opacity:0}}
.cake{font-size:85px}
footer{padding:30px}
</style>
</head>
<body>

<header>
<p>🌸 A LITTLE SURPRISE FOR YOU 🌸</p>
<h1>Happy Birthday Bestie! 🎂</h1>
<p>Someone amazing deserves a magical day 💗</p>
<p>Made with love by <b>Kiran</b> 💌</p>
</header>

<section class="card">
<h2>🎁 Your Surprise Gift</h2>
<p>Tap the gift to open your surprise!</p>
<div id="gift" onclick="openGift()">🎁</div>
<button onclick="openGift()">Open My Gift 💝</button>
<p id="surprise" class="hidden">
✨ SURPRISE! ✨<br>
You are one of the most special people in my life! 💖
</p>
</section>

<section class="card">
<h2>💌 A Secret Letter</h2>
<p>There is something from my heart for you...</p>
<button onclick="toggleLetter()">Unlock Your Letter 🔐</button>
<div id="letter" class="letter hidden">
Happy Birthday, Bestie! 💗🎂

Thank you for all the laughs, memories, and beautiful moments.
I hope your life is always filled with happiness, success,
love, and endless reasons to smile.

May every dream you have come true.
Never stop being the wonderful person you are!

Thank you for being my best friend.
You deserve the most beautiful things in life. 🌷

With lots of love,
Kiran 💕
</div>
</section>

<section class="card">
<h2>🎂 Make a Birthday Wish</h2>
<p>Close your eyes and make a wish!</p>
<div class="cake">🎂</div>
<div id="candles" style="font-size:30px">🕯️ 🕯️ 🕯️</div>
<button onclick="blow()">Blow Out the Candles ✨</button>
<p id="wish" class="hidden">🌟 Your wish is sent to the universe! 💖</p>
</section>

<section class="card">
<h2>📸 Our Memory Gallery</h2>
<p>Choose your favourite photos together!</p>
<input type="file" id="photos" accept="image/*" multiple>
<div id="gallery" class="gallery"></div>
<p><small>Choose photos from your phone to preview them.</small></p>
</section>

<section class="card">
<h2>🎵 Birthday Music</h2>
<p>Tap below to play a little birthday tune.</p>
<button onclick="playMusic()">Play Music ♫</button>
<button onclick="stopMusic()">Stop Music</button>
<p><small>Music plays after you tap the button.</small></p>
</section>

<section class="card">
<h2>💗 One Last Thing...</h2>
<p>May your smile shine brighter than all the stars!</p>
<button onclick="celebrate()">Send You a Million Hearts 💖</button>
</section>

<footer>
Made with 💗 by Kiran<br>
For the best friend ever 🌸
</footer>

<script>
function openGift(){
 document.getElementById("gift").innerText="💝";
 document.getElementById("surprise").classList.remove("hidden");
 hearts();
}
function toggleLetter(){
 document.getElementById("letter").classList.toggle("hidden");
}
function blow(){
 document.getElementById("candles").innerText="💨 💨 💨";
 document.getElementById("wish").classList.remove("hidden");
 hearts();
}
document.getElementById("photos").addEventListener("change",function(){
 const gallery=document.getElementById("gallery");
 gallery.innerHTML="";
 [...this.files].slice(0,9).forEach(file=>{
  if(!file.type.startsWith("image/"))return;
  const img=document.createElement("img");
  img.src=URL.createObjectURL(file);
  img.alt="Birthday memory";
  gallery.appendChild(img);
 });
});
let ctx, timers=[];
function playMusic(){
 stopMusic();
 const AC=window.AudioContext||window.webkitAudioContext;
 if(!AC){alert("Music is not supported in this browser.");return}
 ctx=new AC();
 const notes=[523,659,784,659,587,698,784,1047];
 notes.forEach((note,i)=>{
  const osc=ctx.createOscillator();
  const gain=ctx.createGain();
  osc.frequency.value=note;
  gain.gain.value=.08;
  osc.connect(gain);
  gain.connect(ctx.destination);
  const start=ctx.currentTime+i*.3;
  osc.start(start);
  gain.gain.setValueAtTime(.08,start);
  gain.gain.setValueAtTime(0,start+.23);
  osc.stop(start+.24);
 });
 timers.push(setTimeout(stopMusic,notes.length*300+500));
}
function stopMusic(){
 timers.forEach(clearTimeout);timers=[];
 if(ctx){ctx.close();ctx=null}
}
function hearts(){
 const symbols=["💗","💕","💖","🌸","✨"];
 for(let i=0;i<22;i++){
  const el=document.createElement("span");
  el.className="heart";
  el.innerText=symbols[Math.floor(Math.random()*symbols.length)];
  el.style.left=Math.random()*100+"vw";
  el.style.fontSize=(18+Math.random()*20)+"px";
  el.style.animationDuration=(3+Math.random()*3)+"s";
  document.body.appendChild(el);
  setTimeout(()=>el.remove(),6500);
 }
}
function celebrate(){hearts()}
</script>
</body>
</html>

