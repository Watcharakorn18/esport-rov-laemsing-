<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RoV Arena | ระบบจัดการแข่ง</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Anuphan:wght@400;600;800&family=Russo+One&display=swap');

  :root{
    --bg: #08070f;
    --panel: #15121f;
    --panel-2: #1c1830;
    --line: #2e2848;
    --gold: #f3c34d;
    --purple: #8b5cf6;
    --teal: #34d8c4;
    --text: #e8e6f0;
    --muted: #8a84a3;
    --danger: #f06b6b;
  }

  *{margin:0;padding:0;box-sizing:border-box;}
  html{ perspective: 1400px; }
  body{
    background:
      radial-gradient(circle at 12% -10%, color-mix(in srgb, var(--purple) 28%, transparent) 0%, transparent 45%),
      radial-gradient(circle at 92% 110%, color-mix(in srgb, var(--teal) 22%, transparent) 0%, transparent 45%),
      var(--bg);
    color: var(--text);
    font-family: 'Anuphan', sans-serif;
    min-height: 100vh;
    padding-bottom: 60px;
    transition: background .4s;
  }

  header{
    padding: 32px 20px 22px;
    text-align:center;
    border-bottom: 1px solid var(--line);
    position:relative;
  }
  header h1{
    font-family:'Russo One', sans-serif;
    font-size: 30px;
    letter-spacing: 3px;
    color: var(--gold);
    text-shadow: 0 0 22px color-mix(in srgb, var(--gold) 45%, transparent), 0 2px 0 rgba(0,0,0,0.6);
    transition: color .3s;
  }
  header p{
    color: var(--muted);
    margin-top:7px;
    font-size: 13px;
  }

  nav{
    display:flex;
    justify-content:center;
    gap: 8px;
    margin: 22px auto 0;
    max-width: 600px;
    padding: 0 12px;
    position: sticky;
    top: 0;
    z-index: 10;
  }
  nav button{
    flex:1;
    position:relative;
    background: var(--panel);
    border: 1px solid var(--line);
    color: var(--muted);
    font-family:'Anuphan',sans-serif;
    font-weight:600;
    font-size: 13px;
    padding: 11px 6px;
    border-radius: 10px;
    cursor:pointer;
    transition: color .25s, border-color .25s;
    overflow:hidden;
    transform-style: preserve-3d;
  }
  nav button.active{
    color: #fff;
    border-color: var(--purple);
    box-shadow: 0 0 0 1px color-mix(in srgb, var(--purple) 60%, transparent), 0 6px 18px -6px color-mix(in srgb, var(--purple) 70%, transparent), inset 0 0 18px color-mix(in srgb, var(--purple) 25%, transparent);
  }
  nav button.active::before{
    content:"";
    position:absolute; top:0; left:-60%;
    width: 60%; height: 100%;
    background: linear-gradient(100deg, transparent, rgba(255,255,255,0.35), transparent);
    animation: sweep 1.8s ease-in-out infinite;
  }
  @keyframes sweep{
    0%{ left:-60%; }
    60%{ left: 110%; }
    100%{ left: 110%; }
  }

  main{
    max-width: 540px;
    margin: 24px auto;
    padding: 0 16px;
  }

  .card{
    background: linear-gradient(155deg, var(--panel), var(--panel-2));
    border: 1px solid var(--line);
    border-radius: 16px;
    padding: 20px;
    margin-bottom: 16px;
    transform-style: preserve-3d;
    transition: transform .25s ease, box-shadow .25s ease;
    box-shadow: 0 14px 30px -16px rgba(0,0,0,0.7), 0 0 0 1px rgba(255,255,255,0.02) inset;
  }
  .card:hover{
    box-shadow: 0 22px 40px -16px color-mix(in srgb, var(--purple) 40%, transparent), 0 0 0 1px rgba(255,255,255,0.04) inset;
  }
  .card h2{
    font-size: 16px;
    color: var(--teal);
    margin-bottom: 4px;
    font-family:'Russo One', sans-serif;
    letter-spacing: 1px;
    transition: color .3s;
  }
  .card .sub{
    font-size: 12px; color: var(--muted); margin-bottom: 14px;
  }
  .card h3{
    font-size: 13px;
    color: var(--text);
    margin: 18px 0 4px;
    font-weight:800;
  }

  label{
    display:block;
    font-size: 12px;
    color: var(--muted);
    margin: 12px 0 6px;
  }
  input[type="text"], input[type="password"], input[type="number"]{
    width:100%;
    background: var(--bg);
    border: 1px solid var(--line);
    border-radius: 8px;
    padding: 11px 12px;
    color: var(--text);
    font-family:'Anuphan',sans-serif;
    font-size: 14px;
    outline:none;
    transition: border-color .2s, box-shadow .2s;
  }
  input:focus{ border-color: var(--purple); box-shadow: 0 0 0 3px color-mix(in srgb, var(--purple) 20%, transparent); }

  input[type="color"]{
    width: 100%;
    height: 40px;
    border: 1px solid var(--line);
    border-radius: 8px;
    background: var(--bg);
    cursor:pointer;
    padding: 4px;
  }
  .color-grid{
    display:grid;
    grid-template-columns: repeat(4,1fr);
    gap: 10px;
    margin-top: 8px;
  }
  .color-grid div label{ text-align:center; margin-bottom:6px; }

  .btn{
    width:100%;
    margin-top: 18px;
    background: linear-gradient(135deg, var(--purple), color-mix(in srgb, var(--purple) 60%, #2a1f55));
    color: #fff;
    border:none;
    border-radius: 10px;
    padding: 13px;
    font-weight:800;
    font-size: 14px;
    cursor:pointer;
    letter-spacing: .5px;
    transition: transform .15s, box-shadow .15s;
    box-shadow: 0 8px 20px -8px color-mix(in srgb, var(--purple) 70%, transparent);
  }
  .btn:hover{ transform: translateY(-2px); }
  .btn:active{ transform: scale(.98); }
  .btn.secondary{
    background: linear-gradient(135deg, #2c2748, #221f3a);
    border: 1px solid var(--line);
    box-shadow:none;
  }
  .btn.logout{
    background: transparent;
    border: 1px solid var(--line);
    color: var(--muted);
    box-shadow:none;
    margin-top: 0;
  }

  .pill{
    display:inline-block;
    background: var(--panel-2);
    border:1px solid var(--line);
    color: var(--gold);
    font-size: 11px;
    font-weight:700;
    padding: 4px 10px;
    border-radius: 999px;
    margin-bottom: 10px;
    transition: color .3s;
  }

  .team-name{
    font-family:'Russo One', sans-serif;
    font-size: 24px;
    color: #fff;
    margin: 6px 0 4px;
    text-shadow: 0 0 16px color-mix(in srgb, var(--purple) 60%, transparent);
  }
  .roster{
    list-style:none;
    margin-top: 12px;
  }
  .roster li{
    display:flex;
    align-items:center;
    gap:10px;
    padding: 10px 0;
    border-bottom: 1px solid var(--line);
    font-size: 14px;
  }
  .roster li:last-child{border-bottom:none;}
  .avatar{
    width: 32px; height:32px; border-radius: 50%;
    background: linear-gradient(135deg, var(--teal), var(--purple));
    display:flex; align-items:center; justify-content:center;
    font-size: 12px; font-weight:800; color:#fff;
    flex-shrink:0;
    box-shadow: 0 4px 10px -4px color-mix(in srgb, var(--purple) 80%, transparent);
  }
  .role-tag{
    margin-left:auto;
    font-size: 11px;
    color: var(--muted);
    background: var(--bg);
    padding: 3px 8px;
    border-radius: 6px;
  }
  .you-tag{
    color: var(--gold);
    font-weight:800;
  }

  .bracket{
    overflow-x:auto;
    padding-bottom: 10px;
  }
  .rounds{
    display:flex;
    gap: 0;
    min-width: 980px;
    padding: 10px 2px;
    position:relative;
  }
  .round{
    display:flex;
    flex-direction:column;
    justify-content: space-around;
    gap: 30px;
    flex:1;
    min-width: 220px;
    padding: 0 32px;
    position:relative;
  }
  .round-title{
    font-size:13px;
    color: var(--muted);
    text-align:center;
    margin-bottom: 12px;
    text-transform:uppercase;
    letter-spacing: 1.5px;
    font-weight:700;
  }
  .match{
    background: var(--panel-2);
    border:1px solid var(--line);
    border-radius: 12px;
    overflow:hidden;
    font-size: 15px;
    position:relative;
    z-index:2;
  }
  .match .slot{
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding: 14px 16px;
    gap: 10px;
  }
  .match .slot:first-child{border-bottom:1px solid var(--line);}
  .match .slot.win{ color: var(--gold); font-weight:800; }
  .match .slot.tbd{ color: var(--muted); font-style:italic;}
  .match .score{
    font-family:'Russo One',sans-serif;
    font-size: 16px;
    opacity:.8;
  }

  .connectors{
    position:absolute;
    top:0; right:-32px;
    width: 32px; height:100%;
    pointer-events:none;
  }
  .connectors svg{ width:100%; height:100%; }
  .connectors path{
    fill:none;
    stroke: var(--line);
    stroke-width: 2;
  }
  .connectors path.lit{ stroke: var(--purple); }

  .empty{
    text-align:center;
    color: var(--muted);
    font-size: 13px;
    padding: 20px 0;
  }
  .note{
    font-size: 11px;
    color: var(--muted);
    text-align:center;
    margin-top: 18px;
    line-height:1.6;
  }
  .error-text{
    color: var(--danger);
    font-size: 12px;
    margin-top: 8px;
    display:none;
  }

  .admin-row{
    display:grid;
    grid-template-columns: 1.3fr 1fr 1fr auto;
    gap: 6px;
    align-items:center;
    padding: 8px 0;
    border-bottom: 1px solid var(--line);
  }
  .admin-row:last-child{ border-bottom:none; }
  .admin-row input{ font-size:12px; padding: 8px; }
  .admin-row select{
    font-size:12px; padding: 8px;
    background: var(--bg); border:1px solid var(--line);
    border-radius: 8px; color: var(--text);
  }
  .icon-btn{
    background: var(--bg);
    border: 1px solid var(--line);
    color: var(--danger);
    border-radius: 8px;
    width: 32px; height: 32px;
    cursor:pointer;
    font-size: 14px;
    line-height:1;
  }
  .admin-head{
    display:grid;
    grid-template-columns: 1.3fr 1fr 1fr auto;
    gap:6px;
    font-size: 11px;
    color: var(--muted);
    margin-bottom: 6px;
    padding-bottom: 6px;
    border-bottom: 1px solid var(--line);
  }

  /* bracket admin editor */
  .bm-row{
    display:grid;
    grid-template-columns: 1fr 50px;
    gap:6px;
    margin-bottom:6px;
    align-items:center;
  }
  .bm-block{
    border: 1px solid var(--line);
    border-radius: 10px;
    padding: 10px;
    margin-bottom: 10px;
    background: var(--bg);
  }
  .bm-block .bm-title{
    font-size:11px; color: var(--muted); margin-bottom:8px;
    text-transform:uppercase; letter-spacing:1px;
  }

  /* admin login */
  .login-box{
    max-width: 340px;
    margin: 0 auto;
    text-align:center;
  }
  .login-box .lock{
    width: 52px; height:52px;
    margin: 0 auto 14px;
    border-radius: 50%;
    background: var(--panel-2);
    border: 1px solid var(--line);
    display:flex; align-items:center; justify-content:center;
    font-family:'Russo One',sans-serif;
    font-size: 20px;
    color: var(--purple);
  }
</style>
</head>
<body>

<header>
  <h1 id="site-title">RoV ARENA</h1>
  <p id="site-subtitle">ระบบลงทะเบียนและจัดสายการแข่งขัน</p>
</header>

<nav>
  <button class="active" data-tab="register">ลงทะเบียน</button>
  <button data-tab="myteam">ทีมของฉัน</button>
  <button data-tab="bracket">สายการแข่ง</button>
  <button data-tab="admin">แอดมิน</button>
</nav>

<main>

  <section id="register">
    <div class="card">
      <span class="pill" id="reg-pill">ขั้นตอนที่ 1</span>
      <h2 id="reg-title">ลงทะเบียนเข้าร่วมแข่งขัน</h2>
      <div class="sub" id="reg-sub">กรอกข้อมูลให้ครบทั้ง 3 ช่อง ระบบจะตรวจสอบและพาไปยังทีมของคุณโดยอัตโนมัติ</div>

      <label id="reg-label-name">ชื่อ-นามสกุลจริง</label>
      <input id="reg-name" type="text" placeholder="เช่น สมชาย ใจดี">

      <label id="reg-label-gameid">ชื่อในเกม / ไอดีเกม</label>
      <input id="reg-gameid" type="text" placeholder="เช่น ShadowBlade_TH">

      <label id="reg-label-contact">เบอร์โทรติดต่อ</label>
      <input id="reg-contact" type="text" placeholder="เช่น 081-234-5678">

      <button class="btn" onclick="register()" id="reg-button">ลงทะเบียน</button>
      <div class="error-text" id="reg-error"></div>
    </div>

    <div class="note" id="reg-note">
      * แอดมินจะเป็นผู้กำหนดล่วงหน้าว่าชื่อใดอยู่ทีมไหน เมื่อผู้สมัครลงทะเบียนด้วยชื่อที่ตรงกัน ระบบจะจับเข้าทีมนั้นให้อัตโนมัติ
    </div>
  </section>

  <section id="myteam" style="display:none">
    <div class="card" id="myteam-card"></div>
    <div class="card" id="myteam-logo-card" style="display:none">
      <span class="pill">ปรับแต่งทีม</span>
      <h2>โลโก้ทีม</h2>
      <div class="sub">อัปโหลดรูปโลโก้สำหรับทีมของคุณ (จะแสดงให้ทุกคนเห็น)</div>
      <div style="display:flex;align-items:center;gap:14px;margin-top:10px">
        <img id="myteam-logo-preview" src="" alt="logo" style="width:64px;height:64px;border-radius:50%;object-fit:cover;border:1px solid var(--line);display:none">
        <div id="myteam-logo-placeholder" class="avatar" style="width:64px;height:64px;font-size:18px;display:none"></div>
        <input id="myteam-logo-input" type="file" accept="image/*" style="flex:1">
      </div>
      <button class="btn" onclick="uploadTeamLogo()">บันทึกโลโก้</button>
      <div class="error-text" id="myteam-logo-error"></div>
    </div>
    <div class="card" id="myteam-match" style="display:none">
      <h2>แมตช์ถัดไปของทีมคุณ</h2>
      <div class="sub" id="mm-round"></div>
      <div class="match" id="mm-match" style="max-width:300px"></div>
    </div>
  </section>

  <section id="bracket" style="display:none; max-width: 1040px; margin: 0 auto; width: 100%; position: relative; left: 50%; transform: translateX(-50%);">
    <div class="card">
      <span class="pill">สายการแข่งขัน</span>
      <h2 id="bracket-title">สาย A — Knockout</h2>
      <div class="sub">เลื่อนซ้าย-ขวาเพื่อดูรอบต่อไป — เส้นแสดงเส้นทางสู่รอบถัดไป</div>

      <div class="bracket">
        <div class="rounds" id="bracket-rounds"></div>
      </div>
    </div>

    <div class="note">
      * เมื่อแอดมินกรอกผลของแมตช์ใดในแอดมินแพแนล ทีมที่ชนะ (สีทอง) จะปรากฏในรอบถัดไปโดยอัตโนมัติ
    </div>
  </section>

  <!-- ADMIN: locked -->
  <section id="admin" style="display:none">

    <div class="card login-box" id="admin-login">
      <div class="lock">🔒</div>
      <span class="pill">เฉพาะแอดมิน</span>
      <h2>เข้าสู่ระบบแอดมิน</h2>
      <div class="sub">กรอกรหัสผ่านเพื่อแก้ไขข้อมูลทั้งหมดของเว็บไซต์</div>
      <input id="admin-pass" type="password" placeholder="รหัสผ่านแอดมิน">
      <button class="btn" onclick="adminLogin()">เข้าสู่ระบบ</button>
      <div class="error-text" id="admin-login-error"></div>
    </div>

    <div id="admin-panel" style="display:none">

      <div class="card">
        <span class="pill">ตั้งค่าเว็บไซต์</span>
        <h2>หัวข้อและสีของธีม</h2>
        <div class="sub">ปรับชื่อเว็บ คำอธิบาย และโทนสีหลักของเว็บไซต์</div>

        <label>ชื่อเว็บไซต์ (หัวข้อบนสุด)</label>
        <input id="set-title" type="text">

        <label>คำอธิบายใต้หัวข้อ</label>
        <input id="set-subtitle" type="text">

        <label>ชื่อหัวข้อสายการแข่ง</label>
        <input id="set-bracket-title" type="text">

        <h3>ข้อความหน้าลงทะเบียน</h3>
        <label>ป้ายขั้นตอน</label>
        <input id="set-reg-pill" type="text">

        <label>หัวข้อ</label>
        <input id="set-reg-title" type="text">

        <label>คำอธิบาย</label>
        <input id="set-reg-sub" type="text">

        <label>ชื่อช่อง: ชื่อ-นามสกุล</label>
        <input id="set-reg-label-name" type="text">

        <label>ชื่อช่อง: ไอดีเกม</label>
        <input id="set-reg-label-gameid" type="text">

        <label>ชื่อช่อง: เบอร์โทร</label>
        <input id="set-reg-label-contact" type="text">

        <label>ข้อความปุ่ม</label>
        <input id="set-reg-button" type="text">

        <label>ข้อความหมายเหตุด้านล่าง</label>
        <input id="set-reg-note" type="text">

        <h3>สีของธีม</h3>
        <div class="color-grid">
          <div><label>สีทอง (หัวข้อ)</label><input id="col-gold" type="color"></div>
          <div><label>สีม่วง (ปุ่ม/ไฮไลต์)</label><input id="col-purple" type="color"></div>
          <div><label>สีเขียวอมฟ้า</label><input id="col-teal" type="color"></div>
          <div><label>สีตัวอักษรหลัก</label><input id="col-text" type="color"></div>
        </div>

        <button class="btn" onclick="saveSettings()">บันทึกการตั้งค่า</button>
      </div>

      <div class="card">
        <span class="pill">จัดการผู้เล่นและทีม</span>
        <h2>รายชื่อผู้เข้าแข่งขัน</h2>
        <div class="sub">แก้ไขชื่อ ตำแหน่ง และทีมของผู้เล่นแต่ละคนได้โดยตรง</div>

        <div class="admin-head">
          <span>ชื่อ-นามสกุล</span>
          <span>ตำแหน่ง</span>
          <span>ทีม</span>
          <span></span>
        </div>
        <div id="admin-list"></div>

        <button class="btn secondary" onclick="addRosterRow()">+ เพิ่มผู้เล่น</button>
      </div>

      <div class="card">
        <h2>สรุปทีมทั้งหมด</h2>
        <ul class="roster" id="team-summary"></ul>
      </div>

      <div class="card">
        <span class="pill">จัดการสายการแข่ง</span>
        <h2>แก้ไขคู่แข่งและผลการแข่ง</h2>
        <div class="sub">แก้ชื่อทีมในรอบ 1 และกรอกผลคะแนน — ทีมที่ชนะจะเลื่อนเข้ารอบถัดไปอัตโนมัติ</div>
        <div id="bracket-admin"></div>
      </div>

      <button class="btn logout" onclick="adminLogout()">ออกจากระบบแอดมิน</button>
    </div>

  </section>

</main>

<script>
/* ---------- 3D tilt ---------- */
function attachTilt(card){
  card.addEventListener('mousemove', e=>{
    const r = card.getBoundingClientRect();
    const x = (e.clientX - r.left)/r.width - 0.5;
    const y = (e.clientY - r.top)/r.height - 0.5;
    card.style.transform = `rotateY(${x*6}deg) rotateX(${-y*6}deg) translateZ(4px)`;
  });
  card.addEventListener('mouseleave', ()=>{
    card.style.transform = 'rotateY(0) rotateX(0) translateZ(0)';
  });
}
document.querySelectorAll('.card').forEach(attachTilt);

/* ---------- Tabs ---------- */
const tabs = document.querySelectorAll('nav button');
const sections = {
  register: document.getElementById('register'),
  myteam: document.getElementById('myteam'),
  bracket: document.getElementById('bracket'),
  admin: document.getElementById('admin'),
};
tabs.forEach(btn => btn.addEventListener('click', () => {
  tabs.forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  Object.values(sections).forEach(s => s.style.display = 'none');
  sections[btn.dataset.tab].style.display = 'block';
  if(btn.dataset.tab === 'bracket') drawBracket();
  if(btn.dataset.tab === 'admin' && isAdmin) renderAdminAll();
}));

/* ---------- Site settings (theme, titles) ---------- */
let settings = {
  title: 'RoV ARENA',
  subtitle: 'ระบบลงทะเบียนและจัดสายการแข่งขัน',
  bracketTitle: 'สาย A — Knockout',
  colGold: '#f3c34d',
  colPurple: '#8b5cf6',
  colTeal: '#34d8c4',
  colText: '#e8e6f0',
  regPill: 'ขั้นตอนที่ 1',
  regTitle: 'ลงทะเบียนเข้าร่วมแข่งขัน',
  regSub: 'กรอกข้อมูลให้ครบทั้ง 3 ช่อง ระบบจะตรวจสอบและพาไปยังทีมของคุณโดยอัตโนมัติ',
  regLabelName: 'ชื่อ-นามสกุลจริง',
  regLabelGameid: 'ชื่อในเกม / ไอดีเกม',
  regLabelContact: 'เบอร์โทรติดต่อ',
  regButton: 'ลงทะเบียน',
  regNote: '* แอดมินจะเป็นผู้กำหนดล่วงหน้าว่าชื่อใดอยู่ทีมไหน เมื่อผู้สมัครลงทะเบียนด้วยชื่อที่ตรงกัน ระบบจะจับเข้าทีมนั้นให้อัตโนมัติ',
};

function applySettings(){
  document.getElementById('site-title').textContent = settings.title;
  document.getElementById('site-subtitle').textContent = settings.subtitle;
  document.getElementById('bracket-title').textContent = settings.bracketTitle;
  const root = document.documentElement.style;
  root.setProperty('--gold', settings.colGold);
  root.setProperty('--purple', settings.colPurple);
  root.setProperty('--teal', settings.colTeal);
  root.setProperty('--text', settings.colText);

  document.getElementById('reg-pill').textContent = settings.regPill;
  document.getElementById('reg-title').textContent = settings.regTitle;
  document.getElementById('reg-sub').textContent = settings.regSub;
  document.getElementById('reg-label-name').textContent = settings.regLabelName;
  document.getElementById('reg-label-gameid').textContent = settings.regLabelGameid;
  document.getElementById('reg-label-contact').textContent = settings.regLabelContact;
  document.getElementById('reg-button').textContent = settings.regButton;
  document.getElementById('reg-note').textContent = settings.regNote;
}
applySettings();

function loadSettingsToForm(){
  document.getElementById('set-title').value = settings.title;
  document.getElementById('set-subtitle').value = settings.subtitle;
  document.getElementById('set-bra<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RoV Arena | ระบบจัดการแข่ง</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Anuphan:wght@400;600;800&family=Russo+One&display=swap');

  :root{
    --bg: #08070f;
    --panel: #15121f;
    --panel-2: #1c1830;
    --line: #2e2848;
    --gold: #f3c34d;
    --purple: #8b5cf6;
    --teal: #34d8c4;
    --text: #e8e6f0;
    --muted: #8a84a3;
    --danger: #f06b6b;
  }

  *{margin:0;padding:0;box-sizing:border-box;}
  html{ perspective: 1400px; }
  body{
    background:
      radial-gradient(circle at 12% -10%, color-mix(in srgb, var(--purple) 28%, transparent) 0%, transparent 45%),
      radial-gradient(circle at 92% 110%, color-mix(in srgb, var(--teal) 22%, transparent) 0%, transparent 45%),
      var(--bg);
    color: var(--text);
    font-family: 'Anuphan', sans-serif;
    min-height: 100vh;
    padding-bottom: 60px;
    transition: background .4s;
  }

  header{
    padding: 32px 20px 22px;
    text-align:center;
    border-bottom: 1px solid var(--line);
    position:relative;
  }
  header h1{
    font-family:'Russo One', sans-serif;
    font-size: 30px;
    letter-spacing: 3px;
    color: var(--gold);
    text-shadow: 0 0 22px color-mix(in srgb, var(--gold) 45%, transparent), 0 2px 0 rgba(0,0,0,0.6);
    transition: color .3s;
  }
  header p{
    color: var(--muted);
    margin-top:7px;
    font-size: 13px;
  }

  nav{
    display:flex;
    justify-content:center;
    gap: 8px;
    margin: 22px auto 0;
    max-width: 600px;
    padding: 0 12px;
    position: sticky;
    top: 0;
    z-index: 10;
  }
  nav button{
    flex:1;
    position:relative;
    background: var(--panel);
    border: 1px solid var(--line);
    color: var(--muted);
    font-family:'Anuphan',sans-serif;
    font-weight:600;
    font-size: 13px;
    padding: 11px 6px;
    border-radius: 10px;
    cursor:pointer;
    transition: color .25s, border-color .25s;
    overflow:hidden;
    transform-style: preserve-3d;
  }
  nav button.active{
    color: #fff;
    border-color: var(--purple);
    box-shadow: 0 0 0 1px color-mix(in srgb, var(--purple) 60%, transparent), 0 6px 18px -6px color-mix(in srgb, var(--purple) 70%, transparent), inset 0 0 18px color-mix(in srgb, var(--purple) 25%, transparent);
  }
  nav button.active::before{
    content:"";
    position:absolute; top:0; left:-60%;
    width: 60%; height: 100%;
    background: linear-gradient(100deg, transparent, rgba(255,255,255,0.35), transparent);
    animation: sweep 1.8s ease-in-out infinite;
  }
  @keyframes sweep{
    0%{ left:-60%; }
    60%{ left: 110%; }
    100%{ left: 110%; }
  }

  main{
    max-width: 540px;
    margin: 24px auto;
    padding: 0 16px;
  }

  .card{
    background: linear-gradient(155deg, var(--panel), var(--panel-2));
    border: 1px solid var(--line);
    border-radius: 16px;
    padding: 20px;
    margin-bottom: 16px;
    transform-style: preserve-3d;
    transition: transform .25s ease, box-shadow .25s ease;
    box-shadow: 0 14px 30px -16px rgba(0,0,0,0.7), 0 0 0 1px rgba(255,255,255,0.02) inset;
  }
  .card:hover{
    box-shadow: 0 22px 40px -16px color-mix(in srgb, var(--purple) 40%, transparent), 0 0 0 1px rgba(255,255,255,0.04) inset;
  }
  .card h2{
    font-size: 16px;
    color: var(--teal);
    margin-bottom: 4px;
    font-family:'Russo One', sans-serif;
    letter-spacing: 1px;
    transition: color .3s;
  }
  .card .sub{
    font-size: 12px; color: var(--muted); margin-bottom: 14px;
  }
  .card h3{
    font-size: 13px;
    color: var(--text);
    margin: 18px 0 4px;
    font-weight:800;
  }

  label{
    display:block;
    font-size: 12px;
    color: var(--muted);
    margin: 12px 0 6px;
  }
  input[type="text"], input[type="password"], input[type="number"]{
    width:100%;
    background: var(--bg);
    border: 1px solid var(--line);
    border-radius: 8px;
    padding: 11px 12px;
    color: var(--text);
    font-family:'Anuphan',sans-serif;
    font-size: 14px;
    outline:none;
    transition: border-color .2s, box-shadow .2s;
  }
  input:focus{ border-color: var(--purple); box-shadow: 0 0 0 3px color-mix(in srgb, var(--purple) 20%, transparent); }

  input[type="color"]{
    width: 100%;
    height: 40px;
    border: 1px solid var(--line);
    border-radius: 8px;
    background: var(--bg);
    cursor:pointer;
    padding: 4px;
  }
  .color-grid{
    display:grid;
    grid-template-columns: repeat(4,1fr);
    gap: 10px;
    margin-top: 8px;
  }
  .color-grid div label{ text-align:center; margin-bottom:6px; }

  .btn{
    width:100%;
    margin-top: 18px;
    background: linear-gradient(135deg, var(--purple), color-mix(in srgb, var(--purple) 60%, #2a1f55));
    color: #fff;
    border:none;
    border-radius: 10px;
    padding: 13px;
    font-weight:800;
    font-size: 14px;
    cursor:pointer;
    letter-spacing: .5px;
    transition: transform .15s, box-shadow .15s;
    box-shadow: 0 8px 20px -8px color-mix(in srgb, var(--purple) 70%, transparent);
  }
  .btn:hover{ transform: translateY(-2px); }
  .btn:active{ transform: scale(.98); }
  .btn.secondary{
    background: linear-gradient(135deg, #2c2748, #221f3a);
    border: 1px solid var(--line);
    box-shadow:none;
  }
  .btn.logout{
    background: transparent;
    border: 1px solid var(--line);
    color: var(--muted);
    box-shadow:none;
    margin-top: 0;
  }

  .pill{
    display:inline-block;
    background: var(--panel-2);
    border:1px solid var(--line);
    color: var(--gold);
    font-size: 11px;
    font-weight:700;
    padding: 4px 10px;
    border-radius: 999px;
    margin-bottom: 10px;
    transition: color .3s;
  }

  .team-name{
    font-family:'Russo One', sans-serif;
    font-size: 24px;
    color: #fff;
    margin: 6px 0 4px;
    text-shadow: 0 0 16px color-mix(in srgb, var(--purple) 60%, transparent);
  }
  .roster{
    list-style:none;
    margin-top: 12px;
  }
  .roster li{
    display:flex;
    align-items:center;
    gap:10px;
    padding: 10px 0;
    border-bottom: 1px solid var(--line);
    font-size: 14px;
  }
  .roster li:last-child{border-bottom:none;}
  .avatar{
    width: 32px; height:32px; border-radius: 50%;
    background: linear-gradient(135deg, var(--teal), var(--purple));
    display:flex; align-items:center; justify-content:center;
    font-size: 12px; font-weight:800; color:#fff;
    flex-shrink:0;
    box-shadow: 0 4px 10px -4px color-mix(in srgb, var(--purple) 80%, transparent);
  }
  .role-tag{
    margin-left:auto;
    font-size: 11px;
    color: var(--muted);
    background: var(--bg);
    padding: 3px 8px;
    border-radius: 6px;
  }
  .you-tag{
    color: var(--gold);
    font-weight:800;
  }

  .bracket{
    overflow-x:auto;
    padding-bottom: 10px;
  }
  .rounds{
    display:flex;
    gap: 0;
    min-width: 980px;
    padding: 10px 2px;
    position:relative;
  }
  .round{
    display:flex;
    flex-direction:column;
    justify-content: space-around;
    gap: 30px;
    flex:1;
    min-width: 220px;
    padding: 0 32px;
    position:relative;
  }
  .round-title{
    font-size:13px;
    color: var(--muted);
    text-align:center;
    margin-bottom: 12px;
    text-transform:uppercase;
    letter-spacing: 1.5px;
    font-weight:700;
  }
  .match{
    background: var(--panel-2);
    border:1px solid var(--line);
    border-radius: 12px;
    overflow:hidden;
    font-size: 15px;
    position:relative;
    z-index:2;
  }
  .match .slot{
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding: 14px 16px;
    gap: 10px;
  }
  .match .slot:first-child{border-bottom:1px solid var(--line);}
  .match .slot.win{ color: var(--gold); font-weight:800; }
  .match .slot.tbd{ color: var(--muted); font-style:italic;}
  .match .score{
    font-family:'Russo One',sans-serif;
    font-size: 16px;
    opacity:.8;
  }

  .connectors{
    position:absolute;
    top:0; right:-32px;
    width: 32px; height:100%;
    pointer-events:none;
  }
  .connectors svg{ width:100%; height:100%; }
  .connectors path{
    fill:none;
    stroke: var(--line);
    stroke-width: 2;
  }
  .connectors path.lit{ stroke: var(--purple); }

  .empty{
    text-align:center;
    color: var(--muted);
    font-size: 13px;
    padding: 20px 0;
  }
  .note{
    font-size: 11px;
    color: var(--muted);
    text-align:center;
    margin-top: 18px;
    line-height:1.6;
  }
  .error-text{
    color: var(--danger);
    font-size: 12px;
    margin-top: 8px;
    display:none;
  }

  .admin-row{
    display:grid;
    grid-template-columns: 1.3fr 1fr 1fr auto;
    gap: 6px;
    align-items:center;
    padding: 8px 0;
    border-bottom: 1px solid var(--line);
  }
  .admin-row:last-child{ border-bottom:none; }
  .admin-row input{ font-size:12px; padding: 8px; }
  .admin-row select{
    font-size:12px; padding: 8px;
    background: var(--bg); border:1px solid var(--line);
    border-radius: 8px; color: var(--text);
  }
  .icon-btn{
    background: var(--bg);
    border: 1px solid var(--line);
    color: var(--danger);
    border-radius: 8px;
    width: 32px; height: 32px;
    cursor:pointer;
    font-size: 14px;
    line-height:1;
  }
  .admin-head{
    display:grid;
    grid-template-columns: 1.3fr 1fr 1fr auto;
    gap:6px;
    font-size: 11px;
    color: var(--muted);
    margin-bottom: 6px;
    padding-bottom: 6px;
    border-bottom: 1px solid var(--line);
  }

  /* bracket admin editor */
  .bm-row{
    display:grid;
    grid-template-columns: 1fr 50px;
    gap:6px;
    margin-bottom:6px;
    align-items:center;
  }
  .bm-block{
    border: 1px solid var(--line);
    border-radius: 10px;
    padding: 10px;
    margin-bottom: 10px;
    background: var(--bg);
  }
  .bm-block .bm-title{
    font-size:11px; color: var(--muted); margin-bottom:8px;
    text-transform:uppercase; letter-spacing:1px;
  }

  /* admin login */
  .login-box{
    max-width: 340px;
    margin: 0 auto;
    text-align:center;
  }
  .login-box .lock{
    width: 52px; height:52px;
    margin: 0 auto 14px;
    border-radius: 50%;
    background: var(--panel-2);
    border: 1px solid var(--line);
    display:flex; align-items:center; justify-content:center;
    font-family:'Russo One',sans-serif;
    font-size: 20px;
    color: var(--purple);
  }
</style>
</head>
<body>

<header>
  <h1 id="site-title">RoV ARENA</h1>
  <p id="site-subtitle">ระบบลงทะเบียนและจัดสายการแข่งขัน</p>
</header>

<nav>
  <button class="active" data-tab="register">ลงทะเบียน</button>
  <button data-tab="myteam">ทีมของฉัน</button>
  <button data-tab="bracket">สายการแข่ง</button>
  <button data-tab="admin">แอดมิน</button>
</nav>

<main>

  <section id="register">
    <div class="card">
      <span class="pill" id="reg-pill">ขั้นตอนที่ 1</span>
      <h2 id="reg-title">ลงทะเบียนเข้าร่วมแข่งขัน</h2>
      <div class="sub" id="reg-sub">กรอกข้อมูลให้ครบทั้ง 3 ช่อง ระบบจะตรวจสอบและพาไปยังทีมของคุณโดยอัตโนมัติ</div>

      <label id="reg-label-name">ชื่อ-นามสกุลจริง</label>
      <input id="reg-name" type="text" placeholder="เช่น สมชาย ใจดี">

      <label id="reg-label-gameid">ชื่อในเกม / ไอดีเกม</label>
      <input id="reg-gameid" type="text" placeholder="เช่น ShadowBlade_TH">

      <label id="reg-label-contact">เบอร์โทรติดต่อ</label>
      <input id="reg-contact" type="text" placeholder="เช่น 081-234-5678">

      <button class="btn" onclick="register()" id="reg-button">ลงทะเบียน</button>
      <div class="error-text" id="reg-error"></div>
    </div>

    <div class="note" id="reg-note">
      * แอดมินจะเป็นผู้กำหนดล่วงหน้าว่าชื่อใดอยู่ทีมไหน เมื่อผู้สมัครลงทะเบียนด้วยชื่อที่ตรงกัน ระบบจะจับเข้าทีมนั้นให้อัตโนมัติ
    </div>
  </section>

  <section id="myteam" style="display:none">
    <div class="card" id="myteam-card"></div>
    <div class="card" id="myteam-logo-card" style="display:none">
      <span class="pill">ปรับแต่งทีม</span>
      <h2>โลโก้ทีม</h2>
      <div class="sub">อัปโหลดรูปโลโก้สำหรับทีมของคุณ (จะแสดงให้ทุกคนเห็น)</div>
      <div style="display:flex;align-items:center;gap:14px;margin-top:10px">
        <img id="myteam-logo-preview" src="" alt="logo" style="width:64px;height:64px;border-radius:50%;object-fit:cover;border:1px solid var(--line);display:none">
        <div id="myteam-logo-placeholder" class="avatar" style="width:64px;height:64px;font-size:18px;display:none"></div>
        <input id="myteam-logo-input" type="file" accept="image/*" style="flex:1">
      </div>
      <button class="btn" onclick="uploadTeamLogo()">บันทึกโลโก้</button>
      <div class="error-text" id="myteam-logo-error"></div>
    </div>
    <div class="card" id="myteam-match" style="display:none">
      <h2>แมตช์ถัดไปของทีมคุณ</h2>
      <div class="sub" id="mm-round"></div>
      <div class="match" id="mm-match" style="max-width:300px"></div>
    </div>
  </section>

  <section id="bracket" style="display:none; max-width: 1040px; margin: 0 auto; width: 100%; position: relative; left: 50%; transform: translateX(-50%);">
    <div class="card">
      <span class="pill">สายการแข่งขัน</span>
      <h2 id="bracket-title">สาย A — Knockout</h2>
      <div class="sub">เลื่อนซ้าย-ขวาเพื่อดูรอบต่อไป — เส้นแสดงเส้นทางสู่รอบถัดไป</div>

      <div class="bracket">
        <div class="rounds" id="bracket-rounds"></div>
      </div>
    </div>

    <div class="note">
      * เมื่อแอดมินกรอกผลของแมตช์ใดในแอดมินแพแนล ทีมที่ชนะ (สีทอง) จะปรากฏในรอบถัดไปโดยอัตโนมัติ
    </div>
  </section>

  <!-- ADMIN: locked -->
  <section id="admin" style="display:none">

    <div class="card login-box" id="admin-login">
      <div class="lock">🔒</div>
      <span class="pill">เฉพาะแอดมิน</span>
      <h2>เข้าสู่ระบบแอดมิน</h2>
      <div class="sub">กรอกรหัสผ่านเพื่อแก้ไขข้อมูลทั้งหมดของเว็บไซต์</div>
      <input id="admin-pass" type="password" placeholder="รหัสผ่านแอดมิน">
      <button class="btn" onclick="adminLogin()">เข้าสู่ระบบ</button>
      <div class="error-text" id="admin-login-error"></div>
    </div>

    <div id="admin-panel" style="display:none">

      <div class="card">
        <span class="pill">ตั้งค่าเว็บไซต์</span>
        <h2>หัวข้อและสีของธีม</h2>
        <div class="sub">ปรับชื่อเว็บ คำอธิบาย และโทนสีหลักของเว็บไซต์</div>

        <label>ชื่อเว็บไซต์ (หัวข้อบนสุด)</label>
        <input id="set-title" type="text">

        <label>คำอธิบายใต้หัวข้อ</label>
        <input id="set-subtitle" type="text">

        <label>ชื่อหัวข้อสายการแข่ง</label>
        <input id="set-bracket-title" type="text">

        <h3>ข้อความหน้าลงทะเบียน</h3>
        <label>ป้ายขั้นตอน</label>
        <input id="set-reg-pill" type="text">

        <label>หัวข้อ</label>
        <input id="set-reg-title" type="text">

        <label>คำอธิบาย</label>
        <input id="set-reg-sub" type="text">

        <label>ชื่อช่อง: ชื่อ-นามสกุล</label>
        <input id="set-reg-label-name" type="text">

        <label>ชื่อช่อง: ไอดีเกม</label>
        <input id="set-reg-label-gameid" type="text">

        <label>ชื่อช่อง: เบอร์โทร</label>
        <input id="set-reg-label-contact" type="text">

        <label>ข้อความปุ่ม</label>
        <input id="set-reg-button" type="text">

        <label>ข้อความหมายเหตุด้านล่าง</label>
        <input id="set-reg-note" type="text">

        <h3>สีของธีม</h3>
        <div class="color-grid">
          <div><label>สีทอง (หัวข้อ)</label><input id="col-gold" type="color"></div>
          <div><label>สีม่วง (ปุ่ม/ไฮไลต์)</label><input id="col-purple" type="color"></div>
          <div><label>สีเขียวอมฟ้า</label><input id="col-teal" type="color"></div>
          <div><label>สีตัวอักษรหลัก</label><input id="col-text" type="color"></div>
        </div>

        <button class="btn" onclick="saveSettings()">บันทึกการตั้งค่า</button>
      </div>

      <div class="card">
        <span class="pill">จัดการผู้เล่นและทีม</span>
        <h2>รายชื่อผู้เข้าแข่งขัน</h2>
        <div class="sub">แก้ไขชื่อ ตำแหน่ง และทีมของผู้เล่นแต่ละคนได้โดยตรง</div>

        <div class="admin-head">
          <span>ชื่อ-นามสกุล</span>
          <span>ตำแหน่ง</span>
          <span>ทีม</span>
          <span></span>
        </div>
        <div id="admin-list"></div>

        <button class="btn secondary" onclick="addRosterRow()">+ เพิ่มผู้เล่น</button>
      </div>

      <div class="card">
        <h2>สรุปทีมทั้งหมด</h2>
        <ul class="roster" id="team-summary"></ul>
      </div>

      <div class="card">
        <span class="pill">จัดการสายการแข่ง</span>
        <h2>แก้ไขคู่แข่งและผลการแข่ง</h2>
        <div class="sub">แก้ชื่อทีมในรอบ 1 และกรอกผลคะแนน — ทีมที่ชนะจะเลื่อนเข้ารอบถัดไปอัตโนมัติ</div>
        <div id="bracket-admin"></div>
      </div>

      <button class="btn logout" onclick="adminLogout()">ออกจากระบบแอดมิน</button>
    </div>

  </section>

</main>

<script>
/* ---------- 3D tilt ---------- */
function attachTilt(card){
  card.addEventListener('mousemove', e=>{
    const r = card.getBoundingClientRect();
    const x = (e.clientX - r.left)/r.width - 0.5;
    const y = (e.clientY - r.top)/r.height - 0.5;
    card.style.transform = `rotateY(${x*6}deg) rotateX(${-y*6}deg) translateZ(4px)`;
  });
  card.addEventListener('mouseleave', ()=>{
    card.style.transform = 'rotateY(0) rotateX(0) translateZ(0)';
  });
}
document.querySelectorAll('.card').forEach(attachTilt);

/* ---------- Tabs ---------- */
const tabs = document.querySelectorAll('nav button');
const sections = {
  register: document.getElementById('register'),
  myteam: document.getElementById('myteam'),
  bracket: document.getElementById('bracket'),
  admin: document.getElementById('admin'),
};
tabs.forEach(btn => btn.addEventListener('click', () => {
  tabs.forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  Object.values(sections).forEach(s => s.style.display = 'none');
  sections[btn.dataset.tab].style.display = 'block';
  if(btn.dataset.tab === 'bracket') drawBracket();
  if(btn.dataset.tab === 'admin' && isAdmin) renderAdminAll();
}));

/* ---------- Site settings (theme, titles) ---------- */
let settings = {
  title: 'RoV ARENA',
  subtitle: 'ระบบลงทะเบียนและจัดสายการแข่งขัน',
  bracketTitle: 'สาย A — Knockout',
  colGold: '#f3c34d',
  colPurple: '#8b5cf6',
  colTeal: '#34d8c4',
  colText: '#e8e6f0',
  regPill: 'ขั้นตอนที่ 1',
  regTitle: 'ลงทะเบียนเข้าร่วมแข่งขัน',
  regSub: 'กรอกข้อมูลให้ครบทั้ง 3 ช่อง ระบบจะตรวจสอบและพาไปยังทีมของคุณโดยอัตโนมัติ',
  regLabelName: 'ชื่อ-นามสกุลจริง',
  regLabelGameid: 'ชื่อในเกม / ไอดีเกม',
  regLabelContact: 'เบอร์โทรติดต่อ',
  regButton: 'ลงทะเบียน',
  regNote: '* แอดมินจะเป็นผู้กำหนดล่วงหน้าว่าชื่อใดอยู่ทีมไหน เมื่อผู้สมัครลงทะเบียนด้วยชื่อที่ตรงกัน ระบบจะจับเข้าทีมนั้นให้อัตโนมัติ',
};

function applySettings(){
  document.getElementById('site-title').textContent = settings.title;
  document.getElementById('site-subtitle').textContent = settings.subtitle;
  document.getElementById('bracket-title').textContent = settings.bracketTitle;
  const root = document.documentElement.style;
  root.setProperty('--gold', settings.colGold);
  root.setProperty('--purple', settings.colPurple);
  root.setProperty('--teal', settings.colTeal);
  root.setProperty('--text', settings.colText);

  document.getElementById('reg-pill').textContent = settings.regPill;
  document.getElementById('reg-title').textContent = settings.regTitle;
  document.getElementById('reg-sub').textContent = settings.regSub;
  document.getElementById('reg-label-name').textContent = settings.regLabelName;
  document.getElementById('reg-label-gameid').textContent = settings.regLabelGameid;
  document.getElementById('reg-label-contact').textContent = settings.regLabelContact;
  document.getElementById('reg-button').textContent = settings.regButton;
  document.getElementById('reg-note').textContent = settings.regNote;
}
applySettings();

function loadSettingsToForm(){
  document.getElementById('set-title').value = settings.title;
  document.getElementById('set-subtitle').value = settings.subtitle;
  document.getElementById('set-bra
