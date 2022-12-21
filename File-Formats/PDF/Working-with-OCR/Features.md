---
title: Perform OCR on PDF and image files | Syncfusion
description: Learn how to perform OCR on scanned PDF documents and images with different tesseract version using Syncfusion .NET OCR library. 
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
--- 

# OCR Processor Features 

## Performing OCR for an entire document

To perform OCR on a PDF document with the help of [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html) class, refer to the following code snippet. 

{% tabs %}   

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/");

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path.
Using processor As OCRProcessor = New OCRProcessor("@TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Perform OCR with input document and tessdata (Language packs). 
    processor.PerformOCR(document, "@Tessdata/")

    'Create file stream.
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document
    document.Close(True)
End Using

End Using

{% endhighlight %}

{% endtabs %} 

N> The PerformOCR method returns only the text OCRed by OCRProcessor. Other existing text in the PDF page won't be returned in this method. Please check [text extraction](/file-formats/pdf/Working-with-Text-Extraction) feature for this.

## Performing OCR for a region of the document

To perform OCR on a particular region or several regions of a PDF page with the help of [PageRegion](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.PageRegion.html) class, refer to the following code snippet. 

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Assign rectangles to the page.
    RectangleF rect = new RectangleF(0, 100, 950, 150);
    List<PageRegion> pageRegions = new List<PageRegion>();
    //Create page region.
    PageRegion region = new PageRegion();
    //Set page index.
    region.PageIndex = 0;
    //Set page region.
    region.PageRegions = new RectangleF[] { rect };
    //Add region to page region.
    pageRegions.Add(region);
    //Set page regions.
    processor.Settings.Regions = pageRegions;

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/");

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Assign rectangles to the page.
    Dim rect As RectangleF = New RectangleF(0, 100, 950, 150)
    Dim pageRegions As List(Of PageRegion) = New List(Of PageRegion)()
    'Create page region. 
    Dim region As PageRegion = New PageRegion()
    'Set page index.
    region.PageIndex = 0
    'Set page region.
    region.PageRegions = New RectangleF() {rect}
    'Add region to page region.
    pageRegions.Add(region)
    'Set page regions.
    processor.Settings.Regions = pageRegions

    'Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, "Tessdata/")

    'Create file stream.
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using

{% endhighlight %}

{% endtabs %}  

## Performing OCR with tesseract version 3.05

The [TesseractVersion](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html#Syncfusion_OCRProcessor_OCRSettings_TesseractVersion) property is used to switch the tesseract version between 3.02 and 3.05. By default, OCR works with tesseract version 3.02.

N> The starting supported version of Tesserct in ASP.NET Core is 4.0. So the lower tesseract versions 3.02 and 3.05 are not supported and we don't have the property called ``TesseractVersion`` in ASP.NET Core platform.

The following code snippet demonstrates the OCR processor with Tesseract version 3.05 for PDF documents.
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/3.05/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Set tesseract OCR Engine.
    processor.Settings.TesseractVersion = TesseractVersion.Version3_05;

    //Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    processor.PerformOCR(document, @"Tessdata/", true);

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/3.05/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Set tesseract OCR Engine. 
    processor.Settings.TesseractVersion = TesseractVersion.Version3_05

    'Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    processor.PerformOCR(document, "Tessdata/", True)

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using
			
{% endhighlight %}

{% endtabs %}

## Performing OCR with Tesseract Version 4.0

The [TesseractVersion](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html#Syncfusion_OCRProcessor_OCRSettings_TesseractVersion) property is used to switch the tesseract version to 4.0. By default, OCR will be performed with tesseract version 3.02.

N> In ASP.NET Core platform, the default and starting supported version of tesserct is 4.0. So we don't have the property called ``TesseractVersion`` in ASP.NET Core platform. 

The following code example explains the OCR processor with Tesseract version 4.0 for PDF documents.
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/4.0/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Set tesseract OCR Engine.
    processor.Settings.TesseractVersion = TesseractVersion.Version4_0;

    //Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    processor.PerformOCR(document, @"Tessdata/", true);

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/4.0/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Set tesseract OCR Engine. 
    processor.Settings.TesseractVersion = TesseractVersion.Version4_0

    'Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    processor.PerformOCR(document, "Tessdata/", True)

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using

{% endhighlight %}

{% endtabs %}  

## Performing OCR on image

To perform OCR on an image file, refer the below code snippets for the same.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load the input image. 
    FileStream imageStream = new FileStream("Input.jpg", FileMode.Open);
    Bitmap bitmap = new Bitmap(imageStream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    String OCRText = processor.PerformOCR(bitmap, @"Tessdata/");
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load the input image. 
    Dim imageStream As FileStream = New FileStream("Input.jpg", FileMode.Open)
    Dim bitmap As Bitmap = New Bitmap(imageStream)

    'Set OCR language.
    processor.Settings.Language = Languages.English

    'Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    Dim ocrText As String = processor.PerformOCR(bitmap, "Tessdata/")

End Using

{% endhighlight %}

{% endtabs %}  

The following code examples illustrates how to extract Unicode characters from the image file. 

{% highlight c# tabtitle="ASP.NET Core" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load the input image. 
    FileStream imageStream = new FileStream("Input.jpg", FileMode.Open);
    Bitmap bitmap = new Bitmap(imageStream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Get stream from the font file. 
    FileStream fontStream = new FileStream(@"ARIALUNI.ttf", FileMode.Open);
    //Sets Unicode font to preserve the Unicode characters in a PDF document.
    processor.UnicodeFont = new PdfTrueTypeFont(fontStream, 8);

    //Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    String OCRText = processor.PerformOCR(bitmap, @"Tessdata/");
}

{% endhighlight %}

{% highlight c# tabtitle="C#" %}

//By default unicode characters can be extracted from image file in .NET Framework applications like WF, WPF, ASP.NET and ASP.NET MVC.

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

//By default unicode characters can be extracted from image file in .NET Framework applications like WF, WPF, ASP.NET and ASP.NET MVC.

{% endhighlight %}

{% endtabs %}  

## Performing OCR for large PDF documents

To optimize the memory to perform OCR for large PDF documents by enabling the isMemoryOptimized property in [PerformOCR](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html#Syncfusion_OCRProcessor_OCRProcessor_PerformOCR_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_String_System_Boolean_) method of [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html) class. Optimization will be effective only with Multithreading environment or PDF document with more images. Refer the following code examples for more details. 

N> Optimization of memory to perform OCR for large PDF documents is not supported in ASP.NET Core platform. 

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Perform OCR with input document, tessdata (Language packs) and enable isMemoryOptimized property.
    processor.PerformOCR(document, @"Tessdata/", true);

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Perform OCR with input document, tessdata (Language packs) and enable isMemoryOptimized property. 
    processor.PerformOCR(document, "Tessdata/", True)

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document.  
    document.Close(True)
End Using

{% endhighlight %}

{% endtabs %}  

## Performing OCR on rotated page of PDF document

To perform OCR on the rotated page of a PDF document, refer to the following code snippet for the same. 

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Set OCR page auto detection rotation.
    processor.Settings.PageSegment = PageSegmentMode.AutoOsd;

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/");

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Set OCR page auto detection rotation. 
    processor.Settings.PageSegment = PageSegmentMode.AutoOsd

    'Perform OCR with input document and tessdata (Language packs). 
    processor.PerformOCR(document, "Tessdata/")

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream. 
        document.Save(outputFileStream)
    End Using

    'Close the document.
    document.Close(True)
End Using

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

{% endhighlight %}

{% endtabs %}  

## Layout result from OCR

You can get the OCRed text and its bounds from a scanned PDF document by using the [OCRLayoutResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRLayoutResult.html) Class. Refer to the following code snippet. 
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Create the layout result. 
    OCRLayoutResult layoutResult = new OCRLayoutResult();

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/", out layoutResult);

    //Get OCRed line collection from first page.
    OCRLineCollection lines = layoutResult.Pages[0].Lines;

    //Get each OCR'ed line and its bounds.
    foreach (Line line in lines)
    {
        string text = line.Text;
        RectangleF bounds = line.Rectangle;
    }

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language.
    processor.Settings.Language = Languages.English

    'Create the layout result. 
    Dim layoutResult As OCRLayoutResult = New OCRLayoutResult()

    'Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, "Tessdata/", layoutResult)

    'Get OCR'ed line collection from first page. 
    Dim lines As OCRLineCollection = layoutResult.Pages(0).Lines

    'Get each OCR'ed line and its bounds. 
    For Each line As Line In lines
        Dim text As String = line.Text
        Dim bounds As RectangleF = line.Rectangle
    Next

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document.
    document.Close(True)
End Using

{% endhighlight %}

{% endtabs %} 

## Native call

Enable native call will not launch any temporary process for OCR processing, instead it will invoke the native calls.

N> The starting supported version of Tesserct in ASP.NET Core is 4.0. So the lower tesseract versions 3.02 and 3.05 are not supported and we don't have the property called ``TesseractVersion`` in ASP.NET Core platform. 

### Tesseract 3.02

Tesseract 3.02 supports only 32-bit version. By default, OCR works with this Tesseract version 3.02. 

N> Enable native call will not work in 64-bit in Tesseract 3.02 version. Instead a temporary process will be launched for OCR processing.

The following sample code snippet demonstrates the OCR processor with native call support of tesseract 3.02.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/3.02/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Set tesseract OCR Engine.
    processor.Settings.TesseractVersion = TesseractVersion.Version3_02;

    //Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    processor.PerformOCR(document, @"Tessdata/", true);

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/3.02/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Set tesseract OCR Engine. 
    processor.Settings.TesseractVersion = TesseractVersion.Version3_02

    'Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    processor.PerformOCR(document, "Tessdata/", True)

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using
			
{% endhighlight %}

{% endtabs %}

### Tesseract 3.05

Tesseract 3.05 supports the native call for both x86 and x64 architectures. By default, the x86 tesseract binaries are available with Syncfusion NuGet package or the tesseract installer. 

You can download the x64 supporting tesseract binaries from the following link.
[Tesseract 64-bit binaries](http://www.syncfusion.com/downloads/support/directtrac/general/ze/Tesseract3.05_x641904984914)

N> This 64-bit binaries are required only when the native call property is enabled.
N> Make sure to provide the 64-bit binaries path while using the 64-bit environment.

The following sample code snippet demonstrates the OCR processor with native call support of tesseract 3.05.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/3.05/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Set tesseract OCR Engine.
    processor.Settings.TesseractVersion = TesseractVersion.Version3_05;

    //Set enable native call.
    processor.Settings.EnableNativeCall = true;

    //Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    processor.PerformOCR(document, @"Tessdata/", true);

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}


{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/3.05/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Set tesseract OCR Engine. 
    processor.Settings.TesseractVersion = TesseractVersion.Version3_05

    'Set enable native call
    processor.Settings.EnableNativeCall = True

    'Perform OCR with input document, tessdata (Language packs) and enabling isMemoryOptimized property.
    processor.PerformOCR(document, "Tessdata/", True)

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using

{% endhighlight %}

{% endtabs %}  

### Advantages of Native Call over Normal API 

Enabling this property will process OCR with native calls (PInvoke) instead of surrogate process.
For surrogate process, it requires permission for creating and executing a process and native calls (PInvoke) does not required. And also performance will be better in PInvoke instead of surrogate process.

## Customizing temp folder

While performing OCR on an existing scanned PDF document, the OCR Processor will create temporary files (.temp, .tiff, .txt) and the files are deleted after the process is completed. You can change this temporary files folder location using the [TempFolder](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html#Syncfusion_OCRProcessor_OCRSettings_TempFolder) property available in the [OCRSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html) Instance. Refer to the following code snippet to change the path of temp folder when performing the OCR. 

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Set custom temp file path location.
    processor.Settings.TempFolder = "D:/Temp/";

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/");

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Set custom temp file path location.
    processor.Settings.TempFolder = "D:/Temp/"

    'Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, "Tessdata/")

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using

{% endhighlight %}

{% endtabs %} 

## Performing OCR with different Page Segmentation Mode

The PageSegment property is used to set the page segmentation mode. By default, OCR works with the "Auto" page segmentation mode. Kindly refer to the following code example to perform OCR with different page segmentation mode. 

N> The page segmentation mode is supported only in the Tesseract version 4.0 and above.
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //** For .NET Framework only **.
    //processor.Settings.TesseractVersion = TesseractVersion.Version4_0;

    //Set OCR Page segment mode to process.
    processor.Settings.PageSegment = PageSegmentMode.AutoOsd;

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/");

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    ' ** For .NET Framework only **.
    'processor.Settings.TesseractVersion = TesseractVersion.Version4_0

    'Set OCR Page segment mode to process.
    processor.Settings.PageSegment = PageSegmentMode.AutoOsd

    'Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, "Tessdata/")

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using

{% endhighlight %}

{% endtabs %} 

## Performing OCR with different OCR Engine Mode

The OCREngineMode property is used to set the OCR Engine modes. By default, OCR works with OCR Engine mode "Default". Refer to the following code example to perform OCR with different OCR engine mode. 
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Set tesseract version. ** For .NET Framework only. **
    //processor.Settings.TesseractVersion = TesseractVersion.Version4_0;

    //Set OCR engine mode to process.
    processor.Settings.OCREngineMode = OCREngineMode.LSTMOnly;

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/");

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Set tesseract version. ** For .NET Framework only. **
    'processor.Settings.TesseractVersion = TesseractVersion.Version4_0

    'Set OCR engine mode to process.
    processor.Settings.OCREngineMode = OCREngineMode.LSTMOnly

    'Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, "Tessdata/")

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using

{% endhighlight %}

{% endtabs %} 

N> The OCR Engine Mode is supported only in the Tesseract version 4.0 and above.

## White List

A white list specifies a list of characters that the OCR engine is only allowed to recognize. If a character is not on the white list, it cannot be included in the output OCR results. Refer to the following code snippet which explains the same. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Set tesseract version. ** For .NET Framework only. **
    //processor.Settings.TesseractVersion = TesseractVersion.Version4_0;

    //Set OCR engine mode to process.
    processor.Settings.OCREngineMode = OCREngineMode.LSTMOnly;

    //Set WhiteList Property.
    processor.Settings.WhiteList = "PDF";

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/");

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Set tesseract version. ** For .NET Framework only. **
    'processor.Settings.TesseractVersion = TesseractVersion.Version4_0

    'Set OCR engine mode to process.
    processor.Settings.OCREngineMode = OCREngineMode.LSTMOnly

    'Set WhiteList Property.
    processor.Settings.WhiteList = "PDF"

    'Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, "Tessdata/")

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using

{% endhighlight %}
{% endtabs %} 

## Black List

A black list specifies the characters that exclude from the character set used for recognition and the OCR will not return any of the characters which we specified in the list. Refer to the following code snippet which explains the same. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Set tesseract version. ** For .NET Framework only. **
    //processor.Settings.TesseractVersion = TesseractVersion.Version4_0;

    //Set OCR engine mode to process.
    processor.Settings.OCREngineMode = OCREngineMode.LSTMOnly;

    //Set BlackList Property.
    processor.Settings.BlackList = "PDF";

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/");

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor with tesseract binaries folder path. 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/")

    'Load an existing PDF document. 
    Dim stream As FileStream = New FileStream("Input.pdf", FileMode.Open)
    Dim document As PdfLoadedDocument = New PdfLoadedDocument(stream)

    'Set OCR language. 
    processor.Settings.Language = Languages.English

    'Set tesseract version. ** For .NET Framework only. **
    'processor.Settings.TesseractVersion = TesseractVersion.Version4_0

    'Set OCR engine mode to process.
    processor.Settings.OCREngineMode = OCREngineMode.LSTMOnly

    'Set BlackList Property.
    processor.Settings.BlackList = "PDF"

    'Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, "Tessdata/")

    'Create file stream. 
    Using outputFileStream As FileStream = New FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite)
        'Save the PDF document to file stream.
        document.Save(outputFileStream)
    End Using

    'Close the document. 
    document.Close(True)
End Using

{% endhighlight %}

{% endtabs %} 

## OCR an Image to PDF

You can perform OCR on an image and convert it to a searchable PDF document. It is also possible to set PdfConformanceLevel to the output PDF document using OCRSettings. 

N> This PDF conformance option only applies for image OCR to PDF documents.

The following code sample illustrates how to OCR an image to a PDF document:

{% tabs %}

{% highlight c# tabtitle="C#" %}



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}



{% endhighlight %}
{% endtabs %} 

## Performing OCR with Unicode characters

You can perform OCR on Images with Unicode characters. To preserve the Unicode characters in the PDF document, use the UnicodeFont property. Refer to the following code snippet.

{% highlight c# tabtitle="ASP.NET Core" %}

//Initialize the OCR processor with tesseract binaries folder path.
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Windows/"))
{
    //Load an existing PDF document.
    FileStream stream = new FileStream("Input.pdf", FileMode.Open);
    PdfLoadedDocument document = new PdfLoadedDocument(stream);

    //Set OCR language.
    processor.Settings.Language = Languages.English;

    //Sets Unicode font to preserve the Unicode characters in a PDF document.
    FileStream fontStream = new FileStream(@"ARIALUNI.ttf", FileMode.Open);
    processor.UnicodeFont = new PdfTrueTypeFont(fontStream, 8);

    //Perform OCR with input document and tessdata (Language packs).
    processor.PerformOCR(document, @"Tessdata/");

    //Create file stream.
    using (FileStream outputFileStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite))
    {
        //Save the PDF document to file stream.
        document.Save(outputFileStream);
    }

    //Close the document.
    document.Close(true);
}

{% endhighlight %}

{% highlight c# tabtitle="C#" %}

//By default unicode characters can be extracted from image file in .NET Framework applications like WF, WPF, ASP.NET and ASP.NET MVC.

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

//By default unicode characters can be extracted from image file in .NET Framework applications like WF, WPF, ASP.NET and ASP.NET MVC.

{% endhighlight %}
{% endtabs %} 

## Best Practices

**You can improve the accuracy of the OCR process by choosing the correct compression method when converting the scanned paper to a TIFF image and then to a PDF document.**

* Use (zip) lossless compression for color or gray-scale images.
* Use CCITT Group 4 or JBIG2 (lossless) compression for monochrome images. This ensures that optical character recognition works on the highest-quality image, thereby improving the OCR accuracy. This is especially useful in low-resolution scans.
* In addition, rotated images and skewed images can also affect the accuracy and readability of the OCR process.

**Tesseract works best with text when at least 300 dots per inch (DPI) are used, so it is beneficial to resize images.**

For more details regarding quality improvement, refer to the following link:

[https://github.com/tesseract-ocr/tesseract/wiki/ImproveQuality](https://github.com/tesseract-ocr/tesseract/wiki/ImproveQuality )

**You can set the different performance level to the OCRProcessor using [Performance](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.Performance.html) enumeration.**

* Rapid - high speed OCR performance and provide normal OCR accuracy
* Fast - provides moderate OCR processing speed and accuracy
* Slow - Slow OCR performance and provide best OCR accuracy.

Refer below code snippet to set the performance of the OCR.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor by providing the path of the tesseract binaries
OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/")

//set the OCR performance
processor.Settings.Performance = Performance.Fast;

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor by providing the path of the tesseract binaries
Dim processor As New OCRProcessor("TesseractBinaries/")

'Set the OCR performance
processor.Settings.Performance = Performance.Fast

{% endhighlight %}

{% endtabs %}  