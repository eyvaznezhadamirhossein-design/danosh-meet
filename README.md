
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#090d16">
<title>Danoosh Meet</title>
<style>
:root {
  --bg:#090d16;--panel:rgba(255,255,255,.055);
  --glass:rgba(25,32,48,.72);--line:rgba(255,255,255,.1);
  --text:#f4f6ff;--muted:#929cb2;--purple:#9b87ff;
  --danger:#ef5967;
}
*{box-sizing:border-box}
body{
 margin:0;min-height:100dvh;color:var(--text);
 background:radial-gradient(ellipse at 10% 0%,#28204d 0%,transparent 35%),
 radial-gradient(ellipse at 95% 90%,#112c46 0%,transparent 34%),var(--bg);
 font-family:system-ui,-apple-system,"Segoe UI",sans-serif
}
button,input{font:inherit}button{cursor:pointer}
svg{width:21px;height:21px;fill:none;stroke:currentColor;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round}
button:focus-visible,input:focus-visible{outline:2px solid var(--purple);outline-offset:3px}
.app{width:min(1600px,100%);min-height:100dvh;margin:auto;padding:20px;display:flex;flex-direction:column;gap:20px}
.topbar,.brand,.top-actions,.meeting-head,.head-right{display:flex;align-items:center}
.topbar,.meeting-head{justify-content:space-between;gap:12px}
.brand{gap:12px}.logo{width:45px;height:45px;display:grid;place-items:center;border-radius:15px;background:linear-gradient(140deg,#b6a6ff,#7559e9);box-shadow:0 8px 32px #7962f044}
.logo svg{width:25px;height:25px}.brand-name{font-size:18px;font-weight:750}.brand-sub{color:var(--muted);font-size:12px;margin-top:2px}
.top-actions{gap:9px}.room-chip,.glass-chip{border:1px solid var(--line);background:var(--panel);backdrop-filter:blur(20px);padding:10px 13px;border-radius:13px;color:#dce2f3;font-size:12px}
.status-dot{display:inline-block;width:7px;height:7px;border-radius:50%;background:#58d6a0;margin-left:6px;box-shadow:0 0 12px #58d6a088}
.layout{flex:1;min-height:0;display:grid;grid-template-columns:minmax(0,1fr) 350px;gap:18px}
.meeting{min-width:0;display:flex;flex-direction:column;gap:15px}
.meeting-title{font-size:19px;font-weight:700}.meeting-sub{color:var(--muted);font-size:12px;margin-top:5px}
.head-right{gap:8px}
.icon-button{width:42px;height:42px;display:grid;place-items:center;border:1px solid var(--line);border-radius:14px;background:var(--panel);color:#e6e8f2}
.icon-button:hover{background:#ffffff15}
.video-stage{position:relative;flex:1;min-height:390px;border:1px solid var(--line);border-radius:25px;background:linear-gradient(145deg,#171c2b,#0d121e 65%);overflow:hidden;box-shadow:0 25px 80px #0003}
#localVideo{width:100%;height:100%;min-height:390px;display:block;object-fit:cover;transform:scaleX(-1)}
.video-placeholder{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:13px;background:radial-gradient(ellipse at 50% 40%,#44376a65,transparent 38%),linear-gradient(145deg,#171c2b,#0d121e)}
.avatar{width:92px;height:92px;border-radius:30px;display:grid;place-items:center;background:linear-gradient(145deg,#b7a6ff,#7056df);box-shadow:0 15px 45px #7d65f344;font-size:30px;font-weight:750}
.placeholder-hint{color:var(--muted);font-size:12px}
.video-label{position:absolute;right:15px;bottom:15px;display:flex;align-items:center;gap:8px;padding:10px 12px;border:1px solid #ffffff18;border-radius:12px;background:#101521bd;backdrop-filter:blur(16px);font-size:12px}
.live-label{position:absolute;top:15px;left:15px;display:flex;align-items:center;gap:7px;border:1px solid #ffffff1b;border-radius:10px;padding:8px 10px;background:#101521ad;font-size:11px;backdrop-filter:blur(15px)}
.controls{display:flex;align-items:center;justify-content:center;gap:12px;flex-wrap:wrap;border:1px solid var(--line);background:var(--glass);backdrop-filter:blur(24px);border-radius:22px;padding:14px}
.control{min-width:54px;height:54px;padding:0 17px;display:flex;align-items:center;justify-content:center;gap:9px;border:1px solid var(--line);border-radius:17px;background:#ffffff09;color:white;transition:.2s}
.control:hover{background:#ffffff15}.control-label{font-size:12px}.control.off,.control.end{background:var(--danger);border-color:transparent;color:white}
.control.primary{background:linear-gradient(135deg,#aa98ff,#8069f0);border-color:transparent;color:#151126}
.sidebar{min-height:0;display:flex;flex-direction:column;border:1px solid #ffffff17;border-radius:25px;background:linear-gradient(145deg,rgba(255,255,255,.09),rgba(255,255,255,.025));box-shadow:inset 0 1px 0 #ffffff0b,0 20px 60px #0002;backdrop-filter:blur(30px) saturate(140%);overflow:hidden}
.sidebar-head{padding:19px 18px 14px;border-bottom:1px solid var(--line)}
.sidebar-heading{font-size:16px;font-weight:720;margin-bottom:15px}
.tabs{position:relative;isolation:isolate;display:flex;padding:5px;gap:5px;border:1px solid #ffffff0d;border-radius:15px;background:#080b1280}
.tabs::before{content:"";position:absolute;z-index:-1;top:5px;bottom:5px;right:5px;width:calc(50% - 7.5px);border:1px solid #a493ff3c;border-radius:11px;background:linear-gradient(135deg,#9b87ff2c,#7462ee20);transition:transform .28s cubic-bezier(.2,.8,.2,1)}
.tabs:has([data-tab="users"].active)::before{transform:translateX(-100%)}
.tab{flex:1;border:1px solid transparent;border-radius:11px;padding:10px 8px;color:#a9b2c6;background:transparent;display:flex;align-items:center;justify-content:center;gap:8px;font-size:12px;transition:color .2s}
.tab svg{width:17px;height:17px}.tab.active{color:#eeeaff}
.panel{display:none;flex:1;min-height:0}.panel.active{display:flex;flex-direction:column;animation:panelIn .24s ease both}
@keyframes panelIn{from{opacity:0;transform:translateY(7px)}to{opacity:1;transform:translateY(0)}}
.chat-messages{flex:1;min-height:150px;overflow-y:auto;display:flex;flex-direction:column;gap:15px;padding:18px 15px;scrollbar-width:thin;scrollbar-color:#ffffff22 transparent}
.day-divider{align-self:center;color:#8f9ab0;font-size:10px;padding:6px 10px;border:1px solid #ffffff0c;background:#ffffff06;border-radius:20px}
.message{display:flex;flex-direction:column;gap:6px;max-width:92%}.message.mine{align-self:flex-start;align-items:flex-start}.message.other{align-self:flex-end;align-items:flex-end}
.message-meta{display:flex;align-items:center;gap:7px;color:#a0abc0;font-size:10px}
.message-bubble{padding:11px 13px;border:1px solid #ffffff0c;background:#ffffff0a;border-radius:15px 15px 15px 4px;color:#e3e7f1;font-size:13px;line-height:1.8;overflow-wrap:anywhere}
.message.mine .message-bubble{background:linear-gradient(135deg,#8975ee30,#9b87ff17);border-color:#a493ff24;border-radius:15px 15px 4px 15px}
.chat-composer{padding:14px;border-top:1px solid var(--line);background:#080b121f}
.composer-box{display:flex;align-items:center;gap:8px;padding:6px 8px 6px 6px;border:1px solid #ffffff16;border-radius:17px;background:#070a11a6}
.composer-box:focus-within{border-color:#a493ff77;box-shadow:0 0 0 3px #a493ff0d}
#messageInput{min-width:0;flex:1;border:0;outline:none;color:white;background:transparent;padding:10px 7px;font-size:12px}
#messageInput::placeholder{color:#77839a}
.send-button{width:40px;height:40px;flex-shrink:0;display:grid;place-items:center;border:0;border-radius:13px;background:linear-gradient(135deg,#ad9aff,#826af2);color:#18132b}
.send-button svg{width:19px;height:19px}.composer-note{color:#77839a;font-size:10px;margin:9px 3px 0}
.users-panel{padding:16px;gap:13px}
.user-card{display:flex;align-items:center;gap:11px;padding:12px;border:1px solid #ffffff0c;border-radius:16px;background:#ffffff07}
.user-avatar{width:42px;height:42px;flex-shrink:0;display:grid;place-items:center;border-radius:14px;background:#9b87ff24;color:#c8bdff;font-size:14px;font-weight:750}
.user-info{flex:1;min-width:0}.user-name{font-size:12px;font-weight:650}.user-status{font-size:10px;color:#7dd9b2;margin-top:4px}
.user-actions{display:flex;gap:9px}.status-icon{position:relative;width:20px;height:20px;color:#aeb8cb}
.status-icon svg{width:19px;height:19px}.status-icon.is-off{color:#ff626f}
.status-icon.is-off::after{content:"";position:absolute;width:25px;height:2px;background:#ff4f60;border-radius:4px;left:-3px;top:9px;transform:rotate(-45deg);box-shadow:0 0 5px #ff4f6050}
.panel-info{margin-top:auto;padding:12px;border-radius:14px;color:#9ea9bd;background:#ffffff06;font-size:11px;line-height:1.9}
.toast{position:fixed;z-index:20;bottom:22px;left:50%;transform:translate(-50%,20px);opacity:0;pointer-events:none;background:#222b3d;border:1px solid #ffffff1b;color:white;border-radius:13px;padding:12px 17px;box-shadow:0 10px 35px #0005;font-size:12px;transition:.25s}
.toast.show{opacity:1;transform:translate(-50%,0)}
/* ورود و ساخت اتاق */
.overlay{position:fixed;z-index:30;inset:0;display:flex;align-items:center;justify-content:center;padding:18px;background:#060913bd;backdrop-filter:blur(18px)}
.login-card{width:min(430px,100%);border:1px solid #ffffff20;border-radius:27px;padding:26px;background:linear-gradient(145deg,#22263beF,#101521f5);box-shadow:0 30px 100px #0008;animation:panelIn .3s ease both}
.login-brand{display:flex;align-items:center;gap:12px;margin-bottom:23px}
.login-title{font-size:21px;font-weight:750}.login-sub{font-size:12px;color:var(--muted);margin-top:5px;line-height:1.8}
.field-label{display:block;font-size:12px;color:#d4daea;margin:15px 0 8px}
.field{width:100%;padding:14px;border:1px solid #ffffff18;border-radius:14px;background:#080c16a8;color:white;outline:none}
.field:focus{border-color:#a493ff88}
.login-actions{display:flex;gap:9px;margin-top:18px}
.login-button{flex:1;padding:13px 10px;border:1px solid #ffffff18;border-radius:14px;background:#ffffff0a;color:white;font-size:12px}
.login-button.primary{background:linear-gradient(135deg,#ad9aff,#826af2);color:#17132b;border:0;font-weight:750}
.login-note{font-size:10px;color:#929cb2;line-height:1.8;margin-top:16px}
[hidden]{display:none!important}
@media(min-width:1000px){.layout{min-height:650px}.sidebar{max-height:calc(100dvh - 135px)}}
@media(max-width:999px){.app{padding:13px;gap:15px}.layout{display:flex;flex-direction:column}.video-stage,#localVideo{min-height:48vh}.sidebar{min-height:430px}.panel.active{min-height:320px}.chat-messages{min-height:220px}}
@media(max-width:480px){.brand-name{font-size:16px}.brand-sub{font-size:10px}.logo{width:39px;height:39px}.room-chip{padding:9px}.meeting-title{font-size:16px}.video-stage,#localVideo{min-height:42vh}.controls{gap:8px;padding:10px}.control{width:48px;min-width:48px;height:49px;padding:0;border-radius:15px}.control-label{display:none}.icon-button{width:39px;height:39px}.sidebar{border-radius:20px}.sidebar-head{padding:15px 13px 12px}}
@media(prefers-reduced-motion:reduce){*,*::before,*::after{animation:none!important;transition:none!important}}
</style>
</head>
<body>

<svg aria-hidden="true" style="position:absolute;width:0;height:0;overflow:hidden">
<symbol id="i-video" viewBox="0 0 24 24"><rect x="3" y="6" width="13" height="12" rx="3"/><path d="m16 10 5-3v10l-5-3z"/></symbol>
<symbol id="i-video-off" viewBox="0 0 24 24"><path d="m3 3 18 18M10 6h3a3 3 0 0 1 3 3v2l5-4v10M5 8a3 3 0 0 0-2 3v4a3 3 0 0 0 3 3h7a3 3 0 0 0 2-1"/></symbol>
<symbol id="i-mic" viewBox="0 0 24 24"><rect x="9" y="3" width="6" height="12" rx="3"/><path d="M5 11a7 7 0 0 0 14 0M12 18v3m-4 0h8"/></symbol>
<symbol id="i-mic-off" viewBox="0 0 24 24"><path d="m3 3 18 18M9 9V6a3 3 0 0 1 6 0v7M5 11a7 7 0 0 0 11.5 5.3M19 11a7 7 0 0 1-1 3.5M12 18v3m-4 0h8"/></symbol>
<symbol id="i-monitor" viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="13" rx="2"/><path d="M8 21h8m-4-4v4m-2-12 3 3 5-5"/></symbol>
<symbol id="i-phone" viewBox="0 0 24 24"><path d="M22 16.9v3a2 2 0 0 1-2.2 2A19.8 19.8 0 0 1 11.2 19a19.4 19.4 0 0 1-6-6A19.8 19.8 0 0 1 2.1 4.2 2 2 0 0 1 4.1 2h3a2 2 0 0 1 2 1.7l.5 2.8a2 2 0 0 1-.6 1.9L7.7 9.7a16 16 0 0 0 6 6l1.3-1.3a2 2 0 0 1 1.9-.6l2.8.5a2 2 0 0 1 1.7 2.6z"/></symbol>
<symbol id="i-send" viewBox="0 0 24 24"><path d="m22 2-7 20-4-9-9-4Z"/><path d="M22 2 11 13"/></symbol>
<symbol id="i-chat" viewBox="0 0 24 24"><path d="M21 11.5a8.4 8.4 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.4 8.4 0 0 1-3.8-.9L3 21l1.9-5.7a8.4 8.4 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.4 8.4 0 0 1 3.8-.9h.5a8.5 8.5 0 0 1 8 8z"/></symbol>
<symbol id="i-users" viewBox="0 0 24 24"><path d="M16 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2m6-10a4 4 0 1 0 0-8 4 4 0 0 0 0 8zm10 10v-2a4 4 0 0 0-3-3.9m-1-12.1a4 4 0 0 1 0 7.8"/></symbol>
<symbol id="i-copy" viewBox="0 0 24 24"><rect x="8" y="8" width="13" height="13" rx="2"/><path d="M16 8V5a2 2 0 0 0-2-2H5a2 2 0 0 0-2 2v9a2 2 0 0 0 2 2h3"/></symbol>
<symbol id="i-wifi" viewBox="0 0 24 24"><path d="M5 12.5a10 10 0 0 1 14 0M8.5 16a5 5 0 0 1 7 0M2 9a15 15 0 0 1 20 0"/><circle cx="12" cy="20" r="1"/></symbol>
</svg>

<div class="app">
<header class="topbar">
 <div class="brand"><div class="logo"><svg><use href="#i-video"/></svg></div><div><div class="brand-name">Danoosh Meet</div><div class="brand-sub">فضایی برای گفت‌وگو</div></div></div>
 <div class="top-actions">
  <button class="room-chip" id="copyRoom">کد <strong id="roomCode">DAN-204</strong></button>
  <div class="glass-chip"><span class="status-dot"></span><span id="connectionLabel">آماده جلسه</span></div>
 </div>
</header>

<main class="layout">
<section class="meeting">
 <div class="meeting-head"><div><div class="meeting-title">گفت‌وگوی جلسه</div><div class="meeting-sub">فضای اختصاصی شما برای ملاقات آنلاین</div></div>
 <div class="head-right"><button class="icon-button" id="copyLink" title="کپی لینک" aria-label="کپی لینک"><svg><use href="#i-copy"/></svg></button><button class="icon-button" id="connectionInfo" title="وضعیت اتصال" aria-label="وضعیت اتصال"><svg><use href="#i-wifi"/></svg></button></div></div>
 <div class="video-stage">
  <video id="localVideo" autoplay playsinline muted hidden></video>
  <div class="video-placeholder" id="placeholder"><div class="avatar" id="mainAvatar">D</div><div class="placeholder-hint">برای شروع، دوربینت را روشن کن</div></div>
  <div class="live-label"><span class="status-dot"></span> جلسه محلی</div>
  <div class="video-label"><span id="videoName">شما</span></div>
 </div>
 <div class="controls">
  <button class="control" id="micBtn" title="میکروفون" aria-label="میکروفون"><svg><use href="#i-mic"/></svg><span class="control-label">میکروفون</span></button>
  <button class="control" id="cameraBtn" title="دوربین" aria-label="دوربین"><svg><use href="#i-video"/></svg><span class="control-label">دوربین</span></button>
  <button class="control" id="screenBtn" title="اشتراک صفحه" aria-label="اشتراک صفحه"><svg><use href="#i-monitor"/></svg><span class="control-label">اشتراک صفحه</span></button>
  <button class="control primary" id="startBtn" title="شروع جلسه" aria-label="شروع جلسه"><svg><use href="#i-video"/></svg><span class="control-label">شروع جلسه</span></button>
  <button class="control end" id="endBtn" title="پایان جلسه" aria-label="پایان جلسه"><svg><use href="#i-phone"/></svg><span class="control-label">پایان</span></button>
 </div>
</section>

<aside class="sidebar">
 <div class="sidebar-head"><div class="sidebar-heading">گفت‌وگوی جلسه</div>
  <div class="tabs" role="tablist">
   <button class="tab active" data-tab="chat" role="tab" aria-selected="true"><svg><use href="#i-chat"/></svg>چت</button>
   <button class="tab" data-tab="users" role="tab" aria-selected="false"><svg><use href="#i-users"/></svg>کاربران <span id="userCount">1</span></button>
  </div>
 </div>
 <section class="panel active" id="chatPanel" role="tabpanel">
  <div class="chat-messages" id="messages" aria-live="polite"><div class="day-divider">شروع جلسه</div></div>
  <form class="chat-composer" id="chatForm"><div class="composer-box"><input id="messageInput" maxlength="1000" autocomplete="off" placeholder="پیامت رو اینجا بنویس..." aria-label="پیام جدید"><button class="send-button" type="submit" aria-label="ارسال پیام"><svg><use href="#i-send"/></svg></button></div><div class="composer-note">پیام‌ها فعلاً فقط در همین صفحه ذخیره می‌شوند.</div></form>
 </section>
 <section class="panel users-panel" id="usersPanel" role="tabpanel">
  <div class="user-card"><div class="user-avatar" id="userAvatar">D</div><div class="user-info"><div class="user-name" id="userNameLabel">شما</div><div class="user-status" id="userStatus">آماده اتصال</div></div>
   <div class="user-actions"><span id="userMicIcon" class="status-icon is-off"><svg><use href="#i-mic"/></svg></span><span id="userCameraIcon" class="status-icon is-off"><svg><use href="#i-video"/></svg></span></div>
  </div>
  <div class="panel-info"><strong>درباره جلسه</strong><br>این نسخه پیش‌نمایش محلی است. برای تماس واقعی با کاربران دیگر، به سرور سیگنالینگ و WebRTC نیاز داریم.</div>
 </section>
</aside>
</main>
</div>

<div class="overlay" id="loginOverlay">
 <form class="login-card" id="loginForm">
  <div class="login-brand"><div class="logo"><svg><use href="#i-video"/></svg></div><div><div class="login-title">ورود به Danoosh Meet</div><div class="login-sub">نامت را وارد کن و یک جلسه بساز یا با کد وارد جلسه شو.</div></div></div>
  <label class="field-label" for="displayName">نام نمایشی</label>
  <input class="field" id="displayName" maxlength="32" placeholder="مثلاً امیر" autocomplete="name" required>
  <label class="field-label" for="joinCode">کد ورود (برای پیوستن)</label>
  <input class="field" id="joinCode" maxlength="40" placeholder="کد جلسه را وارد کن" autocomplete="off">
  <div class="login-actions"><button class="login-button primary" type="submit" value="create" id="createRoomBtn">ساخت اتاق</button><button class="login-button" type="submit" value="join" id="joinRoomBtn">ورود با کد</button></div>
  <div class="login-note">در این نسخه اتاق‌ها محلی هستند و با کاربران دیگر همگام نمی‌شوند.</div>
 </form>
</div>
<div class="toast" id="toast" role="status"></div>

<script>
const $=id=>document.getElementById(id);
let localStream=null,screenStream=null,cameraOn=false,micOn=false,displayName="شما",roomCode="DAN-204",toastTimer;
function notify(text){const t=$("toast");t.textContent=text;t.classList.add("show");clearTimeout(toastTimer);toastTimer=setTimeout(()=>t.classList.remove("show"),2500)}
function setIcon(button,name){button.querySelector("use").setAttribute("href","#"+name)}
function randomRoom(){return "DAN-"+Math.random().toString(36).slice(2,7).toUpperCase()}
function switchTab(name){
 document.querySelectorAll(".tab").forEach(t=>{let on=t.dataset.tab===name;t.classList.toggle("active",on);t.setAttribute("aria-selected",String(on))});
 $("chatPanel").classList.toggle("active",name==="chat");
 $("usersPanel").classList.toggle("active",name==="users");
}
document.querySelectorAll(".tab").forEach(t=>t.addEventListener("click",()=>switchTab(t.dataset.tab)));

function updateStatus(){
 $("userStatus").textContent=cameraOn||micOn?"در حال استفاده":"آماده اتصال";
 $("userMicIcon").classList.toggle("is-off",!micOn);
 $("userCameraIcon").classList.toggle("is-off",!cameraOn);
 $("connectionLabel").textContent=localStream?"رسانه فعال":"آماده جلسه";
 $("userCount").textContent="1";
}
function updateIdentity(){
 $("videoName").textContent=displayName;
 $("userNameLabel").textContent=displayName;
 $("userAvatar").textContent=displayName.slice(0,1).toUpperCase();
 $("mainAvatar").textContent=displayName.slice(0,1).toUpperCase();
 $("roomCode").textContent=roomCode;
}
$("loginForm").addEventListener("click",event=>{
 const submitter=event.target.closest("button[type=submit]");
 if(submitter)$("loginForm").dataset.action=submitter.value;
});
$("loginForm").addEventListener("submit",event=>{
 event.preventDefault();
 displayName=$("displayName").value.trim().slice(0,32);
 if(!displayName){notify("لطفاً نامت را وارد کن.");return}
 const action=$("loginForm").dataset.action||"create";
 if(action==="join"){
  const code=$("joinCode").value.trim().toUpperCase();
  if(!code){notify("کد اتاق را وارد کن.");return}
  roomCode=code;
 }else{
  roomCode=randomRoom();
 }
 updateIdentity();
 $("loginOverlay").hidden=true;
 addMessage("سلام! من "+displayName+" هستم.",true);
 notify(action==="join"?"کد اتاق وارد شد.":"اتاق محلی ساخته شد: "+roomCode);
});

function addMessage(text,mine=true){
 const msg=document.createElement("div");msg.className="message "+(mine?"mine":"other");
 const meta=document.createElement("div");meta.className="message-meta";
 const sender=document.createElement("span");sender.textContent=mine?displayName:"دانوش";
 const time=document.createElement("span");time.textContent=new Date().toLocaleTimeString("fa-IR",{hour:"2-digit",minute:"2-digit"});
 meta.append(sender,time);
 const bubble=document.createElement("div");bubble.className="message-bubble";bubble.textContent=text;
 msg.append(meta,bubble);$("messages").appendChild(msg);$("messages").scrollTop=$("messages").scrollHeight;
}
$("chatForm").addEventListener("submit",event=>{event.preventDefault();const input=$("messageInput"),text=input.value.trim();if(!text)return;addMessage(text,true);input.value="";input.focus()});

async function startMedia(){
 if(!navigator.mediaDevices?.getUserMedia){notify("برای دوربین از HTTPS یا localhost استفاده کن.");return}
 let videoTrack=null,audioTrack=null;
 try{const s=await navigator.mediaDevices.getUserMedia({video:true,audio:false});videoTrack=s.getVideoTracks()[0]||null}catch(e){console.warn("Camera:",e)}
 try{const s=await navigator.mediaDevices.getUserMedia({video:false,audio:true});audioTrack=s.getAudioTracks()[0]||null}catch(e){console.warn("Microphone:",e)}
 if(localStream)localStream.getTracks().forEach(t=>t.stop());
 localStream=new MediaStream();
 if(videoTrack)localStream.addTrack(videoTrack);
 if(audioTrack)localStream.addTrack(audioTrack);
 cameraOn=!!videoTrack;micOn=!!audioTrack;
 if(cameraOn){$("localVideo").srcObject=localStream;$("localVideo").hidden=false;$("placeholder").hidden=true;try{await $("localVideo").play()}catch(e){console.warn(e)}}
 else{$("localVideo").hidden=true;$("placeholder").hidden=false}
 $("cameraBtn").classList.toggle("off",!cameraOn);$("micBtn").classList.toggle("off",!micOn);
 setIcon($("cameraBtn"),cameraOn?"i-video":"i-video-off");setIcon($("micBtn"),micOn?"i-mic":"i-mic-off");
 updateStatus();
 notify(cameraOn||micOn?"رسانه‌های در دسترس فعال شدند.":"به دوربین یا میکروفون دسترسی داده نشد.");
}
$("startBtn").addEventListener("click",startMedia);
$("cameraBtn").addEventListener("click",async()=>{
 if(!localStream){await startMedia();return}
 const track=localStream.getVideoTracks()[0];
 if(!track){notify("دوربین در دسترس نیست. مجوز دوربین را بررسی کن.");return}
 cameraOn=!cameraOn;track.enabled=cameraOn;
 $("cameraBtn").classList.toggle("off",!cameraOn);setIcon($("cameraBtn"),cameraOn?"i-video":"i-video-off");
 $("placeholder").hidden=cameraOn||!!screenStream;$("localVideo").hidden=!cameraOn&&!screenStream;updateStatus();
});
$("micBtn").addEventListener("click",async()=>{
 if(!localStream){await startMedia();return}
 const track=localStream.getAudioTracks()[0];
 if(!track){notify("میکروفون در دسترس نیست. مجوز میکروفون را بررسی کن.");return}
 micOn=!micOn;track.enabled=micOn;
 $("micBtn").classList.toggle("off",!micOn);setIcon($("micBtn"),micOn?"i-mic":"i-mic-off");updateStatus();
});
async function stopScreen(){
 if(screenStream){screenStream.getTracks().forEach(t=>t.stop());screenStream=null}
 $("screenBtn").classList.remove("active");
 $("localVideo").srcObject=localStream;
 $("localVideo").hidden=!cameraOn;
 $("placeholder").hidden=cameraOn;
}
$("screenBtn").addEventListener("click",async()=>{
 if(screenStream){stopScreen();return}
 if(!navigator.mediaDevices?.getDisplayMedia){notify("اشتراک صفحه در این مرورگر پشتیبانی نمی‌شود.");return}
 try{
  screenStream=await navigator.mediaDevices.getDisplayMedia({video:true});
  $("localVideo").srcObject=screenStream;$("localVideo").hidden=false;$("placeholder").hidden=true;
  $("screenBtn").classList.add("active");
  screenStream.getVideoTracks()[0].addEventListener("ended",stopScreen,{once:true});
  notify("اشتراک صفحه فعال شد.");
 }catch(e){if(e.name!=="NotAllowedError")notify("اشتراک صفحه انجام نشد.")}
});
$("endBtn").addEventListener("click",()=>{
 if(screenStream)screenStream.getTracks().forEach(t=>t.stop());
 if(localStream)localStream.getTracks().forEach(t=>t.stop());
 localStream=null;screenStream=null;cameraOn=false;micOn=false;
 $("localVideo").srcObject=null;$("localVideo").hidden=true;$("placeholder").hidden=false;
 $("cameraBtn").classList.remove("off");$("micBtn").classList.remove("off");$("screenBtn").classList.remove("active");
 setIcon($("cameraBtn"),"i-video");setIcon($("micBtn"),"i-mic");updateStatus();notify("رسانه‌ها متوقف شدند.");
});
async function copyText(text){
 try{await navigator.clipboard.writeText(text);notify("کپی شد!")}
 catch{const ta=document.createElement("textarea");ta.value=text;document.body.appendChild(ta);ta.select();document.execCommand("copy");ta.remove();notify("کپی شد!")}
}
$("copyRoom").addEventListener("click",()=>copyText(roomCode));
$("copyLink").addEventListener("click",()=>copyText(location.href));
$("connectionInfo").addEventListener("click",()=>notify("تماس بین دستگاه‌ها هنوز راه‌اندازی نشده است."));
updateIdentity();updateStatus();
</script>
</body>
</html>
