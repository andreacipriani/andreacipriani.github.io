---
layout: page
permalink: /books/
title: Andrea's Bookshelf
nav: false
description: Some books that shaped the way I think.
---

<style>
.books-slideshow {
  position: relative;
  max-width: 680px;
  margin: 2rem auto;
  user-select: none; /* prevents accidental text selection while swiping */
}

.books-track-wrapper {
  overflow: hidden;
  border-radius: 12px;
}

.books-track {
  display: flex;
  transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.book-slide {
  min-width: 100%;
  display: flex;
  align-items: center;
  gap: 2rem;
  padding: 2rem;
  background: var(--global-bg-color);
  border: 1px solid var(--global-divider-color);
  border-radius: 12px;
  box-sizing: border-box;
}

.book-cover {
  flex-shrink: 0;
  width: 120px;
  height: 180px;
  object-fit: cover;
  border-radius: 4px;
  box-shadow: 4px 4px 12px rgba(0,0,0,0.25);
}

.book-cover-placeholder {
  flex-shrink: 0;
  width: 120px;
  height: 180px;
  border-radius: 4px;
  background: var(--global-divider-color);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
}

.book-info {
  flex: 1;
  user-select: text;
}

.book-title {
  font-size: 1.4rem;
  font-weight: 700;
  margin: 0 0 0.4rem;
  color: var(--global-text-color);
  line-height: 1.3;
}

.book-author {
  font-size: 1rem;
  color: var(--global-theme-color);
  margin: 0 0 1rem;
  font-style: italic;
}

.book-link {
  display: inline-block;
  font-size: 0.85rem;
  color: var(--global-theme-color);
  text-decoration: none;
  border: 1px solid var(--global-theme-color);
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  transition: background 0.2s, color 0.2s;
}

.book-link:hover {
  background: var(--global-theme-color);
  color: #fff;
  text-decoration: none;
}

.books-nav {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  margin-top: 1.2rem;
}

.books-btn {
  background: none;
  border: 1px solid var(--global-divider-color);
  color: var(--global-text-color);
  width: 38px;
  height: 38px;
  border-radius: 50%;
  font-size: 1rem;
  cursor: pointer;
  transition: border-color 0.2s, background 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
}

.books-btn:hover {
  border-color: var(--global-theme-color);
  background: var(--global-theme-color);
  color: #fff;
}

.books-counter {
  font-size: 0.8rem;
  color: var(--global-text-color-light, #888);
  min-width: 36px;
  text-align: center;
}

.books-dots {
  display: flex;
  gap: 6px;
}

.books-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--global-divider-color);
  cursor: pointer;
  transition: background 0.2s;
  border: none;
  padding: 0;
}

.books-dot.active {
  background: var(--global-theme-color);
}

