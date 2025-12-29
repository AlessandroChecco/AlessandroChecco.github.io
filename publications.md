---
layout: single
title: "Publications"
permalink: /publications/
---

<div id="bib-output"></div>

<!-- Load Citation.js (browser build exposing Cite) -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/citation-js/0.7.20/citation.min.js"></script>

<script>
  fetch('/assets/bibliography.bib')
    .then(response => response.text())
    .then(bibtex => {
      // Create a new citation instance
      const cite = new Cite(bibtex);

      // Format the bibliography as HTML
      const html = cite.format('bibliography', {
        format: 'html',
        template: 'apa',
        lang: 'en-US'
      });

      // Insert into the page
      document.getElementById('bib-output').innerHTML = html;
    })
    .catch(error => {
      console.error('Error loading BibTeX:', error);
      document.getElementById('bib-output').innerText = 'Failed to load bibliography.';
    });
</script>
