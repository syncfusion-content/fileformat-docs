---
title: Converting HTML to PDF with IE | Syncfusion
description: Learn how to convert HTML to PDF using IE rendering engine with various features like HTML string to PDF, PDF A1B etc.
platform: file-formats
control: PDF
documentation: UG
---
# Conversion using IE Rendering

Essential PDF makes use of the Microsoft MSHTML library to convert HTML pages to PDF. The output would like how it is viewed in the Internet Explorer browser.

## Prerequisites

To use the IE rendering engine in the application, the following assemblies or NuGet packages needs to be added as reference to the project.

<b>Assemblies</b>

* Syncfusion.Compression.Base.dll
* Syncfusion.Pdf.Base.dll
* Syncfusion.HtmlConverter.Base.dll
* Microsoft.mshtml.dll

<b>NuGet</b>

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
Windows Forms
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.IE.WinForms.nupkg](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.IE.WinForms/)'| markdownify }}
</td>
</tr>
<tr>
<td>
WPF
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.IE.Wpf.nupkg](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.IE.Wpf/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.IE.AspNet.nupkg](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.IE.AspNet/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET MVC4
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.IE.AspNet.Mvc4.nupkg](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.IE.AspNet.Mvc4/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET MVC5
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.IE.AspNet.Mvc5.nupkg](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.IE.AspNet.Mvc5/)'| markdownify }}
</td>
</tr>
</table>

N> The above mentioned NuGet packages are available in [nuget.org](https://www.nuget.org/)


## Converting the URL to a PDF document

To convert the HTTP or HTTPS website to PDF, use the following the code snippet.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Initialize HTML to PDF converter 

HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(); 

//Convert HTML to PDF document 

PdfDocument document = htmlConverter.Convert("https://www.google.com");
 
//Save and close the PDF document 

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize HTML to PDF converter 

Dim htmlConverter As New HtmlToPdfConverter() 

'Convert HTML to PDF document 

Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com") 

'Save and close the PDF document 

document.Save("Output.pdf") 

document.Close(True)

{% endhighlight %}


{% endtabs %}


## Converting the HTML string to PDF document

To convert the HTML string to PDF, use the following the code snippet.

<b>baseURL:</b> path of the resources (images, style sheets, scripts.,) used in the input HTML string.

For the below HTML string, the baseURL will be the path of the <font color="blue"><i>syncfusion_logo.gif</i></font> image.

For example, if the above image is in <i>“C:\Temp\HTMLFiles\syncfusion_logo.gif”</i> location then the baseURL will be as below,

<b>baseURL:</b> C:\Temp\HTMLFiles\

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Initialize HTML to PDF converter 

HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();

//HTML string and base URL 

string htmlText = "<html><body><img src=\"syncfusion_logo.gif\" alt=\"Syncfusion_logo\" width=\"200\" height=\"70\"><p> Hello World</p></body></html>";

string baseUrl = @"C:/Temp/HTMLFiles/";

//Convert HTML to PDF document 

PdfDocument document = htmlConverter.Convert(htmlText, baseUrl);

//Save and close the PDF document 

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize HTML to PDF converter 

Dim htmlConverter As New HtmlToPdfConverter()

'HTML string and base URL 

Dim htmlText As String = "<html><body><img src=""syncfusion_logo.gif"" alt=""Syncfusion_logo"" width=""200"" height=""70""><p> Hello World</p></body></html>"

Dim baseUrl As String = "C:/Temp/HTMLFiles/"

'Convert HTML to PDF document 

Dim document As PdfDocument = htmlConverter.Convert(htmlText, baseUrl)

'Save and close the PDF document 

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight html %}

<html>
<body>
<img src="syncfusion_logo.gif" alt="Syncfusion_logo" width="200" height="70">
<p> Hello World</p>
</body>
</html>

{% endhighlight %}

{% endtabs %}

## Converting Windows Authenticated web page to PDF document

The webpage you want to convert may protected with windows authentication. IE rendering engine provides support for converting the Windows Authenticated webpage to PDF document by providing the username and password. Refer to the following code snippet,

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Initialize HTML to PDF converter 

HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
 
//IE Converter settings 

IEConverterSettings converterSettings = new IEConverterSettings(); 

converterSettings.Username = "username";

converterSettings.Password = "password";

htmlConverter.ConverterSettings = converterSettings; 

//Convert HTML to PDF document 

PdfDocument document = htmlConverter.Convert("https://www.google.com"); 

//Save and close the PDF document 

document.Save("Output.pdf"); 

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize HTML to PDF converter 

Dim htmlConverter As New HtmlToPdfConverter() 

'IE Converter settings 

Dim converterSettings As New IEConverterSettings() 

converterSettings.Username = "username" 

converterSettings.Password = "password" 

htmlConverter.ConverterSettings = converterSettings 

'Convert HTML to PDF document 

Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com")
 
'Save and close the PDF document 

