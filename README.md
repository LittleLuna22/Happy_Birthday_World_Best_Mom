# Happy_Birthday_World_Best_Mom
🎀 Mom’s Birthday Website — A Heartfelt Digital Surprise  This project is a beautifully designed, interactive birthday website created as a heartfelt gift for my mother. It combines soft, dreamy aesthetics with emotional animations, cute bear illustrations, glitter effects, and a warm message that reflects love, gratitude, and appreciation.
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1.0" />
<title>Happy Birthday — World's Best Mom 💖</title>

<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">

<style>
  /* ========== THEME VARIABLES (pastel colors) ========== */
  :root{
    --bg1: #fdf5f7;        /* Very light pink */
    --bg2: #f0f8ff;        /* Very light blue */
    --accent: #ff69b4;     /* Hot Pink - for main focus */
    --accent-2: #87cefa;   /* Sky Blue */
    --card-bg: rgba(255,255,255,0.95);
    --text: #33334a;
    --muted: #66687a;
    --glass: rgba(255,255,255,0.7);
    --glitter: #fff9ff;
    --max-width: 980px;
    --font-head: 'Playfair Display', serif;
    --font-body: 'Poppins', system-ui, sans-serif;
  }

  /* Basic reset */
  *{box-sizing:border-box}
  html,body{height:100%; font-family:var(--font-body);}
  body{
    margin:0;
    color:var(--text);
    -webkit-font-smoothing:antialiased;
    background: linear-gradient(135deg,var(--bg1),var(--bg2));
    overflow-x:hidden;
    -webkit-touch-callout:none; -webkit-user-select:none; user-select:none;
    position:relative; /* for background animations */
  }

  /* Smooth fade on load */
  .app{opacity:0; animation:appFade 800ms ease forwards;}
  @keyframes appFade{to{opacity:1}}

  .container{max-width:var(--max-width); margin:0 auto; padding:28px;}

  /* Header / hero */
  .hero{
    min-height:80vh; /* Increased height */
    display:flex;
    gap:20px;
    align-items:center;
    justify-content:center;
    flex-direction:column;
    padding:36px 20px;
    position:relative;
    text-align:center;
  }
  
  h1{
    margin:0 0 12px 0;
    font-size: clamp(32px, 6vw, 60px);
    line-height:1.05;
    color:var(--accent);
    letter-spacing: -0.5px;
    text-shadow: 0 8px 20px rgba(255,105,180,0.18);
    font-family: var(--font-head);
  }
  .subtitle{
    color:var(--muted);
    margin:0 0 24px 0;
    font-weight:400;
    font-size:1.1rem;
    font-style: italic;
  }
  
  /* Card styles */
  .card{
    background:var(--card-bg);
    border-radius:24px; /* Softer radius */
    padding:20px;
    box-shadow: 0 12px 40px rgba(21,21,40,0.08);
    backdrop-filter: blur(8px);
    border: 1px solid rgba(255, 255, 255, 0.6);
  }

  .btn{
    background: linear-gradient(180deg,var(--accent), #e85d9a);
    color:white; border:0; border-radius:999px;
    padding:12px 24px; font-weight:600; cursor:pointer;
    box-shadow: 0 8px 25px rgba(255,105,180,0.3);
    transition: transform .18s ease, box-shadow .18s;
  }
  .btn:active{transform:translateY(2px)}
  .small{
    background:transparent; color:var(--accent); border:1px solid var(--accent); padding:10px 18px; border-radius:999px;
    transition: background 0.2s;
  }
  .small:hover{background:rgba(255, 105, 180, 0.05);}

  /* Sections */
  section{padding:50px 0}
  .section-title{font-size:1.2rem; color:var(--accent); margin:0 0 20px 0; font-weight:700; text-align:center; font-family:var(--font-head);}

  /* Timeline / story cards */
  .timeline{display:grid; grid-template-columns:repeat(auto-fit,minmax(250px,1fr)); gap:24px}
  .timeline .item{padding:20px; border-radius:20px; background:linear-gradient(180deg, rgba(255,255,255,0.85), rgba(255,255,255,0.7)); min-height:140px; position:relative; overflow:hidden}
  .timeline .item h3{margin:0 0 8px 0; font-size:1.1rem; color:#d86f92; font-family:var(--font-head);}
  .timeline .item p{margin:0; color:var(--muted); font-size:0.95rem; line-height:1.5}

  /* Gallery / slideshow */
  .slideshow{position:relative; border-radius:20px; overflow:hidden; min-height:300px; max-height:400px; width:100%;}
  .slides{display:flex; transition:transform .8s cubic-bezier(.2,.9,.18,1);}
  .slide{min-width:100%; flex-shrink:0; display:flex; align-items:center; justify-content:center; position:relative}
  /* Updated image rules for consistency/safety */
  .slide img{width:100%; height:auto; max-height:400px; object-fit:cover; display:block; opacity:0; transition:opacity 1.2s ease-in-out;} 
  .slide img.loaded{opacity:1;}
  .slideshow .controls{position:absolute; left:0; right:0; bottom:15px; display:flex; justify-content:center; gap:12px; z-index:10}
  .dot{width:12px;height:12px;border-radius:50%;background:rgba(255,255,255,0.7);box-shadow:0 2px 6px rgba(20,20,30,0.12);pointer-events:auto;cursor:pointer; transition:all 0.3s;}
  .dot.active{background:var(--accent); transform:scale(1.2);}

  /* Message reveal (slide-up) */
  .message-card{margin-top:20px; padding:25px; border-radius:20px; background:linear-gradient(180deg, rgba(255,250,255,1), rgba(255,240,250,0.9)); transform:translateY(30px); opacity:0; transition:all .8s cubic-bezier(.2,.9,.18,1)}
  .message-card.show{transform:translateY(0); opacity:1}
  .secret-message-content{white-space: pre-wrap; font-family: cursive; font-size: 0.95rem; line-height: 1.6; color:#7d3e51}


  /* Glitter effect (soft) */
  .glitter{
    position:fixed; inset:0; pointer-events:none; z-index:2;
    background-image: radial-gradient(circle at 15% 25%, rgba(255,255,255,0.5) 0px, rgba(255,255,255,0.0) 40px),
                      radial-gradient(circle at 75% 85%, rgba(255,250,255,0.45) 0px, rgba(255,250,255,0) 50px);
    mix-blend-mode:screen; opacity:0.8;
    animation:glitterMove 15s linear infinite;
  }
  @keyframes glitterMove{
    0%{transform:translateY(0) rotate(0deg)}
    50%{transform:translateY(-40px) rotate(5deg)}
    100%{transform:translateY(0) rotate(0deg)}
  }

  /* Floating Hearts/Flowers Animation */
  .animated-object {
    position: absolute;
    top: -10%;
    opacity: 0;
    animation: floatUp 15s linear infinite;
    font-size: 24px;
    pointer-events: none;
    z-index: 1;
  }
  @keyframes floatUp {
    0% { transform: translateY(0); opacity: 0; }
    10% { opacity: 1; }
    90% { opacity: 1; }
    100% { transform: translateY(-100vh); opacity: 0; }
  }
@keyframes floatUp {
    0% { transform: translateY(0); opacity: 0; }
    10% { opacity: 1; }
    90% { opacity: 1; }
    100% { transform: translateY(-100vh); opacity: 0; }
  }

  /* Hero Video Container */
  .video-container {
    width: clamp(280px, 60vw, 400px);
    height: clamp(280px, 60vw, 400px);
    border-radius: 50%; /* Circular video to match the vibe */
    overflow: hidden;
    position: relative;
    box-shadow: 0 0 40px rgba(255,105,180,0.4);
    background-color: white;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .video-container video {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }
  /* Fallback style if video doesn't load */
  .video-container:has(video:invalid){
    background-image: url('https://placehold.co/400x400/ffe4e1/ff69b4?text=Video+Placeholder+Unavailable');
    background-size: cover;
    background-position: center;
  }


  /* Hug Pop-up Modal */
  .modal {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(0, 0, 0, 0.6);
    display: none;
    align-items: center;
    justify-content: center;
    z-index: 9999;
    opacity: 0;
    transition: opacity 0.3s;
  }
  .modal.open {
    display: flex;
    opacity: 1;
  }
  .modal-content {
    background: var(--card-bg);
    padding: 20px;
    border-radius: 20px;
    text-align: center;
    box-shadow: 0 10px 50px rgba(0, 0, 0, 0.3);
    position: relative;
    transform: scale(0.8);
    transition: transform 0.3s cubic-bezier(0.68, -0.55, 0.27, 1.55);
  }
  .modal.open .modal-content {
    transform: scale(1);
  }
  .hug-image {
    width: 200px; height: 200px; margin-bottom: 10px;
    border-radius: 15px; /* Added border-radius for aesthetics */
  }
  .close-btn {
    position: absolute; top: 10px; right: 10px;
    background: none; border: none; font-size: 20px;
    cursor: pointer; color: var(--muted);
  }
  .heart-burst {
    position: absolute;
    width: 100%; height: 100%;
    top: 0; left: 0;
    overflow: hidden;
    pointer-events: none;
  }
  .burst-heart {
    position: absolute;
    font-size: 30px;
    opacity: 0;
    animation: burstAnimate 1s ease-out forwards;
  }
  @keyframes burstAnimate {
    0% { opacity: 1; transform: translate(0, 0) scale(0); }
    100% { opacity: 0; transform: translate(var(--x), var(--y)) scale(1.5); }
  }

  /* Subtle entrance animations */
  [data-animate]{opacity:0; transform:translateY(25px); transition:all .8s cubic-bezier(.2,.9,.18,1);}
  [data-animate].in{opacity:1; transform:translateY(0)}
</style>
</head>

<body>
<div class="app">
  <div class="glitter"></div>
  <div class="animated-background" id="animatedBackground"></div>

  <div class="container">

    <header class="hero">
      <div class="video-container" data-animate>
        <!-- 
          *** 1. VIDEO FILE PATH ***
          Replace 'YOUR_VIDEO_FILE_NAME.mp4' with the exact name of your video file (e.g., 'mom_video.mp4')
          Make sure the file is in the same folder as this HTML file!
        -->
        <video id="heroVideo" autoplay muted playsinline loop>
          <source src="YOUR_VIDEO_FILE_NAME.mp4" type="video/mp4"> 
          Your browser does not support the video tag.
        </video>
      </div>

      <div class="hero-content">
        <h1 id="headline" data-animate>Happy Birthday <span id="recipientName">World's Best Mom</span> 🤍</h1>
        <p class="subtitle" data-animate>A heartfelt website built just for you, filled with love, memories, and big promises for the future.</p>

        <div style="display:flex; gap:12px; justify-content:center; flex-wrap:wrap; margin-top:16px" data-animate>
          <button class="btn" id="playBtn" title="Play/Pause music">Play Music ♪</button>
          <button class="small" id="revealBtn">Your Special Message 💌</button>
        </div>
      </div>
    </header>

    <section>
      <div class="section-title" data-animate>Our Journey Together</div>
      <div class="timeline">
        <div class="item card" data-animate>
          <h3>The Beginning 🤍</h3>
          <p>The first look, the first lesson, and the foundation of our unbreakable bond.</p>
        </div>
        <div class="item card" data-animate style="transition-delay: 0.1s;">
          <h3>Your Strength, My Guide 🌹</h3>
          <p>You taught me kindness, resilience, and how to chase dreams with all my heart.</p>
        </div>
        <div class="item card" data-animate style="transition-delay: 0.2s;">
          <h3>Laughter & Memories 💫</h3>
          <p>Every small trip and every quiet moment at home is a treasure I hold close.</p>
        </div>
        <div class="item card" data-animate style="transition-delay: 0.3s;">
        <h3>The Future We Share 💖</h3>
            <p>Looking forward to many more years of love, joy, and new adventures with you.</p>
          </div>
      </div>
    </section>

    <section>
      <div class="section-title" data-animate>Our Precious Memories Gallery</div>
      <div class="card slideshow" id="slideshow" data-animate>
        <div class="slides" id="slides">
          <!-- 
            *** 2. GALLERY IMAGE FILE PATHS ***
          -->
          <div class="slide"><img data-src="YOUR_IMAGE_FILE_1.jpg" alt="Memory 1" /></div>
          <div class="slide"><img data-src="YOUR_IMAGE_FILE_2.jpg" alt="Memory 2" /></div>
          <div class="slide"><img data-src="YOUR_IMAGE_FILE_3.jpg" alt="Memory 3" /></div>
          <div class="slide"><img data-src="YOUR_IMAGE_FILE_4.jpg" alt="Memory 4" /></div>
          <div class="slide"><img data-src="YOUR_IMAGE_FILE_5.jpg" alt="Memory 5" /></div>
          <div class="slide"><img data-src="YOUR_IMAGE_FILE_6.jpg" alt="Memory 6" /></div>
        </div>
        <div class="controls" id="dots"></div>
      </div>
    </section>

    <section>
      <div class="section-title" data-animate>A Note Written Just For You</div>
      <div class="card message-card" id="secret">
        <h3 style="margin:0 0 8px 0; color:var(--accent); font-family:var(--font-head);">My Heartfelt Promise</h3>
        <p class="secret-message-content" id="secret-message">
          𝑯𝒂𝒑𝒑𝒚 𝒃𝒊𝒓𝒕𝒉𝒅𝒂𝒚 𝑴𝒐𝒎 ✦♥︎‿♥︎✦💗🥳💋😘
          
          ┈┈ ☆☆☆☆☆☆☆┈
          ┈┈╭┻┻┻┻┻┻┻┻┻╮┈┈
          ┈┈┃╱╲╱╲╱╲╱╲╱┃┈┈
          ┈╭┻━━━━━━━━━┻╮┈
          ┈┃╱╲╱╲╱╲╱╲╱╲╱┃┈
          ┈┗━━━━━━━━━━━┛┈
          
          𝑾𝒊𝒔𝒉𝒊𝒏𝒈 𝒚𝒐𝒖 𝒂 𝑴𝒂𝒏𝒚 𝒎𝒂𝒏𝒚 𝒉𝒂𝒑𝒑𝒚 𝒓𝒆𝒕𝒖𝒓𝒏𝒔 𝒐𝒇 𝒕𝒉𝒆 𝒅𝒂𝒚 𝒎𝒚 𝒃𝒆𝒂𝒖𝒕𝒊𝒇𝒖𝒍 𝑴𝒐𝒎 🎂👑💕
          𝒀𝒐𝒖 𝒂𝒓𝒆 𝒏𝒐𝒕 𝒋𝒖𝒔𝒕 𝒎𝒚 𝑴𝒐𝒎, 𝒚𝒐𝒖 𝒂𝒓𝒆 𝒎𝒚 𝒉𝒆𝒂𝒓𝒕, 𝒎𝒚 𝒔𝒉𝒂𝒅𝒐𝒘, 𝒎𝒚 𝒔𝒎𝒊𝒍𝒆 ✨💞
          𝑻𝒐𝒅𝒂𝒚 𝒊𝒔 𝒂𝒍𝒍 𝒚𝒐𝒖𝒓𝒔 🎉💝 𝑴𝒂𝒚 𝒀𝒐𝒖𝒓 𝒍𝒊𝒇𝒆 𝒇𝒊𝒍𝒍 𝒘𝒊𝒕𝒉 𝒍𝒐𝒗𝒆, 𝒔𝒖𝒄𝒄𝒆𝒔𝒔, 𝒉𝒂𝒑𝒑𝒊𝒏𝒆𝒔𝒔 & 𝒏𝒆𝒗𝒆𝒓-𝒆𝒏𝒅𝒊𝒏𝒈 𝒔𝒎𝒊𝒍𝒆𝒔 🌹💫
          🇲‌🇦‌🇷‌🇮 ρүɑяⅈ Ꮇ𖽒Ꮇ 👑🌸 𝗸𝗼 𝗷𝗮𝗻𝗺𝗱𝗶 𝗸𝗶 𝗯𝗼𝗵𝗼𝘁 𝗯𝗼𝗵𝗼𝘁 𝗺𝘂𝗯𝗮𝗿𝗮𝗸𝗯𝗮𝗱 🎂🎉💜
          🌸 𝗮𝗹𝗹𝗮𝗵 𝗮𝗽𝗸𝗶 𝘇𝗶𝗻𝗱𝗮𝗴𝗶 𝗺𝗲 𝗵𝗮𝗿 𝗽𝗮𝗹
          𝗸𝗵𝘂𝘀𝗵𝗶𝗼𝗻 💝 𝗼𝗿 𝗽𝘆𝗮𝗿 💫 𝗯𝗮𝗿𝗸𝗮𝘁𝗲𝗶𝗻 🌹
          𝗯𝗮𝗿𝗮𝗸𝗮𝘁 𝗱𝗲 ✨
          🇵‌🇦‌🇷‌ 𝗺𝗲𝗿𝗶 𝗱𝗼𝘀𝘁, 𝗺𝗲𝗿𝗶 𝗷𝗮𝗻, 𝗺𝗲𝗿𝗶 𝗤𝘂𝗲𝗲𝗻 👑
          𝗵𝗮𝗽𝗽𝘆 𝗯𝗶𝗿𝘁𝗵𝗱𝗮𝘆 🎀🎂💜
          💗💖 𝒀𝒐𝒖 𝒂𝒓𝒆 𝒎𝒚 𝒃𝒆𝒔𝒕 𝒇𝒓𝒊𝒆𝒏𝒅, 𝒎𝒚 𝒔𝒐𝒖𝒍-𝒎𝒂𝒕𝒆, 𝒎𝒚 𝑸𝒖𝒆𝒆𝒏 👑💞
          𝑴𝒂𝒚 𝒕𝒉𝒊𝒔 𝒚𝒆𝒂𝒓 𝒃𝒓𝒊𝒏𝒈 𝒖𝒏𝒍𝒊𝒎𝒊𝒕𝒆𝒅 𝒋𝒐𝒚 🎁🎊
          𝑯𝒂𝒑𝒑𝒚 𝑩𝒊𝒓𝒕𝒉𝒅𝒂𝒚 𝒎𝒚 𝒃𝒆𝒔𝒕𝒆𝒔𝒕 𝑴𝒐𝒎𝒎𝒂 💕🌸
          𝓛𝓸𝓿𝓮 𝔂𝓸𝓾 𝓽𝓸 𝓽𝓱𝓮 𝓶𝓸𝓸𝓷 & 𝓫𝓪𝓬𝓴 🌙💖
          #𝐻𝒶𝓅𝓅𝓎𝐵𝒾𝓇𝓉𝒽𝒹𝒶𝓎𝑀𝑜𝓂 🎀👑🎂💐
          
          ╮╭╭╮┏╮┏╮╮╭
          ┣┫┣┫┣╯┣╯╰┫  ☆
          ╯╯╯╯╯╯╯╯╰╯╭━┻━╮
          ┏╮┊┏╮╭╮╮╭╭┻━━━┻╮
          ┣┫┊┃┃┣┫╰┫┣╮╭╮╭╮┃
          ┗╯┊┗╯╯╯╰╯┃╰╯╰╯╰┫
          ━━━━━━━━━╯╳╳╳╳╳╰
          🖤🤍🖤🤍🖤🤍🖤🤍🖤
          ★🎂 ℋ𝑎𝑝𝑝𝑦 ℬ𝑖𝑟𝑡ℎ𝑑𝑎𝑦 🎂★🍰 ⋆｡˚ ᡣ𐭩𓅫𝐻𝒶𝓅𝓅𝓎 𝒷𝒾𝓇𝓉𝒽𝒹𝒶𝓎★...
          ★·.·´¯`·.·★ 💜🎂💫
          ｍɑ𝔯ⅈ ρүɑяⅈ Ꮇ𖽒Ꮇ 👑🌸
          𝘬𝗈 ｍɑη𝗒 ｍɑη𝗒 ђɑρρ𝗒 𝗋𝑒𝗍ù𝗋η𝗌 𝗈𝖿 𝗍һ𝑒 ɗɑ𝗒 💜🎀
          
          {♥︎‿♥︎}{♥︎‿♥︎}{♥︎‿♥︎}
          💜 ｍ𝗒 ｌ𝗂ƒ𝑒, ｍ𝗒 ｈ𝗎𝑔, ｍ𝗒 ｓｍ𝗂𝗅𝑒 🌸
          💫 ｍ𝑒𝗋ⅈ 𝚀𝗎𝑒𝖾η ｍ𖽒ｍ, ｈɑρρ𝗂η𝑒ѕѕ ｋɑ ｂußｄｌ𝑒 💝
          💜 ｍɑ𝗒 ｙ𝗈ù𝗋 ｄ𝗋𝑒ɑｍѕ ｆ𝗅𝗈ω ｌ𝗂ｋ𝑒 ｓ𝑡𝑎𝗋ѕ ｉη ｐυ𝑟ρ𝗅𝑒 ｓ𝗄𝗒 ✨🌌
          
          ★·.·´¯·.·★ 🎂 𝐇𝐀𝐏𝐏𝐘 𝐁𝐈𝐑𝐓𝐇𝐃𝐀𝐘 💜★·.·´¯·.·★
          🌸 ｍ𝗒 ｈ𝑒ɑ𝗋𝗍𝗯𝑒ɑ𝑡 𝑴𝒐𝒎 🌸
          
          {♥︎‿♥︎}{♥︎‿♥︎}{♥︎‿♥︎}
          *🌸⃟‌ٖٖٖٖٖٖ❤️*
          *💞⃝⃪⃕ 🌸*
        </p>
      </div>
    </section>

    <section class="ending">
      <div class="card" style="max-width:720px" data-animate>
        <h2 style="margin:0 0 6px 0; font-family:var(--font-head); color:var(--accent);">I love you, <span id="endName">Mom</span> 🤍</h2>
        <p style="margin:0;color:var(--muted)">You are my home. May your world always be as warm and bright as you make mine.</p>
        <div style="margin-top:16px">
          <button class="btn" id="hugBtn">Tap for a big virtual hug 🤗</button>
        </div>
      </div>
    </section>
        <!-- 
      *** 3. MUSIC FILE PATH: UPDATED ***
    
    -->
    <audio id="bgMusic" loop crossorigin="anonymous">
      <source src="Happy-Birthday-To-You-Ji-Teddy-Kids-Song.mp3" type="audio/mpeg"
    </audio>

  </div> 
</div> 

<div id="hugModal" class="modal">
  <div class="modal-content">
    <button class="close-btn" id="closeModal">&times;</button>
    <div class="heart-burst" id="heartBurst"></div>
    <!-- 
      *** 4. HUG IMAGE/GIF FILE PATH ***
      I've kept a generic placeholder here for safety. If you want to use your GIF, 
      replace the URL below with the file name (e.g., 'bear_hug.gif').
    -->
 <video id="heroVideo" autoplay muted playsinline loop>
          <source src="YOUR_VIDEO_FILE_NAME 2.mp4" type="video/mp4"> 
        </video>
      </div> 
      class="hug-image"/>
    <h3 style="color:var(--accent); font-family:var(--font-head);">Sending Big Hugs!</h3>
    <p style="color:var(--muted); center: 2;">You're the best, Mom! This hug is for you.</p>
  </div>
</div>

<script>
// ---------- CONFIG ----------
  const RECIPIENT_NAME = "World's Best Mom";
  const AUTO_PLAY_MUSIC = false; // Set to true if you want it to try and play automatically (might be blocked by browser)
  const SLIDE_INTERVAL = 4000;
  const VIBRATION_DURATION = 150; // ms

  // ---------- UTIL: read ?name= param ----------
  function getQueryParam(key){
    const params = new URLSearchParams(location.search);
    return params.get(key);
  }

  // ---------- INIT: set name ----------
  const nameFromUrl = getQueryParam('name');
  const nameToShow = (nameFromUrl && nameFromUrl.trim().length>0) ? decodeURIComponent(nameFromUrl) : RECIPIENT_NAME;
  document.getElementById('recipientName').textContent = nameToShow;
  document.getElementById('endName').textContent = nameToShow.split(' ')[0] || nameToShow;
  document.title = `Happy Birthday — ${nameToShow} 💖`;

  // ---------- ANIMATIONS: reveal on scroll ----------
  const observer = new IntersectionObserver((entries)=>{
    entries.forEach(e=>{
      if(e.isIntersecting){ e.target.classList.add('in'); observer.unobserve(e.target); }
    });
  }, {threshold:0.12});
  document.querySelectorAll('[data-animate]').forEach(el=>observer.observe(el));

  // ---------- FLOATING HEARTS/FLOWERS ----------
  const backgroundContainer = document.getElementById('animatedBackground');
  const objects = ['❤️', '🧡', '💛', '💚', '🩵', '💙', '💜', '💐', '🌹', '🌸', '🌼'];
  const count = 20;
  for(let i=0;i<count;i++){
    const obj = document.createElement('div');
    obj.className = 'animated-object';
    obj.textContent = objects[Math.floor(Math.random() * objects.length)];
    obj.style.left = Math.random() * 100 + '%';
    obj.style.animationDuration = (10 + Math.random() * 10).toFixed(2) + 's';
    obj.style.animationDelay = (Math.random() * 10).toFixed(2) + 's';
    obj.style.opacity = (0.2 + Math.random() * 0.5).toFixed(2);
    obj.style.transform = `scale(${(0.8 + Math.random() * 0.4).toFixed(2)})`;
    backgroundContainer.appendChild(obj);
  }

  // ---------- SLIDESHOW ----------
  const slides = document.getElementById('slides');
  const slideItems = Array.from(slides.children);
  let current = 0;
  const dots = document.getElementById('dots');

  // Load images with fade-in effect (Lazy load basic)
  function loadSlideImage(index) {
    const img = slideItems[index].querySelector('img');
    if (!img.src && img.dataset.src) {
      img.src = img.dataset.src;
      img.onerror = () => { img.src = `https://placehold.co/400x400/ffe4e1/ff69b4?text=Image+Missing`; img.classList.add('loaded'); }; // Fallback image on error
      img.onload = () => img.classList.add('loaded');
    }
  }

  function renderDots(){
    dots.innerHTML='';
    slideItems.forEach((_,i)=>{
      const dot = document.createElement('div');
      dot.className='dot' + (i===current?' active':'');
      dot.addEventListener('click', ()=> { goTo(i); resetAuto(); });
      dots.appendChild(dot);
    });
  }
  function updateSlide(){
    slides.style.transform = 'translateX(' + (-current*100) + '%)';
    Array.from(dots.children).forEach((d,i)=> d.classList.toggle('active', i===current));
    // Preload next slide's image
    loadSlideImage(current);
    loadSlideImage((current + 1) % slideItems.length);
  }
  function goTo(i){
    current = (i + slideItems.length) % slideItems.length;
    updateSlide();
  }
  function nextSlide(){ goTo(current+1); }

  renderDots();
  loadSlideImage(0); // Load first image on init
  updateSlide();

  let slideTimer = setInterval(nextSlide, SLIDE_INTERVAL);
  function resetAuto(){ clearInterval(slideTimer); slideTimer = setInterval(nextSlide, SLIDE_INTERVAL); }

  // Add swipe support for mobile
  (function swipeSupport(){
    let startX = 0, endX = 0;
    slides.addEventListener('touchstart', e => { startX = e.touches[0].clientX; e.preventDefault(); });
    slides.addEventListener('touchmove', e => endX = e.touches[0].clientX);
    slides.addEventListener('touchend', ()=> {
      if(startX && endX){
        if(startX - endX > 30) { nextSlide(); resetAuto(); } // swipe left
        else if(endX - startX > 30) { goTo(current-1); resetAuto(); } // swipe right
      }
      startX = endX = 0;
    });
  })();
    // ---------- MUSIC CONTROLS (RESTORED) ----------
  const bgMusic = document.getElementById('bgMusic');
  const playBtn = document.getElementById('playBtn');
  playBtn.addEventListener('click', toggleMusic);

  function toggleMusic(){
    if(bgMusic.paused){ 
      // Use .play() with a catch to handle browsers blocking auto-play without user interaction
      bgMusic.play().catch(e => console.warn("Music Play Failed (Browser restriction):", e)); 
      playBtn.textContent = 'Pause Music ⏸️'; 
      playBtn.classList.remove('small');
      playBtn.classList.add('btn');
    }
    else { 
      bgMusic.pause(); 
      playBtn.textContent = 'Play Music ♪'; 
      playBtn.classList.add('small');
      playBtn.classList.remove('btn');
    }
  }
  // Auto attempt (if config is true)
  if(AUTO_PLAY_MUSIC){ toggleMusic(); }

  // ---------- MESSAGE REVEAL ----------
  const revealBtn = document.getElementById('revealBtn');
  const secretCard = document.getElementById('secret');

  revealBtn.addEventListener('click', ()=>{
      secretCard.classList.add('show');
      revealBtn.style.display = 'none'; // Hide button after reveal
      if(navigator.vibrate) navigator.vibrate(VIBRATION_DURATION);
  });


  // ---------- HUG MODAL ----------
  const hugBtn = document.getElementById('hugBtn');
  const hugModal = document.getElementById('hugModal');
  const closeModal = document.getElementById('closeModal');
  const heartBurst = document.getElementById('heartBurst');

  hugBtn.addEventListener('click', ()=>{
      hugModal.classList.add('open');
      if(navigator.vibrate) navigator.vibrate(VIBRATION_DURATION);
      
      // Heart Burst Effect
      for(let i=0; i<15; i++){
          const heart = document.createElement('div');
          heart.className = 'burst-heart';
          heart.textContent = '💖';
          // Calculate random start and end points
          const startX = 100 + Math.random() * 50;
          const startY = 100 + Math.random() * 50;
          const endX = (Math.random() - 0.5) * 400 + 'px';
          const endY = (Math.random() - 0.5) * 400 + 'px';

          heart.style.left = startX + 'px';
          heart.style.top = startY + 'px';
          heart.style.setProperty('--x', endX);
          heart.style.setProperty('--y', endY);
          heart.style.animationDelay = (Math.random() * 0.3).toFixed(2) + 's';
          heartBurst.appendChild(heart);

          // Clean up element after animation
          heart.addEventListener('animationend', () => heart.remove());
      }
  });

  closeModal.addEventListener('click', () => {
    hugModal.classList.remove('open');
    heartBurst.innerHTML = ''; // Clear hearts
  });

  // Close modal on outside click
  hugModal.addEventListener('click', (e) => {
    if (e.target === hugModal) {
      hugModal.classList.remove('open');
      heartBurst.innerHTML = '';
    }
  });

  // ---------- Finalizing the unfinished function from original code ----------
  function startRainEffect(elementId, item, count) {
      const container = document.getElementById(elementId);
      for(let i=0; i<count; i++) {
          const s = document.createElement('div');
          s.textContent = item[Math.floor(Math.random() * item.length)];
          s.style.position = 'absolute';
          s.style.left = Math.random() * 100 + '%';
          s.style.top = Math.random() * 100 + '%';
          s.style.fontSize = (15 + Math.random() * 20) + 'px';
          s.style.opacity = (0.3 + Math.random() * 0.7).toFixed(2);
          s.style.animationDuration = (1 + Math.random() * 2).toFixed(2) + 's';
          s.style.animationDelay = (Math.random() * 1).toFixed(2) + 's';
          s.style.transform = `scale(${(0.8 + Math.random() * 0.4).toFixed(2)})`;
          container.appendChild(s);
          // Note: This function was never fully called in the original code, but is completed here.
      }
  }

</script>
</body>
</html>
