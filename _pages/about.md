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

news: true # includes a list of news items
latest_posts: true # includes a list of the newest posts
selected_papers: false # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page
---

Ciao! I'm Andrea. I grew up in Italy, live in New York, and build iOS apps for a living, currently at Airbnb. I specialize in **mobile development** at scale, with over a decade of experience.

Throughout my career, I have had the privilege of working for apps used all over the globe, including **Airbnb**, **Apple Sports**, **Spotify**, **SoundCloud** and **Google**.

<div class="company-logos" style="display: flex; flex-wrap: wrap; justify-content: center; align-items: center; gap: 28px; margin-top: 25px; margin-bottom: 28px; font-size: 2.2rem; color: var(--global-text-color);">
  <span title="Airbnb"><i class="fa-brands fa-airbnb"></i></span>
  <span title="Spotify"><i class="fa-brands fa-spotify"></i></span>
  <span title="Apple"><i class="fa-brands fa-apple"></i></span>
  <span title="SoundCloud"><i class="fa-brands fa-soundcloud"></i></span>
  <span title="Google"><i class="fa-brands fa-google"></i></span>
</div>

I love exploring new places and traveling, Hawaii is my favorite so far! I fenced competitively in my twenties and now I enjoy casual (mostly racket) sports, taking a dip in the ocean, testing my skills at Texas Hold'em poker and appreciating beautiful things, mostly in the form of cinema, books and music.


<div style="margin-top: 2rem; margin-bottom: 3rem; padding: 1.2rem 1.5rem; border: 1px solid var(--global-divider-color); border-radius: 10px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem;">
  <span style="font-size: 0.95rem; color: var(--global-text-color);">Want to work together or just say hi?</span>
  <a href="mailto:andreacipriani89@gmail.com" style="font-size: 0.9rem; padding: 0.4rem 1.1rem; border-radius: 20px; border: 1px solid var(--global-theme-color); color: var(--global-theme-color); text-decoration: none; white-space: nowrap;">Get in touch</a>
</div>

<style>
  .hover-effect:hover {
    opacity: 0.8;
    transition: opacity 0.3s ease;
  }

  @media (max-width: 576px) {
    .company-logos { gap: 20px !important; font-size: 1.8rem !important; }
  }

  /* Vision Pro photo on hover */
  .profile .vp-wrap { position: relative; display: block; }
  .profile .vp-wrap .vp-img {
    position: absolute; inset: 0; width: 100%; height: 100%;
    object-fit: cover; opacity: 0; transition: opacity 0.35s ease;
    pointer-events: none;
  }
  .profile .vp-wrap:hover .vp-img { opacity: 1; }
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  var img = document.querySelector('.profile img');
  if (!img) return;
  var host = img.closest('figure') || img.closest('picture') || img;
  var wrap = document.createElement('span');
  wrap.className = 'vp-wrap';
  host.parentNode.insertBefore(wrap, host);
  wrap.appendChild(host);
  var vp = new Image();
  vp.src = '/assets/img/prof_pic_vp.jpg';
  vp.alt = 'Andrea with a Vision Pro';
  vp.className = 'vp-img ' + img.className.replace('hover-effect', '');
  wrap.appendChild(vp);
});
</script>
