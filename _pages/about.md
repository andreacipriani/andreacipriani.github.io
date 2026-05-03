---
layout: about
title: about
permalink: /
subtitle:
profile:
  align: right
  image: prof_pic.jpg
  image_circular: true # crops the image to make it circular
  more_info: >
    <p>🇮🇹🇺🇸 Software Engineer</p>
    <p>🍏 iOS expert</p>
    <p>But really: 🎥🤺🎾🛫🌊</p>
    <p><a href="mailto:andreacipriani89@gmail.com">Contact me</a></p>
    <p style="margin-top:0.6rem; display:block;"><a id="rain-link" href="#" onclick="startIconRain();return false;" style="display:block;">Don't click</a></p>

news: true # includes a list of news items
latest_posts: true # includes a list of the newest posts
selected_papers: false # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page
---

Ciao! I'm Andrea, an Italian Software Engineer based in nyc. I specialize in **mobile development** at scale, with a decade of experience in **iOS**.

Throughout my career, I have had the privilege of working for apps used all over the globe, including **Spotify**, **Apple Sports**, **SoundCloud** and **Google**.

<div style="display: flex; justify-content: center; align-items: center; gap: 32px; margin-top: 25px; margin-bottom: 28px; font-size: 2.2rem; color: var(--global-text-color);">
  <span title="Spotify"><i class="fa-brands fa-spotify"></i></span>
  <span title="Apple"><i class="fa-brands fa-apple"></i></span>
  <span title="SoundCloud"><i class="fa-brands fa-soundcloud"></i></span>
  <span title="Google"><i class="fa-brands fa-google"></i></span>
</div>

When I'm not coding, I love exploring new places and traveling, Hawaii is my favorite so far! I fenced professionally in my twenties and now I enjoy casual (mostly racket) sports, taking a dip in the ocean, testing my skills at Texas Hold'em poker and appreciating beautiful things.


<div style="margin-top: 2rem; margin-bottom: 3rem; padding: 1.2rem 1.5rem; border: 1px solid var(--global-divider-color); border-radius: 10px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem;">
  <span style="font-size: 0.95rem; color: var(--global-text-color);">Want to work together or just say hi?</span>
  <a href="mailto:andreacipriani89@gmail.com" style="font-size: 0.9rem; padding: 0.4rem 1.1rem; border-radius: 20px; border: 1px solid var(--global-theme-color); color: var(--global-theme-color); text-decoration: none; white-space: nowrap;">Get in touch</a>
</div>

