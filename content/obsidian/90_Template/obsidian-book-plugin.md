---
title: "{{title}}"
created: "{{DATE:YYYY-MM-DD}}"
updated: "{{DATE:YYYY-MM-DD}}"
draft: false
cover: "{{coverUrl}}"
isbn: "{{isbn10}} {{isbn13}}"
localCover: "{{localCoverImage}}"
publish: "{{publishDate}}"
publisher: "{{publisher}}"
status: unread
tag:
  - 本
  - "<% tp.file.creation_date(\"YYYY\") %>/<% tp.file.creation_date(\"MM\") %>"
  - "{{author}}"
---

%% To save images locally, enable the 'Enable Cover Image Save' option in the settings and enter as follows: %%
<%* if (tp.frontmatter.localCover && tp.frontmatter.localCover.trim() !== "") { tR += `250` } %>

# {{title}}
