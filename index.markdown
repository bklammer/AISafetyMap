---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

Welcome to the AI Safety Concept Map! This is an attempt to visualize the current (as of June 2024) conceptual landscape of AI existential safety. The current , and links to learn more about any of the concepts represented below can be found at [AI Safety Map](https://docs.google.com/spreadsheets/d/1CFWHZQJPvF98DtyQtjiiK8upqksTPv-lAyKVYNSXCew/edit?usp=sharing) 

![AI Safety Map](/images/AISafetyMap.png)

<div id="sheet-content"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js"></script>

<script>
window.onload = function() {
  // Replace with the URL of your published Google Sheet
  const googleSheetUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vTYhM_ULxIhfVrF18oMrrqPDC6u-zfyIj58_KBMwM2-m4J5CCX-qc3tiQtEjW1nacPQnm1m02gtsSzK/pub?gid=0&single=true&output=csv';

  fetch(googleSheetUrl)
    .then(response => response.text())
    .then(csvString => {
      const data = Papa.parse(csvString, { header: true, skipEmptyLines: true }).data;
      const contentDiv = document.getElementById('sheet-content');

      data.forEach(row => {
        // Specify the fields you want to display
        const fields = ['field1', 'field2', 'field3'];
        const p = document.createElement('p');

        fields.forEach(field => {
          if (row[field]) {
            p.textContent += row[field] + ' ';
          }
        });

        contentDiv.appendChild(p);
      });
    });
}
</script>