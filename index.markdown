---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

Welcome to the AI Safety Concept Map! This is an attempt to visualize the conceptual landscape of AI existential safety (as of June 2024). The current diagram is largely based on the content of the [AI Safety Fundamentals Alignment Course](https://aisafetyfundamentals.com/alignment/) run by BlueDot Impact.

![AI Safety Map](/images/AISafetyMap.png)

Here's a breakdown of the concepts and themes visualized above alongside links to learn more. If you have any feedback on anything, checkout the "About" page or comment on [AI Safety Concept Map](https://docs.google.com/spreadsheets/d/1CFWHZQJPvF98DtyQtjiiK8upqksTPv-lAyKVYNSXCew/edit?usp=sharing).

<div id="sheet-content"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js"></script>

<script>
window.onload = function() {
  // URL of published Google Sheet
  const googleSheetUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vTYhM_ULxIhfVrF18oMrrqPDC6u-zfyIj58_KBMwM2-m4J5CCX-qc3tiQtEjW1nacPQnm1m02gtsSzK/pub?gid=0&single=true&output=csv';

  fetch(googleSheetUrl)
    .then(response => response.text())
    .then(csvString => {
      const data = Papa.parse(csvString, { header: true, skipEmptyLines: true }).data;
      const contentDiv = document.getElementById('sheet-content');

      // Sort the data by the "tags" field
      data.sort((a, b) => a.tags.localeCompare(b.tags));

      // Declare counter to keep track of the section
      let current_section = "";

      data.forEach(row => {
        // Generate section titles
        const h2 = document.createElement('h2');

        if (row.tags !== current_section) {
          current_section = row.tags;
          h2.textContent = current_section;
        }

        contentDiv.appendChild(h2);

        // Generate topic titles
        const h3 = document.createElement('h3');
        h3.textContent = row['LongLabel'];
        contentDiv.appendChild(h3);

        // Generate description and link preamble
        const p = document.createElement('p');
        p.textContent = row['Description'];
        contentDiv.appendChild(p);
        
        // Generate links
        const ul = document.createElement('ul');
        const li1 = document.createElement('li');
        const li2 = document.createElement('li');
        const a1 = document.createElement('a');
        const a2 = document.createElement('a');
        a1.href = row['Link'];
        a1.textContent = row['LinkTitle'];
        li1.appendChild(a1);
        ul.appendChild(li1);
        a2.href = row['AISFLink'];
        a2.textContent = row['AISFLinkTitle'];
        li2.appendChild(a2);
        ul.appendChild(li2);
        contentDiv.appendChild(ul);
      });
    });
};
</script>