#  Issue #2: List Formatting XML Validation Error
## Problem
"Couldn't save highlighted changes" error triggered only when typing within an indented numbered list.
## Diagnosis & Root Cause 
Corrupted `List Definition ID` in the document's underlying XML schema. The document was attempting to map new text to a list structure imported/malformed during PDF conversion.

## Resolution
Cleared existing style formatting and re-initialized the list structure using the native ribbon controls. This forced a regeneration of the list's `XML schema`, bypassing the validation conflict.

## Lessons Learned
* Sometimes even in a second version of your document, problems persist.
* Clearing formatting is a useful option
* Web-based MS 365 Word (my only option without buying a home MS Office license) has limited formatting functionality (ex. no double underlining)
  
## *Final Thoughts*
The 5 I was typing was triggering a re-calculation of the document's internal indexing. Because the PDF-to-Word conversion left behind orphaned XML nodes (likely from the original footnotes or bookmarks), the auto-save service is triggering a validation conflict between the local browser cache and the server's XML schema. When typing at the far left, I am in the "Normal" style. As soon as I move to an indented numbered list, the Word processor attempts to apply a List Definition ID (a specific XML tag that controls list numbering and indention). The document had a "broken" list definition inherited from the PDF conversion. The server was trying to map the new 5 to a list ID that doesn't exist or is corrupted, and it failed the save validation.
