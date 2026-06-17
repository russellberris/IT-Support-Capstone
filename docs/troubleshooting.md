## 6/17/26 Day 1
## Issue 1: Corrupted MS Word Document (XML/Footnote Error)

## Problem Statement
While working on the Capstone documentation in Microsoft Word (Online), I wanted to add a footnot explaining one of my instruction steps. In that step, I termed Per Scholas as "the company", and wanted to add an explanatory footnote that the word "company" refers to Per Scholas in the context of their instructions on how to complete the assignment, and not to an actual real-world business.  In an effort to view the footnote I had created, which had disappeared for some unknown reason, I switched to another view mode I was unfamiliar with, and a `file synchronization error` occurred, resulting in the file becoming read-only and displaying a `document contains footnotes that are invalid` error. Standard interface controls (Ribbon, Save As) were locked, preventing access to the content. The Esc key did nothing, and the page provided no `Undo` option. I used Google Gemini to walk me through how to recover my work.

## Diagnosis
* **Root Cause:** A OneDrive synchronization failure ("Purple X") caused the internal XML structure of the document to become malformed.
* **Specific Issue:** The footnote objects (which rely on complex cross-reference XML pointers) were no longer mapping correctly to the document body, causing the web-based renderer to lock the file for protection.

## Solution Steps
1.  **Extraction:** When direct editing was locked, I exported the document as a PDF to ensure data preservation.
2.  **Conversion:** I then used an online PDF-to-Word (.docx) conversion utility to strip the malformed XML structure and rebuild the document framework.
3.  **Recovery:** I re-uploaded the sanitized file to the Microsoft 365 cloud environment to restore full editing functionality. There were some lingering conversion artifacts, mainly bookmark symbols that had appeared in the left margins, but these were removed by unchecking a `show bookmarks` option in Word.

## Lessons Learned
* **Versioning:** Relying on autosave in a single cloud instance is a risk during network instability. Moving forward, I will utilize manual local backups.
* **File Stability:** Avoid using proprietary "Reader Modes" when working with documents containing complex elements like cross-references or footnotes.
* **Technical Agility:** By utilizing different file formats (PDF, DOCX) and platforms (Office 365, .docx > PDF conversion, PDF > .docx conversion), I was able to decouple the content from the corrupted formatting.

## Final Thoughts
In retrospect, I probably tried to get too fancy in my formatting when I attempted in Microsoft 365 (cloud-based) Word to add footnotes. I clicked on a reader/view mode that I knew nothing about in an attempt to view my footnote I had just typed. In the future, I will stick to what I know inside MS Word, and not go snooping around into modes I am unfamiliar with.  The cloud environment of MS Office can be a little trickier than the conventional home-licensed MS Office that I grew up on in the 90s and 2000s. I realized my word processing skills are a little rusty, and that I should simplify my approach in order to not only avoid crashes like that in the future, but to finish my project on time.

## 6/17/26 Day 1
  ### Issue 2: List Formatting XML Validation Error
*   **Symptom:** "Couldn't save highlighted changes" error triggered only when typing within an indented numbered list.
*   **Root Cause:** Corrupted `List Definition ID` in the document's underlying XML schema. The document was attempting to map new text to a list structure imported/malformed during PDF conversion.
*   **Resolution:** Cleared existing style formatting and re-initialized the list structure using the native ribbon controls. This forced a regeneration of the list's XML schema, bypassing the validation conflict.

# The Technical Explanation: The 5 you are typing is triggering a re-calculation of the document's internal indexing. Because your PDF-to-Word conversion left behind orphaned XML nodes (likely from the original footnotes or bookmarks), the auto-save service is triggering a validation conflict between the local browser cache and the server's XML schema. When you type at the far left, you are in the "Normal" style. As soon as you move to an indented numbered list, the Word processor attempts to apply a List Definition ID (a specific XML tag that controls list numbering and indention). Your document currently has a "broken" list definition inherited from the PDF conversion. The server is trying to map your new 5 to a list ID that doesn't exist or is corrupted, and it is failing the save validation.