<style>
  .hover-effect:hover {
    opacity: 0.8;
    transition: opacity 0.3s ease;
  }

  /* ── visionOS spatial environment ── */
  body.vp-env {
    background: #06060f !important;
    transition: background 0.6s ease;
  }

  body.vp-env::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 80% 60% at 50% 50%, transparent 40%, rgba(0,0,20,0.92) 100%),
      radial-gradient(ellipse 120% 80% at 20% 80%, rgba(30,10,60,0.4) 0%, transparent 60%),
      radial-gradient(ellipse 100% 60% at 80% 20%, rgba(0,20,60,0.3) 0%, transparent 60%);
    pointer-events: none;
    z-index: 9980;
    transition: opacity 0.6s ease;
  }

  body.vp-env .post,
  body.vp-env nav {
    background: rgba(255,255,255,0.07) !important;
    backdrop-filter: blur(24px) saturate(1.4) !important;
    -webkit-backdrop-filter: blur(24px) saturate(1.4) !important;
    border-radius: 22px !important;
    box-shadow:
      0 0 0 1px rgba(255,255,255,0.12),
      0 40px 120px rgba(0,0,0,0.7),
      0 0 60px rgba(80,120,255,0.08) !important;
    transform: perspective(1400px) rotateX(1.5deg) translateZ(0) !important;
    transition: all 0.6s cubic-bezier(0.4,0,0.2,1) !important;
    color: rgba(255,255,255,0.9) !important;
  }

  body.vp-env-out .post,
  body.vp-env-out nav {
    transform: perspective(1400px) rotateX(0deg) translateZ(0) !important;
    transition: all 0.5s cubic-bezier(0.4,0,0.2,1) !important;
  }

  @keyframes iconFall {
    0%   { transform: translateY(-80px) rotate(0deg); opacity: 1; }
    80%  { opacity: 1; }
    100% { transform: translateY(105vh) rotate(360deg); opacity: 0; }
  }

  @keyframes pageShake {
    0%,100% { transform: translate(0, 0) rotate(0deg); }
    10%      { transform: translate(-3px, 2px) rotate(-0.4deg); }
    20%      { transform: translate(3px, -2px) rotate(0.4deg); }
    30%      { transform: translate(-4px, 1px) rotate(-0.3deg); }
    40%      { transform: translate(4px, -1px) rotate(0.3deg); }
    50%      { transform: translate(-2px, 3px) rotate(-0.2deg); }
    60%      { transform: translate(2px, -3px) rotate(0.2deg); }
    70%      { transform: translate(-3px, 1px) rotate(-0.3deg); }
    80%      { transform: translate(3px, 2px) rotate(0.2deg); }
    90%      { transform: translate(-1px, -2px) rotate(-0.1deg); }
  }

  body.vp-shaking .post {
    animation: pageShake 0.35s ease-in-out infinite;
    transform-origin: center center;
  }

  .rain-icon {
    position: fixed;
    top: 0;
    pointer-events: none;
    z-index: 9999;
    animation: iconFall linear forwards;
    user-select: none;
  }
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  var link = document.getElementById('rain-link');
  if (link && window.matchMedia('(hover: none) and (pointer: coarse)').matches) {
    link.textContent = "Don't tap";
  }
});

var RAIN_DURATION = 3000; // ms — single source of truth for all effect timings
var FADE_DURATION = 600;

function _showVisionPro() {
  var img = document.querySelector('.profile img');
  if (!img) return;
  var src = img.src;
  var picture = img.closest('picture');
  var sources = picture ? picture.querySelectorAll('source') : [];

  sources.forEach(function(s) { s._saved = s.srcset; s.srcset = ''; });
  img.src = '/assets/img/prof_pic_vp.jpg';

  setTimeout(function() {
    img.src = src;
    sources.forEach(function(s) { s.srcset = s._saved || ''; });
  }, RAIN_DURATION);
}

/* ── Icon rain ── */
function startIconRain() {
  if (window._rainActive) return;
  window._rainActive = true;

  // visionOS environment in
  document.body.classList.add('vp-env', 'vp-shaking');

  // everything fades out together at RAIN_DURATION
  setTimeout(function() {
    document.body.classList.remove('vp-shaking');
    document.body.classList.add('vp-env-out');
    setTimeout(function() {
      document.body.classList.remove('vp-env', 'vp-env-out');
      window._rainActive = false;
    }, FADE_DURATION);
  }, RAIN_DURATION);

  _showVisionPro();

  var icons = [
    '📱','🍎','🎵','🎧','⌚','💻','📸','🎮','✈️','🌊',
    '🎾','🃏','🏃','🎬','🗺️','🤺','🍕','🌴','🏄','🎯',
    '🚀','💡','🔮','🎨','🎸','🏆','🌺','🐙','🎪','⚡'
  ];
  for (var i = 0; i < 65; i++) {
    (function(idx) {
      setTimeout(function() {
        var el = document.createElement('div');
        el.className = 'rain-icon';
        el.textContent = icons[Math.floor(Math.random() * icons.length)];
        var size = 18 + Math.random() * 28;
        var duration = 1.8 + Math.random() * 2.2;
        el.style.left = (Math.random() * 98) + 'vw';
        el.style.fontSize = size + 'px';
        el.style.animationDuration = duration + 's';
        document.body.appendChild(el);
        setTimeout(function() { el.remove(); }, duration * 1000 + 100);
      }, idx * 45);
    })(i);
  }

}
</script>
