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

<script type="module">
  import { Cite } from "https://cdn.jsdelivr.net/npm/@citation-js/core@0.7.21/+esm";
  import "https://cdn.jsdelivr.net/npm/@citation-js/plugin-bibtex@0.7.21/+esm";
  import "https://cdn.jsdelivr.net/npm/@citation-js/plugin-csl@0.7.21/+esm";

  const bibUrl = "{{ '/assets/bibliography.bib' | relative_url }}";

  try {
    const bibtex = await fetch(bibUrl).then(r => {
      if (!r.ok) throw new Error(`BibTeX fetch failed: ${r.status} ${r.statusText}`);
      return r.text();
    });

    const cite = new Cite(bibtex);

    // Basic bibliography HTML (APA). If you want a different style later, we can load/register it.
    const entries = cite.get({ format: "object" });

    const html = entries.map(item => {
      const key = item.id || item._id || item.citationKey || "";
      const jpg = "{{ '/assets/images/pubs/' | relative_url }}" + key + ".jpg";
      const png = "{{ '/assets/images/pubs/' | relative_url }}" + key + ".png";

      const entryHtml = new Cite(item).format("bibliography", {
        format: "html",
        template: "apa",
        lang: "en-US"
      });

      return `
        <div class="pub-item">
          <div class="pub-thumb">
            ${key ? `<img src="${jpg}" alt="${key}"
                 onerror="if(!this.dataset.f){this.dataset.f=1; this.src='${png}'} else {this.style.display='none'}">` : ""}
          </div>
          <div class="pub-citation">${entryHtml}</div>
        </div>
      `;
    }).join("");

    document.getElementById("bib-output").innerHTML = html || "No publications found.";
  } catch (e) {
    console.error(e);
    document.getElementById("bib-output").textContent = "Failed to render publications (see console).";
  }
</script>