document.Save("Output.pdf") 

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Converting with PDFA conformance

IE HTML to PDF converter provides support for converting the web pages to PDF with PDFA1B conformance, which embeds all the fonts into the PDF document. The following code snippet illustrates how to convert HTML pages to PDF document with PDFA1B conformance.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Initialize HTML to PDF converter

HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(); 

//IE Converter settings 

IEConverterSettings converterSettings = new IEConverterSettings();
 
//PDFA1B conformance 

converterSettings.IsPDFA1B = true; 

htmlConverter.ConverterSettings = converterSettings; 

//Convert HTML to PDF document 

PdfDocument document = htmlConverter.Convert("https://www.google.com"); 

//Save and close the PDF document 

document.Save("Output.pdf"); 

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter() 

'IE Converter settings 
Dim converterSettings As New IEConverterSettings()
 
'PDFA1B conformance 
converterSettings.IsPDFA1B = True 

htmlConverter.ConverterSettings = converterSettings 

'Convert HTML to PDF document 
Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com") 

'Save and close the PDF document 
document.Save("Output.pdf") 

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Limitations in the IE Rendering Engine

Syncfusion’s IE HTML to PDF converter relied on Microsoft’s MSHTML library to do the conversion from HTML to PDF. The actual conversion happens in two steps.

* Convert HTML into a Metafile. 
* Rendering the Metafile to PDF. 

The main advantage of this kind of conversion is that the text rendered remains searchable in PDF. 
With version 9 of Internet Explorer, Microsoft started using hardware acceleration to produce bitmap images instead of metafiles, completely removing the ability to render selectable or searchable text within PDF. Users can work around the problem by making some registry changes, but may not be satisfied with the result, so a better alternative was needed. Hence a new converter based on the <b>WebKit renderer</b> was created. 
The WebKit rendered document contains vector graphics instead of scalar images. This reduces file size and allows users to perform various operations such as text search, selection, and clipboard copy. Apart from overcoming the limitations in the Internet Explorer rendering engine, the new WebKit render also provides better support to render HTML5, CSS3, and SVG content.


## Troubleshooting

<table>
<tr>
<th>
Issue
</th>
<td>
The following conditions may occur while converting HTML to PDF by using the IE rendering engine.
<ol>

<li>Converted PDF document contains content as a Bitmap.</li>
<li>Page break may not be applied in the resultant PDF document.</li>
<li>Text could not be selected in the PDF document.</li>
<li>Converted PDF looks blurry.</li>
</ol>
</td>
</tr>
<tr>
<th>
Solution
</th>

<td>

The above issues may occur in the machines with IE9 or later versions installed. As the Internet Explorer version 9 and above supports hardware acceleration, the rendered content would be in the form of Bitmap, where many features are not supported. <br/>&nbsp;<br/>

To overcome this issue, the key FEATURE_IVIEWOBJECTDRAW_DMLT9_WITH_GDI should be updated in the registry as explained in the link below.
<br/><br/>
<a href="http://msdn.microsoft.com/en-us/library/ee330732(v=vs.85).aspx#iviewobject_draw">http://msdn.microsoft.com/en-us/library/ee330732(v=vs.85).aspx#iviewobject_draw</a>
<br/><br/>
<ul>
<li>Run the legacy drawing utility placed in <span style="color:gray;font-size:14px">($SystemDrive: \Program Files\Syncfusion\Essential Studio\$Version # \Utilities\PDF\Legacy Drawing)</span> to perform the above changes automatically.</li>
<li>While manually changing the registry key, the changes should be done on both HKEY_LOCAL_MACHINE and HKEY_CURRENT_USER as below.</li>
</ul>
<table>
<thead>
<tr>
<th>Name</th>
<th>Type</th>
<th>Data</th>
</tr>
</thead>
<tbody>
<tr>
<td>
*<br/><br/></td><td>
REG_DWORD<br/><br/></td><td>
0x00000001<br/><br/></td></tr>
</tbody>
</table>

</td>
</tr>
</table>


<table>
<tr>
<th>Issue
</th>
<td>
<b>Images or other contents in the HTML are missing in the resultant PDF document</b>
</td>
</tr>
<tr>
<th>
Solution
</th>
<td>
The issue may be due to the slow Internet connection or due to the behavior that the conversion completed before the URL is loaded completely. To overcome this issue, add suitable delay to the conversion using AdditionalDelay property of the HTMLConverter.
</td>
</tr>
</table>

<table>
	<tr>
		<th style="font-size:14px" colspan="2">HTML conversion support in Azure</th>
	</tr>
	<tr>
		<th style="font-size:14px">Azure App Service</th>
		<td>No</td>
	</tr>
	<tr>
		<th style="font-size:14px">Azure Functions</th>
		<td>No</td>
	</tr>
	<tr>
		<th style="font-size:14px">Azure Cloud Service</th>
		<td>Yes</td>
	</tr>
</table>
