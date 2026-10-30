[index (60).html](https://github.com/user-attachments/files/34200638/index.60.html)<!doctype html>
<html lang="et">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Pomminimetajad</title>
<style>
  :root{--bg:#14161a;--panel:#1f232a;--yellow:#f2c230;--red:#e5483b;--green:#3fbf6a;--paper:#f6efdc;--ink:#2a241a}
  html,body{margin:0;height:100%;background:var(--bg);font-family:system-ui,-apple-system,"Segoe UI",sans-serif;color:#eee}
  canvas{display:block}
  .hide{display:none!important}
  #start{position:fixed;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:18px;padding:16px;text-align:center;background:radial-gradient(circle at 50% 30%,#2a2f38,#0d0f12);z-index:30}
  #start h1{font-size:clamp(34px,8vw,64px);margin:0;color:var(--yellow);letter-spacing:.06em;text-shadow:0 3px 0 #000}
  #start p{max-width:560px;opacity:.85;line-height:1.5;margin:0}
  .roles{display:flex;gap:16px;flex-wrap:wrap;justify-content:center}
  .role{width:250px;padding:22px 18px;border-radius:16px;border:3px solid var(--yellow);background:#22262d;color:#fff;cursor:pointer;font-size:16px;line-height:1.4}
  .role b{display:block;font-size:24px;margin-bottom:6px;color:var(--yellow)}
  .role:hover{background:#2e333c}
  #codeBox{display:flex;flex-direction:column;gap:10px;align-items:center}
  #codeIn{font-size:44px;width:190px;text-align:center;letter-spacing:.2em;border-radius:12px;border:3px solid var(--yellow);background:#111;color:#fff;padding:6px}
  .btn{font-size:20px;padding:10px 26px;border-radius:12px;border:0;background:var(--yellow);color:#111;font-weight:bold;cursor:pointer}
  #bombHud{position:fixed;left:12px;top:12px;max-width:330px;background:rgba(20,22,26,.88);border:2px solid var(--yellow);border-radius:12px;padding:12px 14px;font-size:13px;line-height:1.55;z-index:5}
  #bombHud b{color:var(--yellow)} #bombHud .code{font-size:30px;font-weight:bold;letter-spacing:.15em;color:#fff}
  /* juhend */
  #manual{background:#d9cfb4;min-height:100%;color:var(--ink)}
  #mbar{position:sticky;top:0;z-index:10;display:flex;align-items:center;gap:14px;flex-wrap:wrap;padding:10px 14px;background:#1d2026;color:#fff;border-bottom:4px solid var(--yellow)}
  #mbar .t{font-size:34px;font-weight:bold;font-family:ui-monospace,monospace;color:var(--red);min-width:100px}
  #mbar .s{font-size:22px;color:var(--red);letter-spacing:.1em}
  #mbar .st{font-size:14px;opacity:.9}
  #mnav{display:flex;gap:6px;flex-wrap:wrap;padding:8px 14px;background:#2a2e36;position:sticky;top:64px;z-index:9}
  #mnav a{color:#fff;text-decoration:none;background:#3a3f49;padding:6px 10px;border-radius:8px;font-size:14px}
  .page{max-width:820px;margin:16px auto;background:var(--paper);padding:22px 26px;border-radius:6px;box-shadow:0 4px 18px rgba(0,0,0,.25)}
  .page h2{margin:0 0 6px;font-size:28px;border-bottom:3px solid var(--ink);padding-bottom:4px}
  .page h3{margin:16px 0 6px}
  .page p,.page li{line-height:1.55;font-size:17px}
  .page ol li{margin:4px 0}
  table{border-collapse:collapse;margin:8px 0;font-size:17px}
  td,th{border:2px solid var(--ink);padding:5px 10px;text-align:center}
  th{background:#e8dcbc}
  .mazes{display:grid;grid-template-columns:repeat(auto-fill,minmax(170px,1fr));gap:14px}
  .mazes div{text-align:center;font-weight:bold}
  .warn{background:#f3d36b;border-left:6px solid #b8860b;padding:8px 12px;margin:10px 0}
  #modeSw{margin-left:auto;display:flex;gap:6px}
  #modeSw button{font-size:15px;padding:7px 12px;border-radius:10px;border:2px solid #f2c230;background:#2a2e36;color:#fff;cursor:pointer}
  #modeSw button.on{background:#f2c230;color:#111;font-weight:bold}
  #kid{max-width:860px;margin:14px auto;padding:0 10px 60px;color:#2a241a}
  .kcard{background:#fff8e6;border-radius:18px;padding:18px;box-shadow:0 4px 16px rgba(0,0,0,.18);margin-bottom:14px;text-align:center}
  .kq{font-size:clamp(22px,4.5vw,32px);font-weight:800;margin:4px 0 14px}
  .ksub{font-size:18px;opacity:.75;margin:-6px 0 12px}
  .kgrid{display:flex;flex-wrap:wrap;gap:12px;justify-content:center}
  .kbtn{font-size:clamp(20px,4vw,28px);font-weight:800;padding:14px 20px;min-width:90px;border-radius:16px;border:4px solid #2a241a;background:#fff;cursor:pointer;color:#2a241a;box-shadow:0 4px 0 #2a241a}
  .kbtn:active{transform:translateY(3px);box-shadow:0 1px 0 #2a241a}
  .kbtn.big{font-size:30px;padding:18px 28px}
  .kbtn.sm{font-size:17px;padding:8px 14px;min-width:0;box-shadow:0 3px 0 #2a241a}
  .sw{width:86px;height:86px;border-radius:50%;border:5px solid #2a241a;cursor:pointer;box-shadow:0 4px 0 #2a241a;font-size:15px;font-weight:800;display:flex;align-items:flex-end;justify-content:center;padding-bottom:4px}
  .tile{width:130px;padding:10px;box-sizing:content-box;border-radius:18px;border:4px solid #2a241a;background:#fff;cursor:pointer;box-shadow:0 5px 0 #2a241a;font-size:22px;font-weight:800}
  .tile svg{width:126px;height:99px}
  .ans{font-size:clamp(26px,6vw,44px);font-weight:900;color:#b0301e;margin:10px 0}
  .digit{display:inline-block;font-size:clamp(50px,13vw,96px);font-weight:900;font-family:ui-monospace,monospace;background:#111;color:#40ff80;border-radius:14px;padding:4px 18px;margin:4px}
  .chips{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;font-size:16px}
  .chip{background:#efe3c2;border-radius:20px;padding:5px 12px}
  .steps{font-size:16px;opacity:.7;margin-bottom:6px}
  .arrows{font-size:clamp(40px,10vw,70px);letter-spacing:6px;line-height:1.25}
  .arrows span{display:inline-block;background:#fff;border:4px solid #2a241a;border-radius:14px;margin:4px;padding:0 10px;position:relative}
  .arrows small{position:absolute;top:-2px;left:6px;font-size:14px;letter-spacing:0}
  .animal{width:120px;padding:8px;border-radius:16px;border:4px solid #2a241a;background:#fff;cursor:pointer;box-shadow:0 4px 0 #2a241a}
  .animal div:first-child{font-size:56px}.animal div:last-child{font-weight:800;font-size:18px}
  #mnav{display:flex;align-items:center;gap:6px;flex-wrap:wrap;color:#fff;font-size:14px}
  #mnav button{border:0;border-radius:8px;background:#3a3f49;color:#fff;padding:6px 10px;font-size:14px;cursor:pointer}
  #mnav button.on{background:#f2c230;color:#111;font-weight:bold}
  #mnav .pg{font-size:18px;padding:6px 14px;background:#f2c230;color:#111;font-weight:bold}
  .pgn{font-weight:bold;font-size:16px;min-width:90px;text-align:center}.pgsep{width:10px}
  .phead{display:flex;justify-content:space-between;font-size:13px;opacity:.6;border-bottom:1px solid #b9ab88;margin-bottom:12px;padding-bottom:4px}
  .pfoot{display:flex;justify-content:space-between;margin-top:20px}
  .pfoot button{font-size:18px;padding:8px 16px;border-radius:10px;border:2px solid #2a241a;background:#fff;cursor:pointer}
  .fluff{color:#5a5040;font-size:15px!important;font-style:italic}
  table.spec td{text-align:left;font-size:14px;padding:3px 10px}
  .symcols{display:grid;grid-template-columns:repeat(auto-fill,minmax(80px,1fr));gap:8px}
  .symcols div{display:flex;flex-direction:column;align-items:center;background:#fff;border:2px solid #2a241a;border-radius:8px;padding:6px}
  .symcols canvas{width:52px;height:52px;border-bottom:1px solid #ddd}
  table.toc td{text-align:left;padding:6px 14px} table.morse td{padding:4px 10px}
  .lines{height:220px;background:repeating-linear-gradient(#f6efdc 0 31px,#c9bc98 31px 32px)}
  #banner{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;font-size:clamp(40px,12vw,110px);font-weight:900;z-index:20;pointer-events:none}
</style>
<script src="https://cdn.jsdelivr.net/npm/peerjs@1.5.4/dist/peerjs.min.js"></script>
<script type="importmap">
{"imports":{"three":"https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js","three/addons/":"https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/"}}
</script>
</head>
<body>
<div id="start">
  <h1>💣 POMMINIMETAJAD</h1>
  <p>Kahe mängija mäng. <b>Pommimees</b> näeb pommi, aga mitte juhendit. <b>Juhendaja</b> näeb juhendit, aga mitte pommi. Rääkige omavahel ja muukige pomm lahti enne, kui aeg otsa saab!</p>
  <div class="roles" id="roles">
    <div class="role" id="rBomb"><b>💣 Pommimees</b>Quest VR prillides või arvutis. Sinu ette tuleb pomm.</div>
    <div class="role" id="rMan"><b>📖 Juhendaja</b>Arvutis või telefonis. Sa näed pommi juhendit.</div>
  </div>
  <div id="codeBox" class="hide">
    <p>Sisesta ruumi kood, mis on pommimehe ees:</p>
    <input id="codeIn" inputmode="numeric" maxlength="4" placeholder="0000">
    <button class="btn" id="codeGo">Ühenda</button>
  </div>
  <p style="font-size:13px;opacity:.6">Mõlemad avavad sama lehe. Ühendus käib ruumikoodiga, kõige parem samas wifis.</p>
</div>

<div id="bombHud" class="hide">
  <div>Ruumi kood: <span class="code" id="hudCode">----</span></div>
  <div id="hudNet">Ootan juhendajat…</div>
  <hr style="border-color:#444">
  <b>Quest:</b> vajuta all <b>ENTER VR</b>. Päästik = vajuta/lõika. Haare = võta pomm kätte ja keera.<br>
  <b>Arvutis:</b> vasak klõps = vajuta/lõika (hoia nuppu all, kui vaja). Parem nupp + lohista = keera pommi. F = pööra ümber (ekspert: moodulid ka taga!). Tühik = tagasi. Ratas = suumi.
  <br><button class="btn" style="font-size:13px;padding:4px 10px;margin-top:6px" onclick="this.parentNode.classList.add('hide')">Peida</button>
</div>

<div id="manual" class="hide">
  <div id="mbar"><span class="t" id="mTime">-:--</span><span class="s" id="mStrikes"></span><span class="st" id="mStat">Ühendan…</span><span id="modeSw"><button id="mKid">👶 Piltidega</button><button id="mFull">📖 Täisjuhend</button></span></div>
  <div id="kid"></div>
  <div id="mnav"></div>
  <div id="mbody"></div>
</div>
<div id="banner" class="hide"></div>

<script type="module">
import * as THREE from 'three';
import { VRButton } from 'three/addons/webxr/VRButton.js';
import { XRControllerModelFactory } from 'three/addons/webxr/XRControllerModelFactory.js';

/* ============ ÜHINE: REEGLID ============ */
const $ = id => document.getElementById(id);
const PI = Math.PI;
const clamp = (v, a, b) => v < a ? a : v > b ? b : v;
const rnd = (a = 0, b = 1) => a + Math.random() * (b - a);
const rint = n => (Math.random() * n) | 0;
const pick = a => a[rint(a.length)];
function mulberry(a) { return function () { a |= 0; a = a + 0x6D2B79F5 | 0; let t = Math.imul(a ^ a >>> 15, 1 | a); t = t + Math.imul(t ^ t >>> 7, 61 | t) ^ t; return ((t ^ t >>> 14) >>> 0) / 4294967296; }; }

const WCOL = ['punane', 'sinine', 'kollane', 'valge', 'must', 'roheline'];
const WHEX = { punane: '#d23a2e', sinine: '#2f62d8', kollane: '#f0c820', valge: '#f2f2f2', must: '#1a1a1a', roheline: '#2f9a44' };
const VOWELS = 'AEIOU';
const ORDN = ['esimene', 'teine', 'kolmas', 'neljas', 'viies', 'kuues'];
const ORDG = ['esimest', 'teist', 'kolmandat', 'neljandat', 'viiendat', 'kuuendat'];
function lastDigit(ser) { for (let i = ser.length - 1; i >= 0; i--) if (/\d/.test(ser[i])) return +ser[i]; return 0; }
const cnt = (a, c) => a.filter(x => x === c).length;
const rp = (r, a) => a[(r() * a.length) | 0];
function shuffleR(a, r) { a = a.slice(); for (let i = a.length - 1; i > 0; i--) { const j = (r() * (i + 1)) | 0; [a[i], a[j]] = [a[j], a[i]]; } return a; }
const BCOL = ['punane', 'sinine', 'kollane', 'valge'], BLAB = ['VAJUTA', 'HOIA', 'STOPP', 'OOTA'];
const WORDS = { KASS: '3172', KOER: '5904', HUNT: '8261', KARU: '4417', REBANE: '6038', 'PÕDER': '1725', ILVES: '9350', 'JÄNES': '2846', SIIL: '7093', ORAV: '3561', KONN: '0482', KULL: '6614' };
const MCOL = ['punane', 'oranž', 'kollane', 'roheline', 'sinine', 'lilla'];
const MHEX = { punane: '#d23a2e', 'oranž': '#ee8a20', kollane: '#e8c418', roheline: '#2f9a44', sinine: '#2f62d8', lilla: '#9a4ad8' };
const MN = 5;
function makeMaze(seed) {
  const r = mulberry(seed * 7919 + 13); const E = [], Sw = []; for (let y = 0; y < MN; y++) { E.push(Array(MN).fill(true)); Sw.push(Array(MN).fill(true)); }
  const seen = new Set(); const st = [[0, 0]]; seen.add('0,0');
  while (st.length) { const [x, y] = st[st.length - 1]; const nb = [[1, 0], [-1, 0], [0, 1], [0, -1]].map(([dx, dy]) => [x + dx, y + dy, dx, dy]).filter(([a, b]) => a >= 0 && b >= 0 && a < MN && b < MN && !seen.has(a + ',' + b));
    if (!nb.length) { st.pop(); continue; } const [a, b, dx, dy] = nb[(r() * nb.length) | 0];
    if (dx === 1) E[y][x] = false; if (dx === -1) E[y][a] = false; if (dy === 1) Sw[y][x] = false; if (dy === -1) Sw[b][x] = false; seen.add(a + ',' + b); st.push([a, b]); }
  for (let i = 0; i < 3; i++) { const x = (r() * (MN - 1)) | 0, y = (r() * MN) | 0; E[y][x] = false; }
  return { E, S: Sw };
}
function canMove(mz, x, y, dx, dy) { const nx = x + dx, ny = y + dy; if (nx < 0 || ny < 0 || nx >= MN || ny >= MN) return false; if (dx === 1) return !mz.E[y][x]; if (dx === -1) return !mz.E[y][nx]; if (dy === 1) return !mz.S[y][x]; return !mz.S[ny][x]; }
// --- uued moodulid ---
const PCOL = ['punane', 'sinine', 'roheline', 'kollane'];
const PHEX = { punane: '#e8302a', sinine: '#2a6aff', roheline: '#22c050', kollane: '#ffd020' };
const MW = ['KALA', 'MAJA', 'PUU', 'KIVI', 'LUMI', 'TULI', 'VESI', 'AKEN', 'LAUD', 'KOOL', 'LINN', 'PILV'];
const FREQS = MW.map((w, i) => (3.505 + i * 0.01).toFixed(3));
const MORSE = { A: '.-', B: '-...', C: '-.-.', D: '-..', E: '.', F: '..-.', G: '--.', H: '....', I: '..', J: '.---', K: '-.-', L: '.-..', M: '--', N: '-.', O: '---', P: '.--.', R: '.-.', S: '...', T: '-', U: '..-', V: '...-', Z: '--..' };
const QCOL = ['punane', 'sinine', 'must'], QLET = ['A', 'B', 'C'];
// sümbolid: igaüks on kahe kujundi kombinatsioon
const PRIM = [
  g => { g.beginPath(); g.arc(0, 0, .7, 0, Math.PI * 2); g.stroke(); },
  g => { g.beginPath(); g.arc(0, .15, .7, Math.PI, 0); g.stroke(); },
  g => { g.beginPath(); g.moveTo(-.7, .6); g.lineTo(0, -.7); g.lineTo(.7, .6); g.closePath(); g.stroke(); },
  g => { g.beginPath(); g.moveTo(-.7, -.6); g.lineTo(0, .7); g.lineTo(.7, -.6); g.stroke(); },
  g => { g.strokeRect(-.55, -.55, 1.1, 1.1); },
  g => { g.beginPath(); g.moveTo(0, -.8); g.lineTo(.8, 0); g.lineTo(0, .8); g.lineTo(-.8, 0); g.closePath(); g.stroke(); },
  g => { g.beginPath(); g.moveTo(0, -.85); g.lineTo(0, .85); g.stroke(); },
  g => { g.beginPath(); g.moveTo(-.85, 0); g.lineTo(.85, 0); g.stroke(); },
  g => { g.beginPath(); g.moveTo(-.6, -.6); g.lineTo(.6, .6); g.moveTo(.6, -.6); g.lineTo(-.6, .6); g.stroke(); },
  g => { g.beginPath(); g.arc(0, 0, .17, 0, Math.PI * 2); g.fill(); },
  g => { g.beginPath(); g.arc(-.38, -.58, .13, 0, Math.PI * 2); g.arc(.38, -.58, .13, 0, Math.PI * 2); g.fill(); },
  g => { g.beginPath(); for (let i = 0; i <= 20; i++) { const x = -.8 + i * .08, y = Math.sin(i / 20 * Math.PI * 3) * .25 + .45; i ? g.lineTo(x, y) : g.moveTo(x, y); } g.stroke(); },
  g => { g.beginPath(); g.moveTo(-.4, -.4); g.lineTo(0, -.85); g.lineTo(.4, -.4); g.stroke(); },
  g => { g.beginPath(); g.moveTo(.3, -.8); g.lineTo(.3, .35); g.arc(0, .35, .3, 0, Math.PI); g.stroke(); },
  g => { g.beginPath(); g.moveTo(-.75, .5); g.lineTo(-.4, -.4); g.lineTo(0, .5); g.lineTo(.4, -.4); g.lineTo(.75, .5); g.stroke(); },
  g => { g.beginPath(); g.arc(0, 0, .7, Math.PI * .3, Math.PI * 1.7); g.stroke(); },
  g => { g.beginPath(); g.arc(0, -.55, .22, 0, Math.PI * 2); g.stroke(); },
  g => { g.beginPath(); g.moveTo(0, .3); g.lineTo(0, .9); g.moveTo(-.3, .9); g.lineTo(.3, .9); g.stroke(); },
];
const GLYPHS = (() => { const r = mulberry(4242), pairs = []; for (let i = 0; i < PRIM.length; i++) for (let j = i + 1; j < PRIM.length; j++) pairs.push([i, j]); return shuffleR(pairs, r).slice(0, 28); })();
function drawGlyph(g, id, cx, cy, sz, col) { g.save(); g.translate(cx, cy); g.scale(sz / 2, sz / 2); g.strokeStyle = col; g.fillStyle = col; g.lineWidth = 0.13; g.lineCap = 'round'; g.lineJoin = 'round'; for (const p of GLYPHS[id]) PRIM[p](g); g.restore(); }
// --- väljaanded ---
const RULES = {};
function RU(ed = 1) {
  if (RULES[ed]) return RULES[ed]; const r = mulberry(ed * 1013 + 77), R = { ed }; const bit = () => (r() * 2) | 0;
  if (ed === 1) R.w = { c3: 'must', d3: 2, def3: 0, par4: 0, c4a: 'kollane', c4b: 'punane', c4n: 'roheline', d4p: 1, d4n: 0, def4: 3, c5l: 'sinine', d5l: 0, c5w: 'valge', bat5: 2, def5: 2, c6n: 'punane', d6n: 4, c6o: 'must', def6: 5 };
  else { const cs = shuffleR(WCOL, r); R.w = { c3: cs[0], d3: rp(r, [1, 2]), def3: rp(r, [0, 1, 2]), par4: bit(), c4a: cs[1], c4b: cs[2], c4n: cs[3], d4p: rp(r, [0, 1, 2]), d4n: rp(r, [0, 3]), def4: rp(r, [1, 2, 3]), c5l: cs[4], d5l: rp(r, [0, 1]), c5w: cs[5], bat5: 1 + ((r() * 3) | 0), def5: rp(r, [2, 3, 4]), c6n: cs[2], d6n: rp(r, [2, 3, 4]), c6o: cs[0], def6: rp(r, [1, 5]) }; }
  if (ed === 1) R.b = { c1: 'sinine', l1: 'OOTA', a1: 'hold', batT: 2, c2: 'punane', a2: 'hold', l2: 'VAJUTA', a3: 'tap', def: 'hold', strip: { punane: 2, kollane: 7, sinine: 6, roheline: 0 } };
  else { const c1 = rp(r, BCOL), l1 = rp(r, BLAB), dg = shuffleR([0, 1, 2, 3, 4, 5, 6, 7, 8, 9], r); R.b = { c1, l1, a1: rp(r, ['hold', 'tap']), batT: 1 + ((r() * 3) | 0), c2: rp(r, BCOL.filter(c => c !== c1)), a2: rp(r, ['hold', 'tap']), l2: rp(r, BLAB.filter(l => l !== l1)), a3: rp(r, ['hold', 'tap']), def: 'hold', strip: { punane: dg[0], kollane: dg[1], sinine: dg[2], roheline: dg[3] } }; }
  R.s = ed === 1 ? { all: 1, one: 0, two: 0, p3a: [1, 0, 1, 0, 1], p3b: [0, 1, 0, 1, 0], four: 0 } : { all: bit(), one: bit(), two: bit(), p3a: [bit(), bit(), bit(), bit(), bit()], p3b: [bit(), bit(), bit(), bit(), bit()], four: bit() };
  R.k = ed === 1 ? { codes: WORDS, ind: 'MAA', lit: true } : { codes: Object.fromEntries(Object.keys(WORDS).map(w => [w, String((r() * 10000) | 0).padStart(4, '0')])), ind: rp(r, ['MAA', 'VAL', 'TUL', 'KAS']), lit: r() < 0.5 };
  R.mz = MCOL.map((c, i) => makeMaze(ed === 1 ? i + 1 : ed * 100 + i));
  R.p = [0, 1, 2].map(() => shuffleR(PCOL, r));
  R.f = shuffleR(FREQS, r);
  R.cols = (() => { for (let t = 0; t < 200; t++) { const cols = [0, 1, 2, 3, 4, 5].map(() => shuffleR([...Array(28).keys()], r).slice(0, 7)); return cols; } })();
  R.m = [0, 1, 2, 3].map(s => [0, 1, 2, 3].map(() => { const t = s === 0 ? rp(r, ['pos', 'lab']) : rp(r, ['pos', 'lab', 'ppos', 'plab', 'pos']); return { t, v: t.startsWith('p') && t !== 'pos' ? 1 + ((r() * s) | 0) : 1 + ((r() * 4) | 0) }; }));
  R.q = Object.fromEntries(QCOL.map(c => [c, [...Array(9)].map(() => { const s = QLET.filter(() => r() < 0.45); return s.length ? s : [rp(r, QLET)]; })]));
  return RULES[ed] = R;
}
const STRIP = RU(1).b.strip, MAZES = RU(1).mz;
function wireAnswer(c, B) { const w = RU(B.ed || 1).w, n = c.length;
  if (n === 3) { if (c[0] === w.c3) return w.d3; if (new Set(c).size === 2) { for (let i = 0; i < 3; i++) if (cnt(c, c[i]) === 1) return i; } return w.def3; }
  if (n === 4) { if (lastDigit(B.serial) % 2 === w.par4) return w.d4p; if (cnt(c, w.c4a) > cnt(c, w.c4b)) return c.lastIndexOf(w.c4a); if (!c.includes(w.c4n)) return w.d4n; return w.def4; }
  if (n === 5) { if (c[4] === w.c5l) return w.d5l; if (B.batteries >= w.bat5 && c.includes(w.c5w)) return c.indexOf(w.c5w); return w.def5; }
  if (!c.includes(w.c6n)) return w.d6n; if (cnt(c, w.c6o) === 1) return c.indexOf(w.c6o); if ([...B.serial].some(ch => VOWELS.includes(ch))) return 0; return w.def6; }
function buttonAction(col, lab, B) { const b = RU(B.ed || 1).b; if (col === b.c1 && lab === b.l1) return b.a1; if (B.batteries > b.batT) return 'tap'; if (col === b.c2) return b.a2; if (lab === b.l2) return b.a3; return b.def; }
function switchTarget(L, R = RU(1)) { const s = R.s, k = L.filter(Boolean).length; if (k === 0 || k === 5) return [s.all, s.all, s.all, s.all, s.all]; if (k === 1) return L.map(x => x ? 1 ^ s.one : s.one); if (k === 2) return L.map(x => x ? s.two : 1 ^ s.two); if (k === 3) return L[0] ? s.p3a.slice() : s.p3b.slice(); return L.map(x => x ? s.four : 1 ^ s.four); }
function keypadCode(word, B) { const k = RU(B.ed || 1).k; const c = k.codes[word]; return (B.indicator === k.ind && B.indLit === k.lit) ? [...c].reverse().join('') : c; }
const batRow = b => b <= 1 ? 0 : b <= 3 ? 1 : 2;
window.RULESX = { RU, canMove, batRow, PCOL, FREQS };


/* ============ ÜHINE: VÕRK ============ */
const PEER_PREFIX = 'pomminimetajad-v1-';
function makeNet(code, role, onMsg, onStatus) {
  const net = { conns: [], send() { }, destroy() { } };
  let bc = null; try { bc = new BroadcastChannel('pomminimetajad-' + code); bc.onmessage = e => onMsg(e.data); } catch (e) { }
  net.send = m => { if (bc) bc.postMessage(m); for (const c of net.conns) if (c.open) { try { c.send(m); } catch (e) { } } };
  net.destroy = () => { try { bc && bc.close(); } catch (e) { } try { net.peer && net.peer.destroy(); } catch (e) { } };
  if (!window.Peer) { onStatus('nopeer'); return net; }
  try {
    if (role === 'bomb') {
      const peer = new Peer(PEER_PREFIX + code, { debug: 0 }); net.peer = peer;
      peer.on('open', () => onStatus('ready'));
      peer.on('connection', c => { c.on('open', () => net.conns.push(c)); c.on('data', onMsg); c.on('close', () => { const i = net.conns.indexOf(c); if (i >= 0) net.conns.splice(i, 1); }); });
      peer.on('error', e => onStatus('err:' + e.type));
      peer.on('disconnected', () => { try { peer.reconnect(); } catch (e) { } });
    } else {
      const peer = new Peer({ debug: 0 }); net.peer = peer; let busy = false;
      const tryConn = () => { if (busy) return; busy = true; const c = peer.connect(PEER_PREFIX + code, { reliable: true });
        c.on('open', () => { busy = false; net.conns = [c]; onStatus('conn'); c.send({ type: 'hi' }); });
        c.on('data', onMsg); c.on('close', () => { busy = false; net.conns = []; onStatus('lost'); setTimeout(tryConn, 2000); });
        setTimeout(() => { if (busy && !c.open) { busy = false; tryConn(); } }, 6000); };
      peer.on('open', tryConn); peer.on('error', e => { busy = false; onStatus('err:' + e.type); if (e.type === 'peer-unavailable') setTimeout(tryConn, 2500); });
    }
  } catch (e) { onStatus('nopeer'); }
  return net;
}

/* ============ ALGUS ============ */
const params = new URLSearchParams(location.search);
$('rBomb').onclick = () => startBomb();
$('rMan').onclick = () => { $('roles').classList.add('hide'); $('codeBox').classList.remove('hide'); $('codeIn').focus(); };
$('codeGo').onclick = () => { const c = $('codeIn').value.replace(/\D/g, ''); if (c.length === 4) startManual(c); else $('codeIn').style.borderColor = 'red'; };
$('codeIn').addEventListener('keydown', e => { if (e.key === 'Enter') $('codeGo').click(); });
if (params.get('roll') === 'pomm') setTimeout(() => startBomb(params.get('kood')), 0);
if (params.get('roll') === 'juhend' && params.get('kood')) setTimeout(() => startManual(params.get('kood')), 0);

/* ============ JUHENDAJA ============ */
function startManual(code) {
  $('start').classList.add('hide'); $('manual').classList.remove('hide'); document.body.style.background = '#d9cfb4';
  buildManual(); setupKid();
  let last = 0, st = null, netStat = '', lastPhase = '', lastDiff = '';
  const net = makeNet(code, 'manual', m => { if (m && m.type === 'st') { last = performance.now(); st = m; render(); } }, s => { netStat = s; render(); });
  setInterval(() => net.send({ type: 'hi' }), 1500); net.send({ type: 'hi' });
  setInterval(render, 500);
  function render() {
    const alive = st && performance.now() - last < 4000;
    if (!alive) { $('mStat').textContent = `Kood ${code} · ` + (netStat === 'nopeer' ? 'võrguühendus puudub – proovi sama arvuti teist vahelehte' : netStat.startsWith('err') ? 'ootan pommimeest… (' + netStat.slice(4) + ')' : 'ootan pommimeest…'); $('mTime').textContent = '-:--'; return; }
    const ph = st.phase;
    if (ph === 'play' && lastPhase !== 'play' && lastPhase !== '') kidReset(); lastPhase = ph;
    if (st.diff !== lastDiff) { lastDiff = st.diff; if (st.diff === 'expert' && !$('kid').classList.contains('hide')) $('mFull').click(); }
    LIVE = ph === 'play' && st.kid ? st : null; if (LIVE && $('kid').classList.contains('hide')) $('mKid').click(); kidRender();
    $('mTime').textContent = ph === 'lobby' ? '-:--' : fmt(st.time);
    $('mStrikes').textContent = ph === 'lobby' ? '' : '✕'.repeat(st.strikes) + '○'.repeat(Math.max(0, st.maxS - st.strikes));
    $('mStat').textContent = `Kood ${code} · ühendatud ✓ · ` + (ph === 'lobby' ? 'oota, kuni pommimees alustab' : ph === 'play' ? `moodulid ${st.solved}/${st.total}` : ph === 'win' ? 'POMM KAHJUTU!' : 'PAUH!');
    const b = $('banner');
    if (ph === 'win' || ph === 'boom') { b.classList.remove('hide'); b.textContent = ph === 'win' ? '✅ KAHJUTU!' : '💥 PAUH!'; b.style.color = ph === 'win' ? '#2f9a44' : '#e5483b'; b.style.textShadow = '0 4px 0 #000'; b.style.opacity = (performance.now() - (st.endAt || 0)) > 0 ? 1 : 1; clearTimeout(render.bt); render.bt = setTimeout(() => b.classList.add('hide'), 3500); }
    else b.classList.add('hide');
  }
}
const fmt = t => { t = Math.max(0, Math.floor(t)); return Math.floor(t / 60) + ':' + String(t % 60).padStart(2, '0'); };
let BOOK_ED = 1, BOOK_PAGE = 0, BOOK = [];
function buildManual() { BOOK = bookPages(RU(BOOK_ED)); renderBook(); addEventListener('keydown', e => { if ($('mbody').classList.contains('hide')) return; if (e.key === 'ArrowRight') turn(1); if (e.key === 'ArrowLeft') turn(-1); }); }
function turn(d) { BOOK_PAGE = clamp(BOOK_PAGE + d, 0, BOOK.length - 1); renderBook(); scrollTo(0, 0); }
function renderBook() {
  const nav = $('mnav');
  nav.innerHTML = `<button class="pg" data-p="-1">◀</button><span class="pgn">Leht ${BOOK_PAGE + 1} / ${BOOK.length}</span><button class="pg" data-p="1">▶</button>
   <span class="pgsep"></span>${BOOK.map((p, i) => `<button class="pgd${i === BOOK_PAGE ? ' on' : ''}" data-go="${i}">${i + 1}</button>`).join('')}
   <span class="pgsep"></span>Väljaanne: ${[1, 2, 3].map(e => `<button class="pge${e === BOOK_ED ? ' on' : ''}" data-ed="${e}">${e}</button>`).join('')}`;
  nav.onclick = e => { const b = e.target.closest('button'); if (!b) return; if (b.dataset.p) turn(+b.dataset.p); if (b.dataset.go) { BOOK_PAGE = +b.dataset.go; renderBook(); scrollTo(0, 0); } if (b.dataset.ed) { BOOK_ED = +b.dataset.ed; BOOK = bookPages(RU(BOOK_ED)); BOOK_PAGE = Math.min(BOOK_PAGE, BOOK.length - 1); renderBook(); } };
  const p = BOOK[BOOK_PAGE];
  $('mbody').innerHTML = `<div class="page"><div class="phead"><span>PX-7 käsiraamat · väljaanne ${BOOK_ED}</span><span>lk ${BOOK_PAGE + 1}</span></div>${p.html}<div class="pfoot">${BOOK_PAGE > 0 ? '<button class="pg" data-p="-1">◀ Eelmine</button>' : '<span></span>'}${BOOK_PAGE < BOOK.length - 1 ? '<button class="pg" data-p="1">Järgmine ▶</button>' : ''}</div></div><div style="height:30px"></div>`;
  $('mbody').onclick = e => { const b = e.target.closest('button[data-p]'); if (b) turn(+b.dataset.p); };
  p.after && p.after();
}
const PART = { punane: 'punast', sinine: 'sinist', kollane: 'kollast', valge: 'valget', must: 'musta', roheline: 'rohelist' };
const PLP = { punane: 'punaseid', sinine: 'siniseid', kollane: 'kollaseid', valge: 'valgeid', must: 'musti', roheline: 'rohelisi' };
const fluff = t => `<p class="fluff">${t}</p>`;
const spec = rows => `<table class="spec">${rows.map(([a, b]) => `<tr><td>${a}</td><td>${b}</td></tr>`).join('')}</table>`;
function bookPages(R) {
  const w = R.w, b = R.b, s = R.s, k = R.k, ACT = { hold: '<b>hoia all</b>', tap: '<b>vajuta ja lase kohe lahti</b>' };
  const sw = (L) => L.map(x => x ? 'ÜLES' : 'ALLA').join(' – ');
  const pages = [];
  const P = (title, html, after) => pages.push({ title, html, after });
  P('Kaas', `<div style="text-align:center;padding:30px 0"><div style="font-size:15px;letter-spacing:.3em">KONFIDENTSIAALNE</div><h1 style="font-size:40px;margin:16px 0">PX-7 SEADME<br>HOOLDUS- JA LAHTIMUUKIMISJUHEND</h1><div style="font-size:22px">Väljaanne ${R.ed}</div><div style="font-size:70px;margin:20px">💣</div>
    ${fluff('Väljaandja: OÜ Pauk & Pojad, tehnilise dokumentatsiooni osakond. Käesolev juhend on mõeldud ainult volitatud personalile. Juhendi kopeerimine, laenutamine ja kasutamine grillisüütena on keelatud.')}
    <div class="warn">⚠ Enne alustamist küsi pommimehelt, mis <b>väljaande number</b> on pommi peal kirjas, ja vali sama väljaanne lehe ülaosast. Vale väljaande reeglid ei tööta!</div></div>`);
  const toc = [];
  P('Sisukord', '');
  P('Ohutusnõuded', `<h2>1. Üldised ohutusnõuded</h2>${fluff('1.1 Seadmega töötamisel kanna alati kiivrit, kaitseprille ja head tuju.')}${fluff('1.2 Ära söö seadme läheduses kreeka pähkleid. Pähklikoorte krõbin võib häirida pommimehe keskendumist.')}${fluff('1.3 Seadme hoiutemperatuur on +5 kuni +35 °C. Talvel ära jäta seadet auto pagasiruumi.')}${fluff('1.4 Kui seade hakkab laulma, ei ole see tavaliselt märk rikkest. Kui seade laulab valesti, teavita hooldusosakonda.')}${fluff('1.5 Kõik selle peatüki punktid on soovituslikud ega mõjuta lahtimuukimist.')}
    <h3>1.6 Kasulikud sõnad</h3>${fluff('Pommimees – inimene, kes hoiab pommi. Juhendaja – inimene, kes hoiab seda raamatut. Moodul – pommi üks ruut, millel on oma ülesanne.')}`);
  P('Pommi küljed', `<h2>2. Pommi küljed</h2><p>Paljud reeglid vajavad infot pommi külgedelt. Pommimees peab pommi keerama ja vaatama:</p>
    <ul><li><b>Seerianumber</b> – pommi pealmisel küljel, nt <code>KR4-79B</code>. "Viimane number" tähendab seerianumbri viimast numbrit (tähti ei arvestata).</li>
    <li><b>Juhendi väljaanne</b> – samuti pommi pealmisel küljel (nt "JUHEND v2").</li>
    <li><b>Patareid</b> – pommi vasakul küljel. Loe kokku, mitu patareid on.</li>
    <li><b>Indikaator</b> – pommi paremal küljel: kolmetäheline silt (nt MAA) ja lamp, mis põleb või ei põle.</li></ul>
    <p>Täishäälikud on A, E, I, O, U. Iga moodul on valmis, kui selle nurgas süttib <b>roheline tuli</b>. Igal veal on oma ✕. Kui vigu tuleb liiga palju, pomm plahvatab. Ekspert-pommil võivad moodulid olla ka <b>tagaküljel</b>.</p>
    ${fluff('Märkus: patareid on tüüpi AA ja neid ei tohi asendada kartulitega, kuigi kartulist on ka voolu saadud.')}`);
  P('Juhtmed', `<h2>3. Moodul: Juhtmed</h2>${spec([['Mudel', 'JM-6'], ['Juhtmete pikkus', '9 cm'], ['Isolatsioon', 'kuumakindel kuni 120 °C']])}
    <p>Moodulil on 3–6 värvilist juhet. Lõigata tuleb <b>täpselt üks</b> juhe. Juhtmeid loetakse <b>ülevalt alla</b>. Kasuta <b>esimest reeglit, mis sobib</b>.</p>
    <h3>3 juhet</h3><ol><li>Kui esimene juhe on ${w.c3}, lõika ${ORDN[w.d3]}.</li><li>Kui kaks juhet on sama värvi, lõika see juhe, mis on teist värvi.</li><li>Muidu lõika ${ORDN[w.def3]}.</li></ol>
    <h3>4 juhet</h3><ol><li>Kui seerianumbri viimane number on ${w.par4 ? 'paaritu (1, 3, 5, 7, 9)' : 'paarisarv (0, 2, 4, 6, 8)'}, lõika ${ORDN[w.d4p]}.</li><li>Kui ${PLP[w.c4a]} juhtmeid on rohkem kui ${PLP[w.c4b]}, lõika viimane ${w.c4a}.</li><li>Kui ${PART[w.c4n]} juhet pole, lõika ${ORDN[w.d4n]}.</li><li>Muidu lõika ${ORDN[w.def4]}.</li></ol>
    ${fluff('Ajalooline märkus: varasemates mudelites oli juhtmeid kuni 14, kuid kasutajad läksid segadusse.')}
    <h3>5 juhet</h3><ol><li>Kui viimane (viies) juhe on ${w.c5l}, lõika ${ORDN[w.d5l]}.</li><li>Kui patareisid on ${w.bat5} või rohkem ja on ${w.c5w} juhe, lõika esimene ${w.c5w}.</li><li>Muidu lõika ${ORDN[w.def5]}.</li></ol>
    <h3>6 juhet</h3><ol><li>Kui ${PART[w.c6n]} juhet pole, lõika ${ORDN[w.d6n]}.</li><li>Kui on täpselt üks ${w.c6o} juhe, lõika see.</li><li>Kui seerianumbris on täishäälik, lõika esimene.</li><li>Muidu lõika ${ORDN[w.def6]}.</li></ol>`);
  P('Nupp', `<h2>4. Moodul: Nupp</h2>${fluff('Nupu vedru on testitud 2 000 000 vajutusega. Nupu kiri on trükitud kulumiskindla värviga.')}
    <p>Moodulil on suur värviline nupp, millel on kiri. Kasuta <b>esimest reeglit, mis sobib</b>:</p>
    <ol><li>Kui nupp on ${b.c1} ja kiri on <b>${b.l1}</b> → ${ACT[b.a1]}.</li><li>Kui patareisid on rohkem kui ${b.batT} → ${ACT.tap}.</li><li>Kui nupp on ${b.c2} → ${ACT[b.a2]}.</li><li>Kui kiri on <b>${b.l2}</b> → ${ACT[b.a3]}.</li><li>Muidu → ${ACT[b.def]}.</li></ol>
    <h3>Kui nuppu tuleb all hoida</h3><p>Nupu kõrval süttib värviline riba. Lase nupp lahti, kui <b>taimeri viimane number</b> on:</p>
    <table><tr><th>Riba</th><th>Viimane number</th></tr>${Object.entries(b.strip).map(([c, d]) => `<tr><td>${c}</td><td>${d}</td></tr>`).join('')}</table>
    ${fluff('Kui nuppu hoida üle 30 minuti, võib tekkida pöidla väsimus.')}`);
  P('Lülitid', `<h2>5. Moodul: Lülitid</h2><p>Üleval on 5 lampi, all 5 lülitit. Lülitid loetakse <b>vasakult paremale</b>. Pane lülitid paika ja vajuta <b>VALMIS</b>.</p>
    <table><tr><th>Mitu lampi põleb?</th><th>Lülitid</th></tr>
    <tr><td>0 või 5</td><td>kõik <b>${s.all ? 'ÜLES' : 'ALLA'}</b></td></tr>
    <tr><td>1</td><td>põleva lambi all <b>${s.one ? 'ALLA' : 'ÜLES'}</b>, teised <b>${s.one ? 'ÜLES' : 'ALLA'}</b></td></tr>
    <tr><td>2</td><td>põlevate lampide all <b>${s.two ? 'ÜLES' : 'ALLA'}</b>, teised <b>${s.two ? 'ALLA' : 'ÜLES'}</b></td></tr>
    <tr><td>3, esimene põleb</td><td>${sw(s.p3a)}</td></tr><tr><td>3, esimene ei põle</td><td>${sw(s.p3b)}</td></tr>
    <tr><td>4</td><td>kustunud lambi all <b>${s.four ? 'ALLA' : 'ÜLES'}</b>, teised <b>${s.four ? 'ÜLES' : 'ALLA'}</b></td></tr></table>
    ${fluff('Lambid on LED-tüüpi, eluiga umbes 50 000 tundi. Lampe ei pea vahetama.')}`);
  P('Tehnilised andmed', `<h2>6. Tehnilised andmed</h2>${spec([['Kaal', '4,2 kg'], ['Mõõdud', '46 × 32 × 14 cm'], ['Toide', 'AA patareid või vooluvõrk 230 V'], ['Taimeri täpsus', '±0,01 s'], ['Värvus', 'tumehall'], ['Garantii', '0 kuud'], ['Lemmikloom', 'kass']])}${fluff('Kõik selle lehe andmed on informatiivsed. Lahtimuukimiseks pole neid vaja.')}`);
  const ws = Object.entries(k.codes);
  P('Koodilukk', `<h2>7. Moodul: Koodilukk</h2><p>Ekraanil on loomanimi. Leia nimi tabelist ja ütle 4-kohaline kood.</p>
    <div class="warn">Kui pommi indikaatori silt on <b>${k.ind}</b> ja selle lamp <b>${k.lit ? 'põleb' : 'EI põle'}</b>, tuleb kood sisestada <b>tagurpidi</b>.</div>
    <table><tr><th>Sõna</th><th>Kood</th><th>Sõna</th><th>Kood</th></tr>${ws.slice(0, 6).map(([x, c], i) => `<tr><td>${x}</td><td><b>${c}</b></td><td>${ws[i + 6][0]}</td><td><b>${ws[i + 6][1]}</b></td></tr>`).join('')}</table>
    <p>Klahv <b>C</b> kustutab. Vale kood on viga.</p>${fluff('Loomanimed valiti Eesti metsade ja koduste loomade hulgast. Ükski loom ei saanud selle juhendi koostamisel viga.')}`);
  P('Labürint', `<h2>8. Moodul: Labürint</h2><p>Moodulil on 5×5 täppidega ekraan ja 4 noolt. <b>Roheline ring</b> on pommimees, <b>punane rist</b> on siht. Pommimees <b>ei näe seinu</b>! Raami värv ütleb, milline labürint see on. Vastu seina minek on viga.</p>
    <div class="mazes">${MCOL.map((c, i) => `<div><canvas id="mz${i}" width="170" height="170"></canvas><br>${c}</div>`).join('')}</div>`, () => MCOL.forEach((c, i) => drawMazeManual($('mz' + i), R.mz[i], MHEX[c])));
  P('Hooldus', `<h2>9. Hooldus ja hoiustamine</h2>${fluff('9.1 Puhasta pommi korpust kord kuus pehme lapiga. Ära kasuta kraanikausipuhastit.')}${fluff('9.2 Hoia pommi kuivas kohas, eemal lastest, lemmikloomadest ja ämmadest.')}${fluff('9.3 Kui pommi taimer näitab 88:88, on see lihtsalt ekraani test.')}${fluff('9.4 Seade ei ole mõeldud kasutamiseks vannis.')}${fluff('9.5 Kui tunned pommist tugevat sibulalõhna, on keegi seal lõunat söönud.')}`);
  P('Värvimälu', `<h2>10. Moodul: Värvimälu</h2><p>Moodulil on 4 värvilist nuppu. Nupud <b>vilguvad</b> järjest. Iga vilkunud värvi asemel tuleb vajutada <b>teist värvi</b> nuppu – vaata tabelist. Vajuta kõik vastused samas järjekorras, nagu nupud vilkusid. Iga vooru järel lisandub üks vilge. Kui kõik vooru tuled (ülal) põlevad roheliselt, on moodul valmis.</p>
    <table><tr><th>Patareisid</th>${PCOL.map(c => `<th>vilgub ${c}</th>`).join('')}</tr>${['0–1', '2–3', '4'].map((t, i) => `<tr><td>${t}</td>${R.p[i].map(c => `<td><b>${c}</b></td>`).join('')}</tr>`).join('')}</table>
    ${fluff('Värvid on valitud nii, et need oleksid hästi eristatavad ka hämaras ruumis.')}`);
  P('Raadio', `<h2>11. Moodul: Raadio</h2><p>Moodulil vilgub lamp <b>morsekoodis</b> üht sõna, uuesti ja uuesti. Lühike vilge on <b>punkt</b> (·), pikk vilge on <b>kriips</b> (–). Pikem paus on tähtede vahel, väga pikk paus tähendab, et sõna algab otsast.</p>
    <p>Leia sõna ja ütle sagedus. Pommimees valib nooltega sageduse ja vajutab <b>SAADA</b>.</p>
    <table><tr><th>Sõna</th><th>Sagedus</th><th>Sõna</th><th>Sagedus</th></tr>${MW.slice(0, 6).map((x, i) => `<tr><td>${x}</td><td><b>${R.f[i]} MHz</b></td><td>${MW[i + 6]}</td><td><b>${R.f[i + 6]} MHz</b></td></tr>`).join('')}</table>
    <h3>Morse tähestik</h3><table class="morse">${Object.entries(MORSE).map(([L, c], i) => (i % 4 === 0 ? '<tr>' : '') + `<td><b>${L}</b></td><td style="font-family:monospace;font-size:22px">${c.replace(/\./g, '·').replace(/-/g, '–')}</td>` + (i % 4 === 3 ? '</tr>' : '')).join('')}</table>
    ${fluff('Raadio töötab ka ilma antennita. Kohalikku raadiojaama see vastu ei võta.')}`);
  P('Sümbolid', `<h2>12. Moodul: Sümbolid</h2><p>Moodulil on 4 nuppu imelike märkidega. Allpool on 6 tulpa. <b>Ainult ühes tulbas</b> on kõik 4 märki. Vajuta nupud selles järjekorras, nagu need selles tulbas <b>ülevalt alla</b> on.</p>
    <div class="symcols">${R.cols.map((c, i) => `<div><b>Tulp ${i + 1}</b>${c.map(id => `<canvas data-g="${id}" width="64" height="64"></canvas>`).join('')}</div>`).join('')}</div>
    ${fluff('Märgid on pärit muistsest kalendrist, mille täpne tähendus on teadmata. Võimalik, et need on ostunimekiri.')}`, () => document.querySelectorAll('canvas[data-g]').forEach(c => drawGlyph(c.getContext('2d'), +c.dataset.g, 32, 32, 50, '#2a241a')));
  const MT = { pos: v => `vajuta nuppu <b>kohal ${v}</b> (vasakult)`, lab: v => `vajuta nuppu, millel on number <b>${v}</b>`, ppos: v => `vajuta nuppu <b>samal kohal</b>, mis etapil ${v}`, plab: v => `vajuta nuppu <b>sama numbriga</b>, mis etapil ${v}` };
  P('Mälu', `<h2>13. Moodul: Mälu</h2><p>Moodulil on ekraan ühe numbriga (1–4) ja 4 nuppu numbritega. Moodulil on <b>4 etappi</b> (paremal 4 tulukest). Igal etapil vaata ekraani numbrit ja tee, mida tabel ütleb. <b>Pea meeles</b>, mida igal etapil vajutati (koht ja number) – hiljem võib seda vaja minna! Vale vajutus = viga ja moodul algab otsast.</p>
    ${[0, 1, 2, 3].map(st => `<h3>Etapp ${st + 1}</h3><ul>${R.m[st].map((x, d) => `<li>Ekraanil <b>${d + 1}</b> → ${MT[x.t](x.v)}.</li>`).join('')}</ul>`).join('')}`);
  P('Juhtmejada', `<h2>14. Moodul: Juhtmejada</h2><p>Moodulil on 3 lehte juhtmeid. Iga juhe läheb vasakult numbrilt paremale tähele (A, B või C). Lõika juhe ainult siis, kui selle sihttäht on tabelis. Loe, mitmes <b>sama värvi</b> juhe see on – loendus jätkub järgmistel lehtedel! Kui leht on tehtud, vajuta <b>▼</b>. Kui jätad lõikamata juhtme, mis oleks pidanud lõigatud olema, on see viga.</p>
    <table><tr><th>Mitmes</th>${QCOL.map(c => `<th>${c}</th>`).join('')}</tr>${[...Array(9)].map((_, i) => `<tr><td>${i + 1}.</td>${QCOL.map(c => `<td>${R.q[c][i].join(' või ')}</td>`).join('')}</tr>`).join('')}</table>`);
  P('KKK', `<h2>15. Korduma kippuvad küsimused</h2>${fluff('<b>K: Kas pommi saab välja lülitada?</b><br>V: Jah, lahtimuukimise teel.')}${fluff('<b>K: Mis juhtub, kui taimer jõuab nulli?</b><br>V: Seda on parem mitte teada.')}${fluff('<b>K: Kas juhendit saab lugeda tagant ettepoole?</b><br>V: Saab, aga see ei muuda midagi.')}${fluff('<b>K: Miks on juhendis nii palju lehti?</b><br>V: Juhend on koostatud põhjalikult.')}`);
  P('Garantii', `<h2>16. Garantiitingimused</h2>${fluff('Tootja ei vastuta kahjude eest, mis tekivad seadme plahvatamisel, kukkumisel, valel kasutamisel ega liiga hilisel lahtimuukimisel. Garantii ei kehti, kui seade on plahvatanud. Garantii ei kehti ka siis, kui seade ei ole plahvatanud. Pretensioonid palume esitada kirjalikult 3 päeva jooksul pärast plahvatust.')}<h3>Märkmed</h3><div class="lines"></div>`);
  pages[1].html = `<h2>Sisukord</h2><table class="toc">${pages.map((p, i) => `<tr><td style="text-align:left">${p.title}</td><td>${i + 1}</td></tr>`).join('')}</table>${fluff('Sisukord on koostatud tähestikulises järjekorras kõige tähtsamate peatükkide järgi.')}`;
  return pages;
}
function drawMazeManual(cv, mz, col) {
  const g = cv.getContext('2d'), S = 170, pad = 14, cs = (S - pad * 2) / MN;
  g.fillStyle = '#fff'; g.fillRect(0, 0, S, S); g.strokeStyle = col; g.lineWidth = 10; g.strokeRect(5, 5, S - 10, S - 10);
  g.fillStyle = '#999'; for (let y = 0; y < MN; y++) for (let x = 0; x < MN; x++) { g.beginPath(); g.arc(pad + cs * (x + 0.5), pad + cs * (y + 0.5), 3, 0, PI * 2); g.fill(); }
  g.strokeStyle = '#111'; g.lineWidth = 4; g.lineCap = 'round'; g.strokeRect(pad, pad, cs * MN, cs * MN);
  for (let y = 0; y < MN; y++) for (let x = 0; x < MN; x++) {
    if (x < MN - 1 && mz.E[y][x]) { g.beginPath(); g.moveTo(pad + cs * (x + 1), pad + cs * y); g.lineTo(pad + cs * (x + 1), pad + cs * (y + 1)); g.stroke(); }
    if (y < MN - 1 && mz.S[y][x]) { g.beginPath(); g.moveTo(pad + cs * x, pad + cs * (y + 1)); g.lineTo(pad + cs * (x + 1), pad + cs * (y + 1)); g.stroke(); }
  }
}

/* ============ PILTIDEGA JUHEND (lastele) ============ */
let E = {}, K = {}, LIVE = null, liveSig = '';
function kidReset() { E = { bat: null, last: null, vowel: null, maa: null }; K = { mod: null }; kidRender(); }
function setupKid() {
  let mode = 'kid'; try { mode = localStorage.getItem('pomm_mode') || 'kid'; } catch (e) { }
  const set = m => { mode = m; try { localStorage.setItem('pomm_mode', m); } catch (e) { } $('mKid').classList.toggle('on', m === 'kid'); $('mFull').classList.toggle('on', m === 'full'); $('kid').classList.toggle('hide', m !== 'kid'); $('mnav').classList.toggle('hide', m === 'kid'); $('mbody').classList.toggle('hide', m === 'kid'); scrollTo(0, 0); };
  $('mKid').onclick = () => set('kid'); $('mFull').onclick = () => set('full'); set(mode);
  $('kid').addEventListener('click', e => { const t = e.target.closest('[data-a]'); if (!t) return; kidAct(t.dataset.a, t.dataset.v); });
  kidReset();
}
const NEED = k => { if (E[k] === null || E[k] === undefined) throw { need: k }; return E[k]; };
function wiresK(c) { const n = c.length;
  if (n === 3) { if (c[0] === 'must') return 2; if (new Set(c).size === 2) { for (let i = 0; i < 3; i++) if (cnt(c, c[i]) === 1) return i; } return 0; }
  if (n === 4) { if (NEED('last') % 2 === 0) return 1; if (cnt(c, 'kollane') > cnt(c, 'punane')) return c.lastIndexOf('kollane'); if (!c.includes('roheline')) return 0; return 3; }
  if (n === 5) { if (c[4] === 'sinine') return 0; if (c.includes('valge') && NEED('bat') >= 2) return c.indexOf('valge'); return 2; }
  if (!c.includes('punane')) return 4; if (cnt(c, 'must') === 1) return c.indexOf('must'); if (NEED('vowel')) return 0; return 5; }
function buttonK(col, lab) { if (col === 'sinine' && lab === 'OOTA') return 'hold'; if (NEED('bat') > 2) return 'tap'; if (col === 'punane') return 'hold'; if (lab === 'VAJUTA') return 'tap'; return 'hold'; }
const ANIM = { KASS: '🐱', KOER: '🐶', HUNT: '🐺', KARU: '🐻', REBANE: '🦊', 'PÕDER': '🦌', ILVES: '🐆', 'JÄNES': '🐰', SIIL: '🦔', ORAV: '🐿️', KONN: '🐸', KULL: '🦅' };
const ORD = ['1.', '2.', '3.', '4.', '5.', '6.'];
// --- pildid ---
function svgWires(cols, n, cut) { const h = 40 + n * 44; let s = `<svg viewBox="0 0 320 ${h}" style="width:min(100%,340px)"><rect x="4" y="4" width="312" height="${h - 8}" rx="16" fill="#3c4148"/><rect x="40" y="16" width="16" height="${h - 32}" fill="#d8d0b8"/><rect x="264" y="16" width="16" height="${h - 32}" fill="#d8d0b8"/>`;
  for (let i = 0; i < n; i++) { const y = 40 + i * 44, c = cols[i]; s += `<text x="20" y="${y + 7}" font-size="20" font-weight="800" fill="#fff" text-anchor="middle">${i + 1}</text>`;
    if (c) { if (i === cut) s += `<path d="M48 ${y} Q110 ${y + 6} 140 ${y + 2}" stroke="${WHEX[c]}" stroke-width="12" fill="none" stroke-linecap="round"/><path d="M180 ${y + 2} Q220 ${y + 6} 272 ${y}" stroke="${WHEX[c]}" stroke-width="12" fill="none" stroke-linecap="round"/><text x="160" y="${y + 14}" font-size="38" text-anchor="middle">✂️</text><circle cx="160" cy="${y}" r="30" fill="none" stroke="#ff2a1a" stroke-width="5" stroke-dasharray="8 5"/>`;
      else s += `<path d="M48 ${y} Q160 ${y + 12} 272 ${y}" stroke="${c === 'must' ? '#111' : '#000'}" stroke-width="14" fill="none" opacity="${c === 'must' ? 0 : 0.35}"/><path d="M48 ${y} Q160 ${y + 12} 272 ${y}" stroke="${WHEX[c]}" stroke-width="11" fill="none" stroke-linecap="round" ${c === 'must' ? 'style="filter:drop-shadow(0 0 2px #fff)"' : ''}/>`; }
    else s += `<path d="M48 ${y} Q160 ${y + 12} 272 ${y}" stroke="#888" stroke-width="8" fill="none" stroke-dasharray="10 8"/><text x="160" y="${y + 8}" font-size="24" fill="#ddd" text-anchor="middle" font-weight="800">?</text>`; }
  return s + '</svg>'; }
function svgButton(col, lab) { const fc = col ? WHEX[col] : '#999'; const tc = col === 'valge' || col === 'kollane' ? '#111' : '#fff'; return `<svg viewBox="0 0 200 200" style="width:170px"><rect x="4" y="4" width="192" height="192" rx="20" fill="#3c4148"/><circle cx="100" cy="100" r="74" fill="#1a1c20"/><circle cx="100" cy="100" r="62" fill="${fc}"/><text x="100" y="110" font-size="${lab && lab.length > 4 ? 26 : 32}" font-weight="900" fill="${tc}" text-anchor="middle">${lab || '?'}</text></svg>`; }
function svgLamps(L, target) { let s = `<svg viewBox="0 0 340 ${target ? 230 : 110}" style="width:min(100%,380px)"><rect x="4" y="4" width="332" height="${target ? 222 : 102}" rx="16" fill="#3c4148"/>`;
  L.forEach((on, i) => { const x = 50 + i * 60; s += `<g data-a="lamp" data-v="${i}" style="cursor:pointer"><circle cx="${x}" cy="55" r="26" fill="${on ? '#ffe040' : '#3a3520'}" stroke="#111" stroke-width="4"/>${on ? `<circle cx="${x}" cy="55" r="34" fill="none" stroke="#ffe040" stroke-width="3" opacity=".6"/>` : ''}</g>`;
    if (target) { const up = target[i]; s += `<rect x="${x - 14}" y="110" width="28" height="70" rx="8" fill="#1a1c20"/><line x1="${x}" y1="145" x2="${x}" y2="${up ? 112 : 178}" stroke="#d8dce2" stroke-width="9" stroke-linecap="round"/><text x="${x}" y="214" font-size="30" text-anchor="middle">${up ? '⬆️' : '⬇️'}</text>`; } });
  return s + '</svg>'; }
function svgMaze(mi, me, goal, path, clickable) { const mz = MAZES[mi], cs = 60, pad = 20, W = pad * 2 + cs * MN; let s = `<svg viewBox="0 0 ${W} ${W}" style="width:min(100%,380px);touch-action:manipulation"><rect x="4" y="4" width="${W - 8}" height="${W - 8}" rx="14" fill="#fff" stroke="${MHEX[MCOL[mi]]}" stroke-width="12"/>`;
  for (let y = 0; y < MN; y++) for (let x = 0; x < MN; x++) s += `<rect x="${pad + x * cs}" y="${pad + y * cs}" width="${cs}" height="${cs}" fill="transparent" ${clickable ? `data-a="cell" data-v="${x},${y}" style="cursor:pointer"` : ''}/><circle cx="${pad + cs * (x + 0.5)}" cy="${pad + cs * (y + 0.5)}" r="5" fill="#aaa" pointer-events="none"/>`;
  if (path && me) { let d = `M${pad + cs * (me[0] + 0.5)} ${pad + cs * (me[1] + 0.5)}`; let [x, y] = me; for (const [dx, dy] of path) { x += dx; y += dy; d += ` L${pad + cs * (x + 0.5)} ${pad + cs * (y + 0.5)}`; } s += `<path d="${d}" stroke="#30c060" stroke-width="10" fill="none" stroke-linecap="round" stroke-linejoin="round" opacity=".7" pointer-events="none"/>`; }
  s += `<g stroke="#111" stroke-width="6" stroke-linecap="round" pointer-events="none"><rect x="${pad}" y="${pad}" width="${cs * MN}" height="${cs * MN}" fill="none"/>`;
  for (let y = 0; y < MN; y++) for (let x = 0; x < MN; x++) { if (x < MN - 1 && mz.E[y][x]) s += `<line x1="${pad + cs * (x + 1)}" y1="${pad + cs * y}" x2="${pad + cs * (x + 1)}" y2="${pad + cs * (y + 1)}"/>`; if (y < MN - 1 && mz.S[y][x]) s += `<line x1="${pad + cs * x}" y1="${pad + cs * (y + 1)}" x2="${pad + cs * (x + 1)}" y2="${pad + cs * (y + 1)}"/>`; }
  s += '</g>';
  if (goal) { const cx = pad + cs * (goal[0] + 0.5), cy = pad + cs * (goal[1] + 0.5); s += `<path d="M${cx - 16} ${cy - 16} L${cx + 16} ${cy + 16} M${cx + 16} ${cy - 16} L${cx - 16} ${cy + 16}" stroke="#e02020" stroke-width="8" stroke-linecap="round" pointer-events="none"/>`; }
  if (me) s += `<circle cx="${pad + cs * (me[0] + 0.5)}" cy="${pad + cs * (me[1] + 0.5)}" r="19" fill="none" stroke="#20b050" stroke-width="7" pointer-events="none"/>`;
  return s + '</svg>'; }
function mazePath(mi, a, b) { const mz = MAZES[mi], k = (x, y) => x + ',' + y, prev = { [k(...a)]: null }, q = [a]; while (q.length) { const [x, y] = q.shift(); if (x === b[0] && y === b[1]) break; for (const [dx, dy] of [[1, 0], [-1, 0], [0, 1], [0, -1]]) { if (!canMove(mz, x, y, dx, dy)) continue; const nk = k(x + dx, y + dy); if (nk in prev) continue; prev[nk] = [x, y, dx, dy]; q.push([x + dx, y + dy]); } }
  const p = []; let c = b; while (prev[k(...c)]) { const [x, y, dx, dy] = prev[k(...c)]; p.unshift([dx, dy]); c = [x, y]; } return p; }
const TILE = {
  juhtmed: `<svg viewBox="0 0 140 110"><rect x="2" y="2" width="136" height="106" rx="12" fill="#3c4148"/><rect x="18" y="12" width="8" height="86" fill="#d8d0b8"/><rect x="114" y="12" width="8" height="86" fill="#d8d0b8"/>${['#d23a2e', '#2f62d8', '#f0c820', '#f2f2f2'].map((c, i) => `<path d="M22 ${24 + i * 21} Q70 ${30 + i * 21} 118 ${24 + i * 21}" stroke="${c}" stroke-width="7" fill="none"/>`).join('')}</svg>`,
  nupp: `<svg viewBox="0 0 140 110"><rect x="2" y="2" width="136" height="106" rx="12" fill="#3c4148"/><circle cx="62" cy="55" r="40" fill="#1a1c20"/><circle cx="62" cy="55" r="33" fill="#d23a2e"/><text x="62" y="61" font-size="15" font-weight="900" fill="#fff" text-anchor="middle">HOIA</text><rect x="112" y="20" width="12" height="70" rx="4" fill="#111"/></svg>`,
  lulitid: `<svg viewBox="0 0 140 110"><rect x="2" y="2" width="136" height="106" rx="12" fill="#3c4148"/>${[1, 0, 1, 1, 0].map((on, i) => `<circle cx="${22 + i * 24}" cy="28" r="9" fill="${on ? '#ffe040' : '#3a3520'}"/><rect x="${16 + i * 24}" y="48" width="12" height="30" rx="3" fill="#1a1c20"/><line x1="${22 + i * 24}" y1="63" x2="${22 + i * 24}" y2="${i % 2 ? 76 : 50}" stroke="#ddd" stroke-width="4" stroke-linecap="round"/>`).join('')}<rect x="44" y="88" width="52" height="14" rx="4" fill="#2a6a3a"/></svg>`,
  kood: `<svg viewBox="0 0 140 110"><rect x="2" y="2" width="136" height="106" rx="12" fill="#3c4148"/><rect x="20" y="10" width="100" height="26" rx="4" fill="#062010"/><text x="70" y="29" font-size="16" font-weight="900" fill="#40ff80" text-anchor="middle">KASS</text>${[...Array(9)].map((_, i) => `<rect x="${38 + (i % 3) * 23}" y="${42 + ((i / 3) | 0) * 21}" width="18" height="16" rx="3" fill="#d8d8d0"/>`).join('')}</svg>`,
  lab: `<svg viewBox="0 0 140 110"><rect x="2" y="2" width="136" height="106" rx="12" fill="#3c4148"/><rect x="34" y="12" width="72" height="72" fill="#0a0c10" stroke="#2f9a44" stroke-width="5"/>${[...Array(25)].map((_, i) => `<circle cx="${43 + (i % 5) * 13.5}" cy="${21 + ((i / 5) | 0) * 13.5}" r="2" fill="#667"/>`).join('')}<circle cx="56" cy="61" r="5" fill="none" stroke="#30ff70" stroke-width="2.5"/><text x="97" y="30" font-size="12" fill="#f33" font-weight="900">✕</text><text x="70" y="104" font-size="14" fill="#ddd" text-anchor="middle">▲ ▼ ◀ ▶</text></svg>`,
};
const MODNAME = { juhtmed: 'Juhtmed', nupp: 'Nupp', lulitid: 'Lülitid', kood: 'Koodilukk', lab: 'Labürint' };
function edgeQ(k) {
  const q = { bat: ['🔋 Mitu patareid on pommi VASAKUL küljel?', 'Pommimees peab pommi keerama ja lugema.', [0, 1, 2, 3, 4].map(n => `<button class="kbtn big" data-a="edge" data-v="bat:${n}">${n ? '🔋'.repeat(n) : '🚫'}<br>${n}</button>`).join('')],
    last: ['🔢 Mis on seerianumbri VIIMANE number?', 'Seerianumber on pommi peal, nt KR4-7<b>9</b>B → 9. Tähti ei loe!', [...'0123456789'].map(n => `<button class="kbtn big" data-a="edge" data-v="last:${n}">${n}</button>`).join('')],
    vowel: ['🔤 Kas seerianumbris on täht A, E, I, O või U?', 'Seerianumber on pommi peal.', `<button class="kbtn big" data-a="edge" data-v="vowel:1">👍 JAH</button><button class="kbtn big" data-a="edge" data-v="vowel:0">👎 EI</button>`],
    maa: ['💡 Kas pommi PAREMAL küljel on kiri MAA ja tuli põleb?', 'Mõlemad peavad olema: kiri on MAA ja kõrval olev tuli põleb.', `<button class="kbtn big" data-a="edge" data-v="maa:1">👍 JAH</button><button class="kbtn big" data-a="edge" data-v="maa:0">👎 EI</button>`] }[k];
  return `<div class="steps">Enne vastust on vaja teada pommi külje kohta:</div><div class="kq">${q[0]}</div><div class="ksub">${q[1]}</div><div class="kgrid">${q[2]}</div>`;
}
const swBtn = (cols, act, names) => cols.map(c => `<div class="sw" data-a="${act}" data-v="${c}" style="background:${(names || WHEX)[c]};color:${['valge', 'kollane'].includes(c) ? '#111' : '#fff'}">${c}</div>`).join('');
const doneBtns = `<div class="kgrid" style="margin-top:16px"><button class="kbtn" data-a="home" style="background:#c8f0c8">✅ Tehtud! Järgmine moodul</button><button class="kbtn sm" data-a="redo">↩ Alusta seda uuesti</button></div>`;
function kidBody() {
  if (!K.mod) return `<div class="kq">Mida pommimees näeb?</div><div class="ksub">Vali pilt, mis on pommil. Rohelise tulega moodul on juba tehtud.</div><div class="kgrid">${Object.keys(MODNAME).map(m => `<div class="tile" data-a="mod" data-v="${m}">${TILE[m]}<div>${MODNAME[m]}</div></div>`).join('')}</div>`;
  const back = `<div style="text-align:left"><button class="kbtn sm" data-a="home">⬅ Tagasi</button></div>`;
  try {
    if (K.mod === 'juhtmed') {
      if (!K.n) return back + `<div class="steps">Samm 1 / 3</div><div class="kq">Mitu juhet on?</div><div class="kgrid">${[3, 4, 5, 6].map(n => `<div class="tile" data-a="wn" data-v="${n}" style="width:130px">${svgWires([], n).replace('style="width:min(100%,340px)"', 'style="width:110px"')}<div>${n}</div></div>`).join('')}</div>`;
      if (K.cols.length < K.n) return back + `<div class="steps">Samm 2 / 3</div><div class="kq">Mis värvi on ${ORD[K.cols.length]} juhe?</div><div class="ksub">Loe ülevalt alla.</div>${svgWires(K.cols, K.n)}<div class="kgrid" style="margin-top:12px">${swBtn(WCOL, 'wc')}</div><div style="margin-top:10px"><button class="kbtn sm" data-a="wundo">↩ Võta tagasi</button></div>`;
      const i = wiresK(K.cols); return back + `<div class="steps">Samm 3 / 3 – VASTUS</div><div class="ans">✂️ Lõika ${ORD[i]} juhe</div><div class="kq" style="color:${WHEX[K.cols[i]] === '#f2f2f2' ? '#777' : WHEX[K.cols[i]]}">(${K.cols[i]})</div>${svgWires(K.cols, K.n, i)}` + doneBtns;
    }
    if (K.mod === 'nupp') {
      if (!K.col) return back + `<div class="steps">Samm 1</div><div class="kq">Mis värvi on nupp?</div><div class="kgrid">${swBtn(BCOL, 'bc')}</div>`;
      if (!K.lab) return back + `<div class="steps">Samm 2</div>${svgButton(K.col)}<div class="kq">Mis on nupule kirjutatud?</div><div class="kgrid">${BLAB.map(l => `<button class="kbtn big" data-a="bl" data-v="${l}">${l}</button>`).join('')}</div>`;
      const a = buttonK(K.col, K.lab);
      if (a === 'tap') return back + `${svgButton(K.col, K.lab)}<div class="ans">👆 VAJUTA JA LASE KOHE LAHTI!</div><div class="ksub">Ainult üks kiire klõps.</div>` + doneBtns;
      if (!K.strip) return back + `${svgButton(K.col, K.lab)}<div class="ans">✊ HOIA NUPPU ALL!</div><div class="kq">Ära lase lahti! Mis värvi riba süttis nupu kõrval?</div><div class="kgrid">${swBtn(Object.keys(STRIP), 'bs')}</div>`;
      return back + `<div class="kq">Lase nupp lahti, kui taimeri VIIMANE number on:</div><div class="digit">${STRIP[K.strip]}</div><div class="ksub" style="margin-top:12px">Näiteks taimer 2:3<b>${STRIP[K.strip]}</b> → nüüd lase lahti!</div>` + doneBtns;
    }
    if (K.mod === 'lulitid') {
      if (!K.ldone) return back + `<div class="steps">Samm 1</div><div class="kq">Klõpsa lampe, mis PÕLEVAD 💡</div><div class="ksub">Küsi pommimehelt vasakult paremale.</div>${svgLamps(K.lamps)}<div style="margin-top:14px"><button class="kbtn big" data-a="ldone" style="background:#c8f0c8">Valmis ➜</button></div>`;
      const t = switchTarget(K.lamps); return back + `<div class="steps">VASTUS</div><div class="kq">Pane lülitid nii:</div>${svgLamps(K.lamps, t)}<div class="ans" style="font-size:clamp(22px,5vw,34px)">${t.map(x => x ? 'ÜLES' : 'ALLA').join(' · ')}</div><div class="kq">Siis vajuta rohelist nuppu VALMIS ✅</div>` + doneBtns;
    }
    if (K.mod === 'kood') {
      if (!K.word) return back + `<div class="steps">Samm 1</div><div class="kq">Mis loom on ekraanil?</div><div class="kgrid">${Object.keys(WORDS).map(w => `<div class="animal" data-a="word" data-v="${w}"><div>${ANIM[w]}</div><div>${w}</div></div>`).join('')}</div>`;
      const rev = NEED('maa'); const c = rev ? [...WORDS[K.word]].reverse().join('') : WORDS[K.word];
      return back + `<div style="font-size:70px">${ANIM[K.word]}</div><div class="kq">Ütle pommimehele need numbrid:</div><div>${[...c].map(d => `<span class="digit">${d}</span>`).join('')}</div>${rev ? '<div class="ksub" style="margin-top:10px">(tagurpidi, sest MAA tuli põleb)</div>' : ''}` + doneBtns;
    }
    if (K.mod === 'lab') {
      if (K.mi == null) return back + `<div class="steps">Samm 1 / 3</div><div class="kq">Mis värvi on ekraani raam?</div><div class="kgrid">${swBtn(MCOL, 'mc', MHEX)}</div>`;
      if (!K.me) return back + `<div class="steps">Samm 2 / 3</div><div class="kq">Klõpsa, kus on <span style="color:#20b050">ROHELINE RING</span> ⭕</div>${svgMaze(K.mi, null, null, null, true)}`;
      if (!K.goal) return back + `<div class="steps">Samm 3 / 3</div><div class="kq">Klõpsa, kus on <span style="color:#e02020">PUNANE RIST</span> ❌</div>${svgMaze(K.mi, K.me, null, null, true)}<div><button class="kbtn sm" data-a="mundo">↩ Võta tagasi</button></div>`;
      const p = mazePath(K.mi, K.me, K.goal); const AR = { '1,0': '➡️', '-1,0': '⬅️', '0,1': '⬇️', '0,-1': '⬆️' };
      return back + `<div class="steps">VASTUS</div><div class="kq">Ütle need nooled järjest:</div><div class="arrows">${p.map((d, i) => `<span><small>${i + 1}</small>${AR[d.join()]}</span>`).join('')}</div>${svgMaze(K.mi, K.me, K.goal, p)}<div><button class="kbtn sm" data-a="mundo">↩ Vale koht? Muuda</button></div>` + doneBtns;
    }
  } catch (e) { if (e && e.need) return back + edgeQ(e.need); throw e; }
}
function kidRender() {
  if (LIVE) { const sig = JSON.stringify([LIVE.kid, LIVE.focus, Math.floor(LIVE.time) % 10, LIVE.strikes]); if (sig === liveSig) return; liveSig = sig; $('kid').innerHTML = liveView(LIVE); return; }
  if (liveSig) { liveSig = ''; }
  const chips = []; if (E.bat != null) chips.push(`🔋 patareid: ${E.bat}`); if (E.last != null) chips.push(`🔢 viimane number: ${E.last}`); if (E.vowel != null) chips.push(`🔤 A/E/I/O/U: ${E.vowel ? 'jah' : 'ei'}`); if (E.maa != null) chips.push(`💡 MAA põleb: ${E.maa ? 'jah' : 'ei'}`);
  $('kid').innerHTML = (chips.length ? `<div class="kcard" style="padding:10px"><div class="chips">${chips.map(c => `<span class="chip">${c}</span>`).join('')}<button class="kbtn sm" data-a="edgereset">Uus pomm – unusta</button></div></div>` : '') + `<div class="kcard">${kidBody()}</div>`;
}

let etVoice = null; try { const pv = () => { etVoice = speechSynthesis.getVoices().find(v => (v.lang || '').toLowerCase().startsWith('et')) || null; }; pv(); speechSynthesis.onvoiceschanged = pv; } catch (e) { }
function speakEt(t) { if (!etVoice) return; try { speechSynthesis.cancel(); const u = new SpeechSynthesisUtterance(t); u.voice = etVoice; u.lang = etVoice.lang; speechSynthesis.speak(u); } catch (e) { } }
const CW = c => `<b style="color:${c === 'valge' ? '#777' : WHEX[c]};text-shadow:${c === 'valge' ? '0 0 2px #000' : 'none'}">${c.toUpperCase()}</b>`;
const ARW = { '1,0': ['➡️', 'PAREMALE'], '-1,0': ['⬅️', 'VASAKULE'], '0,1': ['⬇️', 'ALLA'], '0,-1': ['⬆️', 'ÜLES'] };
function liveCard(m, i, st) {
  const focus = st.focus === i;
  const wrap = (body, say) => `<div class="kcard" style="${focus ? 'outline:6px solid #f2c230;' : ''}">${focus ? '<div class="steps" style="font-size:20px;opacity:1">👀 Pommimees vaatab seda!</div>' : ''}${body}${say && etVoice ? `<div><button class="kbtn sm" data-a="say" data-v="${say}">🔊 Loe ette</button></div>` : ''}</div>`;
  if (m.solved) return `<div class="kcard" style="padding:8px;opacity:.7"><b style="font-size:22px">✅ ${MODNAME[m.id]} – tehtud!</b></div>`;
  if (m.id === 'juhtmed') { const c = m.cols[m.ans]; return wrap(`<div class="kq">Ütle: ✂️ Lõika ${CW(c)} juhe!</div><div class="ksub">See on ${m.ans + 1}. juhe ülevalt.</div>${svgWires(m.cols, m.cols.length, m.ans)}`, `Lõika ${c} juhe. See on ${m.ans + 1}. juhe ülevalt.`); }
  if (m.id === 'nupp') {
    if (m.act === 'tap') return wrap(`${svgButton(m.col, m.lab)}<div class="ans">👆 Ütle: "Vajuta üks kord kiiresti!"</div>`, 'Vajuta nuppu üks kord kiiresti.');
    if (!m.held) return wrap(`${svgButton(m.col, m.lab)}<div class="ans">✊ Ütle: "Vajuta ja HOIA all!"</div><div class="ksub">Ära lase lahti enne, kui ütlen!</div>`, 'Vajuta nuppu ja hoia all.');
    if (!m.strip) return wrap(`${svgButton(m.col, m.lab)}<div class="ans">✊ Hoia… hoia…</div>`);
    const dg = STRIP[m.strip], now = Math.floor(st.time) % 10 === dg;
    return wrap(now ? `<div style="background:#2fbf5a;border-radius:20px;padding:30px 10px;animation:none"><div style="font-size:clamp(44px,12vw,90px);font-weight:900;color:#fff">LASE LAHTI<br>NÜÜD! 🎉</div></div>` : `<div class="ans">⏳ Ütle: "Hoia veel…"</div><div class="ksub">Kui taimeri lõpus on <b>${dg}</b>, hüüa "NÜÜD!"</div><div class="digit" style="color:#888">${Math.floor(st.time) % 10}</div>`, now ? 'Lase lahti nüüd!' : '');
  }
  if (m.id === 'lulitid') { const wrong = m.pos.map((p, k) => p !== m.target[k]); const allOk = !wrong.some(Boolean);
    return wrap(`${svgLamps(m.lamps, m.target)}${allOk ? '<div class="ans" style="color:#2f9a44">✅ Ütle: "Vajuta rohelist VALMIS nuppu!"</div>' : `<div class="kq">Ütle, mis lüliti tuleb keerata:</div><div class="kgrid">${wrong.map((w, k) => w ? `<span class="kbtn" style="cursor:default">${k + 1}. ${m.target[k] ? '⬆️ ÜLES' : '⬇️ ALLA'}</span>` : '').join('')}</div>`}`,
      allOk ? 'Vajuta rohelist valmis nuppu.' : wrong.map((w, k) => w ? `${k + 1}. lüliti ${m.target[k] ? 'üles' : 'alla'}` : '').filter(Boolean).join(', '));
  }
  if (m.id === 'kood') { const n = m.entry.length; return wrap(`<div style="font-size:64px">${ANIM[m.word]}</div><div class="kq">Ütle numbrid:</div><div>${[...m.code].map((d, k) => `<span class="digit" style="${k < n ? 'background:#1d5a2a;color:#9fffb8' : k === n ? 'outline:5px solid #f2c230' : 'opacity:.5'}">${d}</span>`).join('')}</div><div class="ans">Järgmine: ${m.code[n] ?? ''}</div>`, `Vajuta ${m.code[n]}`); }
  if (m.id === 'lab') { const path = mazePath(m.mi, m.p, m.goal); const nx = path[0] ? ARW[path[0].join()] : null;
    return wrap(`${nx ? `<div style="font-size:90px;line-height:1">${nx[0]}</div><div class="ans">Ütle: "${nx[1]}!"</div>` : ''}${svgMaze(m.mi, m.p, m.goal, path)}`, nx ? nx[1].toLowerCase() : ''); }
  return '';
}
function liveView(st) {
  const order = st.kid.map((m, i) => i).sort((a, b) => (b === st.focus) - (a === st.focus) || st.kid[a].solved - st.kid[b].solved);
  const recent = Date.now() - (st.strikeAt || 0) < 1500;
  return `<div class="kcard" style="padding:10px;background:#fff3c4"><b style="font-size:20px">👶 Väike režiim – pilt näitab, mida öelda!</b></div>${recent ? '<div class="kcard" style="background:#ffd0c8;font-size:28px;font-weight:900">😬 Oih! Viga – proovi uuesti</div>' : ''}${order.map(i => liveCard(st.kid[i], i, st)).join('')}`;
}
function kidAct(a, v) {
  if (a === 'say') { speakEt(v); return; }
  if (a === 'home') K = { mod: null };
  else if (a === 'mod') K = { mod: v, cols: [], lamps: [0, 0, 0, 0, 0] };
  else if (a === 'redo') K = { mod: K.mod, cols: [], lamps: [0, 0, 0, 0, 0] };
  else if (a === 'edge') { const [k, x] = v.split(':'); E[k] = +x; }
  else if (a === 'edgereset') kidReset();
  else if (a === 'wn') K.n = +v; else if (a === 'wc') K.cols.push(v); else if (a === 'wundo') { if (K.cols.length) K.cols.pop(); else K.n = 0; }
  else if (a === 'bc') K.col = v; else if (a === 'bl') K.lab = v; else if (a === 'bs') K.strip = v;
  else if (a === 'lamp') { if (!K.ldone) K.lamps[+v] ^= 1; } else if (a === 'ldone') K.ldone = true;
  else if (a === 'word') K.word = v;
  else if (a === 'mc') K.mi = MCOL.indexOf(v); else if (a === 'cell') { const c = v.split(',').map(Number); if (!K.me) K.me = c; else if (!K.goal) { if (c[0] === K.me[0] && c[1] === K.me[1]) return; K.goal = c; } } else if (a === 'mundo') { if (K.goal) K.goal = null; else K.me = null; }
  kidRender(); if (['mod', 'home', 'redo'].includes(a)) scrollTo(0, 0);
}

/* ============ POMMIMEES ============ */
function startBomb(forced) {
  $('start').classList.add('hide'); $('bombHud').classList.remove('hide');
  let code = forced && /^\d{4}$/.test(forced) ? forced : String(1000 + rint(9000));
  let net, lastHi = -1e9, netStatus = '';
  const connect = () => { net && net.destroy(); $('hudCode').textContent = code; net = makeNet(code, 'bomb', m => { if (m && m.type === 'hi') { lastHi = performance.now(); sendState(); } }, s => { netStatus = s; if (s === 'err:unavailable-id') { code = String(1000 + rint(9000)); connect(); } menu && (menu.last = ''); }); };

  /* --- renderdaja --- */
  const renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setPixelRatio(Math.min(devicePixelRatio, 2)); renderer.setSize(innerWidth, innerHeight);
  renderer.outputColorSpace = THREE.SRGBColorSpace; renderer.toneMapping = THREE.ACESFilmicToneMapping; renderer.toneMappingExposure = 1.15;
  renderer.shadowMap.enabled = true; renderer.shadowMap.type = THREE.PCFSoftShadowMap;
  renderer.xr.enabled = true; renderer.xr.setReferenceSpaceType('local-floor');
  document.body.appendChild(renderer.domElement);
  const scene = new THREE.Scene(); scene.background = new THREE.Color('#0e1013'); scene.fog = new THREE.Fog('#0e1013', 4, 12);
  const camera = new THREE.PerspectiveCamera(55, innerWidth / innerHeight, 0.01, 50); camera.rotation.order = 'YXZ';
  addEventListener('resize', () => { camera.aspect = innerWidth / innerHeight; camera.updateProjectionMatrix(); renderer.setSize(innerWidth, innerHeight); });
  const rig = new THREE.Group(); scene.add(rig); rig.add(camera);
  scene.add(new THREE.HemisphereLight('#8090a8', '#20180f', 0.7));
  const spot = new THREE.SpotLight('#fff1d6', 40, 5, 0.6, 0.5, 1.5); spot.position.set(0.3, 2.3, -0.2); spot.target.position.set(0, 0.95, -0.45); spot.castShadow = true; spot.shadow.mapSize.set(1024, 1024); spot.shadow.bias = -0.0005; scene.add(spot, spot.target);
  const fill = new THREE.PointLight('#6080ff', 2, 4); fill.position.set(-1, 1.6, 0.5); scene.add(fill);
  const alarm = new THREE.PointLight('#ff2010', 0, 6); alarm.position.set(0, 2.3, -1.6); scene.add(alarm);

  /* --- abi --- */
  const cnv = (w, h) => { const c = document.createElement('canvas'); c.width = w; c.height = h; return c; };
  const ctex = c => { const t = new THREE.CanvasTexture(c); t.colorSpace = THREE.SRGBColorSpace; t.anisotropy = 4; return t; };
  const M = (color, o = {}) => new THREE.MeshStandardMaterial(Object.assign({ color, roughness: 0.6, metalness: 0.2 }, o));
  function mesh(geo, mat, x = 0, y = 0, z = 0, parent = scene) { const m = new THREE.Mesh(geo, mat); m.position.set(x, y, z); m.castShadow = true; m.receiveShadow = true; parent.add(m); return m; }
  function rr(g, x, y, w, h, r) { g.beginPath(); g.moveTo(x + r, y); g.arcTo(x + w, y, x + w, y + h, r); g.arcTo(x + w, y + h, x, y + h, r); g.arcTo(x, y + h, x, y, r); g.arcTo(x, y, x + w, y, r); g.closePath(); }
  function txt(g, s, x, y, size, col, align = 'center', bold = true, font = 'system-ui,sans-serif') { g.font = `${bold ? 'bold ' : ''}${size}px ${font}`; g.fillStyle = col; g.textAlign = align; g.textBaseline = 'middle'; g.fillText(s, x, y); }
  function fit(g, s, x, y, size, col, maxW, align = 'center', bold = true) { let fs = size; g.font = `${bold ? 'bold ' : ''}${fs}px system-ui`; while (g.measureText(s).width > maxW && fs > 12) { fs -= 2; g.font = `${bold ? 'bold ' : ''}${fs}px system-ui`; } txt(g, s, x, y, fs, col, align, bold); }
  function canvasPlane(w, h, W, H, draw, parent, x = 0, y = 0, z = 0, basic = true) { const c = cnv(W, H); const m = new THREE.Mesh(new THREE.PlaneGeometry(w, h), basic ? new THREE.MeshBasicMaterial({ map: ctex(c), transparent: true }) : new THREE.MeshStandardMaterial({ map: ctex(c), roughness: 0.7 })); m.position.set(x, y, z); parent.add(m); m.redraw = (...a) => { const g = c.getContext('2d'); g.clearRect(0, 0, W, H); draw(g, W, H, ...a); m.material.map.needsUpdate = true; }; m.redraw(); return m; }

  /* --- heli --- */
  let AC = null, master;
  const initAudio = () => { if (AC) { if (AC.state === 'suspended') AC.resume(); return; } try { AC = new (window.AudioContext || window.webkitAudioContext)(); master = AC.createGain(); master.gain.value = 0.7; master.connect(AC.destination); } catch (e) { } };
  const tone = (f1, f2, dur, type = 'sine', vol = 0.2, delay = 0) => { if (!AC) return; const t = AC.currentTime + delay; const o = AC.createOscillator(), g = AC.createGain(); o.type = type; o.frequency.setValueAtTime(f1, t); o.frequency.exponentialRampToValueAtTime(Math.max(1, f2), t + dur); g.gain.setValueAtTime(vol, t); g.gain.exponentialRampToValueAtTime(0.0001, t + dur); o.connect(g).connect(master); o.start(t); o.stop(t + dur + 0.02); };
  const noise = (dur, vol, f, type = 'bandpass', delay = 0) => { if (!AC) return; const t = AC.currentTime + delay; const b = AC.createBuffer(1, Math.max(1, AC.sampleRate * dur | 0), AC.sampleRate), d = b.getChannelData(0); for (let i = 0; i < d.length; i++) d[i] = (Math.random() * 2 - 1) * Math.pow(1 - i / d.length, 1.5); const s = AC.createBufferSource(); s.buffer = b; const fl = AC.createBiquadFilter(); fl.type = type; fl.frequency.value = f; const g = AC.createGain(); g.gain.value = vol; s.connect(fl).connect(g).connect(master); s.start(t); };
  const sfx = {
    tick: hi => tone(hi ? 1800 : 1200, hi ? 1800 : 1200, 0.03, 'square', hi ? 0.06 : 0.035), click: () => tone(900, 600, 0.04, 'square', 0.05),
    snip: () => { noise(0.08, 0.6, 4000); tone(2600, 1800, 0.05, 'triangle', 0.1); }, strike: () => { tone(160, 120, 0.5, 'sawtooth', 0.18); tone(165, 125, 0.5, 'square', 0.08); },
    solve: () => { tone(880, 880, 0.1, 'sine', 0.15); tone(1320, 1320, 0.25, 'sine', 0.15, 0.1); },
    boom: () => { noise(2.5, 1.2, 400, 'lowpass'); noise(0.4, 0.8, 2000, 'lowpass'); tone(70, 30, 1.5, 'sine', 0.6); },
    win: () => [523, 659, 784, 1046, 1318].forEach((f, i) => tone(f, f, 0.35, 'triangle', 0.14, i * 0.11)), key: () => tone(1500, 1500, 0.05, 'sine', 0.06),
    sw: () => { noise(0.03, 0.4, 3000, 'highpass'); tone(400, 300, 0.03, 'square', 0.04); },
  };
  const haptic = (hand, v, ms) => { const s = renderer.xr.getSession(); if (!s) return; for (const src of s.inputSources) if (src.handedness === hand) src.gamepad?.hapticActuators?.[0]?.pulse?.(v, ms); };

  /* --- tuba --- */
  (() => {
    const c = cnv(256, 256), g = c.getContext('2d'); g.fillStyle = '#3a3c3f'; g.fillRect(0, 0, 256, 256); for (let i = 0; i < 6000; i++) { g.fillStyle = `rgba(${Math.random() < 0.5 ? '0,0,0' : '255,255,255'},${Math.random() * 0.06})`; g.fillRect(Math.random() * 256, Math.random() * 256, 2, 2); }
    const ft = ctex(c); ft.wrapS = ft.wrapT = THREE.RepeatWrapping; ft.repeat.set(5, 5);
    mesh(new THREE.PlaneGeometry(10, 10).rotateX(-PI / 2), new THREE.MeshStandardMaterial({ map: ft, roughness: 0.9 }), 0, 0, -1).castShadow = false;
    const wm = new THREE.MeshStandardMaterial({ color: '#2a2e33', roughness: 0.95 });
    const w1 = mesh(new THREE.PlaneGeometry(10, 4), wm, 0, 2, -2.2); w1.castShadow = false;
    const w2 = mesh(new THREE.PlaneGeometry(6, 4), wm, -2.5, 2, 0.5); w2.rotation.y = PI / 2; w2.castShadow = false;
    const w3 = mesh(new THREE.PlaneGeometry(6, 4), wm, 2.5, 2, 0.5); w3.rotation.y = -PI / 2; w3.castShadow = false;
    // laud
    const wood = M('#4a3a2a', { roughness: 0.8, metalness: 0 });
    mesh(new THREE.BoxGeometry(1.4, 0.05, 0.75), M('#5a5e64', { metalness: 0.6, roughness: 0.4 }), 0, 0.8, -0.55);
    for (const [x, z] of [[-0.65, -0.88], [0.65, -0.88], [-0.65, -0.22], [0.65, -0.22]]) mesh(new THREE.BoxGeometry(0.05, 0.8, 0.05), M('#3a3e44', { metalness: 0.6 }), x, 0.4, z);
    // tööriistad laual
    mesh(new THREE.CylinderGeometry(0.012, 0.012, 0.16, 8).rotateZ(PI / 2), M('#c03020'), 0.45, 0.835, -0.35);
    mesh(new THREE.BoxGeometry(0.03, 0.01, 0.12), M('#aab0b8', { metalness: 0.9 }), 0.52, 0.83, -0.45);
    mesh(new THREE.BoxGeometry(0.22, 0.01, 0.3), M('#e8e0c8', { roughness: 1, metalness: 0 }), -0.45, 0.83, -0.5).rotation.y = 0.2;
    // hoiatussilt
    const sc = cnv(512, 256), sg = sc.getContext('2d'); sg.fillStyle = '#f2c230'; sg.fillRect(0, 0, 512, 256); sg.fillStyle = '#111'; sg.fillRect(12, 12, 488, 232); sg.fillStyle = '#f2c230'; sg.fillRect(24, 24, 464, 208); txt(sg, '⚠ OHT!', 256, 95, 90, '#111'); txt(sg, 'LÕHKEAINE', 256, 180, 60, '#111');
    mesh(new THREE.PlaneGeometry(0.8, 0.4), new THREE.MeshStandardMaterial({ map: ctex(sc) }), 0.9, 1.9, -2.19);
    mesh(new THREE.CylinderGeometry(0.08, 0.1, 0.12, 16), M('#801010', { emissive: '#300000' }), 0, 2.35, -2.15).rotation.x = PI / 2;
    mesh(new THREE.BoxGeometry(0.6, 0.9, 0.05), M('#3a4048', { metalness: 0.5 }), -1.3, 1.4, -2.17);
  })();

  /* --- paneelid --- */
  const UI = [], PANELS = [];
  class Panel {
    constructor(w, h, W, H, draw) { Object.assign(this, { W, H, draw, buttons: [], hover: -1, last: '' }); this.c = cnv(W, H); this.g = this.c.getContext('2d'); this.mesh = new THREE.Mesh(new THREE.PlaneGeometry(w, h), new THREE.MeshBasicMaterial({ map: ctex(this.c), transparent: true })); this.mesh.userData.panel = this; UI.push(this.mesh); PANELS.push(this); this.refresh(); }
    refresh() { this.g.clearRect(0, 0, this.W, this.H); this.buttons = []; this.draw(this.g, this); this.mesh.material.map.needsUpdate = true; }
    btn(x, y, w, h, label, fn, o = {}) { const i = this.buttons.length; this.buttons.push({ x, y, w, h, fn }); const g = this.g, hov = this.hover === i; rr(g, x, y, w, h, 18); g.fillStyle = o.on ? '#f2c230' : hov ? '#3a404a' : '#262a31'; g.fill(); g.lineWidth = 5; g.strokeStyle = o.col || '#f2c230'; g.stroke(); fit(g, label, x + w / 2, y + h / 2 + (o.sub ? -10 : 0), o.fs || 40, o.on ? '#111' : '#fff', w - 20); if (o.sub) fit(g, o.sub, x + w / 2, y + h / 2 + 24, 24, o.on ? '#222' : '#aab', w - 20, 'center', false); }
    indexAt(uv) { const x = uv.x * this.W, y = (1 - uv.y) * this.H; return this.buttons.findIndex(b => x >= b.x && x <= b.x + b.w && y >= b.y && y <= b.y + b.h); }
    click(uv) { const i = this.indexAt(uv); if (i >= 0) { sfx.click(); this.buttons[i].fn(); this.last = ''; this.refresh(); } }
  }
  const DIFF = { kid: { n: 2, time: 480, name: 'Väike 👶', sub: 'lastele · 8:00' }, expert: null, easy: { n: 3, time: 300, name: 'Lihtne', sub: '3 moodulit · 5:00' }, mid: { n: 4, time: 240, name: 'Keskmine', sub: '4 moodulit · 4:00' }, hard: { n: 5, time: 210, name: 'Raske', sub: '5 moodulit · 3:30' } };
  delete DIFF.expert; DIFF.expert = { n: 10, time: 360, name: 'Ekspert 💀', sub: '6:00 · 1 viga' };
  const TOPK = 'pomm_top';
  const getTop = d => { try { return (JSON.parse(localStorage.getItem(TOPK) || '{}')[d] || []); } catch (e) { return []; } };
  const addTop = (d, t, s) => { try { const all = JSON.parse(localStorage.getItem(TOPK) || '{}'); const L = all[d] || []; L.push({ t: Math.floor(t), s, d: new Date().toLocaleDateString('et') }); L.sort((a, b) => b.t - a.t || a.s - b.s); all[d] = L.slice(0, 5); localStorage.setItem(TOPK, JSON.stringify(all)); return all[d][0].t === Math.floor(t) && all[d][0].s === s; } catch (e) { return false; } };
  const G = { phase: 'lobby', diff: 'easy', time: 0, strikes: 0, maxS: 3, mods: [], B: null, endAt: 0 };
  const manualOn = () => performance.now() - lastHi < 5000;
  const menu = new Panel(0.8, 0.62, 1000, 780, (g, P) => {
    rr(g, 6, 6, P.W - 12, P.H - 12, 30); g.fillStyle = 'rgba(18,20,24,0.95)'; g.fill(); g.lineWidth = 10; g.strokeStyle = '#f2c230'; g.stroke();
    txt(g, '💣 POMMINIMETAJAD', P.W / 2, 64, 54, '#f2c230');
    txt(g, 'Ruumi kood', P.W / 2, 130, 34, '#aab'); txt(g, code, P.W / 2, 200, 110, '#fff', 'center', true, 'ui-monospace,monospace');
    const on = manualOn(); txt(g, on ? 'Juhendaja on ühendatud ✓' : (netStatus === 'nopeer' ? 'Võrk puudub – juhendaja: sama arvuti teine vaheleht' : 'Juhendaja: ava sama leht, vali JUHENDAJA ja sisesta kood'), P.W / 2, 280, on ? 36 : 26, on ? '#3fbf6a' : '#ddd');
    if (G.phase === 'lobby' && !on && !G.solo) {
      g.fillStyle = '#121418'; g.fillRect(20, 235, P.W - 40, 520);
      const dots = '.'.repeat(1 + Math.floor(G.clock * 2) % 3);
      txt(g, '⏳ Ootan juhendajat' + dots, P.W / 2, 300, 48, '#f2c230');
      const steps = ['1. Juhendaja avab sama lehe arvutis või telefonis', '2. Valib  📖 JUHENDAJA', `3. Sisestab koodi  ${code}`];
      steps.forEach((t, i) => fit(g, t, P.W / 2, 380 + i * 58, 36, '#fff', P.W - 80));
      if (netStatus === 'nopeer') fit(g, '(Võrk puudub – proovi sama arvuti teist vahelehte)', P.W / 2, 560, 24, '#e5483b', P.W - 80, 'center', false);
      for (let i = 0; i < 3; i++) { const a = G.clock * 3 + i * 2.1; g.fillStyle = '#f2c230'; g.globalAlpha = 0.3 + 0.7 * Math.abs(Math.sin(a)); g.beginPath(); g.arc(P.W / 2 - 50 + i * 50, 610, 14, 0, PI * 2); g.fill(); } g.globalAlpha = 1;
      P.btn(300, 660, 400, 80, 'Mängi üksi', () => { G.solo = true; }, { col: '#666', fs: 30 });
    } else if (G.phase === 'lobby') {
      Object.entries(DIFF).forEach(([k, d], i) => P.btn(30 + i * 190, 330, 180, 130, d.name, () => { G.diff = k; }, { on: G.diff === k, sub: d.sub, fs: 30, col: k === 'expert' ? '#e5483b' : undefined }));
      const tp = getTop(G.diff); if (tp.length) txt(g, `🏆 Parim (${DIFF[G.diff].name}): ${fmt(tp[0].t)} jäi aega`, P.W / 2, 482, 28, '#f2c230');
      P.btn(40, 510, 920, 160, 'ALUSTA', startGame, { fs: 80, col: '#e5483b' });
      txt(g, on ? 'Kõik on valmis – vali raskus ja alusta!' : 'Mängid üksi (juhendajat pole)', P.W / 2, 720, 28, on ? '#3fbf6a' : '#888');
    } else if (G.phase === 'play') {
      txt(g, `Moodulid: ${G.mods.filter(m => m.solved).length}/${G.mods.length}   Vead: ${G.strikes}/${G.maxS}`, P.W / 2, 380, 44, '#fff');
      txt(g, 'Räägi juhendajaga! Keera pommi, et näha külgi.', P.W / 2, 450, 30, '#aab');
      P.btn(300, 560, 400, 110, 'Loobu', () => explode(), { col: '#666', fs: 36 });
    } else {
      const win = G.phase === 'win'; txt(g, win ? '✅ POMM KAHJUTU!' : '💥 PAUH!', P.W / 2, 400, 90, win ? '#3fbf6a' : '#e5483b');
      txt(g, win ? `Aega jäi: ${fmt(G.time)} · vigu: ${G.strikes}` : 'Pomm plahvatas. Proovi uuesti!', P.W / 2, 470, 36, '#fff');
      if (win && G.record) txt(g, '🏆 UUS REKORD!', P.W / 2, 520, 40, '#f2c230');
      const tp = getTop(G.diff).slice(0, 3); if (tp.length) txt(g, '🏆 ' + tp.map((x, i) => `${i + 1}. ${fmt(x.t)}`).join('   '), P.W / 2, 730, 30, '#f2c230');
      P.btn(200, 560, 600, 130, 'UUS POMM', () => { G.phase = 'lobby'; clearBomb(); placeMenu(); sendState(); }, { fs: 60, col: '#3fbf6a' });
    }
  });
  scene.add(menu.mesh);
  function placeMenu() { if (G.phase === 'play') { menu.mesh.position.set(-0.78, 1.32, -0.6); menu.mesh.rotation.set(0, 0.6, 0); menu.mesh.scale.setScalar(0.8); } else { menu.mesh.position.set(0, 1.27, -1.0); menu.mesh.rotation.set(-0.12, 0, 0); menu.mesh.scale.setScalar(1); } if (!renderer.xr.isPresenting && typeof deskCam === 'function') deskCam(); }
  placeMenu();

  /* --- pomm --- */
  const BOMB_HOME = new THREE.Vector3(0, 0.99, -0.45);
  let bomb = null; let HITS = [];
  const plateMat = M('#3c4148', { metalness: 0.7, roughness: 0.35 }), caseMat = M('#2a2d31', { metalness: 0.7, roughness: 0.45 }), screwM = M('#a0a4aa', { metalness: 0.9, roughness: 0.3 });
  function hazardTex() { const c = cnv(512, 32), g = c.getContext('2d'); g.fillStyle = '#f2c230'; g.fillRect(0, 0, 512, 32); g.fillStyle = '#111'; for (let x = -32; x < 512; x += 32) { g.beginPath(); g.moveTo(x, 0); g.lineTo(x + 16, 0); g.lineTo(x + 48, 32); g.lineTo(x + 32, 32); g.fill(); } const t = ctex(c); t.wrapS = THREE.RepeatWrapping; return t; }
  const HAZ = hazardTex();
  function base() { const g = new THREE.Group(); mesh(new THREE.BoxGeometry(0.128, 0.128, 0.01), plateMat, 0, 0, -0.005, g); for (const [x, y] of [[-1, -1], [1, -1], [-1, 1], [1, 1]]) mesh(new THREE.CylinderGeometry(0.004, 0.004, 0.003, 8).rotateX(PI / 2), screwM, x * 0.057, y * 0.057, 0.001, g);
    const led = mesh(new THREE.SphereGeometry(0.0055, 12, 8), new THREE.MeshStandardMaterial({ color: '#222', emissive: '#000', roughness: 0.3 }), 0.052, 0.052, 0.003, g); return { g, led }; }
  const hit = (m, mod, part) => { m.userData.hit = { mod, part }; HITS.push(m); return m; };
  function setLed(m, c) { m.led.material.color.set(c); m.led.material.emissive.set(c); }

  // --- moodul: juhtmed
  function modWires(B) {
    const b = base(); const n = 3 + rint(4); let cols; do { cols = Array.from({ length: n }, () => pick(WCOL)); } while (n === 3 && new Set(cols).size === 1);
    const m = { id: 'juhtmed', ...b, cols, ans: wireAnswer(cols, B), solved: false, cut: [] };
    for (const s of [-1, 1]) mesh(new THREE.BoxGeometry(0.012, 0.1, 0.01), M('#d8d0b8', { roughness: 0.8 }), s * 0.047, -0.004, 0.004, b.g);
    const step = 0.085 / (n - 1);
    cols.forEach((c, i) => {
      const y = 0.038 - i * step; const sag = rnd(-0.006, 0.006);
      const curve = new THREE.QuadraticBezierCurve3(new THREE.Vector3(-0.045, y, 0.008), new THREE.Vector3(0, y + sag, 0.02), new THREE.Vector3(0.045, y, 0.008));
      const mat = M(WHEX[c], { roughness: 0.5, metalness: 0 });
      const w = mesh(new THREE.TubeGeometry(curve, 24, 0.0032, 8), mat, 0, 0, 0, b.g);
      const h = new THREE.Mesh(new THREE.TubeGeometry(curve, 12, 0.008, 6), new THREE.MeshBasicMaterial({ visible: false })); b.g.add(h); hit(h, m, i);
      for (const s of [-1, 1]) mesh(new THREE.CylinderGeometry(0.004, 0.004, 0.006, 8).rotateX(PI / 2), screwM, s * 0.045, y, 0.009, b.g);
      m.cut.push({ w, curve, mat, done: false });
    });
    m.down = i => { const W = m.cut[i]; if (W.done || m.solved) return; W.done = true; W.w.visible = false; sfx.snip();
      for (const [a, z] of [[0, 0.42], [0.58, 1]]) { const pts = []; for (let k = 0; k <= 8; k++) pts.push(W.curve.getPoint(a + (z - a) * k / 8)); const t = mesh(new THREE.TubeGeometry(new THREE.CatmullRomCurve3(pts), 10, 0.0032, 8), W.mat, 0, 0, 0, b.g); const end = a === 0 ? pts[pts.length - 1] : pts[0]; mesh(new THREE.SphereGeometry(0.0028, 8, 6), M('#d08a3a', { metalness: 0.9 }), end.x, end.y, end.z, b.g); }
      if (i === m.ans) solve(m); else strike(m); };
    return m;
  }
  // --- moodul: nupp
  function modButton(B) {
    const b = base(); const SB = RU(B.ed).b.strip; const col = pick(BCOL), lab = pick(BLAB);
    const m = { id: 'nupp', ...b, col, lab, act: buttonAction(col, lab, B), solved: false, held: false, t0: 0, strip: null };
    const ring = mesh(new THREE.CylinderGeometry(0.043, 0.043, 0.008, 32).rotateX(PI / 2), M('#1a1c20', { metalness: 0.5 }), -0.01, 0, 0.004, b.g);
    const cap = new THREE.Group(); cap.position.set(-0.01, 0, 0.008); b.g.add(cap);
    const capM = mesh(new THREE.CylinderGeometry(0.036, 0.038, 0.016, 32).rotateX(PI / 2), M(WHEX[col], { roughness: 0.35 }), 0, 0, 0.008, cap);
    const lc = cnv(256, 256), lg = lc.getContext('2d'); fit(lg, lab, 128, 128, 64, col === 'valge' || col === 'kollane' ? '#111' : '#fff', 220);
    const labM = new THREE.Mesh(new THREE.CircleGeometry(0.034, 32), new THREE.MeshBasicMaterial({ map: ctex(lc), transparent: true })); labM.position.z = 0.0165; cap.add(labM);
    hit(capM, m, 'btn'); hit(labM, m, 'btn');
    const stripM = new THREE.MeshStandardMaterial({ color: '#333', emissive: '#000', roughness: 0.3 });
    mesh(new THREE.BoxGeometry(0.014, 0.08, 0.004), M('#111'), 0.048, -0.01, 0.002, b.g); m.stripMesh = mesh(new THREE.BoxGeometry(0.009, 0.072, 0.004), stripM, 0.048, -0.01, 0.004, b.g);
    m.down = () => { if (m.solved) return; m.held = true; m.t0 = G.clock; cap.position.z = 0.002; sfx.click(); };
    m.up = () => { if (!m.held) return; m.held = false; cap.position.z = 0.008; const dur = G.clock - m.t0; const strip = m.strip; m.strip = null; stripM.color.set('#333'); stripM.emissive.set('#000');
      if (m.solved) return;
      if (m.act === 'tap') { if (dur < 0.5) solve(m); else strike(m); return; }
      if (dur < 0.5 || !strip) { strike(m); return; }
      if (Math.floor(G.time) % 10 === SB[strip]) solve(m); else strike(m); };
    m.update = () => { if (m.held && !m.strip && G.clock - m.t0 > 0.5) { m.strip = pick(Object.keys(SB)); const hx = { punane: '#ff2a1a', kollane: '#ffd020', sinine: '#2a6aff', roheline: '#20e050' }[m.strip]; stripM.color.set(hx); stripM.emissive.set(hx); } };
    return m;
  }
  // --- moodul: lülitid
  function modSwitches(B) {
    const b = base(); let lamps; do { lamps = Array.from({ length: 5 }, () => Math.random() < 0.5); } while (false);
    const target = switchTarget(lamps, RU(B.ed)); let pos; do { pos = Array.from({ length: 5 }, () => rint(2)); } while (pos.join() === target.join());
    const m = { id: 'lulitid', ...b, lamps, target, pos, solved: false, levers: [] };
    for (let i = 0; i < 5; i++) { const x = -0.044 + i * 0.022;
      mesh(new THREE.CylinderGeometry(0.0075, 0.0075, 0.004, 14).rotateX(PI / 2), M('#111'), x, 0.038, 0.002, b.g);
      mesh(new THREE.SphereGeometry(0.0062, 14, 10), lamps[i] ? new THREE.MeshStandardMaterial({ color: '#fff3a0', emissive: '#ffd030', emissiveIntensity: 2 }) : M('#3a3520', { roughness: 0.3 }), x, 0.038, 0.004, b.g);
      mesh(new THREE.BoxGeometry(0.014, 0.03, 0.006), M('#1a1c20'), x, 0.0, 0.003, b.g);
      const lv = new THREE.Group(); lv.position.set(x, 0, 0.006); b.g.add(lv); const stick = mesh(new THREE.CylinderGeometry(0.0022, 0.003, 0.022, 8).rotateX(PI / 2).translate(0, 0, 0.011), M('#c8ccd2', { metalness: 0.9, roughness: 0.25 }), 0, 0, 0, lv); mesh(new THREE.SphereGeometry(0.0035, 8, 6), M('#e0e4ea', { metalness: 0.9 }), 0, 0, 0.022, lv);
      const hb = new THREE.Mesh(new THREE.BoxGeometry(0.018, 0.034, 0.03), new THREE.MeshBasicMaterial({ visible: false })); hb.position.set(x, 0, 0.012); b.g.add(hb); hit(hb, m, i);
      m.levers.push(lv); }
    const lab = canvasPlane(0.11, 0.012, 330, 36, (g, W, H) => { txt(g, 'ÜLES', 30, H / 2, 22, '#ccc'); txt(g, 'ALLA', W - 30, H / 2, 22, '#ccc'); }, b.g, 0, 0.02, 0.001);
    const ok = mesh(new THREE.BoxGeometry(0.06, 0.018, 0.008), M('#2a6a3a'), 0, -0.042, 0.004, b.g); const okL = canvasPlane(0.058, 0.016, 200, 56, (g, W, H) => txt(g, 'VALMIS', W / 2, H / 2, 38, '#fff'), b.g, 0, -0.042, 0.0085); hit(ok, m, 'ok'); hit(okL, m, 'ok');
    const sync = () => m.levers.forEach((l, i) => l.rotation.x = m.pos[i] ? -0.55 : 0.55); sync();
    m.down = p => { if (m.solved) return; if (p === 'ok') { sfx.click(); if (m.pos.join() === m.target.join()) solve(m); else strike(m); return; } m.pos[p] ^= 1; sync(); sfx.sw(); };
    return m;
  }
  // --- moodul: koodilukk
  function modKeypad(B) {
    const b = base(); const word = pick(Object.keys(WORDS)); const m = { id: 'kood', ...b, word, code: keypadCode(word, B), entry: '', solved: false };
    mesh(new THREE.BoxGeometry(0.1, 0.032, 0.004), M('#0a0a0a'), 0, 0.038, 0.002, b.g);
    const scr = canvasPlane(0.094, 0.028, 400, 120, (g, W, H, e = '') => { g.fillStyle = '#062010'; g.fillRect(0, 0, W, H); fit(g, word, W / 2, 40, 54, '#40ff80', W - 20); txt(g, (e + '____').slice(0, 4).split('').join(' '), W / 2, 92, 40, '#a0ffc0', 'center', true, 'ui-monospace,monospace'); }, b.g, 0, 0.038, 0.0045);
    const keys = ['1', '2', '3', '4', '5', '6', '7', '8', '9', 'C', '0'];
    keys.forEach((k, i) => { const x = (i % 3 - 1) * 0.024, y = 0.009 - ((i / 3) | 0) * 0.019; if (k === 'C') { } const km = mesh(new THREE.BoxGeometry(0.019, 0.015, 0.007), M(k === 'C' ? '#8a2a20' : '#d8d8d0', { roughness: 0.5 }), x, y, 0.0035, b.g);
      const kl = canvasPlane(0.017, 0.013, 64, 52, (g, W, H) => txt(g, k, W / 2, H / 2, 40, k === 'C' ? '#fff' : '#111'), b.g, x, y, 0.0072); hit(km, m, k); hit(kl, m, k); km.userData.k = k; m['k' + k] = km; });
    m.down = k => { if (m.solved) return; sfx.key(); const km = m['k' + k]; km.position.z = 0.002; setTimeout(() => km.position.z = 0.0035, 120);
      if (k === 'C') { m.entry = ''; scr.redraw(''); return; } m.entry += k; scr.redraw(m.entry);
      if (m.entry.length === 4) { if (m.entry === m.code) solve(m); else { strike(m); setTimeout(() => { m.entry = ''; scr.redraw(''); }, 500); } } };
    return m;
  }
  // --- moodul: labürint
  function modMaze(B) {
    const b = base(); const mi = rint(6); const mz = RU(B.ed).mz[mi]; let p, g2; do { p = [rint(MN), rint(MN)]; g2 = [rint(MN), rint(MN)]; } while (Math.abs(p[0] - g2[0]) + Math.abs(p[1] - g2[1]) < 4);
    const m = { id: 'lab', ...b, mi, mz, p, goal: g2, solved: false };
    const scr = canvasPlane(0.074, 0.074, 300, 300, (g, W, H) => { g.fillStyle = '#0a0c10'; g.fillRect(0, 0, W, H); g.strokeStyle = MHEX[MCOL[mi]]; g.lineWidth = 18; g.strokeRect(9, 9, W - 18, H - 18); const pad = 34, cs = (W - pad * 2) / MN;
      for (let y = 0; y < MN; y++) for (let x = 0; x < MN; x++) { g.fillStyle = '#556'; g.beginPath(); g.arc(pad + cs * (x + 0.5), pad + cs * (y + 0.5), 5, 0, PI * 2); g.fill(); }
      const [gx, gy] = m.goal; g.strokeStyle = '#ff3030'; g.lineWidth = 7; const cx = pad + cs * (gx + 0.5), cy = pad + cs * (gy + 0.5); g.beginPath(); g.moveTo(cx - 12, cy - 12); g.lineTo(cx + 12, cy + 12); g.moveTo(cx + 12, cy - 12); g.lineTo(cx - 12, cy + 12); g.stroke();
      g.strokeStyle = '#30ff70'; g.lineWidth = 6; g.beginPath(); g.arc(pad + cs * (m.p[0] + 0.5), pad + cs * (m.p[1] + 0.5), 14, 0, PI * 2); g.stroke(); }, b.g, 0, 0.006, 0.003);
    const arrows = [['U', 0, 0.051, 0, -1, 0], ['D', 0, -0.041, 0, 1, PI], ['L', -0.049, 0.006, -1, 0, PI / 2], ['R', 0.049, 0.006, 1, 0, -PI / 2]];
    for (const [id, x, y, dx, dy, rot] of arrows) { const a = mesh(new THREE.ConeGeometry(0.009, 0.014, 3).rotateZ(rot), M('#d8d8d0'), x, y, 0.005, b.g); const hb = new THREE.Mesh(new THREE.BoxGeometry(0.022, 0.022, 0.015), new THREE.MeshBasicMaterial({ visible: false })); hb.position.set(x, y, 0.006); b.g.add(hb); hit(hb, m, [dx, dy]); hit(a, m, [dx, dy]); }
    m.down = ([dx, dy]) => { if (m.solved) return; sfx.click(); if (!canMove(mz, m.p[0], m.p[1], dx, dy)) { strike(m); return; } m.p = [m.p[0] + dx, m.p[1] + dy]; scr.redraw(); if (m.p[0] === m.goal[0] && m.p[1] === m.goal[1]) solve(m); };
    return m;
  }
  // --- taimer
  let timerScr, strikeScr;
  // --- moodul: värvimälu
  function modSimon(B) {
    const b = base(); const R = RU(B.ed), N = G.diff === 'expert' ? 4 : 3; const seq = Array.from({ length: N }, () => pick(PCOL));
    const m = { id: 'varv', ...b, seq, stage: 1, idx: 0, solved: false, t: 0, pause: 0, pads: {} };
    const pos = { punane: [0, 0.03], sinine: [0.03, 0], roheline: [0, -0.03], kollane: [-0.03, 0] };
    for (const c of PCOL) { const mat = new THREE.MeshStandardMaterial({ color: PHEX[c], emissive: '#000', roughness: 0.35 }); const pd = mesh(new THREE.BoxGeometry(0.03, 0.03, 0.01), mat, pos[c][0], pos[c][1] - 0.01, 0.005, b.g); pd.rotation.z = PI / 4; hit(pd, m, c); m.pads[c] = mat; }
    const lights = [...Array(N)].map((_, i) => mesh(new THREE.SphereGeometry(0.004, 8, 6), new THREE.MeshStandardMaterial({ color: '#222', emissive: '#000' }), -0.045 + i * 0.012, 0.052, 0.003, b.g));
    const lit = (c, on) => { m.pads[c].emissive.set(on ? PHEX[c] : '#000'); m.pads[c].emissiveIntensity = on ? 1.6 : 0; };
    const syncL = () => lights.forEach((l, i) => { const on = i < m.stage - 1 || m.solved; l.material.color.set(on ? '#20ff60' : '#222'); l.material.emissive.set(on ? '#20ff60' : '#000'); });
    m.update = dt => { if (m.solved) return; if (m.pause > 0) { m.pause -= dt; if (m.press > 0) { m.press -= dt; if (m.press <= 0) PCOL.forEach(c => lit(c, false)); } return; }
      m.t += dt; const per = 0.7, cyc = m.stage * per + 2.2; const tt = m.t % cyc; const k = Math.floor(tt / per); PCOL.forEach(c => lit(c, false));
      if (k < m.stage && tt % per < 0.45) { lit(m.seq[k], true); if (!m.beeped || m.beeped !== Math.floor(m.t / per)) { m.beeped = Math.floor(m.t / per); tone(440 + PCOL.indexOf(m.seq[k]) * 110, 440 + PCOL.indexOf(m.seq[k]) * 110, 0.2, 'sine', 0.06); } } };
    m.down = c => { if (m.solved) return; PCOL.forEach(x => lit(x, false)); lit(c, true); m.press = 0.25; m.pause = 3; m.t = 0; tone(440 + PCOL.indexOf(c) * 110, 440 + PCOL.indexOf(c) * 110, 0.15, 'square', 0.05);
      const need = R.p[batRow(B.batteries)][PCOL.indexOf(m.seq[m.idx])];
      if (c !== need) { m.idx = 0; strike(m); return; } m.idx++; if (m.idx >= m.stage) { m.idx = 0; m.stage++; m.pause = 1.2; syncL(); if (m.stage > N) { solve(m); syncL(); } } };
    syncL(); return m;
  }
  // --- moodul: raadio (morse)
  function modMorse(B) {
    const b = base(); const R = RU(B.ed); const word = pick(MW); const ans = R.f[MW.indexOf(word)]; const freqs = FREQS.slice().sort();
    const m = { id: 'raadio', ...b, word, ans, i: rint(freqs.length), solved: false, t: 0 };
    const u = 0.22, tl = []; for (const L of word) { for (const sym of MORSE[L]) { tl.push([1, sym === '.' ? u : 3 * u]); tl.push([0, u]); } tl[tl.length - 1][1] = 3 * u; } tl[tl.length - 1][1] = 7 * u; const total = tl.reduce((a, x) => a + x[1], 0);
    const lampM = new THREE.MeshStandardMaterial({ color: '#4a3a10', emissive: '#000', roughness: 0.3 }); mesh(new THREE.CylinderGeometry(0.011, 0.011, 0.004, 14).rotateX(PI / 2), M('#111'), -0.035, 0.038, 0.002, b.g); mesh(new THREE.SphereGeometry(0.009, 14, 10), lampM, -0.035, 0.038, 0.004, b.g);
    canvasPlane(0.05, 0.012, 200, 48, (g, W, H) => txt(g, 'RAADIO', W / 2, H / 2, 34, '#ccc'), b.g, 0.018, 0.038, 0.001);
    mesh(new THREE.BoxGeometry(0.084, 0.026, 0.004), M('#050505'), 0, 0.004, 0.002, b.g);
    const scr = canvasPlane(0.08, 0.022, 360, 100, (g, W, H) => { g.fillStyle = '#1a0e02'; g.fillRect(0, 0, W, H); txt(g, freqs[m.i] + ' MHz', W / 2, H / 2 + 4, 60, '#ffb040', 'center', true, 'ui-monospace,monospace'); }, b.g, 0, 0.004, 0.0045);
    for (const [d, x, rot] of [[-1, -0.03, PI / 2], [1, 0.03, -PI / 2]]) { const a = mesh(new THREE.ConeGeometry(0.008, 0.013, 3).rotateZ(rot), M('#d8d8d0'), x, -0.022, 0.005, b.g); const hb = new THREE.Mesh(new THREE.BoxGeometry(0.022, 0.02, 0.015), new THREE.MeshBasicMaterial({ visible: false })); hb.position.set(x, -0.022, 0.006); b.g.add(hb); hit(hb, m, d); hit(a, m, d); }
    const tx = mesh(new THREE.BoxGeometry(0.05, 0.016, 0.008), M('#8a2a20'), 0, -0.046, 0.004, b.g); const txl = canvasPlane(0.048, 0.014, 200, 56, (g, W, H) => txt(g, 'SAADA', W / 2, H / 2, 38, '#fff'), b.g, 0, -0.046, 0.0085); hit(tx, m, 'tx'); hit(txl, m, 'tx');
    m.update = dt => { if (m.solved) { lampM.emissive.set('#000'); return; } m.t = (m.t + dt) % total; let a = 0, on = 0; for (const [o, d] of tl) { if (m.t < a + d) { on = o; break; } a += d; } lampM.emissive.set(on ? '#ffd040' : '#000'); lampM.emissiveIntensity = on ? 3 : 0; };
    m.down = p => { if (m.solved) return; sfx.click(); if (p === 'tx') { if (freqs[m.i] === m.ans) solve(m); else strike(m); return; } m.i = clamp(m.i + p, 0, freqs.length - 1); scr.redraw(); };
    return m;
  }
  // --- moodul: sümbolid
  function modSymbols(B) {
    const b = base(); const R = RU(B.ed); let col, four;
    for (let t = 0; t < 500; t++) { col = rint(6); four = R.cols[col].slice().sort(() => Math.random() - 0.5).slice(0, 4); if (R.cols.filter((c, i) => i !== col && four.every(x => c.includes(x))).length === 0) break; }
    const order = R.cols[col].filter(x => four.includes(x)); const m = { id: 'sym', ...b, order, done: 0, solved: false, leds: {} };
    four.forEach((id, i) => { const x = (i % 2 ? 1 : -1) * 0.026, y = (i < 2 ? 1 : -1) * 0.025 - 0.005;
      const key = mesh(new THREE.BoxGeometry(0.044, 0.04, 0.007), M('#e8e2d0', { roughness: 0.6 }), x, y, 0.0035, b.g);
      const gl = canvasPlane(0.036, 0.036, 128, 128, (g, W, H) => drawGlyph(g, id, W / 2, H / 2 + 6, 90, '#1a1a1a'), b.g, x, y - 0.002, 0.0072); hit(key, m, id); hit(gl, m, id);
      m.leds[id] = mesh(new THREE.BoxGeometry(0.012, 0.003, 0.003), new THREE.MeshStandardMaterial({ color: '#222', emissive: '#000' }), x, y + 0.016, 0.0075, b.g); m['k' + id] = key; });
    m.down = id => { if (m.solved || m.leds[id].userData.ok) return; const k = m['k' + id]; k.position.z = 0.0015; setTimeout(() => k.position.z = 0.0035, 120); sfx.key();
      if (m.order[m.done] === id) { m.leds[id].userData.ok = 1; m.leds[id].material.color.set('#20ff60'); m.leds[id].material.emissive.set('#20ff60'); m.done++; if (m.done === 4) solve(m); } else strike(m); };
    return m;
  }
  // --- moodul: mälu
  function modMemory(B) {
    const b = base(); const R = RU(B.ed); const m = { id: 'mal', ...b, stage: 0, hist: [], solved: false };
    mesh(new THREE.BoxGeometry(0.06, 0.04, 0.004), M('#050505'), -0.01, 0.026, 0.002, b.g);
    const scr = canvasPlane(0.056, 0.036, 200, 128, (g, W, H) => { g.fillStyle = '#04140a'; g.fillRect(0, 0, W, H); txt(g, String(m.disp || ''), W / 2, H / 2 + 4, 110, '#40ff80', 'center', true, 'ui-monospace,monospace'); }, b.g, -0.01, 0.026, 0.0045);
    const st = [0, 1, 2, 3].map(i => mesh(new THREE.BoxGeometry(0.008, 0.006, 0.003), new THREE.MeshStandardMaterial({ color: '#222', emissive: '#000' }), 0.045, 0.04 - i * 0.011, 0.002, b.g));
    const keys = [0, 1, 2, 3].map(i => { const x = -0.039 + i * 0.026; const k = mesh(new THREE.BoxGeometry(0.022, 0.03, 0.007), M('#d8d8d0'), x, -0.03, 0.0035, b.g); const lab = canvasPlane(0.018, 0.024, 64, 84, (g, W, H, v = '') => txt(g, String(v), W / 2, H / 2 + 3, 64, '#111'), b.g, x, -0.03, 0.0072); hit(k, m, i); hit(lab, m, i); return { k, lab }; });
    const roll = () => { m.disp = 1 + rint(4); m.labels = [1, 2, 3, 4].sort(() => Math.random() - 0.5); scr.redraw(); keys.forEach((k, i) => k.lab.redraw(m.labels[i])); st.forEach((l, i) => { const on = i < m.stage; l.material.color.set(on ? '#20ff60' : '#222'); l.material.emissive.set(on ? '#20ff60' : '#000'); }); };
    const expect = () => { const r = R.m[m.stage][m.disp - 1]; if (r.t === 'pos') return r.v - 1; if (r.t === 'lab') return m.labels.indexOf(r.v); if (r.t === 'ppos') return m.hist[r.v - 1].pos; return m.labels.indexOf(m.hist[r.v - 1].lab); };
    m.down = i => { if (m.solved) return; const k = keys[i].k; k.position.z = 0.0015; setTimeout(() => k.position.z = 0.0035, 120); sfx.key();
      if (i !== expect()) { m.stage = 0; m.hist = []; strike(m); setTimeout(roll, 400); return; } m.hist.push({ pos: i, lab: m.labels[i] }); m.stage++; if (m.stage >= 4) { m.disp = ''; scr.redraw(); st.forEach(l => { l.material.color.set('#20ff60'); l.material.emissive.set('#20ff60'); }); solve(m); } else setTimeout(roll, 250); };
    roll(); return m;
  }
  // --- moodul: juhtmejada
  function modSeq(B) {
    const b = base(); const R = RU(B.ed); const panels = []; const seen = { punane: 0, sinine: 0, must: 0 }; let total = 0;
    while (total < 4) { panels.length = 0; total = 0; for (const k in seen) seen[k] = 0;
      for (let p = 0; p < 3; p++) { const n = 1 + rint(3); const froms = [0, 1, 2].sort(() => Math.random() - 0.5).slice(0, n).sort(); panels.push(froms.map(f => { const c = pick(QCOL); seen[c]++; const to = rint(3); return { f, to, c, cut: R.q[c][seen[c] - 1].includes(QLET[to]), done: false }; })); total += n; } }
    const m = { id: 'jada', ...b, panels, pi: 0, solved: false }; const grp = new THREE.Group(); b.g.add(grp);
    for (let i = 0; i < 3; i++) { canvasPlane(0.012, 0.012, 48, 48, (g, W, H) => txt(g, String(i + 1), W / 2, H / 2 + 2, 40, '#fff'), b.g, -0.05, 0.035 - i * 0.025, 0.002); canvasPlane(0.012, 0.012, 48, 48, (g, W, H) => txt(g, QLET[i], W / 2, H / 2 + 2, 40, '#fff'), b.g, 0.05, 0.035 - i * 0.025, 0.002); }
    const pnum = canvasPlane(0.04, 0.012, 160, 48, (g, W, H) => txt(g, `leht ${m.pi + 1}/3`, W / 2, H / 2 + 2, 34, '#ccc'), b.g, -0.025, -0.05, 0.002);
    const nx = mesh(new THREE.BoxGeometry(0.026, 0.016, 0.008), M('#2a4a8a'), 0.03, -0.05, 0.004, b.g); const nxl = canvasPlane(0.024, 0.014, 96, 56, (g, W, H) => txt(g, '▼', W / 2, H / 2 + 2, 44, '#fff'), b.g, 0.03, -0.05, 0.0085); hit(nx, m, 'next'); hit(nxl, m, 'next');
    const show = () => { while (grp.children.length) { const c = grp.children.pop(); c.geometry && c.geometry.dispose(); } HITS = HITS.filter(h => h.userData.hit?.mod !== m || typeof h.userData.hit.part !== 'number'); hit(nx, m, 'next'); hit(nxl, m, 'next');
      (m.panels[m.pi] || []).forEach((w, k) => { const a = new THREE.Vector3(-0.042, 0.035 - w.f * 0.025, 0.008), c = new THREE.Vector3(0.042, 0.035 - w.to * 0.025, 0.008); const mid = a.clone().add(c).multiplyScalar(0.5); mid.z = 0.016; const curve = new THREE.QuadraticBezierCurve3(a, mid, c); const mat = M(WHEX[w.c], { roughness: 0.5, metalness: 0 });
        if (w.done) { for (const [s0, s1] of [[0, 0.4], [0.6, 1]]) { const pts = []; for (let q = 0; q <= 6; q++) pts.push(curve.getPoint(s0 + (s1 - s0) * q / 6)); mesh(new THREE.TubeGeometry(new THREE.CatmullRomCurve3(pts), 8, 0.003, 6), mat, 0, 0, 0, grp); } }
        else { mesh(new THREE.TubeGeometry(curve, 20, 0.003, 8), mat, 0, 0, 0, grp); const h = new THREE.Mesh(new THREE.TubeGeometry(curve, 10, 0.008, 6), new THREE.MeshBasicMaterial({ visible: false })); grp.add(h); hit(h, m, k); } }); pnum.redraw(); };
    m.down = p => { if (m.solved) return; if (p === 'next') { sfx.click(); const left = m.panels[m.pi].filter(w => w.cut && !w.done); if (left.length) { left.forEach(w => w.cut = false); strike(m); } m.pi++; if (m.pi >= 3) { solve(m); m.pi = 2; } show(); return; }
      const w = m.panels[m.pi][p]; if (!w || w.done) return; w.done = true; sfx.snip(); if (!w.cut) strike(m); show(); };
    show(); return m;
  }
  function modTimer() { const b = base(); b.led.visible = false;
    mesh(new THREE.BoxGeometry(0.108, 0.05, 0.004), M('#050505'), 0, 0.014, 0.002, b.g);
    timerScr = canvasPlane(0.102, 0.044, 400, 172, (g, W, H, t = 0, mode = '') => { g.fillStyle = '#100404'; g.fillRect(0, 0, W, H); txt(g, '8:88', W / 2, H / 2 + 6, 140, '#2a0a08', 'center', true, 'ui-monospace,monospace'); txt(g, mode || fmt(t), W / 2, H / 2 + 6, mode ? 70 : 140, mode ? '#40ff70' : '#ff3020', 'center', true, 'ui-monospace,monospace'); }, b.g, 0, 0.014, 0.0045);
    strikeScr = canvasPlane(0.08, 0.026, 300, 96, (g, W, H, s = 0, max = 3) => { g.fillStyle = '#100404'; g.fillRect(0, 0, W, H); for (let i = 0; i < max; i++) txt(g, '✕', W / 2 + (i - (max - 1) / 2) * 80, H / 2, 70, i < s ? '#ff3020' : '#2a0a08'); }, b.g, 0, -0.035, 0.003);
    return { id: 'timer', ...b, solved: true }; }
  function modBlank() { const b = base(); b.led.visible = false; for (let i = 0; i < 5; i++) mesh(new THREE.BoxGeometry(0.08, 0.005, 0.003), M('#1a1c20'), 0, 0.03 - i * 0.015, 0.001, b.g); return { g: b.g, solved: true }; }

  function buildBomb() {
    clearBomb(); HITS = [];
    const L = 'ABCDEFGHKLMNPRSTUVZ', D = '0123456789';
    const X = G.diff === 'expert'; const B = { serial: pick(L) + pick(L) + pick(D) + '-' + pick(D) + pick(D) + pick(L), batteries: rint(5), indicator: pick(['MAA', 'VAL', 'TUL', 'KAS']), indLit: Math.random() < 0.5, ed: X ? 1 + rint(3) : 1 };
    G.B = B;
    bomb = new THREE.Group(); bomb.position.copy(BOMB_HOME); bomb.rotation.set(-0.55, 0, 0); scene.add(bomb);
    const W = 0.46, H = 0.32, Dp = 0.14;
    const body = mesh(new THREE.BoxGeometry(W, H, Dp), caseMat, 0, 0, 0, bomb); body.userData.bombBody = true;
    for (const [w, h, x, y] of [[W + 0.004, 0.014, 0, H / 2 - 0.007], [W + 0.004, 0.014, 0, -H / 2 + 0.007], [0.014, H, W / 2 - 0.007, 0], [0.014, H, -W / 2 + 0.007, 0]]) { const L2 = Math.max(w, h); const tx = HAZ.clone(); tx.needsUpdate = true; tx.repeat.set(L2 / 0.03, 1); const s = mesh(new THREE.BoxGeometry(L2, 0.014, 0.004), new THREE.MeshStandardMaterial({ map: tx, roughness: 0.6 }), x, y, Dp / 2 + 0.001, bomb); if (h > w) s.rotation.z = PI / 2; }
    for (const s of [-1, 1]) { const hd = mesh(new THREE.TorusGeometry(0.035, 0.007, 8, 16, PI), M('#1a1a1a', { metalness: 0.5 }), s * (W / 2 + 0.002), 0, 0, bomb); hd.rotation.set(0, s * PI / 2, PI / 2); }
    // küljed
    canvasPlane(0.11, 0.04, 330, 120, (g, Wd, Hd) => { g.fillStyle = '#f2c230'; rr(g, 4, 4, Wd - 8, Hd - 8, 14); g.fill(); txt(g, 'JUHEND', Wd / 2, 38, 32, '#111'); txt(g, 'v' + B.ed, Wd / 2, 84, 48, '#111'); }, bomb, -0.15, H / 2 + 0.001, 0, false).rotation.x = -PI / 2;
    canvasPlane(0.2, 0.05, 600, 150, (g, Wd, Hd) => { g.fillStyle = '#f4f4f0'; rr(g, 4, 4, Wd - 8, Hd - 8, 16); g.fill(); txt(g, 'SN', 60, Hd / 2, 44, '#666'); txt(g, B.serial, Wd / 2 + 40, Hd / 2 + 2, 76, '#111', 'center', true, 'ui-monospace,monospace'); }, bomb, 0.05, H / 2 + 0.001, 0, false).rotation.x = -PI / 2;
    const left = new THREE.Group(); left.position.set(-W / 2 - 0.001, 0, 0); left.rotation.y = -PI / 2; bomb.add(left);
    mesh(new THREE.BoxGeometry(0.11, 0.22, 0.008), M('#1a1a1a'), 0, 0, 0.004, left);
    for (let i = 0; i < B.batteries; i++) { const y = 0.075 - i * 0.05; const bt = mesh(new THREE.CylinderGeometry(0.012, 0.012, 0.07, 14).rotateZ(PI / 2), M(i % 2 ? '#c89020' : '#2a2a2a', { metalness: 0.6, roughness: 0.3 }), 0, y, 0.02, left); mesh(new THREE.CylinderGeometry(0.0123, 0.0123, 0.025, 14).rotateZ(PI / 2), M('#c8a050', { metalness: 0.8 }), 0.022, y, 0.02, left); mesh(new THREE.CylinderGeometry(0.004, 0.004, 0.006, 8).rotateZ(PI / 2), screwM, 0.038, y, 0.02, left); }
    if (!B.batteries) canvasPlane(0.09, 0.03, 300, 100, (g, Wd, Hd) => txt(g, 'tühi', Wd / 2, Hd / 2, 50, '#666'), left, 0, 0, 0.009);
    const right = new THREE.Group(); right.position.set(W / 2 + 0.001, 0, 0); right.rotation.y = PI / 2; bomb.add(right);
    canvasPlane(0.09, 0.04, 300, 133, (g, Wd, Hd) => { g.fillStyle = '#111'; rr(g, 4, 4, Wd - 8, Hd - 8, 12); g.fill(); txt(g, B.indicator, Wd / 2, Hd / 2, 86, '#f0f0f0', 'center', true, 'ui-monospace,monospace'); }, right, 0.02, 0, 0.002, false);
    mesh(new THREE.SphereGeometry(0.012, 14, 10), B.indLit ? new THREE.MeshStandardMaterial({ color: '#fff3a0', emissive: '#ffd030', emissiveIntensity: 2.5 }) : M('#333', { roughness: 0.2 }), -0.045, 0, 0.004, right);
    if (!X) canvasPlane(0.3, 0.12, 900, 360, (g, Wd, Hd) => { txt(g, 'MUDEL PX-7', Wd / 2, 90, 80, '#888'); txt(g, 'ÄRA AVA', Wd / 2, 200, 90, '#a03020'); txt(g, '⚠ ⚠ ⚠', Wd / 2, 300, 70, '#f2c230'); }, bomb, 0, 0, -Dp / 2 - 0.001, false).rotation.y = PI;
    else { const bk = canvasPlane(0.3, 0.08, 900, 240, (g, Wd, Hd) => { txt(g, 'MUDEL PX-7 · ÄRA AVA', Wd / 2, 120, 70, '#a03020'); }, bomb, 0, -H / 2 - 0.001, 0, false); bk.rotation.x = PI / 2;
      for (const [w, h, x, y] of [[W + 0.004, 0.014, 0, H / 2 - 0.007], [W + 0.004, 0.014, 0, -H / 2 + 0.007], [0.014, H, W / 2 - 0.007, 0], [0.014, H, -W / 2 + 0.007, 0]]) { const L2 = Math.max(w, h); const tx = HAZ.clone(); tx.needsUpdate = true; tx.repeat.set(L2 / 0.03, 1); const s = mesh(new THREE.BoxGeometry(L2, 0.014, 0.004), new THREE.MeshStandardMaterial({ map: tx, roughness: 0.6 }), x, y, -Dp / 2 - 0.001, bomb); if (h > w) s.rotation.z = PI / 2; } }
    // moodulid
    const kinds = X ? ['juhtmed', 'nupp', 'lulitid', 'kood', 'lab', 'varv', 'raadio', 'sym', 'mal', 'jada'].sort(() => Math.random() - 0.5) : ['juhtmed', 'nupp', 'lulitid', 'kood', 'lab'].sort(() => Math.random() - 0.5).slice(0, DIFF[G.diff].n);
    const slots = [[-0.145, 0.075], [0, 0.075], [0.145, 0.075], [-0.145, -0.075], [0, -0.075], [0.145, -0.075]];
    const mods = kinds.map(k => ({ juhtmed: () => modWires(B), nupp: () => modButton(B), lulitid: () => modSwitches(B), kood: () => modKeypad(B), lab: () => modMaze(B), varv: () => modSimon(B), raadio: () => modMorse(B), sym: () => modSymbols(B), mal: () => modMemory(B), jada: () => modSeq(B) })[k]());
    const order = [0, 2, 3, 4, 5].sort(() => Math.random() - 0.5).map(si => [si, 1]); if (X) order.push(...[0, 1, 2, 3, 4, 5].sort(() => Math.random() - 0.5).map(si => [si, -1]));
    const tm = modTimer(); tm.g.position.set(slots[1][0], slots[1][1], Dp / 2 + 0.001); bomb.add(tm.g);
    order.forEach(([si, side], i) => { const mm = mods[i] || modBlank(); mm.g.position.set(side * slots[si][0], slots[si][1], side * (Dp / 2 + 0.001)); if (side < 0) mm.g.rotation.y = PI; bomb.add(mm.g); });
    G.mods = mods; return B;
  }
  function clearBomb() { if (!bomb) return; scene.remove(bomb); bomb.traverse(o => { if (o.geometry) o.geometry.dispose(); }); bomb = null; HITS = []; }
  function startGame() { initAudio(); buildBomb(); G.phase = 'play'; G.time = DIFF[G.diff].time; G.strikes = 0; G.maxS = G.diff === 'kid' ? 5 : G.diff === 'expert' ? 1 : 3; G.dark = 0; G.darkNext = rnd(25, 40); G.record = false; G.rate = 1; timerScr.redraw(G.time); strikeScr.redraw(0, G.maxS); placeMenu(); sendState(); }
  function strike(m) { if (G.phase !== 'play') return; G.strikes++; G.strikeAt = Date.now(); G.rate = G.diff === 'kid' ? 1 : 1 + 0.25 * G.strikes; sfx.strike(); haptic('left', 1, 300); haptic('right', 1, 300); strikeScr.redraw(G.strikes, G.maxS); if (m && m.led) { setLed(m, '#ff2010'); setTimeout(() => !m.solved && setLed(m, '#222'), 900); } flashT = 0.35; flashCol = '#ff2010'; if (G.strikes >= G.maxS) explode(); sendState(); }
  function solve(m) { m.solved = true; G.focus = -1; setLed(m, '#20ff60'); sfx.solve(); haptic('right', 0.5, 80); if (G.mods.every(x => x.solved)) win(); sendState(); }
  function win() { G.record = addTop(G.diff, G.time, G.strikes); G.phase = 'win'; G.endAt = Date.now(); timerScr.redraw(G.time, 'KAHJUTU'); sfx.win(); alarm.intensity = 0; flashT = 0.6; flashCol = '#20ff60'; menu.last = ''; setTimeout(() => G.phase === 'win' && placeMenu(), 2500); sendState(); }
  function explode() { if (G.phase !== 'play') return; G.phase = 'boom'; G.endAt = Date.now(); sfx.boom(); haptic('left', 1, 1500); haptic('right', 1, 1500); boomT = 3; if (bomb) bomb.visible = false; sparks(); menu.last = ''; placeMenu(); sendState(); }
  function kidInfo(m) { const o = { id: m.id, solved: m.solved };
    if (m.id === 'juhtmed') Object.assign(o, { cols: m.cols, ans: m.ans });
    if (m.id === 'nupp') Object.assign(o, { col: m.col, lab: m.lab, act: m.act, held: m.held, strip: m.strip });
    if (m.id === 'lulitid') Object.assign(o, { lamps: m.lamps, target: m.target, pos: m.pos });
    if (m.id === 'kood') Object.assign(o, { word: m.word, code: m.code, entry: m.entry });
    if (m.id === 'lab') Object.assign(o, { mi: m.mi, p: m.p, goal: m.goal });
    return o; }
  function sendState() { if (!net) return; const msg = { type: 'st', phase: G.phase, time: G.time, strikes: G.strikes, maxS: G.maxS, solved: G.mods.filter(m => m.solved).length, total: G.mods.length, diff: G.diff, endAt: G.endAt, strikeAt: G.strikeAt || 0 };
    if (G.diff === 'kid' && G.phase === 'play') { msg.kid = G.mods.map(kidInfo); msg.focus = G.focus ?? -1; } net.send(msg); }

  /* --- efektid --- */
  let flashT = 0, flashCol = '#fff', boomT = 0;
  const flash = new THREE.Mesh(new THREE.SphereGeometry(0.2, 16, 12), new THREE.MeshBasicMaterial({ color: '#fff', side: THREE.BackSide, transparent: true, opacity: 0, depthTest: false, fog: false })); flash.renderOrder = 999; camera.add(flash);
  const SP = []; const spIM = new THREE.InstancedMesh(new THREE.BoxGeometry(0.02, 0.02, 0.02), new THREE.MeshBasicMaterial({ color: '#ffa030' }), 120); spIM.frustumCulled = false; scene.add(spIM); for (let i = 0; i < 120; i++) { SP.push({ p: new THREE.Vector3(), v: new THREE.Vector3(), l: 0 }); spIM.setMatrixAt(i, new THREE.Matrix4().makeScale(0, 0, 0)); }
  function sparks() { const c = bomb ? bomb.position : BOMB_HOME; for (const s of SP) { s.p.copy(c); s.v.set(rnd(-1, 1), rnd(0, 1.5), rnd(-1, 1)).normalize().multiplyScalar(rnd(2, 6)); s.l = rnd(0.6, 1.5); } }
  const _m = new THREE.Matrix4(), _q = new THREE.Quaternion(), _s = new THREE.Vector3();
  const torch = new THREE.SpotLight('#fff6e0', 0, 5, 0.32, 0.45, 1.2); scene.add(torch, torch.target); let torchCtrl = null;
  const baseI = { spot: spot.intensity, fill: fill.intensity }; const hemiL = scene.children.find(o => o.isHemisphereLight); baseI.hemi = hemiL.intensity;
  function updateDark(dt) {
    const X = G.diff === 'expert' && G.phase === 'play';
    if (X) { G.darkNext -= dt; if (G.darkNext <= 0 && !G.dark) { G.dark = rnd(6, 10); G.darkNext = rnd(25, 45); noise(0.3, 0.4, 200, 'lowpass'); tone(90, 40, 0.6, 'sawtooth', 0.12); } if (G.dark > 0) { G.dark -= dt; if (G.dark <= 0) { G.dark = 0; tone(200, 400, 0.2, 'sine', 0.08); } } } else G.dark = 0;
    const k = G.dark > 0 ? (Math.random() < 0.02 ? 0.25 : 0.02) : 1; spot.intensity = baseI.spot * k; fill.intensity = baseI.fill * k; hemiL.intensity = baseI.hemi * k;
    torch.intensity = X && G.dark > 0 ? 14 : 0;
    if (renderer.xr.isPresenting) { const c = ctrls.find(c => c.userData.hand === 'left' && c.userData.src) || ctrls.find(c => c.userData.src); if (c) { const o = new THREE.Vector3(), d = new THREE.Vector3(); ctrlRay(c, o, d); torch.position.copy(o); torch.target.position.copy(o).addScaledVector(d, 1); } }
    else { torch.position.copy(camera.getWorldPosition(new THREE.Vector3())); torch.target.position.copy(mouseTarget); }
    torch.target.updateMatrixWorld();
  }
  const mouseTarget = new THREE.Vector3(0, 1, -0.5);
  function updateFX(dt) { updateDark(dt);
    if (boomT > 0) { boomT -= dt; flash.material.color.set('#fff4d0'); flash.material.opacity = clamp(boomT / 2, 0, 1); camera.position.x = renderer.xr.isPresenting ? 0 : (Math.random() - 0.5) * 0.03 * boomT; }
    else if (flashT > 0) { flashT -= dt; flash.material.color.set(flashCol); flash.material.opacity = flashT * 0.8; } else flash.material.opacity = 0;
    SP.forEach((s, i) => { if (s.l <= 0) return; s.l -= dt; s.v.y -= 6 * dt; s.p.addScaledVector(s.v, dt); spIM.setMatrixAt(i, s.l > 0 ? _m.compose(s.p, _q, _s.setScalar(s.l)) : _m.makeScale(0, 0, 0)); }); spIM.instanceMatrix.needsUpdate = true;
    alarm.intensity = G.phase === 'play' && G.time < 30 ? (Math.sin(G.clock * 8) > 0 ? 6 : 0.5) : 0;
  }

  /* --- sisend --- */
  const ray = new THREE.Raycaster(); const ctrls = [];
  const ctrlRay = (c, o, d) => { _m.identity().extractRotation(c.matrixWorld); o.setFromMatrixPosition(c.matrixWorld); d.set(0, 0, -1).applyMatrix4(_m).normalize(); };
  function pickAt(o, d) { ray.set(o, d); ray.far = 3; const objs = [...UI, ...HITS]; if (bomb) objs.push(bomb.children[0]); const h = ray.intersectObjects(objs, false)[0]; return h || null; }
  function press(h, who) { if (!h) return null; if (h.object.userData.panel) { h.object.userData.panel.click(h.uv); return null; } const H = h.object.userData.hit; if (!H || G.phase !== 'play') return null; H.mod.down && H.mod.down(H.part); return H; }
  function release(H) { if (H && H.mod.up) H.mod.up(H.part); }
  // VR
  const cmf = new XRControllerModelFactory();
  for (let i = 0; i < 2; i++) {
    const c = renderer.xr.getController(i); c.userData = {}; const gr = renderer.xr.getControllerGrip(i); gr.add(cmf.createControllerModel(gr)); rig.add(c, gr); ctrls.push(c);
    c.addEventListener('connected', e => { c.userData.hand = e.data.handedness; c.userData.src = e.data; });
    c.addEventListener('selectstart', () => { initAudio(); const o = new THREE.Vector3(), d = new THREE.Vector3(); ctrlRay(c, o, d); c.userData.act = press(pickAt(o, d)); if (c.userData.act) haptic(c.userData.hand, 0.3, 30); });
    c.addEventListener('selectend', () => { release(c.userData.act); c.userData.act = null; });
    c.addEventListener('squeezestart', () => { if (!bomb) return; const cp = new THREE.Vector3().setFromMatrixPosition(c.matrixWorld); const o = new THREE.Vector3(), d = new THREE.Vector3(); ctrlRay(c, o, d); const h = pickAt(o, d); if (cp.distanceTo(bomb.position) < 0.4 || (h && !h.object.userData.panel)) { c.userData.grab = new THREE.Matrix4().copy(c.matrixWorld).invert().multiply(bomb.matrixWorld); haptic(c.userData.hand, 0.4, 50); } });
    c.addEventListener('squeezeend', () => { c.userData.grab = null; });
    const line = new THREE.Line(new THREE.BufferGeometry().setFromPoints([new THREE.Vector3(), new THREE.Vector3(0, 0, -1)]), new THREE.LineBasicMaterial({ color: '#f2c230', transparent: true, opacity: 0.7 })); c.add(line); c.userData.line = line;
    const dot = new THREE.Mesh(new THREE.SphereGeometry(0.004, 8, 6), new THREE.MeshBasicMaterial({ color: '#fff', depthTest: false })); dot.renderOrder = 50; scene.add(dot); c.userData.dot = dot;
  }
  // arvuti
  const mouse = new THREE.Vector2(); let mAct = null, rdrag = null; const cvs = renderer.domElement;
  cvs.addEventListener('contextmenu', e => e.preventDefault());
  const mouseRay = e => { mouse.set(e.clientX / innerWidth * 2 - 1, -(e.clientY / innerHeight) * 2 + 1); ray.setFromCamera(mouse, camera); return [ray.ray.origin.clone(), ray.ray.direction.clone()]; };
  cvs.addEventListener('mousedown', e => { initAudio(); if (e.button === 2) { rdrag = { x: e.clientX, y: e.clientY }; return; } if (e.button !== 0) return; const [o, d] = mouseRay(e); mAct = press(pickAt(o, d)); });
  addEventListener('mouseup', e => { if (e.button === 2) rdrag = null; if (e.button === 0) { release(mAct); mAct = null; } });
  addEventListener('mousemove', e => { { const [o0, d0] = mouseRay(e); mouseTarget.copy(o0).addScaledVector(d0, 1); } if (rdrag && bomb) { const dx = e.clientX - rdrag.x, dy = e.clientY - rdrag.y; rdrag = { x: e.clientX, y: e.clientY }; bomb.rotateOnWorldAxis(new THREE.Vector3(0, 1, 0), dx * 0.008); const right = new THREE.Vector3(1, 0, 0).applyQuaternion(camera.quaternion); bomb.rotateOnWorldAxis(right, dy * 0.008); } const [o, d] = mouseRay(e); hoverH = pickAt(o, d); });
  addEventListener('wheel', e => { if (renderer.xr.isPresenting) return; camera.fov = clamp(camera.fov + e.deltaY * 0.03, 22, 70); camera.updateProjectionMatrix(); });
  addEventListener('keydown', e => { if (e.code === 'Space' && bomb) { bomb.position.copy(BOMB_HOME); bomb.rotation.set(-0.55, 0, 0); } if (e.code === 'KeyF' && bomb) bomb.rotateY(PI); });
  let hoverH = null;
  function updatePointers() {
    for (const P of PANELS) P.hoverNext = -1;
    if (renderer.xr.isPresenting) for (const c of ctrls) { if (!c.userData.src) continue; const o = new THREE.Vector3(), d = new THREE.Vector3(); ctrlRay(c, o, d); const h = pickAt(o, d); c.userData.line.scale.z = h ? h.distance : 0.6; c.userData.dot.visible = !!h; if (h) { c.userData.dot.position.copy(h.point); if (h.object.userData.panel) h.object.userData.panel.hoverNext = h.object.userData.panel.indexAt(h.uv); }
      if (c.userData.grab && bomb) { _m.multiplyMatrices(c.matrixWorld, c.userData.grab); _m.decompose(bomb.position, bomb.quaternion, _s); } }
    else if (hoverH && hoverH.object.userData.panel) hoverH.object.userData.panel.hoverNext = hoverH.object.userData.panel.indexAt(hoverH.uv);
    { let fm = null; if (renderer.xr.isPresenting) { for (const c of ctrls) { if (!c.userData.src) continue; const o = new THREE.Vector3(), d = new THREE.Vector3(); ctrlRay(c, o, d); const h = pickAt(o, d); if (h && h.object.userData.hit) { fm = h.object.userData.hit.mod; break; } } } else if (hoverH && hoverH.object.userData.hit) fm = hoverH.object.userData.hit.mod; if (fm) G.focus = G.mods.indexOf(fm); }
    cvs.style.cursor = hoverH && (hoverH.object.userData.panel || hoverH.object.userData.hit) ? 'pointer' : 'default';
    for (const P of PANELS) if (P.hoverNext !== P.hover) { P.hover = P.hoverNext; P.refresh(); }
  }
  function deskCam() { camera.position.set(0, 1.4, 0.02); camera.fov = 50; camera.updateProjectionMatrix(); if (G.phase === 'play') camera.lookAt(0, 1.0, -0.5); else camera.lookAt(0, 1.24, -1.0); }
  deskCam();
  document.body.appendChild(VRButton.createButton(renderer, { optionalFeatures: ['local-floor', 'bounded-floor', 'hand-tracking'] }));
  renderer.xr.addEventListener('sessionstart', () => { initAudio(); camera.position.set(0, 0, 0); camera.rotation.set(0, 0, 0); $('bombHud').classList.add('hide'); });
  renderer.xr.addEventListener('sessionend', () => deskCam());

  /* --- tsükkel --- */
  const clock = new THREE.Clock(); G.clock = 0; let lastSec = -1, sendT = 0, menuT = 0;
  function step(dt) {
    G.clock += dt;
    if (G.phase === 'play') { G.time -= dt * G.rate; const s = Math.floor(G.time); if (s !== lastSec) { lastSec = s; timerScr.redraw(G.time); sfx.tick(G.time < 30); } for (const m of G.mods) m.update && m.update(dt); if (G.time <= 0) { G.time = 0; timerScr.redraw(0); explode(); } }
    updatePointers(); updateFX(dt);
    sendT += dt; if (sendT > (G.diff === 'kid' ? 0.15 : 0.3)) { sendT = 0; sendState(); }
    menuT += dt; if (menuT > 0.5) { menuT = 0; const on = manualOn(); if (on && !G.wasOn) { sfx.solve(); G.solo = false; } G.wasOn = on; const sig = [G.phase, on, netStatus, code, G.strikes, G.mods.filter(m => m.solved).length, G.diff, G.solo, G.phase === 'lobby' && !on ? Math.floor(G.clock * 2) : 0].join('|'); if (sig !== menu.last) { menu.last = sig; menu.refresh(); } $('hudNet').textContent = manualOn() ? 'Juhendaja on ühendatud ✓' : netStatus === 'nopeer' ? 'Võrguteek ei laadinud – testi sama arvuti teise vahelehega' : 'Ootan juhendajat…'; }
  }
  renderer.setAnimationLoop(() => { const dt = Math.min(clock.getDelta(), 0.05); step(dt); renderer.render(scene, camera); });
  connect();
  window.GAME = { G, get bomb() { return bomb; }, get code() { return code; }, startGame, step, press: (mod, part) => mod.down && mod.down(part), up: (mod, part) => mod.up && mod.up(part), sim: s => { for (let t = 0; t < s; t += 0.05) step(0.05); } };
}
</script>
</body>
</html>
