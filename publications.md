---
layout: single
title: "Publications"
permalink: /publications/
---

<div id="bib-output">Loading publications…</div>

<!-- Citation.js browser bundle (defines require() and registers 'citation-js' module) -->
<script src="https://cdn.jsdelivr.net/npm/citation-js"></script>

<script>
  (function () {
    const outputEl = document.getElementById('bib-output');
    const bibUrl = "{{ '/assets/bibliography.bib' | relative_url }}";

    // Basic sanity checks
    if (typeof require !== 'function') {
      outputEl.textContent = "Error: Citation.js bundle did not provide require().";
      return;
    }

    const Cite = require('citation-js');
    if (typeof Cite !== 'function') {
      outputEl.textContent = "Error: citation-js module did not load correctly.";
      return;
    }

    fetch(bibUrl)
      .then(r => {
        if (!r.ok) throw new Error(`BibTeX fetch failed: ${r.status} ${r.statusText}`);
        return r.text();
      })
      .then(bibtex => {
        const cite = new Cite(bibtex);

        const html = cite.format('bibliography', {
          format: 'html',
          template: 'apa',
          lang: 'en-US'
        });

        outputEl.innerHTML = html;
      })
      .catch(err => {
        console.error(err);
        outputEl.textContent = "Failed to render publications (see console).";
      });
  })();
</script>
