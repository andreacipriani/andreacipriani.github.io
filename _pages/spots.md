---
layout: page
permalink: /spots/
title: My favorite spots
description: Restaurants, bars, cafés and more.
nav: false
---

<style>
.spots-intro {
  font-size: 0.95rem;
  color: var(--global-text-color-light, #888);
  margin-bottom: 2.5rem;
}

.spot-city-section {
  margin-bottom: 3rem;
}

.spot-city-header {
  display: flex;
  align-items: baseline;
  gap: 0.7rem;
  margin-bottom: 1rem;
  padding-bottom: 0.6rem;
  border-bottom: 1px solid var(--global-divider-color);
}

.spot-city-name {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--global-text-color);
  margin: 0;
}

.spot-city-flag {
  font-size: 1.2rem;
}

.spot-map-wrapper {
  border-radius: 14px;
  overflow: hidden;
  box-shadow: 0 4px 24px rgba(0,0,0,0.10);
  border: 1px solid var(--global-divider-color);
  position: relative;
  width: 100%;
  padding-top: 56%; /* 16:9 */
}

.spot-map-wrapper iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: none;
  display: block;
}

.amigo-card {
  margin-top: 2.5rem;
  padding: 1.4rem 1.8rem;
  border: 1px solid var(--global-divider-color);
  border-radius: 14px;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.amigo-card-text {
  flex: 1;
  min-width: 200px;
}

.amigo-card-text p {
  margin: 0;
  font-size: 0.92rem;
  color: var(--global-text-color);
  line-height: 1.5;
}

.amigo-card-text strong {
  display: block;
  font-size: 1rem;
  margin-bottom: 0.3rem;
  color: var(--global-text-color);
}

.amigo-badge {
  flex-shrink: 0;
}

.amigo-badge img {
  width: 140px;
  height: auto;
  display: block;
}
</style>

<p class="spots-intro">A curated map of places I actually like — updated as I discover new ones.</p>

<div class="spot-city-section">
  <div class="spot-city-header">
    <span class="spot-city-flag">🗽</span>
    <h3 class="spot-city-name">New York City</h3>
  </div>
  <div class="spot-map-wrapper">
    <iframe src="https://www.google.com/maps/d/embed?mid=1VuOEbXNRlylForz736rzFhNdkboIt88&ehbc=2E312F" allowfullscreen loading="lazy"></iframe>
  </div>
</div>

<div class="spot-city-section">
  <div class="spot-city-header">
    <span class="spot-city-flag">🇮🇹</span>
    <h3 class="spot-city-name">Milano</h3>
  </div>
  <div class="spot-map-wrapper">
    <iframe src="https://www.google.com/maps/d/embed?mid=1BA1coon7YOlv51RkIn_iLBy325-_8ZI" allowfullscreen loading="lazy"></iframe>
  </div>
</div>

<div class="amigo-card">
  <div class="amigo-card-text">
    <strong>More spots on Amigo</strong>
    <p>Follow me on the Amigo app for recommendations from all around the world.</p>
  </div>
  <a class="amigo-badge" href="https://www.amigo.app/user/andreacipriani?userId=62d97757eaf4d30ed74d81a2" target="_blank" rel="noopener">
    <img src="/assets/img/appstore.png" alt="Download on the App Store">
  </a>
</div>
