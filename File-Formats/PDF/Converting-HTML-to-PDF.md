---
title: Converting HTML to PDF | Syncfusion
description: Learn how to convert HTML to PDF using 3 different rendering engines (Blink, WebKit and IE) with various features like TOC, partial web page to PDF etc.
platform: file-formats
control: PDF
documentation: UG
---
## Converting HTML to PDF

Essential PDF supports converting HTML pages to PDF document. The converter offers full support for HTML tags, HTML5, CSS3, JavaScript, SVG and page breaks. The following are the three rendering engines:

* WebKit rendering
* Blink rendering
* IE rendering


## Supported and Unsupported Features by Rendering Engines

The following table shows the IE, WebKit and Blink rendering engines supported features,


<table>
<th style="font-size:14px">Feature</th>
<th style="font-size:14px">IE Renderer</th>
<th style="font-size:14px">WebKit Renderer</th>
<th style="font-size:14px">Blink Renderer</th>
<tr>
<td>Convert URLs to PDF</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Convert HTML string to PDF</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Images</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Hyperlinks</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>CSS</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>JavaScript</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>ActiveX plugin</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>HTML 5</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Page breaks</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Vector Graphics (Selectable/searchable text)</td>
<td>HTML 5 pages are rendered as bitmap.</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Handling image and text split across pages</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Pdf A1-B</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>Tagged PDF</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>Page settings</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Header and Footer</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Windows Authentication</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Form Authentication</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>HTML to Image</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>HTML to SVG</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>HTML to MHTML</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>SVG to PDF</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>HTML Form to PDF Form</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>HTTP GET and POST</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>Partial HTML to PDF</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>Bookmarks</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>Repeat HTML Table Header and Footer</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes">(Works only with print media)</td>
</tr>

<tr>
<td>Auto Create Table of Contents</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>Windows status</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Print Media Type</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>Offline mode conversion</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
</tr>

<tr>
<td>System proxy</td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

<tr>
<td>Manual proxy</td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
<td><img src="DocumentConversion_images/yes.jpg" alt="Yes"></td>
<td><img src="DocumentConversion_images/no.jpg" alt="No"></td>
</tr>

</table>
