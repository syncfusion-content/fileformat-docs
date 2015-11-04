---
title: Working with Document Conversion
description: This section explains converting other document Types into PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Document Conversions

## Converting HTML documents To PDF

Essential PDF allows you to convert HTML pages to PDF document. The converter offers full support for HTML tags, HTML5, CSS3, JavaScript, SVG and page breaks control. There are two rendering engines available. They are

* IE Rendering 
* WebKit Rendering 

### Conversion using IE Rendering


Essential PDF makes use of the Microsoft MSHTML library to convert HTML pages to PDF. The output would similar to how it is viewed in the Internet Explorer browser.

#### Prerequisites

To use the IE rendering engine in your application, the following assemblies needs to be added as reference to the project.

1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.HtmlConverter.Base.dll

#### Converting the URL to a PDF document


To convert the http or https website to PDF, use the following the code snippet. 

{% tabs %}  

{% highlight c# %}


//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

pdfDocument.PageSettings.Margins.All = 0;

//Adds a page to the PDF document.

PdfPage page = pdfDocument.Pages.Add();

SizeF pageSize = page.GetClientSize().ToSize();

AspectRatio dimension = AspectRatio.KeepWidth;

HtmlConverter html = new HtmlConverter();

//Unit converter to convert the PDF page size to pixels.

PdfUnitConvertor convertor = new PdfUnitConvertor();

float width = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point);

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;



// Converts the URL to metafile, to render a searchable PDF.

HtmlToPdfResult result = html.Convert("http://www.google.com", ImageType.Metafile, (int)width, (int)height, dimension);

result.Render(page, metafileFormat);

pdfDocument.Save("Output.pdf");

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Creates a new PDF document.

Dim pdfDocument As New PdfDocument()

pdfDocument.PageSettings.Margins.All = 0

'Adds a page to the PDF document.

Dim page As PdfPage = pdfDocument.Pages.Add()

Dim pageSize As SizeF = page.GetClientSize().ToSize()

Dim dimension As AspectRatio = AspectRatio.KeepWidth

Dim html As New HtmlConverter()

'Unit converter to convert the PDF page size to pixels.

Dim convertor As New PdfUnitConvertor()

Dim width As Single = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point)

Dim height As Single = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point)

'Layout format for Metafile.

Dim metafileFormat As New PdfMetafileLayoutFormat()

metafileFormat.Break = PdfLayoutBreakType.FitPage

metafileFormat.Layout = PdfLayoutType.Paginate

metafileFormat.SplitTextLines = False

metafileFormat.SplitImages = False



'Converts the URL to metafile, to render a searchable PDF.

Dim result As HtmlToPdfResult = html.Convert("http://www.google.com", ImageType.Metafile, CInt(width), CInt(height), dimension)

result.Render(page, metafileFormat)

pdfDocument.Save("Output.pdf")

pdfDocument.Close(True)



{% endhighlight %}

{% endtabs %}  

1. The EnableJavascript property needs to be set to true for websites that contains JavaScript. 
2. ImageType argument of the Convert method needs to be set as Metafile for vector graphics and a searchable PDF document. Selecting the Bitmap type would result in a non-searchable PDF.
3. The Layout property of the PdfMetafileLayoutFormat need to be set as Paginate, to span the conversion across multiple pages.
4. SplitTextLines and SplitImages property of the PdfMetafileLayoutFormat class needs to be set as false, to avoid image and text split across pages.


#### Converting the HTML string to PDF document

To convert the HTML string to PDF document, use the following code snippet.

{% tabs %}  

{% highlight c# %}


//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

pdfDocument.PageSettings.Margins.All = 0;

//Adds a page to the PDF document.

PdfPage page = pdfDocument.Pages.Add();

SizeF pageSize = page.GetClientSize().ToSize();

AspectRatio dimension = AspectRatio.KeepWidth;

HtmlConverter html = new HtmlConverter();

// Unit converter to convert the PDF page size to pixels.

PdfUnitConvertor convertor = new PdfUnitConvertor();

float width = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point);

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;



string htmlText = @"<html><head><title></title></head><body><div>Hello World!!!</div></body></html>";

// Converts the URL to metafile, to render a searchable PDF.

HtmlToPdfResult result = html.Convert(htmlText,"", ImageType.Metafile, (int)width, (int)height, dimension);

result.Render(page, metafileFormat);

pdfDocument.Save("Output.pdf");

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Creates a new PDF document.

Dim pdfDocument As New PdfDocument()

pdfDocument.PageSettings.Margins.All = 0

'Adds a page to the PDF document.

Dim page As PdfPage = pdfDocument.Pages.Add()

Dim pageSize As SizeF = page.GetClientSize().ToSize()

Dim dimension As AspectRatio = AspectRatio.KeepWidth

Dim html As New HtmlConverter()

' Unit converter to convert the PDF page size to pixels.

Dim convertor As New PdfUnitConvertor()

Dim width As Single = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point)

Dim height As Single = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point)

'Layout format for Metafile.

Dim metafileFormat As New PdfMetafileLayoutFormat()

metafileFormat.Break = PdfLayoutBreakType.FitPage

metafileFormat.Layout = PdfLayoutType.Paginate

metafileFormat.SplitTextLines = False

metafileFormat.SplitImages = False

Dim htmlText As String = "<html><head><title></title></head><body><div>Hello World!!!</div></body></html>"

'Converts the URL to metafile, to render a searchable PDF.

Dim result As HtmlToPdfResult = html.Convert(htmlText, "", ImageType.Metafile, CInt(width), CInt(height), dimension)

result.Render(page, metafileFormat)

pdfDocument.Save("Output.pdf")

pdfDocument.Close(True)



{% endhighlight %}

{% endtabs %}  

#### Converting Windows Authenticated webpage to PDF document

To convert the Windows Authenticated webpage to PDF document by providing the username and password, use the following code snippet below.

