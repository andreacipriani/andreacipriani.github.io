---
layout: page
permalink: /playground/
title: SwiftUI Playground
nav: false
description: Real SwiftUI code. Rendered in your browser.
---

<style>
.swiftui-playground {
  font-family: -apple-system, BlinkMacSystemFont, 'SF Pro Display', sans-serif;
  margin: 1.5rem 0;
}

.playground-tabs {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
  flex-wrap: wrap;
}

.playground-tab {
  padding: 6px 16px;
  border-radius: 20px;
  border: 1px solid var(--global-divider-color);
  background: none;
  color: var(--global-text-color);
  font-size: 0.82rem;
  cursor: pointer;
  transition: background 0.2s, color 0.2s, border-color 0.2s;
}

.playground-tab.active {
  background: var(--global-theme-color);
  border-color: var(--global-theme-color);
  color: #fff;
}

.playground-panels {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  align-items: start;
}

@media (max-width: 640px) {
  .playground-panels {
    grid-template-columns: 1fr;
  }
}

/* Code panel */
.code-panel {
  background: #1e1e2e;
  border-radius: 12px;
  overflow: hidden;
  font-size: 0.8rem;
}

.code-panel-titlebar {
  background: #2a2a3e;
  padding: 10px 14px;
  display: flex;
  align-items: center;
  gap: 7px;
}

.titlebar-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}

