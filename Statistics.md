# Drafts

```dataview
TABLE WITHOUT ID
	length(rows.file.name) as Amount,
	join(rows.file.link, ", ") as Files
FROM
	#draft
flatten
	file.tags as tag
group by
	tag
```


```dataview
TABLE
	length(file.inlinks) as Inlinks,
	length(file.outlinks) as Outlinks,
	(file.mday - file.cday).days as "Days Untouched"
FROM #draft
SORT
	length(file.inlinks) DESCENDING,
	(file.mday - file.cday).days DESCENDING
```