{% tabs %}  

{% highlight c# %}


//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

pdfDocument.PageSettings.Margins.All = 0;

//Adds a page to the PDF document.

PdfPage page = pdfDocument.Pages.Add();

SizeF pageSize = page.GetClientSize().ToSize();

AspectRatio dimension = AspectRatio.KeepWidth;

HtmlConverter html = new HtmlConverter();

// Unit converter to convert the PDF page size to pixels.

PdfUnitConvertor convertor = new PdfUnitConvertor();

float width = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point);

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;





//Windows authentication by providing username and password

HtmlToPdfResult result = html.Convert("http://www.syncfusion.com", ImageType.Metafile, (int)width, (int)height, dimension, "username", "password");

result.Render(page, metafileFormat);

pdfDocument.Save("Output.pdf");

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim pdfDocument As New PdfDocument()

pdfDocument.PageSettings.Margins.All = 0

'Adds a page to the PDF document.

Dim page As PdfPage = pdfDocument.Pages.Add()

Dim pageSize As SizeF = page.GetClientSize().ToSize()

Dim dimension As AspectRatio = AspectRatio.KeepWidth

Dim html As New HtmlConverter()

' Unit converter to convert the PDF page size to pixels.

Dim convertor As New PdfUnitConvertor()

Dim width As Single = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point)

Dim height As Single = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point)

' Layout format for Metafile.

Dim metafileFormat As New PdfMetafileLayoutFormat()

metafileFormat.Break = PdfLayoutBreakType.FitPage

metafileFormat.Layout = PdfLayoutType.Paginate

metafileFormat.SplitTextLines = False

metafileFormat.SplitImages = False



'Windows authentication by providing username and password

Dim result As HtmlToPdfResult = html.Convert("http://www.example.com", ImageType.Metafile, CInt(width), CInt(height), dimension, "xxx", _

"yyy")

result.Render(page, metafileFormat)

pdfDocument.Save("Output.pdf")

pdfDocument.Close(True)



{% endhighlight %}

{% endtabs %}  


#### Converting with PDFA conformance

You can also convert the webpages to PDF with PDFA1B conformance, which embeds all the fonts into the PDF document.

The following code snippet illustrates how to convert HTML pages to PDF document with PDFA1B conformance.

{% tabs %}   

{% highlight c# %}


//Creates a new PDFA1B document.

PdfDocument pdfDocument = new PdfDocument(PdfConformanceLevel.Pdf_A1B);

pdfDocument.PageSettings.Margins.All = 0;

//Adds a page to the PDF document.

PdfPage page = pdfDocument.Pages.Add();

SizeF pageSize = page.GetClientSize().ToSize();

AspectRatio dimension = AspectRatio.KeepWidth;

HtmlConverter html = new HtmlConverter();

// Unit converter to convert the PDF page size to pixels.

PdfUnitConvertor convertor = new PdfUnitConvertor();

float width = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point);

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;



//Convert the URL to PDF

HtmlToPdfResult result = html.Convert("http://www.google.com", ImageType.Metafile, (int)width, (int)height, dimension);

result.Render(page, metafileFormat);

pdfDocument.Save("Output.pdf");

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Creates a new PDFA1B document.

Dim pdfDocument As New PdfDocument(PdfConformanceLevel.Pdf_A1B)

pdfDocument.PageSettings.Margins.All = 0

'Adds a page to the PDF document.

Dim page As PdfPage = pdfDocument.Pages.Add()

Dim pageSize As SizeF = page.GetClientSize().ToSize()

Dim dimension As AspectRatio = AspectRatio.KeepWidth

Dim html As New HtmlConverter()

'Unit converter to convert the PDF page size to pixels.

Dim convertor As New PdfUnitConvertor()

Dim width As Single = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point)

Dim height As Single = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point)

'Layout format for Metafile.

Dim metafileFormat As New PdfMetafileLayoutFormat()

metafileFormat.Break = PdfLayoutBreakType.FitPage

metafileFormat.Layout = PdfLayoutType.Paginate

metafileFormat.SplitTextLines = False

metafileFormat.SplitImages = False

'Converts the URL to PDF

Dim result As HtmlToPdfResult = html.Convert("http://www.google.com", ImageType.Metafile, CInt(width), CInt(height), dimension)

result.Render(page, metafileFormat)

pdfDocument.Save("Output.pdf")

pdfDocument.Close(True)



{% endhighlight %}

 {% endtabs %}


#### Troubleshooting

**Issue:**

The following conditions may occur while converting HTML to PDF by using the IE rendering engine.

1. Converted PDF document contains content as a Bitmap.

2. Page break may not be applied in the resultant PDF document.

3. Text could not be selectable in the PDF document

4. Converted PDF is blurry.

**Solution:**

The above issues may occur in the machines with IE9 or later versions installed. As the Internet Explorer version 9 and above supports hardware acceleration, the rendered content would be in the form of Bitmap, where many features are not supported. 

To overcome this issue, the key FEATURE_IVIEWOBJECTDRAW_DMLT9_WITH_GDI should be updated in the registry as explained in the link below. 