.books-loading {
  text-align: center;
  padding: 3rem;
  color: var(--global-text-color-light, #888);
  font-style: italic;
}
</style>

<div class="books-slideshow">
  <div class="books-track-wrapper">
    <div class="books-track" id="booksTrack">
      <div class="books-loading">Loading bookshelf…</div>
    </div>
  </div>

  <div class="books-nav">
    <button class="books-btn" id="booksPrev" aria-label="Previous">&#8592;</button>
    <div class="books-dots" id="booksDots"></div>
    <span class="books-counter" id="booksCounter"></span>
    <button class="books-btn" id="booksNext" aria-label="Next">&#8594;</button>
  </div>
</div>

<script>
(function() {
  function parseCSVLine(line) {
    var result = [];
    var inQuotes = false;
    var val = '';
    for (var i = 0; i < line.length; i++) {
      var ch = line[i];
      if (ch === '"') {
        if (inQuotes && line[i+1] === '"') { val += '"'; i++; }
        else { inQuotes = !inQuotes; }
      } else if (ch === ',' && !inQuotes) {
        result.push(val); val = '';
      } else {
        val += ch;
      }
    }
    result.push(val);
    return result;
  }

  function cleanISBN(raw) {
    // strips ="..." wrapper from Goodreads Excel export: raw = ="0465026567"
    return raw.replace(/^[="]+/, '').replace(/"+$/, '').trim();
  }

  // Books to exclude by ID
  var EXCLUDE_IDS = {
    '49402100': true, // Francesco Costa
    '13329968': true, // What I Talk About... (Harry Styles edition)
    '3228917':  true, // Outliers
    '18807860': true  // Catalogo delle idee chic (duplicate of Dictionary of Accepted Ideas)
  };

  // Title overrides — strip subtitles from verbose Goodreads titles
  var TITLE_OVERRIDES = {
    '141526': 'Pulp',                // Bukowski
    '6751':   'Consider the Lobster' // DFW
  };

  // Hardcoded cover overrides for books with no ISBN or obscure editions
  var COVER_OVERRIDES = {
    '5297':     'https://covers.openlibrary.org/b/isbn/9780141439570-M.jpg', // Dorian Gray Penguin Classics
    '35336032': 'https://covers.openlibrary.org/b/isbn/9780140442274-M.jpg', // Schopenhauer Essays (Penguin)
    '18620743': 'https://covers.openlibrary.org/b/isbn/9780141183534-M.jpg', // Swann's Way Penguin Classics
    '11297':    'https://covers.openlibrary.org/b/isbn/9780375704024-M.jpg', // Norwegian Wood Vintage
    '16107147': 'https://covers.openlibrary.org/b/isbn/9780806508085-M.jpg'  // Artificial Paradises Citadel Press
  };

  // Books to pin to specific positions after sort (0-indexed)
  var PIN_SECOND = '11468377';  // Thinking, Fast and Slow → position 1
  var PIN_LAST   = '5297';      // Dorian Gray → last

  fetch('/assets/data/goodreads.csv')
    .then(function(r) { return r.text(); })
    .then(function(text) {
      var lines = text.split('\n').filter(function(l) { return l.trim(); });
      var headers = parseCSVLine(lines[0]);
      var idxBookId   = headers.indexOf('Book Id');
      var idxTitle    = headers.indexOf('Title');
      var idxAuthor   = headers.indexOf('Author');
      var idxRating   = headers.indexOf('My Rating');
      var idxISBN     = headers.indexOf('ISBN');
      var idxISBN13   = headers.indexOf('ISBN13');

      var books = [];
      for (var i = 1; i < lines.length; i++) {
        var cols = parseCSVLine(lines[i]);
        var id = cols[idxBookId];
        if (EXCLUDE_IDS[id]) continue;
        var rating = parseInt(cols[idxRating], 10);
        if (rating > 3) {
          var isbn = cleanISBN(cols[idxISBN13]) || cleanISBN(cols[idxISBN]);
          books.push({
            id:     id,
            title:  TITLE_OVERRIDES[id] || cols[idxTitle],
            author: cols[idxAuthor],
            isbn:   isbn,
            rating: rating
          });
        }
      }

      // Sort by rating descending, preserving CSV order for ties
      books.sort(function(a, b) { return b.rating - a.rating; });

      // Pin Thinking Fast and Slow to position 1 (second)
      var secondIdx = books.findIndex(function(b) { return b.id === PIN_SECOND; });
      if (secondIdx > 1) {
        books.splice(1, 0, books.splice(secondIdx, 1)[0]);
      }

      // Pin Dorian Gray to last position
      var lastIdx = books.findIndex(function(b) { return b.id === PIN_LAST; });
      if (lastIdx !== -1 && lastIdx !== books.length - 1) {
        books.push(books.splice(lastIdx, 1)[0]);
      }

      var track = document.getElementById('booksTrack');
      var dotsContainer = document.getElementById('booksDots');
      var prevBtn = document.getElementById('booksPrev');
      var nextBtn = document.getElementById('booksNext');
      var counter = document.getElementById('booksCounter');
      var current = 0;

      track.innerHTML = '';
      dotsContainer.innerHTML = '';

      books.forEach(function(book, i) {
        var coverUrl = COVER_OVERRIDES[book.id]
          || (book.isbn ? 'https://covers.openlibrary.org/b/isbn/' + book.isbn + '-M.jpg' : '');
        var goodreadsUrl = 'https://www.goodreads.com/book/show/' + book.id;

        var slide = document.createElement('div');
        slide.className = 'book-slide';
        slide.innerHTML =
          (coverUrl
            ? '<img class="book-cover" src="' + coverUrl + '" alt="' + book.title.replace(/"/g,'&quot;') + '" onerror="this.style.display=\'none\';this.nextElementSibling.style.display=\'flex\';">'
            : '') +
          '<div class="book-cover-placeholder" style="' + (coverUrl ? 'display:none;' : '') + '">📖</div>' +
          '<div class="book-info">' +
            '<p class="book-title">' + book.title + '</p>' +
            '<p class="book-author">' + book.author + '</p>' +
            '<a class="book-link" href="' + goodreadsUrl + '" target="_blank" rel="noopener">View on Goodreads</a>' +
          '</div>';
        track.appendChild(slide);

        var dot = document.createElement('button');
        dot.className = 'books-dot' + (i === 0 ? ' active' : '');
        dot.setAttribute('aria-label', 'Go to book ' + (i + 1));
        dot.addEventListener('click', function() { goTo(i); });
        dotsContainer.appendChild(dot);
      });

      if (counter) counter.textContent = '1 / ' + books.length;

      function goTo(index) {
        current = (index + books.length) % books.length;
        track.style.transform = 'translateX(-' + (current * 100) + '%)';
        dotsContainer.querySelectorAll('.books-dot').forEach(function(d, i) {
          d.classList.toggle('active', i === current);
        });
        if (counter) counter.textContent = (current + 1) + ' / ' + books.length;
      }

      prevBtn.addEventListener('click', function() { goTo(current - 1); });
      nextBtn.addEventListener('click', function() { goTo(current + 1); });

      document.addEventListener('keydown', function(e) {
        if (e.key !== 'ArrowLeft' && e.key !== 'ArrowRight') return;
        var rect = track.getBoundingClientRect();
        if (rect.bottom < 0 || rect.top > window.innerHeight) return;
        if (e.key === 'ArrowLeft') goTo(current - 1);
        if (e.key === 'ArrowRight') goTo(current + 1);
      });
    })
    .catch(function() {
      document.getElementById('booksTrack').innerHTML =
        '<div class="books-loading">Could not load bookshelf.</div>';
    });
})();
</script>
