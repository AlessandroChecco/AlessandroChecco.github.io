---
layout: single
title: "Publications"
permalink: /publications/
---

<div id="bib-output">
  <!-- JavaScript will render the bibliography here -->
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/citation-js/0.7.20/citation.min.js"></script>
<script>
  fetch('/assets/references.bib')
    .then(response => response.text())
    .then(bibtex => {
      const Cite = citation.Cite || citation.Cite; // Citation.js object
      const cite = new Cite(bibtex);
      const html = cite.format('bibliography', {
        format: 'html',
        template: 'apa',
        lang: 'en-US'
      });
      document.getElementById('bib-output').innerHTML = html;
    });
</script>
