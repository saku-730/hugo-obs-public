---
title: "<% tp.file.title %>"
tags:
  - Weekly
  - "<% tp.file.creation_date(\"YYYY\") %>/<% tp.file.creation_date(\"MM\") %>"
date: "<% tp.file.creation_date() %>"
---
[progress]({{< relref "10_Projects/progress.md" >}})

## やらないといけないこと

- [ ] 

## やったほうがいいこと

- [ ]

<%*
	for(let i = 0; i < 7; i++){
		let dailyTitle = tp.date.weekday("YYYY-MM-DD",i);
		
		// Add Link
		let dailyLink = "" + dailyTitle + "";
		tR += "\n" + dailyLink;		
	}
 %>