---
layout: single
title: "Publications"
permalink: /publications/
---

<style>
  .pub-row { display:flex; gap:1rem; margin: 0 0 1rem 0; align-items:flex-start; }
  .pub-thumb { width:120px; flex: 0 0 120px; }
  .pub-thumb img { max-width:120px; height:auto; border-radius:6px; }
  .pub-body { flex: 1 1 auto; }
  .pub-title { font-weight:600; }
  .pub-meta { font-size:0.95em; opacity:0.9; }
</style>

<!-- BibTeX-js reads the BibTeX file from the "src" attribute -->
<bibtex src="{{ '/assets/bibliography.bib' | relative_url }}"></bibtex>

<!-- Template for each entry -->
<div id="bibtex_display">
  <div class="bibtex_template">
    <div class="pub-row">
      <div class="pub-thumb">
        <img class="pub-img" alt="thumbnail" style="display:none;">
        <span class="bibtexkey pub-key" style="display:none;"></span>
      </div>
      <div class="pub-body">
        <div class="pub-title">
          <span class="title"></span>
        </div>
        <div class="pub-meta">
          <span class="author"></span>
          (<span class="year"></span>)
          <span class="journal"></span><span class="booktitle"></span>
        </div>
        <div class="pub-meta">
          <a class="url" target="_blank"></a>
          <a class="doi" target="_blank"></a>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- Load BibTeX-js -->
<script src="https://cdn.jsdelivr.net/gh/pcooksey/bibtex-js@master/src/bibtex_js.js"></script>

<script>
  document.addEventListener('bibtex_js_loaded', function () {

    // DOI links
    document.querySelectorAll('#bibtex_display .doi').forEach(a => {
      const doi = a.textContent.trim();
      if (doi) {
        a.textContent = 'DOI';
        a.href = 'https://doi.org/' + doi;
      } else {
        a.remove();
      }
    });

    // URL links
    document.querySelectorAll('#bibtex_display .url').forEach(a => {
      const url = a.getAttribute('href') || a.textContent.trim();
      if (url) {
        a.textContent = 'Link';
        a.href = url;
      } else {
        a.remove();
      }
    });

    // Thumbnails (retry until bibtex-js has rendered rows)
    const base = "{{ '/assets/images/pubs/' | relative_url }}";
    let tries = 0;

    const timer = setInterval(() => {
      tries += 1;

      const rows = document.querySelectorAll('#bibtex_display .pub-row');
      console.log("thumb rows:", rows.length, "try:", tries);

      rows.forEach(row => {
        const keyEl = row.querySelector('.pub-key');
        const imgEl = row.querySelector('.pub-img');
        if (!keyEl || !imgEl) return;

        // skip if already set
        if (imgEl.dataset.bound) return;
        imgEl.dataset.bound = "1";

        const key = (keyEl.textContent || '').trim();
        if (!key) return;

        const png = base + key + ".png";
        imgEl.onload = () => { imgEl.style.display = ""; };
        imgEl.onerror = () => { imgEl.style.display = "none"; };

        imgEl.src = png;
      });

      // Stop when rows exist or after ~3 seconds
      if (rows.length > 0 || tries >= 10) clearInterval(timer);
    }, 300);
  });
</script>

<script>
  console.log("PUBLICATIONS PAGE CUSTOM JS LOADED");
</script>

