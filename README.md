Claude











Bangun datar ajaib · HTML
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Bangun Datar Ajaib – by herman23</title>
<link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@600;800&family=Nunito:wght@500;700&display=swap" rel="stylesheet">
<style>
:root{--bg:#eaf4ff;--grid:#c9def5;--card:#fff;--ink:#1f2a44;--mute:#5b6a88;--acc:#3d8bfd;--red:#e63946;--line:#1f2a44;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#121a2e;--grid:#22304f;--card:#1b2640;--ink:#f1f5ff;--mute:#a9b7d6;--line:#f1f5ff}}
:root[data-theme="dark"]{--bg:#121a2e;--grid:#22304f;--card:#1b2640;--ink:#f1f5ff;--mute:#a9b7d6;--line:#f1f5ff}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:500 16px/1.5 Nunito,system-ui,sans-serif}
h1,h2{font-family:"Baloo 2",system-ui,sans-serif;margin:0;line-height:1.1}
header{padding:20px 16px 8px;text-align:center}
h1{font-size:clamp(28px,6vw,44px);font-weight:800}
header p{margin:4px 0 0;color:var(--mute)}
#pick{display:flex;gap:8px;overflow-x:auto;padding:10px 16px;justify-content:safe center}
#pick button{flex:none;width:76px;border:3px solid transparent;background:var(--card);border-radius:16px;padding:6px 4px;color:var(--ink);font:700 12px Nunito,sans-serif;cursor:pointer}
#pick button.on{border-color:var(--acc)}
#pick svg{width:48px;height:48px;display:block;margin:0 auto 2px}
main{display:grid;grid-template-columns:minmax(0,1.15fr) minmax(0,1fr);gap:16px;max-width:1040px;margin:0 auto;padding:8px 16px 24px}
@media(max-width:760px){main{grid-template-columns:1fr}}
.stage,.panel{background:var(--card);border-radius:24px;padding:14px}
#sv{width:100%;height:auto;display:block;border-radius:16px;touch-action:none;cursor:grab;
background-color:var(--bg);background-image:linear-gradient(var(--grid) 1px,transparent 1px),linear-gradient(90deg,var(--grid) 1px,transparent 1px);background-size:20px 20px}
#msg{min-height:48px;margin:10px 4px 0;font-weight:700}
.sw{display:flex;gap:8px;align-items:center;flex-wrap:wrap;margin-top:6px}
.sw i{width:34px;height:34px;border-radius:50%;border:3px solid var(--card);box-shadow:0 0 0 2px var(--line);cursor:pointer}
.sw span{color:var(--mute);font-size:14px}
.tabs{display:flex;gap:6px;margin-bottom:12px}
.tabs button{flex:1;padding:10px 4px;border:0;border-radius:14px;background:var(--bg);color:var(--ink);font:800 16px "Baloo 2",sans-serif;cursor:pointer}
.tabs button.on{background:var(--acc);color:#fff}
button.act{border:0;border-radius:14px;padding:10px 14px;background:var(--acc);color:#fff;font:800 15px "Baloo 2",sans-serif;cursor:pointer;margin:6px 6px 0 0}
button.act.alt{background:var(--bg);color:var(--ink)}
button:focus-visible,input:focus-visible,.sw i:focus-visible{outline:3px solid var(--red);outline-offset:2px}
.chip{display:inline-block;border:2px solid var(--acc);border-radius:20px;padding:4px 12px;margin:0 6px 6px 0;background:none;color:var(--ink);font:700 14px Nunito,sans-serif;cursor:pointer}
.chip.on{background:var(--acc);color:#fff}
ul{padding-left:20px;margin:8px 0}
li{margin:4px 0}
.fact{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin:10px 0}
.fact div{background:var(--bg);border-radius:14px;padding:8px 10px;font-size:14px}
.fact b{display:block;font:800 22px "Baloo 2",sans-serif}
input[type=range]{width:100%;accent-color:var(--acc);margin:8px 0}
.hint{color:var(--mute);font-size:14px}
footer{text-align:center;padding:0 16px 24px;color:var(--mute);font-weight:700}
</style>
</head>
<body>
<header><h1>Bangun Datar Ajaib</h1><p>Media belajar Matematika kelas 5 · Geometri · by herman23</p></header>
<nav id="pick" aria-label="Pilih bangun datar"></nav>
<main>
 <section class="stage">
  <svg id="sv" viewBox="0 0 400 360" role="img" aria-label="Bangun datar yang bisa digeser"></svg>
  <div id="msg" aria-live="polite"></div>
  <div class="sw" id="sw"><span>Warna:</span></div>
  <div class="sw"><button class="act alt" id="snd">🔊 Suara: nyala</button><button class="act alt" id="say">🗣️ Bacakan</button></div>
 </section>
 <section class="panel">
  <div class="tabs" id="tabs"></div>
  <div id="pane"></div>
 </section>
</main>
<footer>Sentuh dan geser bangun datarnya. Ketuk untuk mengganti warna.</footer>
<script>
const P=['#ff6b6b','#ffc233','#2bc48a','#3d8bfd','#9b5de5','#ff8fab'];
const S=[
{n:'Persegi',p:[[-70,-70],[70,-70],[70,70],[-70,70]],ax:[0,90,45,135],o:4,sisi:4,sdt:'4 sudut siku-siku',c:['Keempat sisinya sama panjang','Keempat sudutnya siku-siku (90°)','Sisi yang berhadapan sejajar','Kedua diagonalnya sama panjang dan berpotongan tegak lurus']},
{n:'Persegi Panjang',p:[[-90,-55],[90,-55],[90,55],[-90,55]],ax:[0,90],o:2,sisi:4,sdt:'4 sudut siku-siku',c:['Sisi berhadapan sama panjang dan sejajar','Keempat sudutnya siku-siku (90°)','Kedua diagonalnya sama panjang']},
{n:'Segitiga Sama Sisi',p:[[0,-87],[75,43],[-75,43]],ax:[90,30,150],o:3,sisi:3,sdt:'3 sudut sama besar (60°)',c:['Ketiga sisinya sama panjang','Ketiga sudutnya sama besar, yaitu 60°','Jumlah ketiga sudutnya 180°']},
{n:'Jajargenjang',p:[[-90,50],[30,50],[90,-50],[-30,-50]],ax:[],o:2,sisi:4,sdt:'2 sudut tumpul, 2 sudut lancip',c:['Sisi berhadapan sama panjang dan sejajar','Sudut berhadapan sama besar','Tidak punya sumbu simetri lipat','Diagonalnya tidak sama panjang']},
{n:'Belah Ketupat',p:[[0,-90],[60,0],[0,90],[-60,0]],ax:[0,90],o:2,sisi:4,sdt:'sudut berhadapan sama besar',c:['Keempat sisinya sama panjang','Sudut berhadapan sama besar','Kedua diagonalnya berpotongan tegak lurus','Diagonalnya tidak sama panjang']},
{n:'Layang-layang',p:[[0,-90],[60,-20],[0,90],[-60,-20]],ax:[90],o:1,sisi:4,sdt:'1 pasang sudut sama besar',c:['Dua pasang sisi yang sama panjang','Satu pasang sudut berhadapan sama besar','Diagonalnya berpotongan tegak lurus','Punya 1 sumbu simetri lipat']},
{n:'Trapesium Sama Kaki',p:[[-50,-50],[50,-50],[90,50],[-90,50]],ax:[90],o:1,sisi:4,sdt:'sudut alas sama besar',c:['Punya sepasang sisi sejajar','Kedua kakinya sama panjang','Sudut pada alas sama besar','Punya 1 sumbu simetri lipat']},
{n:'Lingkaran',p:null,ax:[0,45,90,135],o:0,sisi:0,sdt:'tidak punya sudut',c:['Tidak punya sudut dan tidak punya sisi lurus','Semua titik tepi berjarak sama dari pusat','Jari-jari adalah jarak pusat ke tepi','Diameter = 2 × jari-jari']}
];
const st={i:0,col:0,dx:0,dy:0,mode:0,ai:0,v:0,r:0,pas:false,snd:true};
const $=id=>document.getElementById(id),sv=$('sv');
let ac;
function tone(f,d=.18,t='sine',v=.15){if(!st.snd)return;try{ac=ac||new (window.AudioContext||window.webkitAudioContext)();const o=ac.createOscillator(),g=ac.createGain();o.type=t;o.frequency.value=f;g.gain.setValueAtTime(v,ac.currentTime);g.gain.exponentialRampToValueAtTime(.001,ac.currentTime+d);o.connect(g).connect(ac.destination);o.start();o.stop(ac.currentTime+d)}catch(e){}}
const note=[523,587,659,784,880,988];
function chime(){[523,659,784].forEach((f,k)=>setTimeout(()=>tone(f,.25,'triangle'),k*110))}
const sh=()=>S[st.i];
function el(c,extra=''){const s=sh();const a=`fill="${c}" fill-opacity=".85" stroke="var(--line)" stroke-width="3" stroke-linejoin="round" ${extra}`;
 return s.p?`<polygon points="${s.p.map(q=>q.join(',')).join(' ')}" ${a}/>`:`<circle r="80" ${a}/>`}
function mark(){const s=sh(),q=s.p?s.p[0]:[80,0];return `<circle cx="${q[0]}" cy="${q[1]}" r="8" fill="#fff" stroke="var(--line)" stroke-width="3"/><path d="M-8 0H8M0 -8V8" stroke="var(--line)" stroke-width="3"/>`}
function draw(){
 const s=sh(),c=P[st.col];let g='';
 if(st.mode==0){
  g=el(c)+(s.p?s.p.map((q,k)=>`<text x="${q[0]*1.22}" y="${q[1]*1.22+6}" text-anchor="middle" font-family="Baloo 2,sans-serif" font-weight="800" font-size="20" fill="var(--ink)">${'ABCD'[k]}</text>`).join(''):'<path d="M0 0H80" stroke="var(--line)" stroke-width="3"/><text x="40" y="-8" text-anchor="middle" font-weight="700" fill="var(--ink)">r</text>')+'<circle r="4" fill="var(--line)"/>';
 }else if(st.mode==1){
  const a=axes()[st.ai],k=Math.cos(Math.PI*st.v/100);
  g=`<g transform="rotate(${a})"><g clip-path="url(#bot)"><g transform="rotate(${-a})">${el(c)}${mark()}</g></g></g>
  <g transform="rotate(${a})"><g transform="scale(1,${k})" clip-path="url(#top)"><g transform="rotate(${-a})">${el(c)}${mark()}</g></g>
  <line x1="-170" x2="170" stroke="var(--red)" stroke-width="3" stroke-dasharray="9 6"/></g>`;
 }else{
  g=`<g opacity=".6">${el('none','stroke-dasharray="8 6"')}</g><g transform="rotate(${st.r})">${el(c)}${mark()}</g>`;
 }
 sv.innerHTML=`<defs><clipPath id="top"><rect x="-300" y="0" width="600" height="300"/></clipPath><clipPath id="bot"><rect x="-300" y="-300" width="600" height="300"/></clipPath></defs><g transform="translate(${200+st.dx},${180+st.dy})">${g}</g>`;
}
function axes(){const s=sh();return s.ax.length?s.ax:[0]}
function setMsg(t){$('msg').textContent=t}
function stepDeg(){const o=sh().o;return o?360/o:360}
function check(){
 const s=sh();let ok=false;
 if(st.mode==1){ok=st.v>=99;const demo=!s.ax.length;
  if(ok&&!st.pas){st.pas=true;if(demo){tone(160,.4,'sawtooth');setMsg('Tidak berimpit! Garis ini bukan sumbu simetri lipat. Jajargenjang tidak punya simetri lipat.')}else{chime();setMsg('Berimpit tepat! Garis merah ini adalah sumbu simetri lipat.')}}
  if(!ok&&st.v<95){st.pas=false;setMsg('Geser penggeser untuk melipat bangun di sepanjang garis merah.')}}
 if(st.mode==2){const d=stepDeg(),m=st.r%d,hit=(m<2||d-m<2)&&st.r>1;
  if(s.o==0&&st.r>1&&st.r<359)hit&&0;
  if(hit&&!st.pas){st.pas=true;chime();setMsg(`Pas! Diputar ${Math.round(st.r)}° bangun menempati bingkai semula.`)}
  if(!hit){st.pas=false;if(st.r<2)setMsg('Putar bangun dan perhatikan titik putih.')}}
}
function anim(get,set,to,ms,done){const f=get(),t0=performance.now();(function fr(t){const k=Math.min(1,(t-t0)/ms),e=k<.5?2*k*k:1-Math.pow(-2*k+2,2)/2;set(f+(to-f)*e);if(k<1)requestAnimationFrame(fr);else done&&done()})(t0)}
function pane(){
 const s=sh(),p=$('pane');
 if(st.mode==0){
  p.innerHTML=`<h2>${s.n}</h2><div class="fact"><div><b>${s.p?s.sisi:'0'}</b>sisi</div><div><b>${s.p?s.p.length:'0'}</b>titik sudut</div></div><p class="hint">${s.sdt}</p><ul>${s.c.map(x=>`<li>${x}</li>`).join('')}</ul><div class="fact"><div><b>${s.o?s.ax.length:'∞'}</b>simetri lipat</div><div><b>${s.o?s.o:'∞'}</b>simetri putar</div></div>`;
 }else if(st.mode==1){
  const n=s.o?s.ax.length:'tak terhingga';
  p.innerHTML=`<h2>Simetri lipat</h2><p>${s.ax.length?`${s.n} punya <b>${n}</b> sumbu simetri lipat. Pilih garis lipat:`:s.o?'Jajargenjang tidak punya sumbu simetri lipat. Coba lipat di garis ini dan lihat hasilnya:':`Lingkaran punya sumbu simetri lipat tak terhingga. Ini empat contohnya:`}</p>
  <div>${axes().map((a,k)=>`<button class="chip ${k==st.ai?'on':''}" data-a="${k}">Garis ${k+1}</button>`).join('')}</div>
  <input type="range" id="fv" min="0" max="100" value="${st.v}" aria-label="Lipat bangun">
  <button class="act" id="fauto">Lipat otomatis</button><button class="act alt" id="fopen">Buka lagi</button>
  <p class="hint">Simetri lipat: bangun dilipat pada sumbu dan kedua bagian saling menutupi persis.</p>`;
  $('fv').oninput=e=>{st.v=+e.target.value;draw();check()};
  $('fauto').onclick=()=>{tone(300,.2);anim(()=>st.v,v=>{st.v=v;$('fv').value=v;draw();check()},100,1600)};
  $('fopen').onclick=()=>{anim(()=>st.v,v=>{st.v=v;$('fv').value=v;draw();check()},0,900)};
  p.querySelectorAll('.chip').forEach(b=>b.onclick=()=>{st.ai=+b.dataset.a;st.v=0;st.pas=false;pane();draw();setMsg('Geser penggeser untuk melipat.')});
 }else{
  const d=stepDeg();
  p.innerHTML=`<h2>Simetri putar</h2><p>${s.o?(s.o==1?`${s.n} hanya menempati bingkai semula setelah diputar penuh 360°. Simetri putarnya <b>tingkat 1</b>.`:`${s.n} punya simetri putar <b>tingkat ${s.o}</b>: menempati bingkai semula setiap diputar <b>${d}°</b>.`):'Lingkaran menempati bingkai semula pada putaran berapa pun. Simetri putarnya tak terhingga.'}</p>
  <input type="range" id="rv" min="0" max="360" value="${st.r}" aria-label="Putar bangun">
  <button class="act" id="rstep">Putar ${s.o?d+'°':'90°'}</button><button class="act alt" id="rreset">Kembali ke awal</button>
  <p class="hint">Perhatikan titik putih. Garis putus-putus adalah bingkai awal.</p>`;
  $('rv').oninput=e=>{st.r=+e.target.value;draw();check()};
  const mv=v=>{st.r=v;$('rv').value=v;draw();check()};
  $('rstep').onclick=()=>{const q=s.o?d:90;let to=(Math.floor(st.r/q+.001)+1)*q;if(to>360){mv(0);to=q}tone(260,.25);anim(()=>st.r,mv,to,900)};
  $('rreset').onclick=()=>{anim(()=>st.r,mv,0,700)};
 }
}
function setMode(m){st.mode=m;st.v=0;st.r=0;st.ai=0;st.pas=false;
 $('tabs').innerHTML=['Ciri-ciri','Lipat','Putar'].map((t,k)=>`<button class="${k==m?'on':''}" data-m="${k}">${t}</button>`).join('');
 $('tabs').querySelectorAll('button').forEach(b=>b.onclick=()=>{tone(440,.1);setMode(+b.dataset.m)});
 pane();draw();setMsg(['Sentuh bangun, geser, dan ketuk untuk ganti warna.','Pilih garis lipat lalu geser penggeser.','Putar bangun dan perhatikan titik putih.'][m])}
function pick(i){st.i=i;st.dx=st.dy=0;document.querySelectorAll('#pick button').forEach((b,k)=>b.classList.toggle('on',k==i));tone(note[i%6],.2,'triangle');setMode(st.mode)}
// pilihan bangun
$('pick').innerHTML=S.map((s,k)=>{const sv2=s.p?`<polygon points="${s.p.map(q=>(q[0]*.5)+','+(q[1]*.5)).join(' ')}" fill="${P[k%6]}" stroke="var(--line)" stroke-width="3"/>`:`<circle r="40" fill="${P[k%6]}" stroke="var(--line)" stroke-width="3"/>`;
 return `<button data-i="${k}"><svg viewBox="-60 -60 120 120">${sv2}</svg>${s.n}</button>`}).join('');
$('pick').querySelectorAll('button').forEach(b=>b.onclick=()=>pick(+b.dataset.i));
// warna
P.forEach((c,k)=>{const d=document.createElement('i');d.style.background=c;d.tabIndex=0;d.setAttribute('role','button');d.setAttribute('aria-label','Warna '+(k+1));
 const go=()=>{st.col=k;tone(note[k],.2,'triangle');draw()};d.onclick=go;d.onkeydown=e=>{if(e.key=='Enter'||e.key==' '){e.preventDefault();go()}};$('sw').appendChild(d)});
// geser & ketuk
let dr=null;
sv.addEventListener('pointerdown',e=>{if(e.target===sv)return;const r=sv.getBoundingClientRect();dr={x:e.clientX,y:e.clientY,ox:st.dx,oy:st.dy,k:400/r.width,m:false};sv.setPointerCapture(e.pointerId);sv.style.cursor='grabbing'});
sv.addEventListener('pointermove',e=>{if(!dr)return;const mx=e.clientX-dr.x,my=e.clientY-dr.y;if(Math.hypot(mx,my)>5)dr.m=true;if(dr.m){st.dx=Math.max(-120,Math.min(120,dr.ox+mx*dr.k));st.dy=Math.max(-90,Math.min(90,dr.oy+my*dr.k));draw()}});
sv.addEventListener('pointerup',()=>{if(!dr)return;if(!dr.m){st.col=(st.col+1)%P.length;tone(note[st.col],.25,'triangle');draw()}else tone(330,.08);dr=null;sv.style.cursor='grab'});
$('snd').onclick=()=>{st.snd=!st.snd;$('snd').textContent=st.snd?'🔊 Suara: nyala':'🔇 Suara: mati';tone(500,.1)};
$('say').onclick=()=>{const s=sh();let t=`${s.n}. ${s.c.join('. ')}. `;t+=s.o?`Simetri lipat ${s.ax.length}. Simetri putar tingkat ${s.o}.`:'Simetri lipat dan simetri putarnya tak terhingga.';
 try{speechSynthesis.cancel();const u=new SpeechSynthesisUtterance(t);u.lang='id-ID';u.rate=.9;speechSynthesis.speak(u)}catch(e){setMsg('Perangkat ini belum mendukung suara pembaca.')}};
pick(0);
</script>
</body>
</html>
 
