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
  // Make DOI links clickable if present
  document.addEventListener('bibtex_js_loaded', function () {
    document.querySelectorAll('#bibtex_display .doi').forEach(a => {
      const doi = a.textContent.trim();
      if (doi) {
        a.textContent = 'DOI';
        a.href = 'https://doi.org/' + doi;
      } else {
        a.remove();
      }
    });

    // Make URL links pretty
    document.querySelectorAll('#bibtex_display .url').forEach(a => {
      const url = a.getAttribute('href') || a.textContent.trim();
      if (url) {
        a.textContent = 'Link';
        a.href = url;
      } else {
        a.remove();
      }
    });

        document.querySelectorAll('#bibtex_display .pub-row').forEach(row => {
      const keyEl = row.querySelector('.pub-key');
      const imgEl = row.querySelector('.pub-img');
      if (!keyEl || !imgEl) return;

      const key = (keyEl.textContent || '').trim();
      if (!key) return;

      const base = "{{ '/assets/images/pubs/' | relative_url }}";
      imgEl.src = base + key + ".png";
      imgEl.style.display = "";
      
      imgEl.onerror = () => {
        imgEl.style.display = "none";
      };

          
    });
  });
</script>
