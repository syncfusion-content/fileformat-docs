---
title: Troubleshooting PDF OCR failures | Syncfusion
description: Learn how to overcome OCR Processor failures using Syncfusion .NET OCR library with the help of Google's Tesseract Optical Character Recognition engine.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
--- 

# OCR Processor Troubleshooting 

<table>
<th style="font-size:14px">Exception</th>
<th style="font-size:14px">Tesseract has not been initialized exception.</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>The exception may occur if the tesseract binaries and tessdata files are unavailable on the provided path. 
</td>
</tr>
<tr>
<th style="font-size:14px">Solution1</th>
<td>
Set proper tesseract binaries and tessdata folder with all files and inner folders. The tessdata folder name is case-sensitive and should not change.  
<br/><br/>
{% highlight c# tabtitle="C#" %}

//TesseractBinaries - path of the folder tesseract binaries. 
OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/");

//TessData - path of the folder containing the language pack
processor.PerformOCR(lDoc, @"TessData/");

{% endhighlight %}
</td>
</tr>
<tr>
<th style="font-size:14px">Solution2</th>
<td>
Ensure that your data file version is 3.02 since the OCR processor is built with the Tesseract version 3.02.
</td>
</tr>
</table>

<table>
<th style="font-size:14px">Exception</th>
<th style="font-size:14px">Exception has been thrown by the target of an invocation.</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>If the tesseract binaries are not in the required structure.  
</td>
</tr>
<tr>
<th style="font-size:14px">Solution</th>
<td>
To resolve this exception, ensure the tesseract binaries are in the following structure.
<br/><br/>
The tesseract binaries path is TesseractBinaries/Windows, and the assemblies should be in the following structure. 
<br/><br/>
1.<span style="color:gray;font-size:14px"><i>TesseractBinaries/Windows/x64/libletpt1753.dll,libSyncfusionTesseract.dll</i></span><br/>
2.<span style="color:gray;font-size:14px"><i>TesseractBinaries/Windows/x86/libletpt1753.dll,libSyncfusionTesseract.dll</i></span>
</td>
</tr>
</table>

<table>
<th style="font-size:14px">Exception</th>
<th style="font-size:14px">Can't be opened because the developer's identity cannot be confirmed.</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>This error may occur during the initial loading of the OCR processor in Mac environments.     
</td>
</tr>
<tr>
<th style="font-size:14px">Solution</th>
<td>
To resolve this issue, refer this <a href="https://support.shippingeasy.com/hc/en-us/articles/211543683-What-is-the-error-identity-of-the-developer-cannot-be-confirmed-">link</a> for more details.

</td>
</tr>
</table>

<table>
<th style="font-size:14px">Exception</th>
<th style="font-size:14px">The OCR processor doesn't process languages other than English.</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>This issue may occur if the input image has other languages. The language and tessdata are unavailable for those languages.    
</td>
</tr>
<tr>
<th style="font-size:14px">Solution</th>
<td>
The essential PDF supports all the languages the Tesseract engine supports in the OCR processor.
The dictionary packs for the languages can be downloaded from the following online location:<br/>
<a href="https://code.google.com/p/tesseract-ocr/downloads/list">https://code.google.com/p/tesseract-ocr/downloads/list</a>
<br/><br/>
It is also mandatory to change the corresponding language code in the OCRProcessor.Settings.Language property.  <br/>
For example, to perform the optical character recognition in German, the property should be set as  <br/>
"processor.Settings.Language = "deu";"
</td>
</tr>
</table>

<table>
<th style="font-size:14px">Issue</th>
<th style="font-size:14px">Text does not recognize properly when performing OCR on a PDF document with low-quality images</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>The presence of low quality images in the input PDF document may be the cause of this issue.
</td>
</tr>
<tr>
<th style="font-size:14px">Solution</th>
<td>
By using the best tessdata, we can improve the OCR results. For more information, please refer to the links below.
<br/>
* [https://github.com/tesseract-ocr/tessdata_best](https://github.com/tesseract-ocr/tessdata_best)
N> For better performance, kindly use the fast tessdata which is mentioned in below link, <br/>
[https://github.com/tesseract-ocr/tessdata_fast](https://github.com/tesseract-ocr/tessdata_fast) 
</td>
</tr>
</table>
