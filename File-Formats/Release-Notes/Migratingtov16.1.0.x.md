---
title: Essential Studio File Formats 2018 volume 1 Migration document
description: Essential Studio File Formats 2018 volume 1 Migration document
platform: file-formats
keywords: migration, upgrade-changes, 2018vol1-changes
---
## DocIO
 
Complete field code is now included in Document Object Model(DOM). Whereas in v15.4.0.20 and earlier versions, the first paragraph item after field start is not included in Document Object Model(DOM).
<table>
<tr>
<td>
Field type
</td>
<td>
v15.4.0.20 and earlier versions
</td>
<td>
v16.1.x.x and later versions
</td>
</tr>
<tr>
<td>
Simple field (Field code preserved as single paragraph item)

</td>
<td>
The following items are added in DOM.
WField (Field start)
WFieldMark (Field separator) 
ParagraphItem (Field result)
WFieldMark (Field end)
{{'**Note:**'| markdownify }}Field code is internally maintained by `WField` instance. 
</td>
<td>
The following items are added in DOM.
WField (Field start)
ParagraphItem (field code)
WFieldMark (Field separator) 
ParagraphItem (Field result)
WFieldMark (Field end)
</td>
</tr>
<tr>
<td>
Complex field (Field code preserved as multiple paragraph items)
</td>
<td>
The following items are added in DOM.
WField (Field start)
ParagraphItem 2 (field code)
...
...
ParagraphItem N (field code)
WFieldMark (Field separator) 
ParagraphItem (Field result)
WFieldMark (Field end)
{{'**Note:**'| markdownify }}First paragraph item of field code is internally maintained by `WField` instance. 
</td>
<td>
The following items are added in DOM.
WField (Field start)
ParagraphItem 1 (field code)
ParagraphItem 2 (field code)
...
...
ParagraphItem N (field code)
WFieldMark (Field separator) 
ParagraphItem (Field result)
WFieldMark (Field end)

</td>
</tr>
</table>

* Complete field code is now included in Text property of WParagraph class. Whereas in v15.4.0.20 and earlier versions, the partial field code is included (i.e., the first paragraph item after field start is not included in Text property).

* Complete field code is now considered in Find and replace functionality. Whereas in v15.4.0.20 and earlier versions, the partial field code is considered (i.e., the first paragraph item after field start is not considered in Find and replace functionality).

