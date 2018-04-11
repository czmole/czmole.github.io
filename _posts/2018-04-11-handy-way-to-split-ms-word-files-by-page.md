---
layout: post
title: Handy way to split MS Word files by page
---

I was looking for a way to create dynamically the files for [RePEc](https://ideas.repec.org/t/booktemplate.html)  for an academic journal starting from a CSV file.

I used MS Word mail merge function that generated a big file, each record (future .rdf file for RePEc) on a different page, separated by a page break. 

Next I needed to create one file for each of the records. 

After some google search I got to [this page](https://www.extendoffice.com/documents/word/966-word-split-documents-into-multiple-documents.html).

There are multiple solutions offered but I choose the one using some VBA code and steps (I reproduce them below just in case, but  you can also try the other versions, the MS Word plugin they suggest is pretty cool but you can use it for free for 60 days):

1. Press Alt + F11 keys together to open the Microsoft Visual Basic for Application window;

2. Click Insert > Module, and then paste below VBA code into the new opening Module window.

3. Then click Run button or press F5 key to apply the VBA. Note: The splitting documents will be saved to the same place with the original file.

```vba
Sub SplitIntoPages()
	Dim docMultiple As Document
	Dim docSingle As Document
	Dim rngPage As Range
	Dim iCurrentPage As Integer
	Dim iPageCount As Integer
	Dim strNewFileName As String
	Application.ScreenUpdating = False 'Makes the code run faster and reduces screen _
	flicker a bit.
	Set docMultiple = ActiveDocument 'Work on the active document _
	(the one currently containing the Selection)
	Set rngPage = docMultiple.Range 'instantiate the range object
	iCurrentPage = 1
'get the document's page count
	iPageCount = docMultiple.Content.ComputeStatistics(wdStatisticPages)
	Do Until iCurrentPage > iPageCount
		If iCurrentPage = iPageCount Then
			rngPage.End = ActiveDocument.Range.End 'last page (there won't be a next page)
		Else
'Find the beginning of the next page
'Must use the Selection object. The Range.Goto method will not work on a page
			Selection.GoTo wdGoToPage, wdGoToAbsolute, iCurrentPage + 1
'Set the end of the range to the point between the pages
			rngPage.End = Selection.Start
		End If
		rngPage.Copy 'copy the page into the Windows clipboard
		Set docSingle = Documents.Add 'create a new document
		docSingle.Range.Paste 'paste the clipboard contents to the new document
'remove any manual page break to prevent a second blank
		docSingle.Range.Find.Execute Findtext:="^m", ReplaceWith:=""
'build a new sequentially-numbered file name based on the original multi-paged file name and path
		strNewFileName = Replace(docMultiple.FullName, ".doc", "_" & Right$("000" & iCurrentPage, 4) & ".doc")
		docSingle.SaveAs strNewFileName 'save the new single-paged document
		iCurrentPage = iCurrentPage + 1 'move to the next page
		docSingle.Close 'close the new document
		rngPage.Collapse wdCollapseEnd 'go to the next page
	Loop 'go to the top of the do loop
	Application.ScreenUpdating = True 'restore the screen updating
'Destroy the objects.
	Set docMultiple = Nothing
	Set docSingle = Nothing
	Set rngPage = Nothing
End Sub
```