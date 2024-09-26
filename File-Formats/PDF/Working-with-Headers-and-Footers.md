---
title: Working with Headers and Footers | Syncfusion
description: This section explains how to create Headers and Footers in the PDF document using Syncfusion .NET PDF library
platform: file-formats
control: PDF
documentation: UG
---
# Working with Headers and Footers 

Essential PDF supports to draw the header and footer in PDF document using [PdfPageTemplateElement](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageTemplateElement.html) class. The header and footer can contain any types of element including dynamic fields.

## Adding an automatic field in header and footer

Essential PDF supports to add page count, page numbers, date and time using dynamic fields such as [PdfPageCountField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageCountField.html), [PdfPageNumberField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageNumberField.html) etc.

The below code snippet explains how to draw the page numbers in footer using automatic fields.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create a new PDF document.
PdfDocument pdfDocument = new PdfDocument();
//Add a page to the PDF document
PdfPage pdfPage = pdfDocument.Pages.Add();
//Create a header and draw the image.
RectangleF bounds = new RectangleF(0, 0, pdfDocument.Pages[0].GetClientSize().Width, 50);
PdfPageTemplateElement header = new PdfPageTemplateElement(bounds);
//Load the PDF document
FileStream imageStream = new FileStream("Logo.png", FileMode.Open, FileAccess.Read);
PdfImage image = new PdfBitmap(imageStream);
//Draw the image in the header.
header.Graphics.DrawImage(image, new PointF(0, 0), new SizeF(100, 50));
//Add the header at the top.
pdfDocument.Template.Top = header;
//Create a Page template that can be used as footer.
PdfPageTemplateElement footer = new PdfPageTemplateElement(bounds);
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 7);
PdfBrush brush = new PdfSolidBrush(Color.Black);
//Create page number field.
PdfPageNumberField pageNumber = new PdfPageNumberField(font, brush);
//Create page count field.
PdfPageCountField count = new PdfPageCountField(font, brush);
//Add the fields in composite fields.
PdfCompositeField compositeField = new PdfCompositeField(font, brush, "Page {0} of {1}", pageNumber, count);
compositeField.Bounds = footer.Bounds;
//Draw the composite field in footer.
compositeField.Draw(footer.Graphics, new PointF(470, 40));
//Add the footer template at the bottom.
pdfDocument.Template.Bottom = footer;

//Save the document into stream.
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);
//Closes the document.
pdfDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document.
PdfDocument pdfDocument = new PdfDocument();
//Add a page to the PDF document
PdfPage pdfPage = pdfDocument.Pages.Add();
//Create a header and draw the image.
RectangleF bounds = new RectangleF(0, 0, pdfDocument.Pages[0].GetClientSize().Width, 50);
PdfPageTemplateElement header = new PdfPageTemplateElement(bounds);
PdfImage image = new PdfBitmap(@"Logo.png");
//Draw the image in the header.
header.Graphics.DrawImage(image, new PointF(0, 0), new SizeF(100, 50));
//Add the header at the top.
pdfDocument.Template.Top = header;
//Create a Page template that can be used as footer.
PdfPageTemplateElement footer = new PdfPageTemplateElement(bounds);
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 7);
PdfBrush brush = new PdfSolidBrush(Color.Black);
//Create page number field.
PdfPageNumberField pageNumber = new PdfPageNumberField(font, brush);
//Create page count field.
PdfPageCountField count = new PdfPageCountField(font, brush);
//Add the fields in composite fields.
PdfCompositeField compositeField = new PdfCompositeField(font, brush, "Page {0} of {1}", pageNumber, count);
compositeField.Bounds = footer.Bounds;
//Draw the composite field in footer.
compositeField.Draw(footer.Graphics, new PointF(470, 40));
//Add the footer template at the bottom.
pdfDocument.Template.Bottom = footer;

//Save and close the document.
pdfDocument.Save("Output.pdf");
pdfDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new PDF document.
Dim pdfDocument As New PdfDocument()
'Add a page to the PDF document.
Dim pdfPage As PdfPage = pdfDocument.Pages.Add()
'Create a header and draw the image.
Dim bounds As New RectangleF(0, 0, pdfDocument.Pages(0).GetClientSize().Width, 50)
Dim header As New PdfPageTemplateElement(bounds)
Dim image As PdfImage = New PdfBitmap("Logo.jpg")
'Draw the image in the Header.
header.Graphics.DrawImage(image, New PointF(0, 0), New SizeF(100, 50))
'Add the header at the top.
pdfDocument.Template.Top = header
'Create a page template that can be used as footer.
Dim footer As New PdfPageTemplateElement(bounds)
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 7)
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
'Create page number field.
Dim pageNumber As New PdfPageNumberField(font, brush)
'Create page count field.
Dim count As New PdfPageCountField(font, brush)
'Add the fields in composite fields.
Dim compositeField As New PdfCompositeField(font, brush, "Page {0} of {1}", pageNumber, count)
compositeField.Bounds = footer.Bounds
'Draw the composite field in footer.
compositeField.Draw(footer.Graphics, New PointF(470, 40))
'Add the footer template at the bottom.
pdfDocument.Template.Bottom = footer

'Save and close the document.
pdfDocument.Save("Output.pdf")
pdfDocument.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Header%20and%20Footer/Adding-an-automatic-field-in-header-and-footer). 