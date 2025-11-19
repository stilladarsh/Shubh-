# Shubh-<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="description" content="A friendly, soft page for Shubh — simple slider with accessible controls and soft visuals." />
  <title>For Shubh 😊</title>

  <!-- Google font (optional) -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg1: #f7e7ff;
      --bg2: #d6f5ff;
      --card-bg: rgba(255,255,255,0.85);
      --muted: #555;
      --accent: #ffb7d5;
      --radius: 16px;
      --shadow: 0 10px 25px rgba(0,0,0,0.07);
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: "Poppins", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background: linear-gradient(135deg,var(--bg1),var(--bg2));
      display:flex;
      align-items:center;
      justify-content:center;
      padding:32px;
      color: #333;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
    }

    .card{
      width:100%;
      max-width:760px;
      background:var(--card-bg);
      border-radius:calc(var(--radius) + 4px);
      padding:28px;
      box-shadow:var(--shadow);
      backdrop-filter: blur(6px);
      text-align:center;
      animation:pop 600ms ease;
    }
    @keyframes pop{from{transform:scale(.96);opacity:0}to{transform:none;opacity:1}}

    h1{
      margin:0 0 6px 0;
      font-weight:600;
      font-size:2rem;
      color:#2a2a2a;
    }
    .lead{margin:0 0 18px 0;color:var(--muted);font-size:1.05rem}

    /* Slider */
    .slider-wrap{
      position:relative;
      border-radius:var(--radius);
      overflow:hidden;
      background:linear-gradient(180deg, rgba(255,255,255,0.6), rgba(255,255,255,0.4));
      margin:0 auto;
      max-width:680px;
    }

    .slider{
      display:flex;
      width:100%;
      transition:transform 420ms cubic-bezier(.22,.9,.32,1);
      will-change:transform;
    }

    .slide{
      min-width:100%;
      display:flex;
      align-items:center;
      justify-content:center;
      position:relative;
    }

    .slide img{
      width:100%;
      height:380px;
      object-fit:cover;
      display:block;
    }

    .slide-figcaption{
      position:absolute;
      left:12px;
      bottom:12px;
      background:rgba(0,0,0,0.45);
      color:#fff;
      padding:8px 12px;
      border-radius:999px;
      font-size:0.95rem;
      backdrop-filter: blur(4px);
    }

    .btn {
      position:absolute;
      top:50%;
      transform:translateY(-50%);
      background:rgba(255,255,255,0.85);
      border:0;
      padding:10px 12px;
      font-size:1.05rem;
      cursor:pointer;
      border-radius:12px;
      box-shadow:0 6px 14px rgba(0,0,0,0.08);
    }
    .btn:focus{outline:3px solid rgba(0,0,0,0.12)}
    .btn.left{left:12px}
    .btn.right{right:12px}

    .controls{
      display:flex;
      gap:8px;
      justify-content:center;
      margin-top:14px;
      align-items:center;
    }

    .dot{
      width:12px;height:12px;border-radius:50%;
      background:rgba(0,0,0,0.15);border:0;
      cursor:pointer;
    }
    .dot[aria-pressed="true"]{background:var(--accent);box-shadow:0 6px 14px rgba(0,0,0,0.08)}

    .section{
      margin-top:18px;
      font-size:1.05rem;
      background:rgba(255,255,255,0.6);
      padding:14px;
      border-radius:12px;
      color:var(--muted);
      text-align:left;
    }

    /* Responsive */
    @media (max-width:640px){
      .slide img{height:220px}
      h1{font-size:1.6rem}
    }

    /* Respect reduced motion */
    @media (prefers-reduced-motion: reduce){
      .slider{transition:none}
      .card{animation:none}
    }
  </style>