.titlebar-dot.red   { background: #ff5f57; }
.titlebar-dot.yellow{ background: #febc2e; }
.titlebar-dot.green { background: #28c840; }

.titlebar-label {
  margin-left: 6px;
  font-size: 0.75rem;
  color: #888;
  font-family: 'SF Mono', 'Fira Code', monospace;
}

.code-content {
  padding: 18px;
  margin: 0;
  overflow-x: auto;
  color: #cdd6f4;
  font-family: 'SF Mono', 'Fira Code', 'Cascadia Code', monospace;
  line-height: 1.65;
  white-space: pre;
  min-height: 320px;
}

/* Swift syntax colors (Catppuccin-inspired) */
.sw-keyword  { color: #cba6f7; }
.sw-type     { color: #89dceb; }
.sw-string   { color: #a6e3a1; }
.sw-number   { color: #fab387; }
.sw-comment  { color: #6c7086; font-style: italic; }
.sw-param    { color: #89b4fa; }
.sw-modifier { color: #f38ba8; }
.sw-prop     { color: #f9e2af; }

/* Preview panel */
.preview-panel {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 14px;
}

.preview-label {
  font-size: 0.75rem;
  color: var(--global-text-color-light, #888);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  align-self: flex-start;
}

.phone-frame {
  width: 220px;
  background: #1a1a1a;
  border-radius: 36px;
  padding: 12px;
  box-shadow: 0 20px 50px rgba(0,0,0,0.35), inset 0 0 0 1px rgba(255,255,255,0.08);
  position: relative;
}

.phone-notch {
  width: 80px;
  height: 22px;
  background: #1a1a1a;
  border-radius: 0 0 14px 14px;
  margin: 0 auto 6px;
  position: relative;
  z-index: 2;
}

.phone-screen {
  background: #f2f2f7;
  border-radius: 26px;
  min-height: 380px;
  overflow: hidden;
  padding: 16px;
  display: flex;
  flex-direction: column;
}

/* ── Example 1: Task list ── */
.preview-task-header {
  font-size: 1.5rem;
  font-weight: 700;
  color: #000;
  margin-bottom: 12px;
  font-family: -apple-system, sans-serif;
}

.preview-task-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 0;
  border-bottom: 1px solid rgba(0,0,0,0.07);
  font-size: 0.85rem;
  font-family: -apple-system, sans-serif;
  color: #000;
}

.preview-task-check {
  width: 22px;
  height: 22px;
  border-radius: 50%;
  border: 2px solid #007aff;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.preview-task-check.done {
  background: #007aff;
  border-color: #007aff;
}

.preview-task-check.done::after {
  content: '';
  width: 5px;
  height: 9px;
  border: 2px solid #fff;
  border-top: none;
  border-left: none;
  transform: rotate(45deg) translateY(-1px);
}

.preview-task-text.done {
  text-decoration: line-through;
  color: #999;
}

/* ── Example 2: Profile card ── */
.preview-card-screen {
  background: linear-gradient(145deg, #e8eaf6, #e3f2fd);
  justify-content: center;
  align-items: center;
}

.preview-card {
  background: rgba(255,255,255,0.72);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  padding: 22px 20px;
  text-align: center;
  width: 100%;
  box-shadow: 0 4px 20px rgba(0,0,0,0.1);
  font-family: -apple-system, sans-serif;
}

.preview-avatar {
  width: 72px;
  height: 72px;
  border-radius: 50%;
  background: linear-gradient(135deg, #007aff, #5ac8fa);
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 10px;
  font-size: 1.3rem;
  font-weight: 700;
  color: #fff;
}

.preview-card-name {
  font-size: 1rem;
  font-weight: 700;
  color: #000;
  margin-bottom: 3px;
}

.preview-card-role {
  font-size: 0.78rem;
  color: #666;
  margin-bottom: 12px;
}

.preview-card-pills {
  display: flex;
  justify-content: center;
  gap: 8px;
  flex-wrap: wrap;
}

.preview-card-pill {
  font-size: 0.68rem;
  color: #555;
  background: rgba(0,0,0,0.06);
  padding: 3px 9px;
  border-radius: 12px;
}

/* ── Example 3: Animated button ── */
.preview-anim-screen {
  background: #f2f2f7;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

.preview-anim-btn {
  padding: 13px 32px;
  border-radius: 30px;
  font-size: 0.95rem;
  font-weight: 600;
  border: none;
  cursor: pointer;
  font-family: -apple-system, sans-serif;
  transition: background 0.25s, transform 0.15s;
  outline: none;
  color: #fff;
  background: #007aff;
}

.preview-anim-btn.liked {
  background: #ff2d55;
  transform: scale(0.95);
}

.preview-anim-hint {
  font-size: 0.7rem;
  color: #999;
  font-family: -apple-system, sans-serif;
}
</style>

<div class="swiftui-playground">
  <div class="playground-tabs">
    <button class="playground-tab active" onclick="switchExample(0)">Task List</button>
    <button class="playground-tab" onclick="switchExample(1)">Profile Card</button>
    <button class="playground-tab" onclick="switchExample(2)">Animated Button</button>
  </div>

  <div class="playground-panels">
    <!-- Code panel -->
    <div class="code-panel">
      <div class="code-panel-titlebar">
        <div class="titlebar-dot red"></div>
        <div class="titlebar-dot yellow"></div>
        <div class="titlebar-dot green"></div>
        <span class="titlebar-label" id="codeFilename">TaskListView.swift</span>
      </div>
      <pre class="code-content" id="codeContent"></pre>
    </div>

    <!-- Preview panel -->
    <div class="preview-panel">
      <span class="preview-label">▶ Live Preview</span>
      <div class="phone-frame">
        <div class="phone-notch"></div>
        <div class="phone-screen" id="phoneScreen"></div>
      </div>
    </div>
  </div>
</div>

<script>
var examples = [
  {
    filename: 'TaskListView.swift',
    code: [
      {t:'keyword',v:'struct'}, ' ', {t:'type',v:'TaskListView'}, ': ', {t:'type',v:'View'}, ' {\n',
      '  ', {t:'modifier',v:'@State'}, ' ', {t:'keyword',v:'private'}, ' ', {t:'keyword',v:'var'}, ' ', {t:'prop',v:'tasks'}, ' = [\n',
      '    ', {t:'type',v:'Task'}, '(title: ', {t:'string',v:'"Design new feature"'}, ', done: ', {t:'keyword',v:'true'}, '),\n',
      '    ', {t:'type',v:'Task'}, '(title: ', {t:'string',v:'"Review PR #42"'}, ', done: ', {t:'keyword',v:'false'}, '),\n',
      '    ', {t:'type',v:'Task'}, '(title: ', {t:'string',v:'"Ship the update"'}, ', done: ', {t:'keyword',v:'false'}, '),\n',
      '  ]\n\n',
      '  ', {t:'keyword',v:'var'}, ' ', {t:'prop',v:'body'}, ': ', {t:'keyword',v:'some'}, ' ', {t:'type',v:'View'}, ' {\n',
      '    ', {t:'type',v:'VStack'}, '(alignment: .', {t:'param',v:'leading'}, ', spacing: ', {t:'number',v:'12'}, ') {\n',
      '      ', {t:'type',v:'Text'}, '(', {t:'string',v:'"Today"'}, ')\n',
      '        .font(.', {t:'param',v:'largeTitle'}, '.', {t:'param',v:'bold'}, '())\n',
      '        .padding(.', {t:'param',v:'bottom'}, ', ', {t:'number',v:'4'}, ')\n',
      '      ', {t:'type',v:'ForEach'}, '($', {t:'prop',v:'tasks'}, ') { $', {t:'prop',v:'task'}, ' ', {t:'keyword',v:'in\n'},
      '        ', {t:'type',v:'TaskRow'}, '(task: $', {t:'prop',v:'task'}, ')\n',
      '      }\n',
      '    }\n',
      '    .padding()\n',
      '  }\n',
      '}'
    ],
    preview: `
      <div class="preview-task-header">Today</div>
      <div class="preview-task-item">
        <div class="preview-task-check done"></div>
        <span class="preview-task-text done">Design new feature</span>
      </div>
      <div class="preview-task-item">
        <div class="preview-task-check"></div>
        <span class="preview-task-text">Review PR #42</span>
      </div>
      <div class="preview-task-item">
        <div class="preview-task-check"></div>
        <span class="preview-task-text">Ship the update</span>
      </div>
    `,
    screenClass: ''
  },
  {
    filename: 'ProfileCard.swift',
    code: [
      {t:'keyword',v:'struct'}, ' ', {t:'type',v:'ProfileCard'}, ': ', {t:'type',v:'View'}, ' {\n',
      '  ', {t:'keyword',v:'var'}, ' ', {t:'prop',v:'body'}, ': ', {t:'keyword',v:'some'}, ' ', {t:'type',v:'View'}, ' {\n',
      '    ', {t:'type',v:'VStack'}, '(spacing: ', {t:'number',v:'12'}, ') {\n',
      '      ', {t:'type',v:'Circle'}, '()\n',
      '        .fill(.', {t:'param',v:'blue'}, '.', {t:'param',v:'gradient'}, ')\n',
      '        .frame(width: ', {t:'number',v:'80'}, ', height: ', {t:'number',v:'80'}, ')\n',
      '        .overlay(\n',
      '          ', {t:'type',v:'Text'}, '(', {t:'string',v:'"AC"'}, ')\n',
      '            .font(.', {t:'param',v:'title'}, '.', {t:'param',v:'bold'}, '())\n',
      '            .foregroundColor(.', {t:'param',v:'white'}, ')\n',
      '        )\n',
      '      ', {t:'type',v:'Text'}, '(', {t:'string',v:'"Andrea Cipriani"'}, ')\n',
      '        .font(.', {t:'param',v:'title2'}, '.', {t:'param',v:'bold'}, '())\n',
      '      ', {t:'type',v:'Text'}, '(', {t:'string',v:'"iOS Engineer"'}, ')\n',
      '        .foregroundColor(.', {t:'param',v:'secondary'}, ')\n',
      '    }\n',
      '    .padding(', {t:'number',v:'24'}, ')\n',
      '    .background(.', {t:'param',v:'ultraThinMaterial'}, ')\n',
      '    .cornerRadius(', {t:'number',v:'20'}, ')\n',
      '  }\n',
      '}'
    ],
    preview: `
      <div class="preview-avatar">AC</div>
      <div class="preview-card-name">Andrea Cipriani</div>
      <div class="preview-card-role">iOS Engineer</div>
      <div class="preview-card-pills">
        <span class="preview-card-pill">📍 NYC</span>
        <span class="preview-card-pill">⭐ 10 years</span>
      </div>
    `,
    screenClass: 'preview-card-screen',
    wrapClass: 'preview-card'
  },
  {
    filename: 'AnimatedButton.swift',
    code: [
      {t:'keyword',v:'struct'}, ' ', {t:'type',v:'AnimatedButton'}, ': ', {t:'type',v:'View'}, ' {\n',
      '  ', {t:'modifier',v:'@State'}, ' ', {t:'keyword',v:'private'}, ' ', {t:'keyword',v:'var'}, ' ', {t:'prop',v:'isLiked'}, ' = ', {t:'keyword',v:'false'}, '\n\n',
      '  ', {t:'keyword',v:'var'}, ' ', {t:'prop',v:'body'}, ': ', {t:'keyword',v:'some'}, ' ', {t:'type',v:'View'}, ' {\n',
      '    ', {t:'type',v:'Button'}, ' {\n',
      '      ', {t:'type',v:'withAnimation'}, '(.', {t:'param',v:'spring'}, '()) {\n',
      '        ', {t:'prop',v:'isLiked'}, '.', {t:'param',v:'toggle'}, '()\n',
      '      }\n',
      '    } label: {\n',
      '      ', {t:'type',v:'Text'}, '(', {t:'prop',v:'isLiked'}, ' ? ', {t:'string',v:'"Liked ♥"'}, ' : ', {t:'string',v:'"Like"'}, ')\n',
      '        .fontWeight(.', {t:'param',v:'semibold'}, ')\n',
      '        .padding(.', {t:'param',v:'horizontal'}, ', ', {t:'number',v:'28'}, ')\n',
      '        .background(', {t:'prop',v:'isLiked'}, ' ? .', {t:'param',v:'pink'}, ' : .', {t:'param',v:'blue'}, ')\n',
      '        .foregroundColor(.', {t:'param',v:'white'}, ')\n',
      '        .cornerRadius(', {t:'number',v:'25'}, ')\n',
      '        .scaleEffect(', {t:'prop',v:'isLiked'}, ' ? ', {t:'number',v:'0.95'}, ' : ', {t:'number',v:'1.0'}, ')\n',
      '    }\n',
      '  }\n',
      '}'
    ],
    preview: `
      <button class="preview-anim-btn" id="likeBtn" onclick="toggleLike()">Like</button>
      <span class="preview-anim-hint">tap to interact</span>
    `,
    screenClass: 'preview-anim-screen'
  }
];

var currentExample = 0;

function renderCode(tokens) {
  return tokens.map(function(tok) {
    if (typeof tok === 'string') return escHtml(tok);
    return '<span class="sw-' + tok.t + '">' + escHtml(tok.v) + '</span>';
  }).join('');
}

function escHtml(s) {
  return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
}

function switchExample(idx) {
  currentExample = idx;
  var ex = examples[idx];

  document.getElementById('codeFilename').textContent = ex.filename;
  document.getElementById('codeContent').innerHTML = renderCode(ex.code);

  var screen = document.getElementById('phoneScreen');
  screen.className = 'phone-screen ' + (ex.screenClass || '');

  var inner = ex.wrapClass
    ? '<div class="' + ex.wrapClass + '">' + ex.preview + '</div>'
    : ex.preview;
  screen.innerHTML = inner;

  document.querySelectorAll('.playground-tab').forEach(function(t, i) {
    t.classList.toggle('active', i === idx);
  });
}

function toggleLike() {
  var btn = document.getElementById('likeBtn');
  if (!btn) return;
  btn.classList.toggle('liked');
  btn.textContent = btn.classList.contains('liked') ? 'Liked ♥' : 'Like';
}

switchExample(0);
</script>
