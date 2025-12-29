---
layout: single
title: "Publications"
permalink: /publications/
---

<style>
  .pub-item { display:flex; gap:1rem; margin: 0 0 1rem 0; align-items:flex-start; }
  .pub-thumb { width:120px; flex: 0 0 120px; }
  .pub-thumb img { max-width:120px; height:auto; border-radius:6px; }
  .pub-citation { flex: 1 1 auto; }
</style>

<div id="bib-output">Loading publications…</div>

<!-- 1) AMD loader -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.6/require.min.js"></script>

<!-- 2) Citation.js browser bundle (AMD module "citation-js") -->
<script src="https://cdn.jsdelivr.net/npm/citation-js@0.7.21/build/citation.min.js"></script>

<script>
  // 3) Use AMD require() to load the module
  require(['citation-js'], function (Cite) {
    const bibUrl = "{{ '/assets/bibliography.bib' | relative_url }}";

    fetch(bibUrl)
      .then(r => {
        if (!r.ok) throw new Error(`BibTeX fetch failed: ${r.status} ${r.statusText}`);
        return r.text();
      })
      .then(bibtex => {
        const cite = new Cite(bibtex);

        // Cite#format() is the documented way to produce a bibliography
        const entries = cite.data || [];

        const html = entries.map(item => {
          // item.id is typically the BibTeX key after conversion
          const key = item.id || '';

          const jpg = "{{ '/assets/images/pubs/' | relative_url }}" + key + ".jpg";
          const png = "{{ '/assets/images/pubs/' | relative_url }}" + key + ".png";

          const entryHtml = new Cite(item).format('bibliography', {
            format: 'html',
            template: 'apa',
            lang: 'en-US'
          });

          return `
            <div class="pub-item">
              <div class="pub-thumb">
                ${key ? `<img src="${jpg}" alt="${key}"
                     onerror="if(!this.dataset.f){this.dataset.f=1; this.src='${png}'} else {this.style.display='none'}">` : ''}
              </div>
              <div class="pub-citation">${entryHtml}</div>
            </div>
          `;
        }).join('');

        document.getElementById('bib-output').innerHTML = html || 'No publications found.';
      })
      .catch(err => {
        console.error(err);
        document.getElementById('bib-output').textContent = 'Failed to render publications (see console).';
      });
  });
</script>