</head>
<body>

  <main class="card" role="main">
    <h1>Hi Shubh 😊</h1>
    <p class="lead">Bas ek friendly page… kyunki tumhari vibe hamesha soft aur sweet hoti hai ✨💛</p>

    <!-- Carousel / Slider region -->
    <section
      class="slider-wrap"
      id="carousel"
      role="region"
      aria-roledescription="carousel"
      aria-label="Photos for Shubh"
    >
      <button class="btn left" id="prevBtn" type="button" aria-label="Previous slide">◀</button>

      <div class="slider" id="slider" tabindex="0" aria-live="polite">
        <figure class="slide" data-index="0">
          <img src="image1.jpg" alt="Smiling portrait" loading="lazy" />
          <figcaption class="slide-figcaption">A calm smile 😊</figcaption>
        </figure>

        <figure class="slide" data-index="1">
          <img src="image2.jpg" alt="Soft vibes detail" loading="lazy" />
          <figcaption class="slide-figcaption">Soft vibes 🌼</figcaption>
        </figure>

        <figure class="slide" data-index="2">
          <img src="image3.jpg" alt="Simple & classy style" loading="lazy" />
          <figcaption class="slide-figcaption">Simple & classy ✨</figcaption>
        </figure>
      </div>

      <button class="btn right" id="nextBtn" type="button" aria-label="Next slide">▶</button>
    </section>

    <!-- Indicators -->
    <div class="controls" id="indicators" aria-hidden="false"></div>

    <div class="section" aria-label="Things that make you cool">
      <strong>Things that make you cool 😄✨</strong>
      <p style="margin:8px 0 0 0">• Tumhari calm smile 😊<br>
         • Soft vibes 🌼<br>
         • Simple & classy style ✨<br>
         • Intelligent + cute combo 😌</p>
    </div>
  </main>

  <script>
    (function(){
      const slider = document.getElementById('slider');
      const slides = Array.from(slider.children);
      const prevBtn = document.getElementById('prevBtn');
      const nextBtn = document.getElementById('nextBtn');
      const indicatorsEl = document.getElementById('indicators');
      const carousel = document.getElementById('carousel');

      let index = 0;
      const total = slides.length;
      let autoPlayInterval = 4000;
      let timer = null;

      // Build indicators (dots)
      slides.forEach((s, i) => {
        const btn = document.createElement('button');
        btn.className = 'dot';
        btn.type = 'button';
        btn.title = `Go to slide ${i + 1}`;
        btn.setAttribute('aria-pressed', i === 0 ? 'true' : 'false');
        btn.addEventListener('click', () => goTo(i));
        indicatorsEl.appendChild(btn);
      });
      const dots = Array.from(indicatorsEl.children);

      function update() {
        slider.style.transform = `translateX(-${index * 100}%)`;
        dots.forEach((d, i) => d.setAttribute('aria-pressed', i === index ? 'true' : 'false'));
        // Update accessible label for screen readers
        slider.setAttribute('aria-label', `Slide ${index + 1} of ${total}`);
      }

      function prev() { index = (index - 1 + total) % total; update(); }
      function next() { index = (index + 1) % total; update(); }
      function goTo(i){ index = (i + total) % total; update(); }

      prevBtn.addEventListener('click', prev);
      nextBtn.addEventListener('click', next);

      // Keyboard support when slider has focus
      slider.addEventListener('keydown', (e) => {
        if (e.key === 'ArrowLeft') { e.preventDefault(); prev(); resetTimer(); }
        if (e.key === 'ArrowRight') { e.preventDefault(); next(); resetTimer(); }
        if (e.key === 'Home') { e.preventDefault(); goTo(0); resetTimer(); }
        if (e.key === 'End') { e.preventDefault(); goTo(total - 1); resetTimer(); }
      });

      // Auto-play with pause on hover/focus
      function startTimer(){
        if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;
        stopTimer();
        timer = setInterval(()=> { next(); }, autoPlayInterval);
      }
      function stopTimer(){ if (timer) { clearInterval(timer); timer = null; } }
      function resetTimer(){ stopTimer(); startTimer(); }

      [carousel, slider, prevBtn, nextBtn].forEach(el => {
        el.addEventListener('mouseenter', stopTimer);
        el.addEventListener('focusin', stopTimer);
        el.addEventListener('mouseleave', startTimer);
        el.addEventListener('focusout', startTimer);
      });

      // Make images resilient: if image fails to load, show a subtle background and caption
      slides.forEach((fig) => {
        const img = fig.querySelector('img');
        img.addEventListener('error', () => {
          img.style.display = 'none';
          fig.style.background = 'linear-gradient(135deg, #f3e7ff, #e6f8ff)';
          fig.style.minHeight = '200px';
        });
      });

      // Initialize
      update();
      startTimer();

      // Expose controls for debugging (optional)
      window.__carousel = { goTo, next, prev, startTimer, stopTimer };
    })();
  </script>

</body>
</html>
