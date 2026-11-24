learn-chat/
├── index.html
├── style.css
├── app.js
├── manifest.json
├── service-worker.js
├── icon-192.png   (ستنشئه لاحقًا)
└── icon-512.png   (ستنشئه لاحقًا)* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
body {
  font-family: 'Segoe UI', 'Tahoma', sans-serif;
  background: linear-gradient(135deg, #FFF0F5, #FFE4EC);
  color: #4A2C3A;
  min-height: 100vh;
  overflow-x: hidden;
}
.hidden { display: none !important; }
.muted { color: #B08A9A; font-size: 13px; }

/* شاشة البداية */
.splash {
  position: fixed; inset: 0; background: linear-gradient(160deg, #FFB6C1, #FF69B4);
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  color: white; z-index: 999; transition: opacity 0.5s;
}
.splash-avatar { font-size: 90px; animation: bounce 1.5s infinite; }
.splash h1 { font-size: 32px; margin-top: 15px; }
.splash p { font-size: 16px; opacity: 0.9; margin-top: 5px; }
@keyframes bounce { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-15px)} }

/* التطبيق */
.app { padding: 0 0 80px 0; max-width: 500px; margin: 0 auto; }
.page { display: none; padding: 16px; }
.page.active { display: block; animation: fadeIn 0.3s; }
@keyframes fadeIn { from{opacity:0;transform:translateY(8px)} to{opacity:1;transform:translateY(0)} }

.header { text-align: center; padding: 20px 0 15px; }
.header h2 { font-size: 24px; color: #D6336C; }
.header p { color: #B08A9A; margin-top: 4px; font-size: 14px; }

/* بطاقة المعلمة */
.teacher-card {
  background: white; border-radius: 24px; padding: 24px;
  box-shadow: 0 6px 20px rgba(255,105,180,0.15);
  text-align: center; margin-bottom: 16px;
}
.ikram-avatar {
  width: 110px; height: 110px; border-radius: 50%;
  background: linear-gradient(135deg, #FFB6C1, #FF69B4);
  display: flex; align-items: center; justify-content: center;
  font-size: 55px; margin: 0 auto 12px;
  box-shadow: 0 4px 15px rgba(255,105,180,0.4);
}

/* الأزرار */
.btn {
  background: linear-gradient(135deg, #FFB6C1, #FF69B4);
  color: white; border: none; padding: 13px 24px;
  border-radius: 30px; font-size: 15px; font-weight: bold;
  cursor: pointer; margin: 6px 4px; width: 100%;
  transition: transform 0.15s;
}
.btn:active { transform: scale(0.97); }
.btn.danger { background: linear-gradient(135deg, #FF8FA3, #D6336C); }

/* الإحصائيات */
.stats-card {
  display: grid; grid-template-columns: repeat(3,1fr); gap: 10px;
  background: white; border-radius: 20px; padding: 16px;
  box-shadow: 0 4px 12px rgba(255,105,180,0.1);
}
.stats-card > div { text-align: center; }
.stats-card strong { display: block; font-size: 22px; color: #D6336C; }
.stats-card span { font-size: 11px; color: #B08A9A; }

/* بطاقات المستويات */
.level-card {
  background: white; border-radius: 18px; padding: 18px;
  margin-bottom: 12px; cursor: pointer;
  box-shadow: 0 3px 12px rgba(255,105,180,0.12);
  transition: transform 0.15s;
  border-right: 5px solid #FFB6C1;
}
.level-card:active { transform: scale(0.98); }
.level-card h3 { color: #D6336C; font-size: 16px; margin-bottom: 4px; }
.level-card p { color: #B08A9A; font-size: 13px; }

/* المفردات */
.vocab-list { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.vocab-item {
  background: white; border-radius: 15px; padding: 14px;
  text-align: center; box-shadow: 0 3px 10px rgba(255,105,180,0.1);
  cursor: pointer;
}
.vocab-item:active { background: #FFF0F5; }
.vocab-item .en { font-weight: bold; color: #D6336C; font-size: 16px; }
.vocab-item .ar { font-size: 13px; color: #7A5A6A; margin-top: 3px; }
.vocab-item .ex { font-size: 11px; color: #B08A9A; margin-top: 5px; font-style: italic; }

/* المحادثة */
.chat-box {
  background: white; border-radius: 20px; padding: 16px;
  min-height: 300px; max-height: 55vh; overflow-y: auto;
  margin-bottom: 12px; box-shadow: 0 4px 12px rgba(255,105,180,0.1);
}
.msg { margin-bottom: 12px; padding: 10px 14px; border-radius: 16px; max-width: 80%; font-size: 14px; line-height: 1.5; }
.msg.user { background: #FFB6C1; color: white; margin-left: auto; border-bottom-left-radius: 4px; }
.msg.bot { background: #FFF0F5; color: #4A2C3A; margin-right: auto; border-bottom-right-radius: 4px; }
.msg.typing { color: #B08A9A; font-style: italic; }

.chat-input { display: flex; gap: 8px; align-items: center; }
.chat-input input {
  flex: 1; padding: 12px 16px; border-radius: 24px;
  border: 2px solid #FFD1DC; font-size: 14px; outline: none;
}
.chat-input input:focus { border-color: #FF69B4; }
.mic-btn, .send-btn {
  width: 46px; height: 46px; border-radius: 50%; border: none;
  background: linear-gradient(135deg, #FFB6C1, #FF69B4);
  color: white; font-size: 18px; cursor: pointer; flex-shrink: 0;
}
.mic-btn.recording { animation: pulse 1s infinite; }
@keyframes pulse { 0%,100%{box-shadow:0 0 0 0 rgba(255,105,180,0.6)} 50%{box-shadow:0 0 0 12px rgba(255,105,180,0)} }

/* شريط التنقل */
.nav {
  position: fixed; bottom: 0; left: 0; right: 0;
  background: white; display: flex; justify-content: space-around;
  padding: 8px 0; box-shadow: 0 -3px 15px rgba(255,105,180,0.15);
  z-index: 100; max-width: 500px; margin: 0 auto;
}
.nav-item {
  display: flex; flex-direction: column; align-items: center;
  font-size: 11px; color: #B08A9A; cursor: pointer; padding: 4px 8px;
  text-decoration: none;
}
.nav-item.active { color: #D6336C; font-weight: bold; }
.nav-item span { margin-top: 2px; }

/* النافذة المنبثقة */
.modal {
  position: fixed; inset: 0; background: rgba(0,0,0,0.4);
  display: flex; align-items: center; justify-content: center;
  z-index: 200; padding: 20px;
}
.modal-content {
  background: white; border-radius: 24px; padding: 24px;
  max-width: 400px; width: 100%; max-height: 80vh; overflow-y: auto;
  position: relative;
}
.modal-content .close {
  position: absolute; top: 12px; left: 12px; background: none;
  border: none; font-size: 20px; color: #B08A9A; cursor: pointer;
}
.modal-content h3 { color: #D6336C; margin-bottom: 14px; }
.lesson-item {
  background: #FFF0F5; border-radius: 12px; padding: 12px;
  margin-bottom: 8px; cursor: pointer; font-size: 14px;
}
.lesson-item:active { background: #FFE4EC; }
.lesson-item.done { opacity: 0.6; text-decoration: line-through; }<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="theme-color" content="#FFB6C1">
<title>Learn Chat – تعلم وتحدث</title>
<link rel="manifest" href="manifest.json">
<link rel="stylesheet" href="style.css">
</head>
<body>

<!-- شاشة البداية -->
<div id="splash" class="splash">
  <div class="splash-avatar">👩‍🏫</div>
  <h1>Learn Chat</h1>
  <p>معلمتك إكرام</p>
</div>

<!-- التطبيق الرئيسي -->
<div id="app" class="app hidden">

  <!-- الصفحة الرئيسية -->
  <section id="page-home" class="page active">
    <header class="header">
      <h2>مرحبًا بك 💕</h2>
      <p>أنا إكرام، معلمتك الذكية</p>
    </header>
    <div class="teacher-card">
      <div class="ikram-avatar">👩‍🏫</div>
      <h3>إكرام</h3>
      <p class="muted">اسأليني أي شيء عن الإنجليزية</p>
      <button class="btn" onclick="speak('مرحباً بك! أنا إكرام، معلمتك. هل أنت مستعد لتعلم الإنجليزية؟')">🔊 اسمعي إكرام</button>
      <button class="btn" onclick="go('chat')">💬 ابدئي المحادثة</button>
    </div>
    <div class="stats-card">
      <div><strong id="stat-progress">0%</strong><span>التقدم</span></div>
      <div><strong id="stat-lessons">0</strong><span>دروس مكتملة</span></div>
      <div><strong id="stat-words">0</strong><span>كلمات محفوظة</span></div>
    </div>
  </section>

  <!-- صفحة التعلم -->
  <section id="page-learn" class="page">
    <header class="header"><h2>📚 التعلم</h2></header>
    <div class="level-card" onclick="openLevel(1)">
      <h3>المستوى 1: المبتدئ</h3>
      <p>الحروف، الأرقام، الكلمات الأساسية</p>
    </div>
    <div class="level-card" onclick="openLevel(2)">
      <h3>المستوى 2: تحسين النطق</h3>
      <p>نطق الكلمات والجمل + القواعد</p>
    </div>
    <div class="level-card" onclick="openLevel(3)">
      <h3>المستوى 3: المحادثة والطلاقة</h3>
      <p>محادثات ومواقف يومية</p>
    </div>
  </section>

  <!-- صفحة المفردات -->
  <section id="page-vocab" class="page">
    <header class="header"><h2>📖 المفردات</h2></header>
    <div id="vocab-list" class="vocab-list"></div>
  </section>

  <!-- صفحة المحادثة -->
  <section id="page-chat" class="page">
    <header class="header"><h2>💬 المحادثة مع إكرام</h2></header>
    <div id="chat-box" class="chat-box"></div>
    <div class="chat-input">
      <button class="mic-btn" onclick="startListening()">🎤</button>
      <input id="chat-input" type="text" placeholder="اكتبي رسالتك..." onkeypress="if(event.key==='Enter')sendText()">
      <button class="send-btn" onclick="sendText()">➤</button>
    </div>
  </section>

  <!-- صفحة الملف الشخصي -->
  <section id="page-profile" class="page">
    <header class="header"><h2>👤 الملف الشخصي</h2></header>
    <div class="teacher-card">
      <div class="ikram-avatar">👩‍🏫</div>
      <h3>إكرام</h3>
      <p class="muted">معلمتك الذكية</p>
    </div>
    <div class="stats-card">
      <div><strong id="profile-progress">0%</strong><span>التقدم</span></div>
      <div><strong id="profile-lessons">0</strong><span>دروس</span></div>
      <div><strong id="profile-words">0</strong><span>كلمات</span></div>
    </div>
    <button class="btn danger" onclick="resetProgress()">🔄 إعادة تعيين التقدم</button>
  </section>

  <!-- شريط التنقل -->
  <nav class="nav">
    <a onclick="go('home')" class="nav-item active" data-page="home">🏠<span>الرئيسية</span></a>
    <a onclick="go('learn')" class="nav-item" data-page="learn">📚<span>التعلم</span></a>
    <a onclick="go('vocab')" class="nav-item" data-page="vocab">📖<span>المفردات</span></a>
    <a onclick="go('chat')" class="nav-item" data-page="chat">💬<span>المحادثة</span></a>
    <a onclick="go('profile')" class="nav-item" data-page="profile">👤<span>الملف</span></a>
  </nav>
</div>

<!-- نافذة المستوى -->
<div id="level-modal" class="modal hidden">
  <div class="modal-content">
    <button class="close" onclick="closeLevel()">✕</button>
    <h3 id="level-title"></h3>
    <div id="level-content"></div>
  </div>
</div>

<script src="app.js"></script>
</body>
</html>// ====== الإعدادات ======
const AI_API_KEY = ''; // ضع مفتاح Groq المجاني هنا (اختياري)
const AI_MODEL = 'llama-3.1-8b-instant';
const AI_URL = 'https://api.groq.com/openai/v1/chat/completions';

// ====== البيانات ======
const VOCAB = [
  { en: 'Hello', ar: 'مرحبًا', ex: 'Hello, how are you?' },
  { en: 'Thank you', ar: 'شكرًا', ex: 'Thank you for your help.' },
  { en: 'Good morning', ar: 'صباح الخير', ex: 'Good morning, teacher.' },
  { en: 'Apple', ar: 'تفاحة', ex: 'I eat an apple.' },
  { en: 'Book', ar: 'كتاب', ex: 'This is my book.' },
  { en: 'Water', ar: 'ماء', ex: 'I drink water.' },
  { en: 'Family', ar: 'عائلة', ex: 'I love my family.' },
  { en: 'Friend', ar: 'صديق', ex: 'She is my friend.' },
  { en: 'Teacher', ar: 'معلمة', ex: 'She is a teacher.' },
  { en: 'School', ar: 'مدرسة', ex: 'I go to school.' },
  { en: 'Beautiful', ar: 'جميل', ex: 'What a beautiful day!' },
  { en: 'Happy', ar: 'سعيد', ex: 'I am happy today.' }
];

const LEVELS = {
  1: { title: 'المستوى 1: المبتدئ', lessons: ['الحروف A-Z', 'الأرقام 1-20', 'التحيات', 'الألوان', 'أفراد الأسرة'] },
  2: { title: 'المستوى 2: تحسين النطق', lessons: ['نطق الحروف', 'نطق الكلمات', 'الجمل والعبارات', 'قواعد: الأزمنة', 'قواعد: حروف الجر'] },
  3: { title: 'المستوى 3: المحادثة', lessons: ['التعارف', 'في المطعم', 'في المطار', 'التسوق', 'في العمل'] }
};

// ====== الحالة ======
let state = JSON.parse(localStorage.getItem('learnchat_state') || '{"lessons":[],"words":[],"level":1}');
function saveState() { localStorage.setItem('learnchat_state', JSON.stringify(state)); updateStats(); }

// ====== التنقل ======
function go(page) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-' + page).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.querySelector(`.nav-item[data-page="${page}"]`).classList.add('active');
  window.scrollTo(0,0);
}

// ====== الصوت: نطق ======
function speak(text, lang = 'ar-SA') {
  if (!('speechSynthesis' in window)) { alert('النطق غير مدعوم'); return; }
  speechSynthesis.cancel();
  const u = new SpeechSynthesisUtterance(text);
  u.lang = lang; u.rate = 0.9;
  speechSynthesis.speak(u);
}

// ====== الصوت: استماع ======
let recognition = null;
function startListening() {
  const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
  if (!SR) { alert('التعرف على الصوت غير مدعوم في هذا المتصفح'); return; }
  if (recognition) recognition.stop();
  recognition = new SR();
  recognition.lang = 'en-US';
  recognition.interimResults = false;
  const mic = document.querySelector('.mic-btn');
  mic.classList.add('recording');
  recognition.onresult = (e) => {
    mic.classList.remove('recording');
    sendMessage(e.results[0][0].transcript);
  };
  recognition.onerror = () => mic.classList.remove('recording');
  recognition.onend = () => mic.classList.remove('recording');
  recognition.start();
}

// ====== المحادثة ======
function addMsg(text, cls) {
  const box = document.getElementById('chat-box');
  const div = document.createElement('div');
  div.className = 'msg ' + cls;
  div.textContent = text;
  box.appendChild(div);
  box.scrollTop = box.scrollHeight;
  return div;
}

async function sendMessage(text) {
  if (!text.trim()) return;
  addMsg(text, 'user');
  document.getElementById('chat-input').value = '';
  const typing = addMsg('إكرام تكتب...', 'bot typing');

  let reply;
  if (AI_API_KEY) {
    try {
      const res = await fetch(AI_URL, {
        method: 'POST',
        headers: { 'Authorization': `Bearer ${AI_API_KEY}`, 'Content-Type': 'application/json' },
        body: JSON.stringify({
          model: AI_MODEL,
          messages: [
            { role: 'system', content: 'أنت إكرام، معلمة لغة إنجليزية لطيفة وأنيقة. تشرحين بالعربية والإنجليزية وتصححين الأخطاء بأسلوب مبسط.' },
            { role: 'user', content: text }
          ]
        })
      });
      const data = await res.json();
      reply = data.choices?.[0]?.message?.content || 'عذرًا، حدث خطأ.';
    } catch (e) { reply = 'تعذر الاتصال بالذكاء الاصطناعي.'; }
  } else {
    reply = getLocalReply(text);
  }

  typing.remove();
  addMsg(reply, 'bot');
  speak(reply);
}

function sendText() {
  sendMessage(document.getElementById('chat-input').value);
}

// رد محلي بدون API
function getLocalReply(t) {
  const s = t.toLowerCase();
  if (/hello|hi|مرحبا/.test(s)) return 'Hello! كيف حالك اليوم؟';
  if (/how are you|كيف حالك/.test(s)) return 'I am fine, thank you! وأنت؟';
  if (/name|اسم/.test(s)) return 'اسمي إكرام، معلمتك.';
  if (/apple|تفاح/.test(s)) return 'Apple تعني تفاحة. Example: I eat an apple.';
  if (/\?|؟/.test(s)) return 'سؤال جيد! دعيني أشرح: ' + t;
  return 'أحسنت! كرري بعدي: ' + t;
}

// ====== المفردات ======
function renderVocab() {
  const list = document.getElementById('vocab-list');
  list.innerHTML = '';
  VOCAB.forEach((v, i) => {
    const div = document.createElement('div');
    div.className = 'vocab-item';
    div.innerHTML = `<div class="en">${v.en}</div><div class="ar">${v.ar}</div><div class="ex">${v.ex}</div>`;
    div.onclick = () => {
      speak(v.en, 'en-US');
      if (!state.words.includes(v.en)) { state.words.push(v.en); saveState(); }
    };
    list.appendChild(div);
  });
}

// ====== المستويات ======
function openLevel(n) {
  const lv = LEVELS[n];
  document.getElementById('level-title').textContent = lv.title;
  const content = document.getElementById('level-content');
  content.innerHTML = '';
  lv.lessons.forEach((lesson, i) => {
    const id = `L${n}-${i}`;
    const div = document.createElement('div');
    div.className = 'lesson-item' + (state.lessons.includes(id) ? ' done' : '');
    div.innerHTML = `📘 ${lesson}`;
    div.onclick = () => {
      if (!state.lessons.includes(id)) { state.lessons.push(id); saveState(); }
      speak(lesson);
      div.classList.add('done');
      addMsg('لنبدأ الدرس: ' + lesson, 'bot');
      go('chat');
      closeLevel();
    };
    content.appendChild(div);
  });
  document.getElementById('level-modal').classList.remove('hidden');
}
function closeLevel() { document.getElementById('level-modal').classList.add('hidden'); }

// ====== الإحصائيات ======
function updateStats() {
  const totalLessons = 15;
  const pct = Math.round((state.lessons.length / totalLessons) * 100);
  ['stat-progress','profile-progress'].forEach(id => { const el = document.getElementById(id); if (el) el.textContent = pct + '%'; });
  ['stat-lessons','profile-lessons'].forEach(id => { const el = document.getElementById(id); if (el) el.textContent = state.lessons.length; });
  ['stat-words','profile-words'].forEach(id => { const el = document.getElementById(id); if (el) el.textContent = state.words.length; });
}

function resetProgress() {
  if (confirm('هل تريدين إعادة تعيين كل التقدم؟')) {
    state = { lessons: [], words: [], level: 1 };
    saveState(); renderVocab(); alert('تمت إعادة التعيين');
  }
}

// ====== التهيئة ======
window.addEventListener('load', () => {
  setTimeout(() => {
    document.getElementById('splash').style.opacity = '0';
    setTimeout(() => {
      document.getElementById('splash').classList.add('hidden');
      document.getElementById('app').classList.remove('hidden');
    }, 500);
  }, 1500);

  renderVocab();
  updateStats();

  // تسجيل Service Worker
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('service-worker.js').catch(() => {});
  }
});const CACHE = 'learnchat-v1';
const ASSETS = ['./', './index.html', './style.css', './app.js', './manifest.json', './icon-192.png', './icon-512.png'];

self.addEventListener('install', e => {
  e.waitUntil(caches.open(CACHE).then(c => c.addAll(ASSETS)).catch(() => {}));
  self.skipWaiting();
});
self.addEventListener('activate', e => {
  e.waitUntil(caches.keys().then(keys => Promise.all(keys.filter(k => k !== CACHE).map(k => caches.delete(k)))));
  self.clients.claim();
});
self.addEventListener('fetch', e => {
  e.respondWith(caches.match(e.request).then(r => r || fetch(e.request).catch(() => caches.match('./index.html'))));
});{
  "name": "Learn Chat – تعلم وتحدث",
  "short_name": "Learn Chat",
  "start_url": "./index.html",
  "display": "standalone",
  "background_color": "#FFF0F5",
  "theme_color": "#FFB6C1",
  "dir": "rtl",
  "lang": "ar",
  "description": "تطبيق تعليمي تفاعلي مدعوم بالذكاء الاصطناعي",
  "icons": [
    { "src": "icon-192.png", "sizes": "192x192", "type": "image/png", "purpose": "any maskable" },
    { "src": "icon-512.png", "sizes": "512x512", "type": "image/png", "purpose": "any maskable" }
  ]
}
