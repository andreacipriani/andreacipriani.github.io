---
layout: page
permalink: /ideas/
title: demos & ideas
nav: true
nav_order: 5
description: Small experiments, toys and half-formed ideas.
---

<style>
.ideas-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 1.25rem;
  margin: 1.5rem 0 3rem;
}
.idea-card {
  display: block;
  padding: 1.4rem 1.5rem;
  border: 1px solid var(--global-divider-color);
  border-radius: 12px;
  color: var(--global-text-color) !important;
  text-decoration: none !important;
  transition: border-color 0.2s ease, transform 0.2s ease;
}
.idea-card:hover {
  border-color: var(--global-theme-color);
  transform: translateY(-2px);
}
.idea-card h3 {
  margin: 0 0 0.5rem;
  font-size: 1.15rem;
}
.idea-card p {
  margin: 0;
  font-size: 0.92rem;
  color: var(--global-text-color-light);
}
.idea-card .idea-tag {
  display: inline-block;
  margin-top: 0.9rem;
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--global-theme-color);
}
</style>

<div class="ideas-grid">
  <a class="idea-card" href="/abstraction/">
    <h3>The Tree of Abstraction</h3>
    <p>A ladder of abstraction. Start from onions and fennel and climb, concept after concept, towards the most abstract idea of all.</p>
    <span class="idea-tag">interactive · demo</span>
  </a>
  <a class="idea-card" href="/parole/">
    <h3>Parole</h3>
    <p>A game of words against time. Type something before the timer runs out, and never repeat the same word twice. How long can you last?</p>
    <span class="idea-tag">game</span>
  </a>
</div>
