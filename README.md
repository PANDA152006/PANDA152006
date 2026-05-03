
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { background: transparent; }

  .banner {
    background: #0d1117;
    border-radius: 16px;
    overflow: hidden;
    border: 1px solid #1e2d1e;
    position: relative;
  }

  .scanlines {
    position: absolute;
    inset: 0;
    background: repeating-linear-gradient(
      to bottom,
      transparent,
      transparent 3px,
      rgba(0,255,65,0.015) 3px,
      rgba(0,255,65,0.015) 4px
    );
    pointer-events: none;
    z-index: 10;
  }

  .header-bar {
    background: #0a0f0a;
    padding: 8px 16px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-bottom: 1px solid #1e2d1e;
  }
  .dot { width: 10px; height: 10px; border-radius: 50%; }
  .d1 { background: #ff5f57; }
  .d2 { background: #febc2e; }
  .d3 { background: #28c840; }
  .htitle { color: #3a5a3a; font-size: 11px; font-family: monospace; margin-left: 6px; }

  .main-content {
    display: flex;
    align-items: stretch;
    min-height: 320px;
  }

  /* LEFT: panda scene */
  .panda-zone {
    width: 260px;
    flex-shrink: 0;
    background: #080d08;
    position: relative;
    display: flex;
    align-items: flex-end;
    justify-content: center;
    padding-bottom: 0;
    border-right: 1px solid #1e2d1e;
    overflow: hidden;
  }

  .desk {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 50px;
    background: #0f1a0f;
    border-top: 2px solid #1e2d1e;
  }

  .monitor {
    position: absolute;
    bottom: 50px;
    left: 50%;
    transform: translateX(-50%);
    width: 110px;
  }
  .monitor-screen {
    background: #0d1117;
    border: 2px solid #00FF41;
    border-radius: 6px;
    height: 68px;
    padding: 6px;
    overflow: hidden;
    box-shadow: 0 0 14px rgba(0,255,65,0.3);
    position: relative;
  }
  .monitor-stand {
    width: 18px;
    height: 10px;
    background: #1e2d1e;
    margin: 0 auto;
  }
  .monitor-base {
    width: 36px;
    height: 4px;
    background: #1e2d1e;
    margin: 0 auto;
    border-radius: 2px;
  }

  .code-lines { font-family: monospace; font-size: 7px; line-height: 1.4; }
  .cl { display: block; white-space: nowrap; overflow: hidden; }
  .ckw  { color: #ff7b72; }
  .cfn  { color: #79c0ff; }
  .cstr { color: #a5d6ff; }
  .cval { color: #ffa657; }
  .ccmt { color: #3a5a3a; }
  .cop  { color: #00FF41; }

  @keyframes blink  { 0%,49%{opacity:1} 50%,100%{opacity:0} }
  @keyframes typing { from{width:0} to{width:100%} }
  @keyframes bobHead { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-4px)} }
  @keyframes blinkEye { 0%,90%,100%{scaleY:1} 95%{scaleY:0.1} }
  @keyframes tailWag { 0%,100%{transform:rotate(-10deg)} 50%{transform:rotate(10deg)} }
  @keyframes typingCursor { 0%,49%{opacity:1} 50%,100%{opacity:0} }
  @keyframes float { 0%,100%{transform:translateY(0px)} 50%{transform:translateY(-6px)} }
  @keyframes glitch { 0%,100%{clip-path:inset(0)} 92%{clip-path:inset(40% 0 50% 0); transform:translateX(-3px)} 94%{clip-path:inset(20% 0 70% 0); transform:translateX(3px)} 96%{clip-path:inset(0)} }
  @keyframes scanH { 0%{top:-10%} 100%{top:110%} }
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.5} }

  .panda-svg {
    position: absolute;
    bottom: 44px;
    left: 50%;
    transform: translateX(-50%);
    animation: float 3s ease-in-out infinite;
  }

  .scan-line {
    position: absolute;
    left: 0; right: 0;
    height: 2px;
    background: rgba(0,255,65,0.15);
    animation: scanH 4s linear infinite;
    pointer-events: none;
  }

  .coffee {
    position: absolute;
    bottom: 52px;
    right: 18px;
  }

  /* RIGHT: content */
  .right-zone {
    flex: 1;
    padding: 24px 28px;
    display: flex;
    flex-direction: column;
    gap: 16px;
    background: #0d1117;
  }

  .glitch-title {
    font-family: monospace;
    font-size: 28px;
    font-weight: 700;
    color: #00FF41;
    line-height: 1.1;
    position: relative;
    animation: glitch 8s infinite;
    text-shadow: 0 0 20px rgba(0,255,65,0.4);
    letter-spacing: -0.5px;
  }
  .glitch-title span { color: #ffffff; }

  .subtitle {
    font-family: monospace;
    font-size: 12px;
    color: #3a5a3a;
    letter-spacing: 2px;
    text-transform: uppercase;
  }

  .typing-line {
    font-family: monospace;
    font-size: 13px;
    color: #8b949e;
    display: flex;
    align-items: center;
    gap: 6px;
    min-height: 20px;
  }
  .typing-prompt { color: #00FF41; }
  .typing-text { color: #c9d1d9; }
  .cursor { display: inline-block; width: 8px; height: 14px; background: #00FF41; animation: blink 1s infinite; vertical-align: middle; }

  .stats-row {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
  }
  .stat-chip {
    background: #0a0f0a;
    border: 1px solid #1e2d1e;
    border-radius: 8px;
    padding: 8px 14px;
    font-family: monospace;
    font-size: 11px;
    color: #3a5a3a;
  }
  .stat-chip strong { color: #00FF41; font-size: 16px; display: block; }

  .clock-row {
    background: #080d08;
    border: 1px solid #1e2d1e;
    border-radius: 10px;
    padding: 10px 16px;
    font-family: monospace;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .clock-icon { color: #00FF41; font-size: 16px; }
  .clock-time { color: #00FF41; font-size: 20px; font-weight: 700; letter-spacing: 2px; }
  .clock-date { color: #3a5a3a; font-size: 11px; }
  .clock-ist  { color: #1e4a1e; font-size: 10px; letter-spacing: 1px; margin-top: 2px; }

  .badge-row { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 4px; }
  .badge {
    font-family: monospace;
    font-size: 10px;
    padding: 3px 10px;
    border-radius: 20px;
    border: 1px solid;
    letter-spacing: 0.5px;
  }
  .b-green { color: #00FF41; border-color: #00FF41; background: rgba(0,255,65,0.05); }
  .b-blue  { color: #58a6ff; border-color: #58a6ff; background: rgba(88,166,255,0.05); }
  .b-amber { color: #ffa657; border-color: #ffa657; background: rgba(255,166,87,0.05); }
  .b-red   { color: #ff7b72; border-color: #ff7b72; background: rgba(255,123,114,0.05); }

  .bottom-bar {
    background: #080d08;
    padding: 8px 20px;
    border-top: 1px solid #1e2d1e;
    display: flex;
    align-items: center;
    gap: 16px;
    font-family: monospace;
    font-size: 10px;
    color: #1e4a1e;
  }
  .bb-item { display: flex; align-items: center; gap: 5px; }
  .bb-dot  { width: 6px; height: 6px; border-radius: 50%; background: #00FF41; animation: pulse 2s infinite; }
</style>

<div class="banner">
  <div class="scanlines"></div>
  <div class="header-bar">
    <div class="dot d1"></div>
    <div class="dot d2"></div>
    <div class="dot d3"></div>
    <span class="htitle">yash@panda152006 ~ profile.md</span>
  </div>

  <div class="main-content">
    <!-- PANDA ZONE -->
    <div class="panda-zone">
      <div class="scan-line"></div>

      <!-- Desk -->
      <div class="desk"></div>

      <!-- Monitor -->
      <div class="monitor">
        <div class="monitor-screen">
          <div class="code-lines">
            <span class="cl"><span class="ckw">def</span> <span class="cfn">build</span><span class="cop">()</span><span class="cop">:</span></span>
            <span class="cl">  <span class="cval">code</span> <span class="cop">=</span> <span class="cstr">[]</span></span>
            <span class="cl">  <span class="ckw">while</span> <span class="cval">True</span><span class="cop">:</span></span>
            <span class="cl">    <span class="cfn">commit</span><span class="cop">()</span></span>
            <span class="cl">    <span class="cfn">ship</span><span class="cop">()</span></span>
            <span class="cl"><span class="ccmt"># never stop</span></span>
          </div>
          <div style="position:absolute;bottom:4px;right:5px;width:4px;height:8px;background:#00FF41;animation:blink 1s infinite;"></div>
        </div>
        <div class="monitor-stand"></div>
        <div class="monitor-base"></div>
      </div>

      <!-- Coffee mug -->
      <div class="coffee">
        <svg width="26" height="30" viewBox="0 0 26 30">
          <rect x="3" y="12" width="18" height="16" rx="3" fill="#1a2a1a" stroke="#2a4a2a" stroke-width="1"/>
          <path d="M21 15 Q27 15 27 20 Q27 25 21 25" fill="none" stroke="#2a4a2a" stroke-width="1.5"/>
          <rect x="5" y="8" width="14" height="4" rx="2" fill="#0d1117"/>
          <path d="M9 6 Q10 2 11 6" fill="none" stroke="#1e4a1e" stroke-width="1" opacity="0.7"/>
          <path d="M13 5 Q14 1 15 5" fill="none" stroke="#1e4a1e" stroke-width="1" opacity="0.7"/>
          <text x="5" y="23" font-size="7" font-family="monospace" fill="#00FF41" opacity="0.8">{}</text>
        </svg>
      </div>

      <!-- PANDA SVG character -->
      <svg class="panda-svg" width="110" height="145" viewBox="0 0 110 145">
        <!-- Body -->
        <ellipse cx="55" cy="105" rx="32" ry="38" fill="#e8e8e8"/>
        <!-- Belly -->
        <ellipse cx="55" cy="112" rx="18" ry="22" fill="#d0d0d0"/>
        <!-- Legs -->
        <ellipse cx="40" cy="138" rx="10" ry="8" fill="#222"/>
        <ellipse cx="70" cy="138" rx="10" ry="8" fill="#222"/>
        <!-- Arms coding position -->
        <ellipse cx="22" cy="102" rx="9" ry="14" fill="#222" transform="rotate(-15 22 102)"/>
        <ellipse cx="88" cy="102" rx="9" ry="14" fill="#222" transform="rotate(15 88 102)"/>
        <!-- Paws on keyboard -->
        <ellipse cx="24" cy="116" rx="8" ry="6" fill="#e8e8e8"/>
        <ellipse cx="86" cy="116" rx="8" ry="6" fill="#e8e8e8"/>
        <!-- Head -->
        <ellipse cx="55" cy="60" rx="30" ry="28" fill="#e8e8e8"/>
        <!-- Ear patches (black) -->
        <ellipse cx="28" cy="38" rx="12" ry="12" fill="#222"/>
        <ellipse cx="82" cy="38" rx="12" ry="12" fill="#222"/>
        <!-- Ear inner -->
        <ellipse cx="28" cy="38" rx="7" ry="7" fill="#3a3a3a"/>
        <ellipse cx="82" cy="38" rx="7" ry="7" fill="#3a3a3a"/>
        <!-- Eye patches -->
        <ellipse cx="43" cy="58" rx="11" ry="10" fill="#222"/>
        <ellipse cx="67" cy="58" rx="11" ry="10" fill="#222"/>
        <!-- Eyes - glowing green -->
        <ellipse cx="43" cy="58" rx="6" ry="6" fill="#001a00"/>
        <ellipse cx="67" cy="58" rx="6" ry="6" fill="#001a00"/>
        <ellipse id="leye" cx="43" cy="58" rx="4" ry="4" fill="#00FF41"/>
        <ellipse id="reye" cx="67" cy="58" rx="4" ry="4" fill="#00FF41"/>
        <!-- Eye shine -->
        <circle cx="45" cy="56" r="1.5" fill="white" opacity="0.8"/>
        <circle cx="69" cy="56" r="1.5" fill="white" opacity="0.8"/>
        <!-- Nose -->
        <ellipse cx="55" cy="68" rx="5" ry="3.5" fill="#555"/>
        <!-- Mouth smile -->
        <path d="M48 74 Q55 80 62 74" fill="none" stroke="#888" stroke-width="1.5" stroke-linecap="round"/>
        <!-- Headphones -->
        <path d="M26 55 Q26 30 55 30 Q84 30 84 55" fill="none" stroke="#222" stroke-width="4" stroke-linecap="round"/>
        <rect x="20" y="52" width="10" height="12" rx="4" fill="#1a1a1a" stroke="#333" stroke-width="1"/>
        <rect x="80" y="52" width="10" height="12" rx="4" fill="#1a1a1a" stroke="#333" stroke-width="1"/>
        <!-- Green LED on headphones -->
        <circle cx="25" cy="58" r="2" fill="#00FF41" opacity="0.9"/>
        <circle cx="85" cy="58" r="2" fill="#00FF41" opacity="0.9"/>
        <!-- Tail -->
        <ellipse cx="87" cy="128" rx="8" ry="6" fill="#e8e8e8" style="transform-origin:87px 128px;animation:tailWag 2s ease-in-out infinite"/>
        <!-- Keyboard under paws -->
        <rect x="18" y="122" width="74" height="10" rx="3" fill="#111" stroke="#1e2d1e" stroke-width="1"/>
        <rect x="22" y="124" width="6" height="5" rx="1" fill="#1a2a1a"/>
        <rect x="31" y="124" width="6" height="5" rx="1" fill="#1a2a1a"/>
        <rect x="40" y="124" width="6" height="5" rx="1" fill="#1a2a1a"/>
        <rect x="49" y="124" width="6" height="5" rx="1" fill="#1a2a1a"/>
        <rect x="58" y="124" width="6" height="5" rx="1" fill="#1a2a1a"/>
        <rect x="67" y="124" width="6" height="5" rx="1" fill="#1a2a1a"/>
        <rect x="76" y="124" width="6" height="5" rx="1" fill="#1a2a1a"/>
      </svg>
    </div>

    <!-- RIGHT CONTENT ZONE -->
    <div class="right-zone">
      <div>
        <div class="subtitle">&gt; boot sequence complete</div>
        <div class="glitch-title">YASH DUTT<br><span>SHARMA</span></div>
      </div>

      <div class="typing-line">
        <span class="typing-prompt">~$</span>
        <span class="typing-text" id="typed-text"></span>
        <span class="cursor"></span>
      </div>

      <div class="clock-row">
        <span class="clock-icon">⧖</span>
        <div>
          <div class="clock-time" id="live-clock">--:--:--</div>
          <div class="clock-date" id="live-date">loading...</div>
          <div class="clock-ist">IST · UTC+5:30</div>
        </div>
        <div style="margin-left:auto;text-align:right">
          <div class="clock-date">UPES Dehradun</div>
          <div class="clock-ist" id="greeting">...</div>
        </div>
      </div>

      <div class="stats-row">
        <div class="stat-chip"><strong id="commits">--</strong>commits</div>
        <div class="stat-chip"><strong id="repos">--</strong>repos</div>
        <div class="stat-chip"><strong id="uptime">--</strong>days coding</div>
      </div>

      <div class="badge-row">
        <span class="badge b-green">Python</span>
        <span class="badge b-blue">React</span>
        <span class="badge b-amber">Flutter</span>
        <span class="badge b-red">FastAPI</span>
        <span class="badge b-green">OpenCV</span>
        <span class="badge b-blue">Django</span>
        <span class="badge b-amber">Three.js</span>
      </div>
    </div>
  </div>

  <div class="bottom-bar">
    <div class="bb-item"><div class="bb-dot"></div> ONLINE</div>
    <div class="bb-item">PANDA152006</div>
    <div class="bb-item">UPES DEHRADUN</div>
    <div style="margin-left:auto" id="bb-time">--:-- IST</div>
  </div>
</div>

<script>
const phrases = [
  "building stuff that matters...",
  "turning caffeine into code ☕",
  "debugging at 2am as usual...",
  "open to collabs & internships",
  "python · flutter · react · ML",
  "one commit at a time 🚀",
];
let pi = 0, ci = 0, deleting = false;

function typeWriter() {
  const el = document.getElementById('typed-text');
  const phrase = phrases[pi];
  if (!deleting) {
    el.textContent = phrase.slice(0, ci + 1);
    ci++;
    if (ci === phrase.length) { deleting = true; setTimeout(typeWriter, 1800); return; }
    setTimeout(typeWriter, 65);
  } else {
    el.textContent = phrase.slice(0, ci - 1);
    ci--;
    if (ci === 0) { deleting = false; pi = (pi + 1) % phrases.length; setTimeout(typeWriter, 300); return; }
    setTimeout(typeWriter, 30);
  }
}
typeWriter();

function tick() {
  const now = new Date(new Date().toLocaleString('en-US', { timeZone: 'Asia/Kolkata' }));
  const h = String(now.getHours()).padStart(2,'0');
  const m = String(now.getMinutes()).padStart(2,'0');
  const s = String(now.getSeconds()).padStart(2,'0');
  document.getElementById('live-clock').textContent = `${h}:${m}:${s}`;
  const days = ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
  const months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  document.getElementById('live-date').textContent = `${days[now.getDay()]}, ${now.getDate()} ${months[now.getMonth()]} ${now.getFullYear()}`;
  document.getElementById('bb-time').textContent = `${h}:${m} IST`;
  const hr = now.getHours();
  const g = hr < 5 ? '🌙 burning midnight oil' : hr < 12 ? '🌅 good morning' : hr < 17 ? '☀️ good afternoon' : hr < 21 ? '🌆 good evening' : '🌙 late night grind';
  document.getElementById('greeting').textContent = g;
  setTimeout(tick, 1000);
}
tick();

// animated counters
function animCount(id, target, suffix='') {
  let cur = 0;
  const step = Math.ceil(target / 40);
  const el = document.getElementById(id);
  const t = setInterval(() => {
    cur = Math.min(cur + step, target);
    el.textContent = cur + suffix;
    if (cur >= target) clearInterval(t);
  }, 40);
}
animCount('commits', 127);
animCount('repos', 18);
animCount('uptime', 312);
</script>
