<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JAKARTA MOTOR GARAGE — Sistem Informasi Bengkel Motor</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@400;500;600;700&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --asphalt:#15171b;
    --panel:#1e2126;
    --panel-2:#262a31;
    --line:#33383f;
    --steel:#8a93a0;
    --steel-dim:#5b626d;
    --white:#f3f5f7;
    --orange:#ff6a13;
    --orange-dim:#7a3a13;
    --amber:#ffc845;
    --green:#3ddc84;
    --red:#ff5252;
    --plate-bg:#0c0d0f;
    --radius:10px;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:var(--asphalt);
    color:var(--white);
    font-family:'Inter',sans-serif;
    min-height:100vh;
    background-image:
      radial-gradient(circle at 15% 10%, rgba(255,106,19,0.05), transparent 40%),
      repeating-linear-gradient(135deg, rgba(255,255,255,0.012) 0px, rgba(255,255,255,0.012) 1px, transparent 1px, transparent 8px);
  }
  h1,h2,h3,h4{font-family:'Oswald',sans-serif; margin:0; letter-spacing:0.02em;}
  .mono{font-family:'JetBrains Mono',monospace;}
  ::selection{background:var(--orange); color:#151515;}
  ::-webkit-scrollbar{width:8px; height:8px;}
  ::-webkit-scrollbar-thumb{background:var(--line); border-radius:4px;}

  /* ---------- Utility ---------- */
  .hidden{display:none !important;}
  button{cursor:pointer; font-family:inherit;}
  input,select,textarea{font-family:inherit;}

  /* ---------- Plate badge (signature element) ---------- */
  .plate{
    display:inline-flex; align-items:center; gap:6px;
    background:var(--plate-bg); border:2px solid #3a3d42;
    border-radius:5px; padding:3px 10px;
    font-family:'JetBrains Mono',monospace; font-weight:700;
    font-size:13px; letter-spacing:1.5px; color:var(--white);
    position:relative; box-shadow: inset 0 0 0 1px rgba(255,255,255,0.04);
    white-space:nowrap;
  }
  .plate::before,.plate::after{
    content:''; position:absolute; width:4px; height:4px; border-radius:50%;
    background:#4a4e54; top:50%; transform:translateY(-50%);
  }
  .plate::before{left:2px;} .plate::after{right:2px;}

  /* ---------- LOGIN SCREEN ---------- */
  #login-screen{
    min-height:100vh; display:flex; align-items:center; justify-content:center;
    position:relative; overflow:hidden;
  }
  .hazard-strip{
    position:absolute; left:0; right:0; height:10px;
    background:repeating-linear-gradient(135deg, var(--orange) 0 18px, #15171b 18px 36px);
    opacity:0.85;
  }
  .hazard-strip.top{top:0;} .hazard-strip.bottom{bottom:0;}
  .login-card{
    background:var(--panel); border:1px solid var(--line); border-radius:14px;
    padding:44px 40px 36px; width:380px; max-width:90vw;
    box-shadow:0 30px 60px rgba(0,0,0,0.45);
    animation:riseIn .5s ease;
  }
  @keyframes riseIn{from{opacity:0; transform:translateY(16px);} to{opacity:1; transform:translateY(0);}}
  .brand{display:flex; align-items:center; gap:12px; margin-bottom:6px;}
  .brand-mark{
    width:44px; height:44px; border-radius:8px;
    background:linear-gradient(160deg, var(--orange), #d9540c);
    display:flex; align-items:center; justify-content:center;
    font-family:'Oswald',sans-serif; font-weight:700; font-size:15px; color:#151515;
    box-shadow:0 4px 14px rgba(255,106,19,0.35);
  }
  .brand h1{font-size:22px; color:var(--white); text-transform:uppercase;}
  .brand span{display:block; font-family:'JetBrains Mono',monospace; font-size:11px; color:var(--steel); letter-spacing:2px; margin-top:2px;}
  .login-sub{color:var(--steel); font-size:13.5px; margin:18px 0 26px; line-height:1.5;}
  .field{margin-bottom:16px;}
  .field label{display:block; font-size:12px; color:var(--steel); margin-bottom:6px; text-transform:uppercase; letter-spacing:0.06em;}
  .field input, .field select{
    width:100%; background:var(--panel-2); border:1px solid var(--line); color:var(--white);
    padding:11px 12px; border-radius:7px; font-size:14px; outline:none; transition:border-color .15s;
  }
  .field input:focus, .field select:focus{border-color:var(--orange);}
  .btn{
    border:none; border-radius:7px; padding:12px 18px; font-weight:600; font-size:14px;
    transition:transform .1s ease, box-shadow .15s ease; letter-spacing:0.02em;
  }
  .btn:active{transform:scale(0.97);}
  .btn-primary{background:var(--orange); color:#181818;}
  .btn-block{width:100%;}
  .btn-primary:hover{box-shadow:0 6px 18px rgba(255,106,19,0.35);}
  .btn-ghost{background:transparent; color:var(--steel); border:1px solid var(--line);}
  .btn-ghost:hover{border-color:var(--steel);}
  .btn-sm{padding:7px 12px; font-size:12.5px; border-radius:6px;}
  .btn-danger{background:rgba(255,82,82,0.12); color:var(--red); border:1px solid rgba(255,82,82,0.3);}
  .login-hint{margin-top:18px; font-size:11.5px; color:var(--steel-dim); text-align:center; line-height:1.6;}
  .login-err{color:var(--red); font-size:12.5px; margin:-6px 0 14px; display:none;}

  /* ---------- APP SHELL ---------- */
  #app{display:flex; min-height:100vh;}
  .sidebar{
    width:230px; background:var(--panel); border-right:1px solid var(--line);
    display:flex; flex-direction:column; padding:22px 0; flex-shrink:0;
  }
  .side-brand{display:flex; align-items:center; gap:10px; padding:0 20px 22px; border-bottom:1px solid var(--line); margin-bottom:14px;}
  .side-brand .brand-mark{width:36px; height:36px; font-size:12px;}
  .side-brand h1{font-size:16px; color:var(--white); text-transform:uppercase;}
  .side-brand span{font-size:9.5px; color:var(--steel); letter-spacing:1.5px;}
  nav.side-nav{display:flex; flex-direction:column; gap:2px; padding:0 12px;}
  .nav-item{
    display:flex; align-items:center; gap:11px; padding:11px 12px; border-radius:8px;
    color:var(--steel); font-size:13.5px; font-weight:500; text-decoration:none;
    border:none; background:transparent; text-align:left; width:100%;
  }
  .nav-item .ic{width:18px; text-align:center; font-size:15px;}
  .nav-item:hover{background:var(--panel-2); color:var(--white);}
  .nav-item.active{background:rgba(255,106,19,0.12); color:var(--orange);}
  .side-foot{margin-top:auto; padding:16px 20px 0 20px; border-top:1px solid var(--line);}
  .who{font-size:12.5px; color:var(--steel);}
  .who b{color:var(--white); display:block; font-size:13.5px;}

  .main{flex:1; padding:26px 34px 60px; min-width:0;}
  .topbar{display:flex; align-items:center; justify-content:space-between; margin-bottom:26px;}
  .topbar h2{font-size:24px; color:var(--white); text-transform:uppercase;}
  .topbar .sub{color:var(--steel); font-size:13px; margin-top:4px;}
  .eyebrow{font-family:'JetBrains Mono',monospace; color:var(--orange); font-size:11px; letter-spacing:2px; text-transform:uppercase; margin-bottom:4px; display:block;}

  .view{animation:fadeUp .35s ease;}
  @keyframes fadeUp{from{opacity:0; transform:translateY(8px);} to{opacity:1; transform:translateY(0);}}

  /* Cards */
  .grid-cards{display:grid; grid-template-columns:repeat(4,1fr); gap:16px; margin-bottom:26px;}
  @media(max-width:1000px){.grid-cards{grid-template-columns:repeat(2,1fr);}}
  .card{
    background:var(--panel); border:1px solid var(--line); border-radius:12px; padding:18px 20px;
    position:relative; overflow:hidden;
  }
  .card .cval{font-family:'Oswald',sans-serif; font-size:30px; font-weight:600; color:var(--white); margin-top:6px;}
  .card .clabel{font-size:12px; color:var(--steel); text-transform:uppercase; letter-spacing:0.05em;}
  .card .cnote{font-size:11.5px; margin-top:6px;}
  .card .cnote.up{color:var(--green);}
  .card .cnote.warn{color:var(--amber);}
  .card .cnote.bad{color:var(--red);}
  .card-bar{position:absolute; left:0; top:0; bottom:0; width:4px;}

  .panel{background:var(--panel); border:1px solid var(--line); border-radius:12px; padding:22px; margin-bottom:22px;}
  .panel-head{display:flex; align-items:center; justify-content:space-between; margin-bottom:16px;}
  .panel-head h3{font-size:16px; color:var(--white); text-transform:uppercase;}

  /* Kanban */
  .kanban{display:grid; grid-template-columns:repeat(3,1fr); gap:16px;}
  @media(max-width:900px){.kanban{grid-template-columns:1fr;}}
  .kcol{background:var(--panel-2); border:1px solid var(--line); border-radius:10px; padding:14px; min-height:120px;}
  .kcol h4{font-size:12.5px; text-transform:uppercase; letter-spacing:0.06em; color:var(--steel); margin-bottom:12px; display:flex; justify-content:space-between; align-items:center;}
  .kcol h4 .cnt{background:var(--panel); border-radius:20px; padding:2px 9px; font-size:11px; color:var(--white);}
  .scard{
    background:var(--panel); border:1px solid var(--line); border-left:3px solid var(--orange);
    border-radius:8px; padding:12px 13px; margin-bottom:10px; font-size:13px;
  }
  .scard .stop{display:flex; justify-content:space-between; align-items:flex-start; gap:8px; margin-bottom:6px;}
  .scard .keluhan{color:var(--steel); font-size:12px; line-height:1.4; margin-bottom:8px;}
  .scard .meta{font-size:11px; color:var(--steel-dim); display:flex; justify-content:space-between; align-items:center;}
  .scard .actions{margin-top:9px; display:flex; gap:6px;}

  /* Table */
  table{width:100%; border-collapse:collapse; font-size:13px;}
  thead th{
    text-align:left; font-size:11px; text-transform:uppercase; letter-spacing:0.05em; color:var(--steel);
    padding:9px 12px; border-bottom:1px solid var(--line);
  }
  tbody td{padding:11px 12px; border-bottom:1px solid var(--line); color:var(--white); vertical-align:middle;}
  tbody tr:hover{background:rgba(255,255,255,0.02);}
  tbody tr:last-child td{border-bottom:none;}
  .row-actions{display:flex; gap:6px;}
  .badge{display:inline-block; padding:3px 10px; border-radius:20px; font-size:11px; font-weight:600; letter-spacing:0.02em;}
  .badge.ok{background:rgba(61,220,132,0.14); color:var(--green);}
  .badge.warn{background:rgba(255,200,69,0.14); color:var(--amber);}
  .badge.bad{background:rgba(255,82,82,0.14); color:var(--red);}
  .badge.info{background:rgba(255,106,19,0.14); color:var(--orange);}
  .stockbar{width:70px; height:6px; background:var(--line); border-radius:3px; overflow:hidden; display:inline-block; vertical-align:middle; margin-right:8px;}
  .stockbar i{display:block; height:100%; background:var(--green);}

  .empty{text-align:center; padding:34px 10px; color:var(--steel-dim); font-size:13px;}

  /* Toolbar */
  .toolbar{display:flex; gap:10px; margin-bottom:18px; flex-wrap:wrap; align-items:center;}
  .toolbar input[type=text], .toolbar select{
    background:var(--panel-2); border:1px solid var(--line); color:var(--white);
    padding:9px 12px; border-radius:7px; font-size:13px; outline:none;
  }
  .toolbar input:focus, .toolbar select:focus{border-color:var(--orange);}
  .spacer{flex:1;}

  /* Modal */
  .modal-back{
    position:fixed; inset:0; background:rgba(10,11,13,0.68); backdrop-filter:blur(2px);
    display:flex; align-items:center; justify-content:center; z-index:60; padding:20px;
    animation:fadeIn .18s ease;
  }
  @keyframes fadeIn{from{opacity:0;} to{opacity:1;}}
  .modal{
    background:var(--panel); border:1px solid var(--line); border-radius:14px; width:480px; max-width:100%;
    max-height:88vh; overflow-y:auto; padding:26px 26px 22px; animation:riseIn .22s ease;
  }
  .modal h3{font-size:18px; color:var(--white); text-transform:uppercase; margin-bottom:18px;}
  .form-row{display:grid; grid-template-columns:1fr 1fr; gap:12px;}
  .modal .field input, .modal .field select, .modal .field textarea{width:100%;}
  .modal .field textarea{resize:vertical; min-height:60px;}
  .modal-actions{display:flex; justify-content:flex-end; gap:10px; margin-top:20px;}

  /* Toast */
  #toast{
    position:fixed; bottom:24px; right:24px; background:var(--panel); border:1px solid var(--line);
    border-left:4px solid var(--green); border-radius:10px; padding:14px 18px; color:var(--white);
    font-size:13.5px; box-shadow:0 12px 30px rgba(0,0,0,0.4); z-index:100;
    transform:translateY(20px); opacity:0; transition:all .25s ease; max-width:320px;
  }
  #toast.show{transform:translateY(0); opacity:1;}

  /* Nota (print) */
  .nota{background:#fff; color:#111; border-radius:10px; padding:24px; font-family:'JetBrains Mono',monospace; font-size:12.5px;}
  .nota h3{color:#111; font-family:'Oswald',sans-serif;}
  .nota .line{border-top:1px dashed #999; margin:10px 0;}
  .nota table{font-size:12px;} .nota td{border-color:#ddd; color:#111;}
  .nota .tot{font-size:15px; font-weight:700;}

  /* Report bars */
  .bars{display:flex; align-items:flex-end; gap:10px; height:160px; margin-top:10px;}
  .bar-col{flex:1; display:flex; flex-direction:column; align-items:center; justify-content:flex-end; height:100%;}
  .bar{width:100%; max-width:34px; background:linear-gradient(180deg,var(--orange),#c94e0c); border-radius:5px 5px 0 0; transition:height .5s ease;}
  .bar-lab{font-size:10.5px; color:var(--steel); margin-top:6px;}
  .bar-val{font-size:10.5px; color:var(--white); margin-bottom:4px; font-family:'JetBrains Mono',monospace;}

  @media(max-width:820px){
    .sidebar{position:fixed; z-index:50; height:100vh; transform:translateX(-100%); transition:transform .25s;}
    .sidebar.open{transform:translateX(0);}
    .main{padding:20px;}
    .grid-cards{grid-template-columns:1fr 1fr;}
    #menuToggle{display:inline-flex !important;}
  }
  #menuToggle{display:none; background:var(--panel-2); border:1px solid var(--line); color:var(--white); border-radius:8px; padding:8px 11px; margin-right:10px;}
</style>
</head>
<body>

<!-- ================= LOGIN ================= -->
<div id="login-screen">
  <div class="hazard-strip top"></div>
  <div class="hazard-strip bottom"></div>
  <div class="login-card">
    <div class="brand">
      <div class="brand-mark">JMG</div>
      <div>
        <h1>Jakarta Motor Garage</h1>
        <span>SISTEM INFORMASI BENGKEL MOTOR</span>
      </div>
    </div>
    <p class="login-sub">Masuk untuk mengelola servis, sparepart, dan transaksi bengkel.</p>
    <div class="login-err" id="loginErr">Username atau password salah.</div>
    <div class="field">
      <label>Username</label>
      <input type="text" id="loginUser" placeholder="admin" value="admin">
    </div>
    <div class="field">
      <label>Password</label>
      <input type="password" id="loginPass" placeholder="••••••••" value="garage123">
    </div>
    <button class="btn btn-primary btn-block" onclick="doLogin()">Masuk ke Sistem</button>
    <div class="login-hint">Demo akun — Username: <b class="mono">admin</b> · Password: <b class="mono">garage123</b></div>
  </div>
</div>

<!-- ================= APP ================= -->
<div id="app" class="hidden">
  <aside class="sidebar" id="sidebar">
    <div class="side-brand">
      <div class="brand-mark">JMG</div>
      <div>
        <h1>Jakarta Motor Garage</h1>
        <span>BENGKEL MOTOR</span>
      </div>
    </div>
    <nav class="side-nav" id="sideNav">
      <button class="nav-item" data-view="dashboard"><span class="ic">◆</span> Dashboard</button>
      <button class="nav-item" data-view="pelanggan"><span class="ic">◆</span> Pelanggan &amp; Kendaraan</button>
      <button class="nav-item" data-view="servis"><span class="ic">◆</span> Antrian Servis</button>
      <button class="nav-item" data-view="sparepart"><span class="ic">◆</span> Sparepart &amp; Stok</button>
      <button class="nav-item" data-view="transaksi"><span class="ic">◆</span> Transaksi</button>
      <button class="nav-item" data-view="laporan"><span class="ic">◆</span> Laporan</button>
    </nav>
    <div class="side-foot">
      <div class="who"><b>Admin Bengkel</b>Jakarta Motor Garage · Shift Pagi</div>
      <button class="btn btn-ghost btn-sm" style="margin-top:12px; width:100%;" onclick="doLogout()">Keluar</button>
    </div>
  </aside>

  <main class="main">
    <div class="topbar">
      <div style="display:flex; align-items:center;">
        <button id="menuToggle" onclick="document.getElementById('sidebar').classList.toggle('open')">☰</button>
        <div>
          <span class="eyebrow" id="viewEyebrow">JAKARTA MOTOR GARAGE / OPERASIONAL</span>
          <h2 id="viewTitle">Dashboard</h2>
          <div class="sub" id="viewSub">Ringkasan aktivitas bengkel hari ini</div>
        </div>
      </div>
      <div id="topAction"></div>
    </div>

    <div id="viewRoot"></div>
  </main>
</div>

<div id="toast"></div>

<script>
/* ================= DATA (in-memory, reset on refresh) ================= */
let seq = 1000;
const nextId = () => seq++;

let mekanik = [
  {id:'M1', nama:'Rudi Hartono', spesialisasi:'Mesin & Injeksi'},
  {id:'M2', nama:'Agus Salim', spesialisasi:'Kelistrikan'},
  {id:'M3', nama:'Dedi Kurniawan', spesialisasi:'Kaki-kaki & Rem'},
];

let pelanggan = [
  {id:nextId(), nama:'Bayu Saputra', hp:'0812-3456-7890', alamat:'Jl. Cihideung No.12'},
  {id:nextId(), nama:'Siti Nurhaliza', hp:'0813-2211-9087', alamat:'Jl. Tamansari No.5'},
  {id:nextId(), nama:'Reza Firmansyah', hp:'0857-4433-1120', alamat:'Jl. Sutisna Senjaya No.31'},
];

let kendaraan = [
  {id:nextId(), pelangganId:pelanggan[0].id, plat:'Z 4821 KZ', merk:'Honda', tipe:'Vario 125'},
  {id:nextId(), pelangganId:pelanggan[1].id, plat:'Z 1190 QF', merk:'Yamaha', tipe:'NMAX'},
  {id:nextId(), pelangganId:pelanggan[2].id, plat:'Z 7723 BD', merk:'Honda', tipe:'Beat Street'},
];

let sparepart = [
  {id:nextId(), nama:'Oli Mesin 1L (Semi Sintetik)', stok:24, minStok:8, harga:55000},
  {id:nextId(), nama:'Kampas Rem Depan', stok:6, minStok:5, harga:65000},
  {id:nextId(), nama:'Busi Iridium', stok:3, minStok:6, harga:48000},
  {id:nextId(), nama:'Filter Udara', stok:14, minStok:5, harga:38000},
  {id:nextId(), nama:'Aki Kering GS', stok:2, minStok:3, harga:295000},
  {id:nextId(), nama:'Rantai + Gear Set', stok:9, minStok:4, harga:210000},
];

const BIAYA_JASA_DEFAULT = 45000;

let servis = [
  {id:nextId(), kendaraanId:kendaraan[0].id, mekanikId:'M1', keluhan:'Servis rutin + ganti oli', status:'selesai',
   items:[{sparepartId:sparepart[0].id, qty:1}], jasa:45000, tanggal:'2026-07-11', dibayar:true},
  {id:nextId(), kendaraanId:kendaraan[1].id, mekanikId:'M3', keluhan:'Kampas rem depan habis, bunyi decit', status:'dikerjakan',
   items:[{sparepartId:sparepart[1].id, qty:1}], jasa:50000, tanggal:'2026-07-13', dibayar:false},
  {id:nextId(), kendaraanId:kendaraan[2].id, mekanikId:'M2', keluhan:'Motor susah starter pagi hari', status:'menunggu',
   items:[], jasa:0, tanggal:'2026-07-13', dibayar:false},
];

/* ================= HELPERS ================= */
const rupiah = n => 'Rp ' + n.toLocaleString('id-ID');
const findPelanggan = id => pelanggan.find(p=>p.id===id);
const findKendaraan = id => kendaraan.find(k=>k.id===id);
const findSparepart = id => sparepart.find(s=>s.id===id);
const findMekanik = id => mekanik.find(m=>m.id===id);

function toast(msg, kind){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.style.borderLeftColor = kind==='err' ? 'var(--red)' : (kind==='warn' ? 'var(--amber)' : 'var(--green)');
  t.classList.add('show');
  clearTimeout(window._toastTimer);
  window._toastTimer = setTimeout(()=>t.classList.remove('show'), 2600);
}

function servisTotal(s){
  const partsTotal = s.items.reduce((sum,it)=>{
    const sp = findSparepart(it.sparepartId);
    return sum + (sp ? sp.harga*it.qty : 0);
  },0);
  return partsTotal + (s.jasa||0);
}

/* ================= AUTH ================= */
function doLogin(){
  const u = document.getElementById('loginUser').value.trim();
  const p = document.getElementById('loginPass').value.trim();
  if(u==='admin' && p==='garage123'){
    document.getElementById('login-screen').classList.add('hidden');
    document.getElementById('app').classList.remove('hidden');
    navigate('dashboard');
  } else {
    document.getElementById('loginErr').style.display='block';
  }
}
function doLogout(){
  document.getElementById('app').classList.add('hidden');
  document.getElementById('login-screen').classList.remove('hidden');
  document.getElementById('loginErr').style.display='none';
}

/* ================= NAVIGATION ================= */
const VIEW_META = {
  dashboard:{title:'Dashboard', sub:'Ringkasan aktivitas bengkel hari ini', eyebrow:'JAKARTA MOTOR GARAGE / OPERASIONAL'},
  pelanggan:{title:'Pelanggan & Kendaraan', sub:'Data pelanggan dan riwayat kendaraan', eyebrow:'JAKARTA MOTOR GARAGE / DATA MASTER'},
  servis:{title:'Antrian Servis', sub:'Kelola alur servis dari masuk hingga selesai', eyebrow:'JAKARTA MOTOR GARAGE / BENGKEL'},
  sparepart:{title:'Sparepart & Stok', sub:'Pantau ketersediaan sparepart', eyebrow:'JAKARTA MOTOR GARAGE / GUDANG'},
  transaksi:{title:'Transaksi', sub:'Pembayaran dan cetak nota servis', eyebrow:'JAKARTA MOTOR GARAGE / KASIR'},
  laporan:{title:'Laporan', sub:'Ringkasan pendapatan bengkel', eyebrow:'JAKARTA MOTOR GARAGE / ANALITIK'},
};
let currentView = 'dashboard';

function navigate(view){
  currentView = view;
  document.querySelectorAll('.nav-item').forEach(b=>b.classList.toggle('active', b.dataset.view===view));
  const meta = VIEW_META[view];
  document.getElementById('viewTitle').textContent = meta.title;
  document.getElementById('viewSub').textContent = meta.sub;
  document.getElementById('viewEyebrow').textContent = meta.eyebrow;
  document.getElementById('sidebar').classList.remove('open');
  render();
}
document.getElementById('sideNav').addEventListener('click', e=>{
  const btn = e.target.closest('.nav-item');
  if(btn) navigate(btn.dataset.view);
});

/* ================= RENDER ROUTER ================= */
function render(){
  const root = document.getElementById('viewRoot');
  const topAction = document.getElementById('topAction');
  topAction.innerHTML = '';
  root.innerHTML = '';
  root.className = 'view';

  if(currentView==='dashboard') renderDashboard(root, topAction);
  if(currentView==='pelanggan') renderPelanggan(root, topAction);
  if(currentView==='servis') renderServis(root, topAction);
  if(currentView==='sparepart') renderSparepart(root, topAction);
  if(currentView==='transaksi') renderTransaksi(root, topAction);
  if(currentView==='laporan') renderLaporan(root, topAction);
}

/* ================= DASHBOARD ================= */
function renderDashboard(root, topAction){
  const today = '2026-07-13';
  const servisHariIni = servis.filter(s=>s.tanggal===today);
  const pendapatanHariIni = servis.filter(s=>s.tanggal===today && s.dibayar).reduce((a,s)=>a+servisTotal(s),0);
  const antrianAktif = servis.filter(s=>s.status!=='selesai').length;
  const stokMenipis = sparepart.filter(s=>s.stok<=s.minStok).length;

  root.innerHTML = `
    <div class="grid-cards">
      <div class="card"><div class="card-bar" style="background:var(--orange)"></div>
        <div class="clabel">Servis Hari Ini</div><div class="cval">${servisHariIni.length}</div>
        <div class="cnote up">${antrianAktif} sedang berjalan</div></div>
      <div class="card"><div class="card-bar" style="background:var(--green)"></div>
        <div class="clabel">Pendapatan Hari Ini</div><div class="cval" style="font-size:24px;">${rupiah(pendapatanHariIni)}</div>
        <div class="cnote up">Dari servis yang lunas</div></div>
      <div class="card"><div class="card-bar" style="background:var(--amber)"></div>
        <div class="clabel">Antrian Aktif</div><div class="cval">${antrianAktif}</div>
        <div class="cnote warn">Menunggu &amp; dikerjakan</div></div>
      <div class="card"><div class="card-bar" style="background:var(--red)"></div>
        <div class="clabel">Stok Menipis</div><div class="cval">${stokMenipis}</div>
        <div class="cnote ${stokMenipis>0?'bad':'up'}">${stokMenipis>0?'Perlu pemesanan ulang':'Stok aman'}</div></div>
    </div>

    <div class="panel">
      <div class="panel-head"><h3>Antrian Servis Terkini</h3>
        <button class="btn btn-primary btn-sm" onclick="navigate('servis')">Kelola Antrian →</button></div>
      <table>
        <thead><tr><th>Kendaraan</th><th>Pelanggan</th><th>Keluhan</th><th>Mekanik</th><th>Status</th></tr></thead>
        <tbody>
          ${servis.slice().reverse().slice(0,5).map(s=>{
            const k = findKendaraan(s.kendaraanId); const p = findPelanggan(k.pelangganId); const m = findMekanik(s.mekanikId);
            return `<tr>
              <td><span class="plate">${k.plat}</span></td>
              <td>${p.nama}</td>
              <td>${s.keluhan}</td>
              <td>${m.nama}</td>
              <td>${statusBadge(s.status)}</td>
            </tr>`;
          }).join('')}
        </tbody>
      </table>
    </div>
  `;
}

function statusBadge(status){
  if(status==='menunggu') return '<span class="badge warn">Menunggu</span>';
  if(status==='dikerjakan') return '<span class="badge info">Dikerjakan</span>';
  return '<span class="badge ok">Selesai</span>';
}

/* ================= PELANGGAN & KENDARAAN ================= */
let pelangganSearch = '';
function renderPelanggan(root, topAction){
  topAction.innerHTML = `<button class="btn btn-primary btn-sm" onclick="openPelangganModal()">+ Tambah Pelanggan</button>`;

  const filtered = pelanggan.filter(p=>{
    const q = pelangganSearch.toLowerCase();
    return p.nama.toLowerCase().includes(q) || p.hp.includes(q);
  });

  root.innerHTML = `
    <div class="panel">
      <div class="toolbar">
        <input type="text" placeholder="Cari nama atau nomor HP..." id="searchPelanggan" value="${pelangganSearch}">
        <div class="spacer"></div>
        <span class="sub" style="color:var(--steel); font-size:12.5px;">${filtered.length} pelanggan</span>
      </div>
      <table>
        <thead><tr><th>Nama</th><th>No. HP</th><th>Alamat</th><th>Kendaraan</th><th></th></tr></thead>
        <tbody id="pelangganBody"></tbody>
      </table>
      ${filtered.length===0 ? '<div class="empty">Belum ada data pelanggan yang cocok.</div>' : ''}
    </div>
  `;
  const body = document.getElementById('pelangganBody');
  body.innerHTML = filtered.map(p=>{
    const kend = kendaraan.filter(k=>k.pelangganId===p.id);
    return `<tr>
      <td><b>${p.nama}</b></td>
      <td class="mono">${p.hp}</td>
      <td>${p.alamat}</td>
      <td>${kend.map(k=>`<span class="plate" style="margin-right:4px;">${k.plat}</span>`).join(' ') || '<span style="color:var(--steel-dim)">—</span>'}</td>
      <td class="row-actions">
        <button class="btn btn-ghost btn-sm" onclick="openKendaraanModal('${p.id}')">+ Kendaraan</button>
        <button class="btn btn-danger btn-sm" onclick="hapusPelanggan('${p.id}')">Hapus</button>
      </td>
    </tr>`;
  }).join('');

  document.getElementById('searchPelanggan').addEventListener('input', e=>{
    pelangganSearch = e.target.value; renderPelanggan(root, topAction);
    document.getElementById('searchPelanggan').focus();
    document.getElementById('searchPelanggan').setSelectionRange(pelangganSearch.length, pelangganSearch.length);
  });
}

function hapusPelanggan(id){
  if(!confirm('Hapus pelanggan ini beserta data kendaraannya?')) return;
  pelanggan = pelanggan.filter(p=>p.id!==id);
  kendaraan = kendaraan.filter(k=>k.pelangganId!==id);
  toast('Data pelanggan dihapus.');
  render();
}

function openPelangganModal(){
  showModal(`
    <h3>Tambah Pelanggan Baru</h3>
    <div class="field"><label>Nama Lengkap</label><input type="text" id="fNama" placeholder="Contoh: Ahmad Fauzi"></div>
    <div class="field"><label>No. HP</label><input type="text" id="fHp" placeholder="0812xxxxxxx"></div>
    <div class="field"><label>Alamat</label><textarea id="fAlamat" placeholder="Alamat lengkap"></textarea></div>
    <div class="modal-actions">
      <button class="btn btn-ghost" onclick="closeModal()">Batal</button>
      <button class="btn btn-primary" onclick="simpanPelanggan()">Simpan Pelanggan</button>
    </div>
  `);
}
function simpanPelanggan(){
  const nama = document.getElementById('fNama').value.trim();
  const hp = document.getElementById('fHp').value.trim();
  const alamat = document.getElementById('fAlamat').value.trim();
  if(!nama || !hp){ toast('Nama dan No. HP wajib diisi.', 'err'); return; }
  pelanggan.push({id:nextId(), nama, hp, alamat: alamat||'-'});
  closeModal(); toast('Pelanggan baru berhasil ditambahkan.'); render();
}

function openKendaraanModal(pelangganId){
  showModal(`
    <h3>Tambah Kendaraan</h3>
    <div class="field"><label>Pemilik</label><input type="text" value="${findPelanggan(pelangganId).nama}" disabled></div>
    <div class="form-row">
      <div class="field"><label>Merk</label><input type="text" id="fMerk" placeholder="Honda / Yamaha"></div>
      <div class="field"><label>Tipe</label><input type="text" id="fTipe" placeholder="Vario 125"></div>
    </div>
    <div class="field"><label>Nomor Polisi</label><input type="text" id="fPlat" placeholder="Z 1234 AB"></div>
    <div class="modal-actions">
      <button class="btn btn-ghost" onclick="closeModal()">Batal</button>
      <button class="btn btn-primary" onclick="simpanKendaraan('${pelangganId}')">Simpan Kendaraan</button>
    </div>
  `);
}
function simpanKendaraan(pelangganId){
  const merk = document.getElementById('fMerk').value.trim();
  const tipe = document.getElementById('fTipe').value.trim();
  const plat = document.getElementById('fPlat').value.trim().toUpperCase();
  if(!merk || !tipe || !plat){ toast('Semua kolom kendaraan wajib diisi.', 'err'); return; }
  kendaraan.push({id:nextId(), pelangganId, merk, tipe, plat});
  closeModal(); toast('Kendaraan berhasil ditambahkan.'); render();
}

/* ================= SERVIS (KANBAN) ================= */
function renderServis(root, topAction){
  topAction.innerHTML = `<button class="btn btn-primary btn-sm" onclick="openServisModal()">+ Servis Baru</button>`;
  const cols = [
    {key:'menunggu', label:'Menunggu'},
    {key:'dikerjakan', label:'Dikerjakan'},
    {key:'selesai', label:'Selesai'},
  ];
  root.innerHTML = `<div class="kanban">${cols.map(c=>{
    const items = servis.filter(s=>s.status===c.key).slice().reverse();
    return `<div class="kcol">
      <h4>${c.label} <span class="cnt">${items.length}</span></h4>
      ${items.map(s=>servisCard(s)).join('') || '<div class="empty" style="padding:18px 4px;">Tidak ada servis</div>'}
    </div>`;
  }).join('')}</div>`;
}

function servisCard(s){
  const k = findKendaraan(s.kendaraanId); const p = findPelanggan(k.pelangganId); const m = findMekanik(s.mekanikId);
  let nextBtn = '';
  if(s.status==='menunggu') nextBtn = `<button class="btn btn-primary btn-sm" onclick="ubahStatus('${s.id}','dikerjakan')">Mulai Kerjakan</button>`;
  if(s.status==='dikerjakan') nextBtn = `<button class="btn btn-primary btn-sm" onclick="ubahStatus('${s.id}','selesai')">Tandai Selesai</button>`;
  return `<div class="scard">
    <div class="stop"><span class="plate">${k.plat}</span>${statusBadge(s.status)}</div>
    <div style="font-size:12.5px; color:var(--white); margin-bottom:3px;"><b>${p.nama}</b> · ${k.merk} ${k.tipe}</div>
    <div class="keluhan">${s.keluhan}</div>
    <div class="meta"><span>🔧 ${m.nama}</span><span class="mono">${rupiah(servisTotal(s))}</span></div>
    <div class="actions">
      ${s.items.length===0 && s.status!=='selesai' ? `<button class="btn btn-ghost btn-sm" onclick="openSparepartUsageModal('${s.id}')">+ Sparepart</button>` : ''}
      ${nextBtn}
    </div>
  </div>`;
}

function ubahStatus(id, status){
  const s = servis.find(x=>x.id===id);
  s.status = status;
  toast(`Servis ${findKendaraan(s.kendaraanId).plat} ditandai "${status}".`);
  render();
}

function openServisModal(){
  showModal(`
    <h3>Servis Baru</h3>
    <div class="field"><label>Kendaraan</label>
      <select id="fKendaraan">${kendaraan.map(k=>{
        const p = findPelanggan(k.pelangganId);
        return `<option value="${k.id}">${k.plat} — ${p.nama} (${k.merk} ${k.tipe})</option>`;
      }).join('')}</select>
    </div>
    <div class="field"><label>Mekanik</label>
      <select id="fMekanik">${mekanik.map(m=>`<option value="${m.id}">${m.nama} — ${m.spesialisasi}</option>`).join('')}</select>
    </div>
    <div class="field"><label>Keluhan / Jenis Servis</label><textarea id="fKeluhan" placeholder="Contoh: Servis rutin, ganti oli, cek rem"></textarea></div>
    <div class="field"><label>Biaya Jasa (Rp)</label><input type="number" id="fJasa" value="${BIAYA_JASA_DEFAULT}"></div>
    <div class="modal-actions">
      <button class="btn btn-ghost" onclick="closeModal()">Batal</button>
      <button class="btn btn-primary" onclick="simpanServis()">Tambahkan ke Antrian</button>
    </div>
  `);
}
function simpanServis(){
  const kendaraanId = document.getElementById('fKendaraan').value;
  const mekanikId = document.getElementById('fMekanik').value;
  const keluhan = document.getElementById('fKeluhan').value.trim();
  const jasa = parseInt(document.getElementById('fJasa').value)||0;
  if(!keluhan){ toast('Keluhan wajib diisi.', 'err'); return; }
  servis.push({id:nextId(), kendaraanId, mekanikId, keluhan, status:'menunggu', items:[], jasa, tanggal:'2026-07-13', dibayar:false});
  closeModal(); toast('Servis baru ditambahkan ke antrian.'); render();
}

function openSparepartUsageModal(servisId){
  showModal(`
    <h3>Tambah Sparepart Terpakai</h3>
    <div class="field"><label>Sparepart</label>
      <select id="fSp">${sparepart.map(sp=>`<option value="${sp.id}" ${sp.stok<=0?'disabled':''}>${sp.nama} (stok ${sp.stok}) — ${rupiah(sp.harga)}</option>`).join('')}</select>
    </div>
    <div class="field"><label>Jumlah</label><input type="number" id="fQty" value="1" min="1"></div>
    <div class="modal-actions">
      <button class="btn btn-ghost" onclick="closeModal()">Batal</button>
      <button class="btn btn-primary" onclick="simpanSparepartUsage('${servisId}')">Tambahkan</button>
    </div>
  `);
}
function simpanSparepartUsage(servisId){
  const sparepartId = document.getElementById('fSp').value;
  const qty = parseInt(document.getElementById('fQty').value)||1;
  const sp = findSparepart(sparepartId);
  if(qty > sp.stok){ toast(`Stok ${sp.nama} tidak cukup (sisa ${sp.stok}).`, 'err'); return; }
  const s = servis.find(x=>x.id===servisId);
  s.items.push({sparepartId, qty});
  sp.stok -= qty;
  closeModal(); toast('Sparepart ditambahkan & stok diperbarui.'); render();
}

/* ================= SPAREPART & STOK ================= */
function renderSparepart(root, topAction){
  topAction.innerHTML = `<button class="btn btn-primary btn-sm" onclick="openSparepartModal()">+ Tambah Sparepart</button>`;
  root.innerHTML = `
    <div class="panel">
      <table>
        <thead><tr><th>Nama Sparepart</th><th>Stok</th><th>Harga</th><th>Status</th><th></th></tr></thead>
        <tbody>
          ${sparepart.map(sp=>{
            const pct = Math.min(100, Math.round((sp.stok/(sp.minStok*3))*100));
            const low = sp.stok<=sp.minStok;
            return `<tr>
              <td><b>${sp.nama}</b></td>
              <td><span class="stockbar"><i style="width:${pct}%; background:${low?'var(--red)':'var(--green)'}"></i></span>${sp.stok} unit</td>
              <td class="mono">${rupiah(sp.harga)}</td>
              <td>${low ? '<span class="badge bad">Stok Menipis</span>' : '<span class="badge ok">Aman</span>'}</td>
              <td class="row-actions">
                <button class="btn btn-ghost btn-sm" onclick="tambahStok('${sp.id}')">+5 Stok</button>
              </td>
            </tr>`;
          }).join('')}
        </tbody>
      </table>
    </div>
  `;
}
function tambahStok(id){
  const sp = findSparepart(id); sp.stok += 5;
  toast(`Stok ${sp.nama} ditambah 5 unit.`); render();
}
function openSparepartModal(){
  showModal(`
    <h3>Tambah Sparepart</h3>
    <div class="field"><label>Nama Sparepart</label><input type="text" id="fSpNama" placeholder="Contoh: Kampas Kopling"></div>
    <div class="form-row">
      <div class="field"><label>Stok Awal</label><input type="number" id="fSpStok" value="10"></div>
      <div class="field"><label>Stok Minimum</label><input type="number" id="fSpMin" value="5"></div>
    </div>
    <div class="field"><label>Harga Satuan (Rp)</label><input type="number" id="fSpHarga" value="50000"></div>
    <div class="modal-actions">
      <button class="btn btn-ghost" onclick="closeModal()">Batal</button>
      <button class="btn btn-primary" onclick="simpanSparepart()">Simpan</button>
    </div>
  `);
}
function simpanSparepart(){
  const nama = document.getElementById('fSpNama').value.trim();
  const stok = parseInt(document.getElementById('fSpStok').value)||0;
  const minStok = parseInt(document.getElementById('fSpMin').value)||0;
  const harga = parseInt(document.getElementById('fSpHarga').value)||0;
  if(!nama){ toast('Nama sparepart wajib diisi.', 'err'); return; }
  sparepart.push({id:nextId(), nama, stok, minStok, harga});
  closeModal(); toast('Sparepart baru ditambahkan.'); render();
}

/* ================= TRANSAKSI ================= */
function renderTransaksi(root, topAction){
  const selesai = servis.filter(s=>s.status==='selesai').slice().reverse();
  root.innerHTML = `
    <div class="panel">
      <table>
        <thead><tr><th>Kendaraan</th><th>Pelanggan</th><th>Tanggal</th><th>Total</th><th>Status Bayar</th><th></th></tr></thead>
        <tbody>
          ${selesai.map(s=>{
            const k = findKendaraan(s.kendaraanId); const p = findPelanggan(k.pelangganId);
            return `<tr>
              <td><span class="plate">${k.plat}</span></td>
              <td>${p.nama}</td>
              <td class="mono">${s.tanggal}</td>
              <td class="mono">${rupiah(servisTotal(s))}</td>
              <td>${s.dibayar ? '<span class="badge ok">Lunas</span>' : '<span class="badge warn">Belum Bayar</span>'}</td>
              <td class="row-actions">
                ${!s.dibayar ? `<button class="btn btn-primary btn-sm" onclick="bayarServis('${s.id}')">Tandai Lunas</button>` : ''}
                <button class="btn btn-ghost btn-sm" onclick="cetakNota('${s.id}')">Cetak Nota</button>
              </td>
            </tr>`;
          }).join('')}
        </tbody>
      </table>
      ${selesai.length===0 ? '<div class="empty">Belum ada servis yang selesai untuk ditransaksikan.</div>' : ''}
    </div>
  `;
}
function bayarServis(id){
  const s = servis.find(x=>x.id===id); s.dibayar = true;
  toast('Pembayaran berhasil dicatat. Servis lunas.'); render();
}
function cetakNota(id){
  const s = servis.find(x=>x.id===id);
  const k = findKendaraan(s.kendaraanId); const p = findPelanggan(k.pelangganId); const m = findMekanik(s.mekanikId);
  const rows = s.items.map(it=>{
    const sp = findSparepart(it.sparepartId);
    return `<tr><td>${sp.nama} x${it.qty}</td><td style="text-align:right">${rupiah(sp.harga*it.qty)}</td></tr>`;
  }).join('');
  showModal(`
    <div class="nota">
      <h3 style="text-align:center;">JAKARTA MOTOR GARAGE</h3>
      <div style="text-align:center; font-size:11px; color:#555;">Nota Servis Kendaraan Bermotor</div>
      <div class="line"></div>
      <div>No. Polisi: <b>${k.plat}</b></div>
      <div>Pelanggan: ${p.nama}</div>
      <div>Kendaraan: ${k.merk} ${k.tipe}</div>
      <div>Mekanik: ${m.nama}</div>
      <div>Tanggal: ${s.tanggal}</div>
      <div class="line"></div>
      <table>
        <tr><td>Jasa Servis</td><td style="text-align:right">${rupiah(s.jasa)}</td></tr>
        ${rows}
      </table>
      <div class="line"></div>
      <div class="tot" style="display:flex; justify-content:space-between;"><span>TOTAL</span><span>${rupiah(servisTotal(s))}</span></div>
      <div style="text-align:center; font-size:10.5px; color:#777; margin-top:14px;">Terima kasih telah servis di Jakarta Motor Garage 🔧</div>
    </div>
    <div class="modal-actions">
      <button class="btn btn-ghost" onclick="closeModal()">Tutup</button>
      <button class="btn btn-primary" onclick="window.print()">Cetak</button>
    </div>
  `);
}

/* ================= LAPORAN ================= */
function renderLaporan(root, topAction){
  const days = ['07-07','07-08','07-09','07-10','07-11','07-12','07-13'];
  const dummyRev = [320000, 410000, 275000, 500000, 460000, 0, servis.filter(s=>s.dibayar).reduce((a,s)=>a+servisTotal(s),0) || 180000];
  const max = Math.max(...dummyRev, 1);
  const totalBulan = dummyRev.reduce((a,b)=>a+b,0) + 4820000;
  const totalServisSelesai = servis.filter(s=>s.status==='selesai').length;

  root.innerHTML = `
    <div class="grid-cards" style="grid-template-columns:repeat(3,1fr);">
      <div class="card"><div class="card-bar" style="background:var(--orange)"></div>
        <div class="clabel">Pendapatan Bulan Ini</div><div class="cval" style="font-size:22px;">${rupiah(totalBulan)}</div>
        <div class="cnote up">Estimasi akumulasi bulan berjalan</div></div>
      <div class="card"><div class="card-bar" style="background:var(--green)"></div>
        <div class="clabel">Servis Selesai</div><div class="cval">${totalServisSelesai}</div>
        <div class="cnote up">Minggu ini</div></div>
      <div class="card"><div class="card-bar" style="background:var(--amber)"></div>
        <div class="clabel">Rata-rata / Servis</div><div class="cval" style="font-size:22px;">${rupiah(Math.round(totalBulan/Math.max(1,(totalServisSelesai+7))))}</div>
        <div class="cnote warn">Termasuk jasa &amp; sparepart</div></div>
    </div>
    <div class="panel">
      <div class="panel-head"><h3>Pendapatan 7 Hari Terakhir</h3></div>
      <div class="bars">
        ${dummyRev.map((v,i)=>`
          <div class="bar-col">
            <div class="bar-val">${(v/1000).toFixed(0)}k</div>
            <div class="bar" style="height:${Math.max(6,(v/max)*130)}px"></div>
            <div class="bar-lab">${days[i]}</div>
          </div>
        `).join('')}
      </div>
    </div>
  `;
}

/* ================= MODAL ================= */
function showModal(innerHtml){
  const back = document.createElement('div');
  back.className = 'modal-back'; back.id = 'modalBack';
  back.innerHTML = `<div class="modal">${innerHtml}</div>`;
  back.addEventListener('click', e=>{ if(e.target===back) closeModal(); });
  document.body.appendChild(back);
}
function closeModal(){
  const back = document.getElementById('modalBack');
  if(back) back.remove();
}
document.addEventListener('keydown', e=>{ if(e.key==='Escape') closeModal(); });

/* init view meta on load (in case app shown without login during dev) */
navigate('dashboard');
</script>
</body>
</html>