[http://msdn.microsoft.com/en-us/library/ee330732(v=vs.85).aspx#iviewobject_draw](http://msdn.microsoft.com/en-us/library/ee330732(v=vs.85).aspx#iviewobject_draw)

* You can run the utility placed in ($system drive: \Program Files\Syncfusion\Essential Studio\$Version # \Utilities\PDF\Legacy Drawing) to perform the above changes automatically.
* While manually changing the registry key, the changes should be done on both HKEY_LOCAL_MACHINE and HKEY_CURRENT_USER as below.

<table>
<thead>  
<tr>
<th><br/>Name<br/><br/></th>
<th>Type<br/><br/></th>
<th>Data<br/><br/></th>
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

**Issue:**

Images or other contents in the HTML are missing in the resultant PDF document

**Solution:**

The issue may be due to the slow internet connection or due to the behavior that the conversion completed before the URL is loaded completely. To overcome this issue, add suitable delay to the conversion using AdditionalDelay property of the HTMLConverter.

### Conversion using WebKit Rendering

Essential PDF also supports HTML to PDF conversion by using the WebKit rendering engine. It is more reliable when compared with IE rendering engine and also the converter provides full support for HTML5, CSS3, Canvas, SVG, Web Fonts and JavaScript.

#### Prerequisites and setting up the WebKit engine for conversion

* To use the HTML to PDF conversion in your application using WebKit rendering engine, the following assemblies needs to be added as reference to the project.
      a. Syncfusion.Compression.Base.dll
      b. Syncfusion.Pdf.Base.dll
      c. Syncfusion.HtmlConverter.Base.dll
      d. Syncfusion.WebKitHtmlConverter.Base.dll
* The QtBinaries available in the WebKitHTMLConverter installed location ($Systemdrive\Program Files (x86)\Syncfusion\WebKitHTMLConverter\xx.x.x.xx\QtBinaries) should be placed in the local machine where the conversion takes place. The physical path of this folder has be set to the WebKitBinaryPath property of the WebkitHtmlConverter class as shown below.



{% highlight c# %}


// Create a new instance of WebKitHtmlConverter class.

WebKitHtmlConverter html = new WebKitHtmlConverter();

string WebKitBinaryPath = "/QtBinaries/";

//WebKit assembly path

html.WebKitPath = WebKitBinaryPath;





{% endhighlight %}

* WebKit conversion also requires VC++ 2010 redistributable to be installed in the machine. You can use the below mentioned download link,

X86 - [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555#)

X64 - [https://www.microsoft.com/en-in/download/details.aspx?id=14632](https://www.microsoft.com/en-in/download/details.aspx?id=14632#)

Instead, the required assemblies below can be added in the Windows system folder (for 64 bit machine, it should be place in $Systemdrive\Windows\SysWOW64 and for 32 bit machine, it should be place in $Systemdrive\Windows\System32),

1. MSVCP100.dll
2. MSVCR100.dll

* For converting https sites, conversion requires OPENSSL libraries to be installed in the machine. You can install the OPENSSL library by downloading its setup from the below link,

X86 - [https://slproweb.com/download/Win32OpenSSL-1_0_2d.exe](https://slproweb.com/download/Win32OpenSSL-1_0_2d.exe# )

X64 - [https://slproweb.com/download/Win64OpenSSL-1_0_2d.exe](https://slproweb.com/download/Win64OpenSSL-1_0_2d.exe# )

Instead, the required assemblies below can added in the Windows system folder (for 64 bit machine, it should be place in $Systemdrive\Windows\SysWOW64 and for 32 bit machine, it should be place in $Systemdrive\Windows\System32),

1. libeay32.dll
2. libssl32.dll
3. ssleay32.dll


#### Converting the URL to a PDF document


To convert website URL or local html file to PDF using WebKit rendering engine, please refer the below code snippet.

{% tabs %}  

{% highlight c# %}


//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Set page margins.

document.PageSettings.Margins.All = 0;

PdfPage page = document.Pages.Add();

PdfUnitConvertor convertor = new PdfUnitConvertor();

float width = convertor.ConvertToPixels(document.PageSettings.Width, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(document.PageSettings.Height, PdfGraphicsUnit.Point);



// Create a new instance of WebKitHtmlConverter class.

WebKitHtmlConverter html = new WebKitHtmlConverter();

string WebKitBinaryPath = "/QtBinaries/";

//WebKit assembly path

html.WebKitPath = WebKitBinaryPath;

// Convert to PDF document.

HtmlToPdfResult result = html.Convert("http://www.google.com" , (int)width, (int)height);

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

//Avoid splitting the text/images across the pages

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;

// Draw metafile in PdfPage.

result.Render(page, metafileFormat);

// Save and close the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Creates a new PDF document.

Dim document As New PdfDocument()

'Set page margins.

document.PageSettings.Margins.All = 0

Dim page As PdfPage = document.Pages.Add()

Dim convertor As New PdfUnitConvertor()

Dim width As Single = convertor.ConvertToPixels(document.PageSettings.Width, PdfGraphicsUnit.Point)

Dim height As Single = convertor.ConvertToPixels(document.PageSettings.Height, PdfGraphicsUnit.Point)

' Create a new instance of WebKitHtmlConverter class.

Dim html As New WebKitHtmlConverter()

Dim WebKitBinaryPath As String = "/QtBinaries/"

'WebKit assembly path

html.WebKitPath = WebKitBinaryPath

' Convert to PDF document.

Dim result As HtmlToPdfResult = html.Convert("http://www.google.com", CInt(width), CInt(height))

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

//Avoid splitting the text/images across the pages

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;

// Draw metafile in PdfPage.

result.Render(page, metafileFormat);

' Save and close the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

 {% endtabs %}  
 

#### Converting the HTML string to PDF document

To convert the HTML string to pdf, use below code snippet.

{% tabs %} 

{% highlight c# %}


//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Set page margins.

document.PageSettings.Margins.All = 0;

PdfPage page = document.Pages.Add();

PdfUnitConvertor convertor = new PdfUnitConvertor();

float width = convertor.ConvertToPixels(document.PageSettings.Width, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(document.PageSettings.Height, PdfGraphicsUnit.Point);



// Create a new instance of WebKitHtmlConverter class.

WebKitHtmlConverter html = new WebKitHtmlConverter();

string WebKitBinaryPath = "/QtBinaries";

//WebKit assembly path

html.WebKitPath = WebKitBinaryPath;

string htmlText = @"<html><head><title></title></head><body><div>Hello World!!!</div></body></html>";

// Convert to PDF document.

HtmlToPdfResult result = html.Convert(htmlText,"", (int)width, (int)height);

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

//Avoid splitting the text/images across the pages

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;

// Draw metafile in PdfPage.

result.Render(page, metafileFormat);

// Save and close the document.

document.Save("Sample.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Creates a new PDF document.

Dim document As New PdfDocument()

'Set page margins.

document.PageSettings.Margins.All = 0

Dim page As PdfPage = document.Pages.Add()

Dim convertor As New PdfUnitConvertor()

Dim width As Single = convertor.ConvertToPixels(document.PageSettings.Width, PdfGraphicsUnit.Point)

Dim height As Single = convertor.ConvertToPixels(document.PageSettings.Height, PdfGraphicsUnit.Point)

'Create a new instance of WebKitHtmlConverter class.

Dim html As New WebKitHtmlConverter()

Dim WebKitBinaryPath As String = "/QtBinaries"

'WebKit assembly path

html.WebKitPath = WebKitBinaryPath

Dim htmlText As String = "<html><head><title></title></head><body><div>Hello World!!!</div></body></html>"

'Convert to PDF document.

Dim result As HtmlToPdfResult = html.Convert(htmlText, "", CInt(width), CInt(height))

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

//Avoid splitting the text/images across the pages

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;

// Draw metafile in PdfPage.

result.Render(page, metafileFormat);

'Save and close the document.

document.Save("Sample.pdf")

document.Close(True)



{% endhighlight %}

 {% endtabs %}  
 

#### Converting an SVG to PDF

You can also convert local SVG files or online SVG URL to PDF using below code snippet.

{% tabs %} 

{% highlight c# %}


//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Set page margins.

document.PageSettings.Margins.All = 0;

PdfPage page = document.Pages.Add();

PdfUnitConvertor convertor = new PdfUnitConvertor();

float width = convertor.ConvertToPixels(document.PageSettings.Width, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(document.PageSettings.Height, PdfGraphicsUnit.Point);



// Create a new instance of WebKitHtmlConverter class.

WebKitHtmlConverter html = new WebKitHtmlConverter();

string WebKitBinaryPath = "/QtBinaries";

//WebKit assembly path

html.WebKitPath = WebKitBinaryPath;

// Convert to PDF document.

HtmlToPdfResult result = html.Convert(@"example.svg", (int)width, (int)height);

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

//Avoid splitting the text/images across the pages

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;

// Draw metafile in PdfPage.

result.Render(page, metafileFormat);

// Save and close the document.

document.Save("Sample.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Creates a new PDF document.

Dim document As New PdfDocument()

'Set page margins.

document.PageSettings.Margins.All = 0

Dim page As PdfPage = document.Pages.Add()

Dim convertor As New PdfUnitConvertor()

Dim width As Single = convertor.ConvertToPixels(document.PageSettings.Width, PdfGraphicsUnit.Point)

Dim height As Single = convertor.ConvertToPixels(document.PageSettings.Height, PdfGraphicsUnit.Point)

' Create a new instance of WebKitHtmlConverter class.

Dim html As New WebKitHtmlConverter()

Dim WebKitBinaryPath As String = "/QtBinaries"

'WebKit assembly path

html.WebKitPath = WebKitBinaryPath

' Convert to PDF document.

Dim result As HtmlToPdfResult = html.Convert("example.svg", CInt(width), CInt(height))

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

//Avoid splitting the text/images across the pages

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;

// Draw metafile in PdfPage.

result.Render(page, metafileFormat);

' Save and close the document.

document.Save("Sample.pdf")

document.Close(True)



{% endhighlight %}

 {% endtabs %}  

 
#### Troubleshooting

**WebKit Converter may create PDF with blank pages under the following cases**

1. When the webpage (html) is not available/accessible.
2. When VC++ 2010 redistributable and OpenSSL package is not installed in the machine.
3. When any Qt binaries are not available in the WebKitPath mentioned location.

**Solution 1:**

Please check your internet connection and if the html page is available in the mentioned location.

**Solution 2:**

2. You can install the VC++ and OpenSSL packages from the below mentioned download links,

X86 - [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555# )

X64 - [https://www.microsoft.com/en-in/download/details.aspx?id=14632](https://www.microsoft.com/en-in/download/details.aspx?id=14632# )

Instead, the required assemblies below can be added in the Windows system folder (for 64 bit machine, it should be place in $Systemdrive\Windows\SysWOW64 and for 32 bit machine, it should be place in $Systemdrive\Windows\System32),

* MSVCP100.dll
* MSVCR100.dll

For converting https sites, it requires OPENSSL libraries to be installed in the machine. You can install the OPENSSL library by downloading its setup from the below link,

X86 - [https://slproweb.com/download/Win32OpenSSL-1_0_2d.exe](https://slproweb.com/download/Win32OpenSSL-1_0_2d.exe# )

X64 - [https://slproweb.com/download/Win64OpenSSL-1_0_2d.exe](https://slproweb.com/download/Win64OpenSSL-1_0_2d.exe# )

Instead, the required assemblies below can added in the Windows system folder (for 64 bit machine, it should be place in $Systemdrive\Windows\SysWOW64 and for 32 bit machine, it should be place in $Systemdrive\Windows\System32),

* libeay32.dll
* libssl32.dll
* ssleay32.dll

**Solution 3:**

You need to place the Qt binaries in the location where the conversion takes place and assign that location to the WebKitPath. The Qt binaries will be available in the WebKitHTMLConverter installed location ($Systemdrive\Program Files (x86)\Syncfusion\WebKitHTMLConverter\xx.x.x.xx\QtBinaries)

**Images or other contents in the HTML are missing in the resultant PDF document.**

The issue may be due to the slow internet connection or due to the behavior that the conversion completed before the page is loaded completely.

**Solution**

To overcome this issue, add suitable delay for the conversion using AdditionalDelay property of the HTMLConverter.

**Converter fails in Azure website, but it works in development machine**
The converter can be used in Windows Azure Cloud Service but it cannot be used in Azure website due to the lack of administrator privilege and few other  restrictions which fails the conversion process. 

**Solution**

You can move the conversion part into the cloud service with web role and add service reference to your Azure website.

## Converting Word documents to PDF

Essential PDF allows you to convert a Word document into PDF. For converting a Word document to PDF, the following assemblies need to be referenced in your application

<table>
<thead>  
<tr>
<th>
Assembly Name<br/><br/></th><th>
Description<br/><br/></th></tr>
</thead>
<tbody>  
<tr>
<td>
Syncfusion.DocIO.Base<br/><br/></td><td>
This assembly has the core features for creating and manipulating Word documents.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to package the Word documents<br/><br/></td></tr>
<tr>
<td>
Syncfusion.DocToPdfConverter.Base<br/><br/></td><td>
This assembly is needed for converting the Word document to PDF.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Pdf.Base<br/><br/></td><td>
This assembly has the core features for creating PDF file.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChart.Base<br/><br/></td><td>
This assembly has features to work with chart in Word document.<br/><br/></td></tr>
</tbody>
</table>

The following assemblies are need to be referred in addition to the above mentioned assemblies for converting the chart present in the Word document into PDF.

<table>
<thead> 
<tr>
<th>
Assembly Name<br/><br/></th><th>
Description<br/><br/></th></tr>
 </thead>
 <tbody>  
<tr>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td><td>
This assembly is used to convert the chart to image.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.SfChart.WPF<br/><br/></td><td>
This is supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Shared.WPF<br/><br/></td><td>
This is supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
</tbody>
</table>


The following namespaces are required to compile the code in this topic.

* using Syncfusion.OfficeChart
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocToPDFConverter
* using Syncfusion.Pdf
* using Syncfusion.OfficeChartToImageConverter

DocToPDFConverter class is responsible for converting a Word document into PDF. The following code snippet illustrates how to convert a Word document into PDF document.

{% tabs %} 

{% highlight c# %}


//Load an existing Word document

WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);

//Initialize chart to image converter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Create an instance of DocToPDFConverter

DocToPDFConverter converter = new DocToPDFConverter();

//Convert Word document into PDF document

PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);

//Save the PDF file 

pdfDocument.Save("WordtoPDF.pdf");

//Close the instance of document objects

pdfDocument.Close(true);

wordDocument.Close();



{% endhighlight %}

{% highlight vb.net %}


'Load an existing Word document

Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)

'Initialize chart to image converter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = New ChartToImageConverter()

'Create an instance of DocToPDFConverter

Dim converter As New DocToPDFConverter()

'Convert Word document into PDF document

Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)

'Save the PDF file 

pdfDocument.Save("WordtoPDF.pdf")

'Close the instance of document objects

pdfDocument.Close(True)

wordDocument.Close()



{% endhighlight %}

 {% endtabs %}  

Note:

* Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications
* Initializing the ChartToImageConverter is mandatory to convert the charts present in the Word document to PDF. Otherwise the charts will not be exported to the converted PDF
* ChartToImageConverter is supported from .NET Framework 4.0 onwards
* Total number of pages may vary  based on unsupported elements in the converted PDF document when compare to Word document


### Customizing the Word document to PDF conversion

Essential DocIO allows you to customize the Word to PDF conversion with the below options:

* Allows to determine the quality of the charts in the converted PDF 
* Allows to determine the quality of the jpeg images in the converted PDF
* Allows to reduce the Main Memory usage in Word to PDF conversion by reusing the identical images.

{% tabs %}  

{% highlight c# %}



//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Sample_Image.docx", FormatType.Docx);

//Initialize chart to image converter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Set the scaling mode for charts

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;

//create an instance of DocToPDFConverter - responsible for Word to PDF conversion

DocToPDFConverter converter = new DocToPDFConverter();

//Set the image quality

converter.Settings.ImageQuality = 100;

//Set the image resolution

converter.Settings.ImageResolution = 640;

//Set true to optimize the memory usage for identical images

converter.Settings.OptimizeIdenticalImages = true;

//Convert Word document into PDF document

PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);

//Save the PDF file to file system

pdfDocument.Save("WordtoPDF.pdf");

//close the instance of document objects

pdfDocument.Close(true);

wordDocument.Close();



{% endhighlight %}

{% highlight vb.net %}


'Loads an existing Word document

Dim wordDocument As New WordDocument("Sample_Image.docx", FormatType.Docx)

'Initialize chart to image converter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = New ChartToImageConverter()

'Set the scaling mode for charts

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal

'create an instance of DocToPDFConverter - responsible for Word to PDF conversion

Dim converter As New DocToPDFConverter()

'Set the image quality

converter.Settings.ImageQuality = 100

'Set the image resolution

converter.Settings.ImageResolution = 640

'Set true to optimize the memory usage for identical images

converter.Settings.OptimizeIdenticalImages = True

'Convert Word document into PDF document

Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)

'Save the PDF file to file system

pdfDocument.Save("WordtoPDF.pdf")

'close the instance of document objects

pdfDocument.Close(True)

wordDocument.Close()



{% endhighlight %}

{% endtabs %}  



## Converting Excel documents to PDF

Essential PDF allows you to convert an entire workbook or a single worksheet into PDF document. For converting an Excel document to PDF, the following assemblies need to be referenced in your application

* Syncfusion.XlsIO.Base.dll
* Syncfusion.Compression.Base.dll
* Syncfusion.ExcelToPDFConverter.Base.dll
* Syncfusion.ExcelChartToImageConverter.Wpf.dll
* Syncfusion.SfChart.Wpf.dll
* Syncfusion.Shared.Wpf.dll
* Syncfusion.Pdf.Base.dll

### Converting  a Workbook to PDF

The following code illustrates how to convert a workbook to PDF Document.

{% tabs %} 

{% highlight c# %}



ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;


IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

//Open the Excel Document to Convert

ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

//Intialize PDF Document

PdfDocument pdfDocument = new PdfDocument();

//Convert Excel Document into PDF document

pdfDocument = converter.Convert();

//Save the pdf file

pdfDocument.Save("ExceltoPDF.pdf");

//Dispose the objects

pdfDocument.Close();

converter.Dispose();

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb.net %}


Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

'Open the Excel Document to Convert

Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

'Intialize the PDF Document

Dim pdfDocument As PdfDocument = New PdfDocument()

'Convert Excel Document into PDF document

pdfDocument = converter.Convert()

'Save the pdf file

pdfDocument.Save("ExceltoPDF.pdf")

'Dispose the objects

pdfDocument.Close()

converter.Dispose()

workbook.Close()

excelEngine.Dispose()       

{% endhighlight %}

 {% endtabs %}  



To know more about ExcelToPdf conversion settings, please refer ExcelToPdfConverterSettings – LINK API reference


### Converting a Worksheet to PDF

The following code shows how to convert a particular sheet to PDF Document.

{% tabs %} 

{% highlight c# %}


ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//convert the sheet to pdf

ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);

PdfDocument pdfDocument= new PdfDocument();

pdfDocument = converter.Convert();

pdfDocument.Save("ExceltoPDF.pdf");

pdfDocument.Close();

converter.Dispose();

workbook.Close();
excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb.net %}


Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Converts the particular sheet 

Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(sheet)

Dim pdfDocument As PdfDocument = New PdfDocument()

pdfDocument = converter.Convert()

'Save the pdf file

pdfDocument.Save("ExceltoPDF.pdf")

'Dispose the objects

pdfDocument.Close()

converter.Dispose()

workbook.Close()

excelEngine.Dispose()       

{% endhighlight %} 



  {% endtabs %}  
  
  

### Creating individual PDF document for each worksheet	

The following code snippet shows how to create an individual PDF document for each worksheet in a workbook.

{% tabs %}  


{% highlight c# %}


ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

PdfDocument pdfDocument = new PdfDocument();



foreach (IWorksheet sheet in workbook.Worksheets)

{

ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);

pdfDocument = converter.Convert();

//Save the pdf file

pdfDocument.Save(sheet.Name+".pdf");

converter.Dispose();

}

//Dispose the objects

pdfDocument.Close();

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb.net %}


Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim pdfDocument As New PdfDocument()

For Each sheet As IWorksheet In workbook.Worksheets

Dim converter As New ExcelToPdfConverter(sheet)

PdfDocument = converter.Convert()

'Save the pdf file

PdfDocument.Save(sheet.Name + ".pdf")

converter.Dispose()

Next

pdfDocument.Close()

workbook.Close()

excelEngine.Dispose()

{% endhighlight %} 

 {% endtabs %}  

### Excel with Chart to PDF

To preserve the charts during Excel to PDF conversion, you should initialize the ChartToImageConverter of IApplication interface, otherwise the charts present in worksheet will get skipped. The following code illustrate how to convert an Excel with chart to PDF document.

{% tabs %}  

{% highlight c# %}


ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

// Instantiating the ChartToImageConverter and 

//Assigning the ChartToImageConverter instance of XlsIO application

application.ChartToImageConverter = new ChartToImageConverter();

// Tuning Chart Image Quality.

application.ChartToImageConverter.ScalingMode = ScalingMode.Best;

IWorkbook workbook = application.Workbooks.Open("chart.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

PdfDocument pdfDocument = new PdfDocument();

pdfDocument = converter.Convert();

pdfDocument.Save("ExceltoPDF.pdf");

converter.Dispose();

pdfDocument.Close();

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb.net %}


Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

' Instantiating the ChartToImageConverter and

'Assigning the ChartToImageConverter instance of XlsIO application

application.ChartToImageConverter = New ChartToImageConverter()

' Tuning Chart Image Quality.

application.ChartToImageConverter.ScalingMode = ScalingMode.Best

Dim workbook As IWorkbook = application.Workbooks.Open("chart.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

Dim converter As New ExcelToPdfConverter(workbook)

Dim pdfDocument As New PdfDocument()

pdfDocument = converter.Convert()

pdfDocument.Save("ExceltoPDF.pdf")

converter.Dispose()

pdfDocument.Close()

workbook.Close()

excelEngine.Dispose()

{% endhighlight %} 

  {% endtabs %}  

N>This section is applicable only to the Windows Forms, ASP.Net, MVC and WPF platforms.



### Supported Elements

This feature provides support for the following elements:

* Styles
* Character formatting
* Headers  and footers
* Images
* Text box
* Hyperlinks
* Document properties
* Comments
* Encryption
* Table Style Support
* Text Rotations
* Excel Page Setup Options
* Unicode Support
* Background Images
* Printing Titles when Converting the Excel to PDF
* Page Break Support
* Print Area Support
* Print Order Support
* Unicode in Headers and Footers

​

### Unsupported Elements 

The following list contains unsupported elements that presently will not be preserved in the generated PDF document. 

* Grouping columns
* OLE Objects
* Text rotations
* Background images

## Converting RTF documents to PDF

Essential PDF allows you to convert a RTF to PDF document. For converting a RTF to PDF, the following assemblies need to be referenced in your application

<table>
<thead> 
<tr>
<th>
Assembly Name<br/><br/></th><th>
Description<br/><br/></th></tr>
</thead>
<tbody>  
<tr>
<td>
Syncfusion.DocIO.Base<br/><br/></td><td>
This assembly has the core features for creating and manipulating RTF documents.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to package the RTF documents<br/><br/></td></tr>
<tr>
<td>
Syncfusion.DocToPdfConverter.Base<br/><br/></td><td>
This assembly is needed for converting the RTF to PDF.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Pdf.Base<br/><br/></td><td>
This assembly has the core features for creating PDF file.<br/><br/></td></tr>
</tbody>
</table>


The following namespaces are required to compile the code in this topic.

* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocToPDFConverter
* using Syncfusion.Pdf

DocToPDFConverter class is responsible for converting a RTF to PDF. The following code snippet illustrates how to convert a RTF to PDF document.

{% tabs %}  

{% highlight c# %}


//Load an existing RTF document

WordDocument rtfDocument = new WordDocument(inputFileName);

//Create an instance of DocToPDFConverter

DocToPDFConverter converter = new DocToPDFConverter();

//Convert Word document into PDF document

PdfDocument pdfDocument = converter.ConvertToPDF(rtfDocument);

//Save the PDF file 

pdfDocument.Save("RTFtoPDF.pdf");

//Close the instance of document objects

pdfDocument.Close(true);

rtfDocument.Close();



{% endhighlight %}

{% highlight vb.net %}


'Load an existing Word document

Dim rtfDocument As New WordDocument(inputFileName)

'Create an instance of DocToPDFConverter

Dim converter As New DocToPDFConverter()

'Convert Word document into PDF document

Dim pdfDocument As PdfDocument = converter.ConvertToPDF(rtfDocument)

'Save the PDF file 

pdfDocument.Save("RTFtoPDF.pdf")

'Close the instance of document objects

pdfDocument.Close(True)

rtfDocument.Close()



{% endhighlight %}

{% endtabs %}  


N> 1. RTF to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications.
N> 2. Total number of pages may vary  based on unsupported elements in the converted PDF document when compare to RTF document.


### Customizing the RTF to PDF conversion

Essential DocIO allows you to customize the RTF to PDF conversion with the below options:

* Allows to determine the quality of the jpeg images in the converted PDF
* Allows to reduce the Main Memory usage in RTF to PDF conversion by reusing the identical images.


{% tabs %}  

{% highlight c# %}



//Loads an existing Word document

WordDocument rtfDocument = new WordDocument(inputFileName);

//create an instance of DocToPDFConverter - responsible for Word to PDF conversion

DocToPDFConverter converter = new DocToPDFConverter();

//Set the image quality

converter.Settings.ImageQuality = 100;

//Set the image resolution

converter.Settings.ImageResolution = 640;

//Set true to optimize the memory usage for identical images

converter.Settings.OptimizeIdenticalImages = true;

//Convert Word document into PDF document

PdfDocument pdfDocument = converter.ConvertToPDF(rtfDocument);

//Save the PDF file to file system

pdfDocument.Save("RTFtoPDF.pdf");

//close the instance of document objects

pdfDocument.Close(true);

rtfDocument.Close();



{% endhighlight %}

{% highlight vb.net %}


'Loads an existing Word document

Dim rtfDocument As New WordDocument(inputFileName)

'create an instance of DocToPDFConverter - responsible for Word to PDF conversion

Dim converter As New DocToPDFConverter()

'Set the image quality

converter.Settings.ImageQuality = 100

'Set the image resolution

converter.Settings.ImageResolution = 640

'Set true to optimize the memory usage for identical images

converter.Settings.OptimizeIdenticalImages = True

'Convert Word document into PDF document

Dim pdfDocument As PdfDocument = converter.ConvertToPDF(rtfDocument)

'Save the PDF file to file system

pdfDocument.Save("RTFtoPDF.pdf")

'close the instance of document objects

pdfDocument.Close(True)

rtfDocument.Close()



{% endhighlight %}

{% endtabs %}  



## Converting TIFF to PDF

### Converting multipage TIFF to PDF

Multi frame TIFF image can be converted to PDF document. This can be done by accessing each frame of the multi frame TIFF image and rendering it in each page of the PDF document.

The code snippet to illustrate the same is given below.

{% tabs %} 

{% highlight c# %}


//Create a PDF document

PdfDocument pdfDocument = new PdfDocument();

//Add a section to the PDF document

PdfSection section = pdfDocument.Sections.Add();

//Declare the PDF page

PdfPage page;

//Declare PDF page graphics

PdfGraphics graphics;

//Load Multiframe Tiff image

PdfBitmap tiffImage = new PdfBitmap("image.tiff");

//Get the frame count

int frameCount = tiffImage.FrameCount;

//Access each frame draw into the page

for (int i = 0; i < frameCount; i++)

{

page = section.Pages.Add();

section.PageSettings.Margins.All = 0;

graphics = page.Graphics;

tiffImage.ActiveFrame = i;

graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height);

}

//Save and close the document

pdfDocument.Save("Sample.pdf");

pdfDocument.Close(true);



{% endhighlight %}



{% highlight vb.net %}


'Create a PDF document

Dim pdfDocument As New PdfDocument()

'Add a section to the PDF document

Dim section As PdfSection = pdfDocument.Sections.Add()

'Declare the PDF page

Dim page As PdfPage

'Declare PDF page graphics

Dim graphics As PdfGraphics

'Load Multiframe Tiff image

Dim tiffImage As New PdfBitmap("image.tiff")

'Get the frame count

Dim frameCount As Integer = tiffImage.FrameCount

'Access each frame draw into the page

For i As Integer = 0 To frameCount - 1

page = section.Pages.Add()

section.PageSettings.Margins.All = 0

graphics = page.Graphics

tiffImage.ActiveFrame = i

graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height)

Next

'Save and close the document

pdfDocument.Save("Sample.pdf")

pdfDocument.Close(True)

{% endhighlight %} 



  {% endtabs %}  

  
### Compression in monochrome images

Essential PDF supports JBIG2 compression for best compression of monochrome images.

Refer the below code snippet to draw a single frame monochrome tiff image with JBIG2 compression

{% tabs %}  

{% highlight c# %}


//Create a PDF document

PdfDocument pdfDocument = new PdfDocument();

//Add a page

PdfPage page = pdfDocument.Pages.Add();

//Load single frame Tiff image

PdfBitmap tiffImage = PdfImage.FromFile("image.tiff") as PdfBitmap;

//Set encode type

tiffImage.Encoding = EncodingType.JBIG2;

//Draw an image

page.Graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height);

//Save and close the document

pdfDocument.Save("Sample.pdf");

pdfDocument.Close(true);



{% endhighlight %}



{% highlight vb.net %}


'Create a PDF document

Dim pdfDocument As New PdfDocument()

'Add a page

Dim page As PdfPage = pdfDocument.Pages.Add()

'Load single frame Tiff image

Dim tiffImage As PdfBitmap = TryCast(PdfImage.FromFile("image.tiff"), PdfBitmap)

'Set encode type

tiffImage.Encoding = EncodingType.JBIG2

'Draw an image

page.Graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height)

'Save and close the document

pdfDocument.Save("Sample.pdf")

pdfDocument.Close(True)

{% endhighlight %} 

 {% endtabs %}  

N> 1. Currently the JBIG2Decode compression is supported only in lossy mode and also only single frame tiff images are supported.
N> 2. By default, all monochrome images will be compressed in CITTT4 compression.


## Converting XPS document to PDF 

The XPS (XML Paper Specification) document format is a fixed document format which consists of structured XML markup that defines the layout of a document and the visual appearance of each page, along with rendering rules for distributing, archiving, rendering, processing and printing the documents.

Essential PDF provides support for converting XPS to PDF using XPSToPdfConverter class.

The below code illustrates how to convert XPS to PDF.

{% tabs %}   

{% highlight c# %}


//Create converter class.

XPSToPdfConverter converter = new XPSToPdfConverter();

//Convert the XPS to PDF.

PdfDocument document = converter.Convert(xpsFileName);

//Save and close the document.

document.Save("Sample.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Create converter class.

Dim converter As New XPSToPdfConverter()

'Convert the XPS to PDF.

Dim document As PdfDocument = converter.Convert(xpsFileName)

'Save and close the document.

document.Save("Sample.pdf")

document.Close(True)

{% endhighlight %} 



  {% endtabs %} 

### Supported Elements

The below table shows the list of elements supported in XPS during the conversion.

<table>
<thead>  
<tr>
<th>
Element<br/><br/></th><th>
Convert to PDF<br/><br/></th></tr>
</thead>
<tbody>  
<tr>
<td>
ArcSegment<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
Canvas<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
DocumentOutline<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
DocumentReference<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
FigureStructure<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
FixedPageResources<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
Glyphs<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
Gradient<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
ImageBrush<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
Intent<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
LinkTarget<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
ListItemStructure<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
ListStructure<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
MatrixTransform<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
NamedElement<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
OutlineEntry<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
PageContent<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
PageContentLinkTargets<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
ParagraphStructure<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
Path<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
PolyBezierSegment<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
PolyLineSegment<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
PolyQuadraticBezierSegment<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
ResourceDictionary<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
SectionStructure<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SignBy<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SignatureDefinition<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SignatureDefinitions<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SigningLocation<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SolidColorBrush<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
SpotLocation<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
Story<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
TableStructure<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
VisualBrush<br/><br/></td><td>
No<br/><br/></td></tr>
</tbody>
</table>


## Converting HTML to Image

Essential PDF allows you to convert a HTML page to an image.

The following code snippet illustrate how to convert HTML to image using Essential PDF.

{% tabs %}  

{% highlight c# %}


HtmlConverter html = new HtmlConverter();

//Converts to Bitmap.

PdfUnitConvertor convertor = new PdfUnitConvertor();

float width = convertor.ConvertToPixels(560, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(890, PdfGraphicsUnit.Point);

Image img = html.ConvertToImage("http://www.google.com", ImageType.Bitmap, (int)width, (int)height, AspectRatio.KeepWidth);

//Save the image to disk

img.Save("Output.png",ImageFormat.Png);

html.Dispose();



{% endhighlight %}

{% highlight vb.net %}


Dim html As New HtmlConverter()

'Converts to Bitmap.

Dim convertor As New PdfUnitConvertor()

Dim width As Single = convertor.ConvertToPixels(560, PdfGraphicsUnit.Point)

Dim height As Single = convertor.ConvertToPixels(890, PdfGraphicsUnit.Point)

Dim img As Image = html.ConvertToImage("http://www.google.com", ImageType.Bitmap, CInt(width), CInt(height), AspectRatio.KeepWidth)

'Save the image to disk

img.Save("Output.png", ImageFormat.Png)

html.Dispose()



{% endhighlight %}

{% endtabs %}  


## Converting PDF to Image

PDF pages can be converted to images. To add PDF to image functionality in an application, you need to add the below mentioned assemblies as reference to the project.

1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.PdfViewer.Windows.dll 

The following code snippet illustrates how to convert PDF page into image.

{% tabs %}    

{% highlight c# %}


PdfDocumentView documentViewer = new PdfDocumentView();

//Load the PDF document

documentViewer.Load("Input.pdf");

//Export PDF page to image

Bitmap img = documentViewer.ExportAsImage(0);

//Save the image.

img.Save("Output.png", ImageFormat.Png);

documentViewer.Dispose();



{% endhighlight %}

{% highlight vb.net %}


Dim documentViewer As New PdfDocumentView()

'Load the PDF document

documentViewer.Load("Input.pdf")

'Export PDF page to image

Dim img As Bitmap = documentViewer.ExportAsImage(0)

'Save the image.

img.Save("Sample.png", ImageFormat.Png)

documentViewer.Dispose()



{% endhighlight %}

{% endtabs %}