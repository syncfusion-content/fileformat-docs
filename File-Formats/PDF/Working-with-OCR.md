---
title: Working with Optical Character Recognition (OCR)
description: This section explains how to process OCR for the existing PDF document
platform: file-formats
control: PDF
documentation: UG
---

# Working with Optical Character Recognition (OCR)

Essential PDF provides support for Optical Character Recognition with the help of Google’s Tesseract Optical Character Recognition engine.

## Prerequisites and setting up the Tesseract Engine

* To use the OCR feature in your application, you need to add reference to the following set of assemblies.
1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.OCRProcessor.Base.dll

* Place the SyncfusionTesseract.dll and liblept168.dll Tesseract assemblies (available in the installed location Installation Location>>\Syncfusion\Essential Studio\<<Version Number>>\OCRProcessor) in the local system and provide the assembly path to the OCR processor.

{% tabs %}  

{% highlight c# %}



OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\")



{% endhighlight %}

{% highlight vb.net %}


Dim processor As New OCRProcessor("TesseractBinaries\")



{% endhighlight %}

{% endtabs %}  

* Place the Tesseract language data {E.g eng.traineddata} (available in the installed location <<Installation Location>>\Syncfusion\Essential Studio\<<Version Number>>\OCRProcessor) in the local system and provide a path to the OCR processor 

{% tabs %}  

{% highlight c# %}



OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\");

processor.PerformOCR(lDoc, @"Tessdata\");



{% endhighlight %}

{% highlight vb.net %}


Dim processor As New OCRProcessor("TesseractBinaries\")

processor.PerformOCR(lDoc, "Tessdata\")



{% endhighlight %}

{% endtabs %}  

You can also download the language packages from below link

[https://code.google.com/p/tesseract-ocr/downloads/list](https://code.google.com/p/tesseract-ocr/downloads/list# )


## Performing OCR for an entire document

You can perform OCR on PDF document with the help of OCRProcessor Class. Refer the below code snippet for the same.

{% tabs %}   

{% highlight c# %}


//Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{

//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");

//Set OCR language to process

processor.Settings.Language = Languages.English;

//Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, @"Tessdata\");

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

lDoc.Close(true);

}



{% endhighlight %}



{% highlight vb.net %}




'Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, "Tessdata\")

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)

End Using



{% endhighlight %}

{% endtabs %} 

N> The PerformOCR method returns only the text OCRed by OCRProcessor. Other existing text in the PDF page won’t be returned in this method. Please check [text extraction](/file-formats/pdf/Working-with-Text-Extraction) feature for this.

## Performing OCR for a region of the document

You can perform OCR on particular region or several regions of a PDF page with the help of PageRegion class. Refer the below code snippet for the same.

{% tabs %} 

{% highlight c# %}


//Initialize the OCR processor by providing the path of the tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{

//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");

//Set OCR language to process

processor.Settings.Language = Languages.English;

RectangleF rect = new RectangleF(0, 100, 950, 150);

//Assign rectangles to the page

List<PageRegion> pageRegions = new List<PageRegion>();

PageRegion region = new PageRegion();

region.PageIndex = 1;

region.PageRegions = new RectangleF[] { rect };

pageRegions.Add(region);

processor.Settings.Regions = pageRegions;

//Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, @"Tessdata\");

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

lDoc.Close(true);

}



{% endhighlight %}



{% highlight vb.net %}


'Initialize the OCR processor by providing the path of the tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

Dim rect As New RectangleF(0, 100, 950, 150)

'Assign rectangles to the page

Dim pageRegions As New List(Of PageRegion)()

Dim region As New PageRegion()

region.PageIndex = 1

region.PageRegions = New RectangleF() {rect}

pageRegions.Add(region)

processor.Settings.Regions = pageRegions

'Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, "Tessdata\")

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)



{% endhighlight %}

 {% endtabs %}  

## Performing OCR on image

You can perform OCR on an image also. Refer the below code snippets for the same.

{% tabs %} 

{% highlight c# %}


//Initialize the OCR processor by providing the path of the tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{

//loading the input image

Bitmap image = new Bitmap("input.jpeg");

//Set OCR language to process

processor.Settings.Language = Languages.English;

//Process OCR by providing the bitmap image, data dictionary and language

string ocrText= processor.PerformOCR(image, @"Tessdata\");

}



{% endhighlight %}



{% highlight vb.net %}


'Initialize the OCR processor by providing the path of the tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'loading the input image

Dim image As New Bitmap("input.jpeg")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Process OCR by providing the bitmap image, data dictionary and language

Dim ocrText As String = processor.PerformOCR(image, "Tessdata\")

End Using



{% endhighlight %}

 {% endtabs %}  
 

## Best Practices

**You can improve the accuracy of the OCR process by choosing the correct compression method when converting the scanned paper to a TIFF image and then to a PDF document.**

* Use (zip) lossless compression for color or gray-scale images.

* Use CCITT Group 4 or JBIG2 (lossless) compression for monochrome images. This ensures that optical character recognition works on the highest-quality image, thereby improving the OCR accuracy. This is especially useful in low-resolution scans.

* In addition, rotated images and skewed images can also affect the accuracy and readability of the OCR process.

**Tesseract works best with text when at least 300 dots per inch (DPI) are used, so it is beneficial to resize images.**

For more details regarding quality improvement, refer to the following link:

[https://code.google.com/p/tesseract-ocr/wiki/ImproveQuality](https://code.google.com/p/tesseract-ocr/wiki/ImproveQuality# )

**You can set the different performance level to the OCRProcessor using “Performance” enumeration.**

* Rapid – high speed OCR performance and provide normal OCR accuracy

* Fast – provides moderate OCR processing speed and accuracy

* Slow – Slow OCR performance and provide best OCR accuracy.

Refer below code snippet to set the performance of the OCR.

{% tabs %}  

{% highlight c# %}


OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\")

//set the OCR performance

processor.Settings.Performance = Performance.Fast;



{% endhighlight %}

{% highlight vb.net %}


Dim processor As New OCRProcessor("TesseractBinaries\")

'Set the OCR performance

processor.Settings.Performance = Performance.Fast



{% endhighlight %}

{% endtabs %}  

## Troubleshooting

**Issue:** You can get the exception “Tesseract has not been initialized” while performing OCR process. 

**Solution:** To resolve this, make sure the path of the Tesseract binaries and Tesseract data are properly provided as shown below.

{% tabs %}  

{% highlight c# %}


//'TesseractBinaries – path of the folder containing SyncfusionTesseract.dll and liblept168.dll

OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\");

//Tessdata – path of the folder containing the language pack

processor.PerformOCR(lDoc, @"Tessdata\");



{% endhighlight %}

{% highlight vb.net %}


'TesseractBinaries – path of the folder containing SyncfusionTesseract.dll and liblept168.dll

Dim processor As New OCRProcessor("TesseractBinaries\")

'Tessdata – path of the folder containing the language pack

processor.PerformOCR(lDoc, "Tessdata\")



{% endhighlight %}

{% endtabs %}  

**Issue:** OCR processor doesn’t process languages other than English.

**Solution:** Essential PDF supports all the languages supported by Tesseract engine.

The dictionary packs for the languages can be downloaded from the following online location:

[https://code.google.com/p/tesseract-ocr/downloads/list](https://code.google.com/p/tesseract-ocr/downloads/list# )

It is also mandatory to change the corresponding language code in the OCRProcessor.Settings.Language property. For example, to perform optical character recognition in German, the property should be set as processor.Settings.Language = "deu";

The following link contains the complete set of languages supported by Tesseract and their language codes.

[http://tesseract-ocr.googlecode.com/svn/trunk/doc/tesseract.1.html#_languages](http://tesseract-ocr.googlecode.com/svn/trunk/doc/tesseract.1.html#_languages)

