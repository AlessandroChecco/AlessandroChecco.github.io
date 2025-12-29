---
layout: single
title: "Publications"
permalink: /publications/
---

<div id="bib-output"></div>

<script src="https://cdn.jsdelivr.net/npm/citation-js@0.7.21/build/citation.min.js"></script>


<script>
  fetch('/assets/bibliography.bib')
    .then(response => response.text())
    .then(bibtex => {
      // parse the BibTeX
      const cite = new Cite(bibtex);

      // format to HTML
      const html = cite.format('bibliography', {
        format: 'html',
        template: 'apa',
        lang: 'en-US'
      });

      document.getElementById('bib-output').innerHTML = html;
    })
    .catch(error => {
      console.error('Error loading bibliography:', error);
      document.getElementById('bib-output').innerText = 'Failed to load bibliography.';
    });
</script>
