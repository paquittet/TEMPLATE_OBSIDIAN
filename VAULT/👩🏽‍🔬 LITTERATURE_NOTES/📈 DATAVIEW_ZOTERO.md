


```dataview  
TABLE
  title AS Title,
  Contribution AS Contribution,
  replace(replace(replace(status, "unread", "🟥"), "progress", "🟧"), "read", "🟩") AS Statut
FROM "👩🏽‍🔬 LITTERATURE_NOTES/ANNOTATIONS"
SORT number(Year) ASC
SORT status ASC
```


