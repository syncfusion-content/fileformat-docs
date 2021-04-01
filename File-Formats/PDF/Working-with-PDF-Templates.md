---
title: Working with PDF templates | Syncfusion
description: This section explains how to create a PDF template is a drawing surface, where contents can be added;
platform: file-formats
control: PDF
documentation: UG
---
# Working with PDF Templates 

A PDF template is a drawing surface, where contents can be added. All the elements that can be added to a [PdfPage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPage.html) is supported in [PdfTemplate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTemplate.html) as well. The template in turn can be drawn over the page or can be positioned at any part of the page.

## Creating a new PDF template

The [PdfTemplate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTemplate.html) class can be used to create a new PDF template. You can add contents to the template using [Graphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTemplate.html#Syncfusion_Pdf_Graphics_PdfTemplate__ctor_System_Drawing_RectangleF_) property of the ```PdfTemplate``` object.

The below code snippet illustrates how to add contents to the ```PdfTemplate``` and render into the new PDF page.

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics 

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new System.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Draw a string using the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

pdfPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the document.

pdfDocument.Save("Output.pdf");

//close the document

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

'Add a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Create a PDF Template.

Dim template As New PdfTemplate(100, 50)

'Draw a rectangle on the template graphics.

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, New System.Drawing.RectangleF(0, 0, 100, 50))

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Draw a string using the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5)

'Draw the template on the page graphics of the document.

pdfPage.Graphics.DrawPdfTemplate(template, PointF.Empty)

'Save the document.

pdfDocument.Save("Output.pdf")

'close the document

pdfDocument.Close(True)


{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics 

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new System.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Color.FromArgb(255, 0, 0, 0));

//Draw a string using the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

pdfPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await pdfDocument.SaveAsync(stream);

//Close the document

pdfDocument.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics 

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new Syncfusion.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Draw a string using the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

pdfPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the document into stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

stream.Position = 0;

//Closes the document

pdfDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics 

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new Syncfusion.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Draw a string using the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

pdfPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

//Closes the document

pdfDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  


The below code snippet illustrates how to render the [PdfTemplate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTemplate.html) on an existing PDF document.

{% tabs %}  

{% highlight c# %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the page into Pdf document.

PdfLoadedPage LoadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics.

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new System.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Draw a string on the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

LoadedPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the modified document.

loadedDocument.Save("Output.pdf");

//close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the page into Pdf document.

Dim LoadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create a PDF Template.

Dim template As New PdfTemplate(100, 50)

'Draw a rectangle on the template graphics.

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, New System.Drawing.RectangleF(0, 0, 100, 50))

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Draw a string on the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5)

'Draw the template on the page graphics of the document.

LoadedPage.Graphics.DrawPdfTemplate(template, PointF.Empty)

'Save the modified document.

loadedDocument.Save("Output.pdf")

'close the document

loadedDocument.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Load the page into Pdf document.

PdfLoadedPage LoadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics.

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new System.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Color.FromArgb(255, 0, 0, 0));

//Draw a string on the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

LoadedPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page into Pdf document.

PdfLoadedPage LoadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics.

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new Syncfusion.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Draw a string on the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

LoadedPage.Graphics.DrawPdfTemplate(template, Syncfusion.Drawing.PointF.Empty);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page into Pdf document.

PdfLoadedPage LoadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics.

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new Syncfusion.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Draw a string on the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

LoadedPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Closes the document

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

## Creating templates from existing PDF document

Essential PDF supports to create the templates from an existing PDF document page and draw it in on a new PDF document.

The below code illustrates how to create the template from an existing page and draw it in new PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create the template from the page.

PdfTemplate template = loadedPage.CreateTemplate();

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Set the document margin

document.PageSettings.SetMargins(2);

//Add the page

PdfPage page = document.Pages.Add();

//Create the graphics

PdfGraphics graphics = page.Graphics;

//Draw the template

graphics.DrawPdfTemplate(template, PointF.Empty,new SizeF(page.Size.Width/2,page.Size.Height));

//Save the new document.

document.Save("output.pdf");

//Close the documents

loadedDocument.Close(true);

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create the template from the page.

Dim template As PdfTemplate = loadedPage.CreateTemplate()

'Create a new PDF document

Dim document As New PdfDocument()

'Set the document margin

document.PageSettings.SetMargins(2)

'Add the page

Dim page As PdfPage = document.Pages.Add()

'Create the graphics

Dim graphics As PdfGraphics = page.Graphics

'Draw the template

graphics.DrawPdfTemplate(template, PointF.Empty, New SizeF(page.Size.Width \ 2, page.Size.Height))

'Save the new document.

document.Save("output.pdf")

'Close the documents

loadedDocument.Close(True)

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create the template from the page.

PdfTemplate template = loadedPage.CreateTemplate();

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Set the document margin

document.PageSettings.SetMargins(2);

//Add the page

PdfPage page = document.Pages.Add();

//Create the graphics

PdfGraphics graphics = page.Graphics;

//Draw the template

graphics.DrawPdfTemplate(template, PointF.Empty, new SizeF(page.Size.Width / 2, page.Size.Height));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create the template from the page.

PdfTemplate template = loadedPage.CreateTemplate();

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Set the document margin

document.PageSettings.SetMargins(2);

//Add the page

PdfPage page = document.Pages.Add();

//Create the graphics

PdfGraphics graphics = page.Graphics;

//Draw the template

graphics.DrawPdfTemplate(template, Syncfusion.Drawing.PointF.Empty, new Syncfusion.Drawing.SizeF(page.Size.Width / 2, page.Size.Height));

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create the template from the page.

PdfTemplate template = loadedPage.CreateTemplate();

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Set the document margin

document.PageSettings.SetMargins(2);

//Add the page

PdfPage page = document.Pages.Add();

//Create the graphics

PdfGraphics graphics = page.Graphics;

//Draw the template

graphics.DrawPdfTemplate(template, PointF.Empty, new SizeF(page.Size.Width / 2, page.Size.Height));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Closes the document

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  



## Working with PdfPageTemplateElement

[PdfPageTemplateElement](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageTemplateElement.html) is template element that can be added to any part of the PDF page such as header, footer etc.

The below code illustrates how to add the page template elements in a PDF document.

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a header and draw the image.

RectangleF bounds = new RectangleF(0, 0, pdfDocument.Pages[0].GetClientSize().Width, 50);

PdfPageTemplateElement header = new PdfPageTemplateElement(bounds );

PdfImage image = new PdfBitmap(@"Logo.png");

//Draw the image in the header.

header.Graphics.DrawImage(image, new PointF(0, 0), new SizeF(100, 50));

//Add the header at the top.

pdfDocument.Template.Top = header;

//Create a Page template that can be used as footer.

PdfPageTemplateElement footer = new PdfPageTemplateElement(bounds );

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

{% highlight vb.net %}


'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

'Add a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Create a header and draw the image.

Dim bounds  As New RectangleF(0, 0, pdfDocument.Pages(0).GetClientSize().Width, 50)

Dim header As New PdfPageTemplateElement(bounds )

Dim image As PdfImage = New PdfBitmap("Logo.jpg")

'Draw the image in the Header.

header.Graphics.DrawImage(image, New PointF(0, 0), New SizeF(100, 50))

'Add the header at the top.

pdfDocument.Template.Top = header

'Create a page template that can be used as footer.

Dim footer As New PdfPageTemplateElement(bounds )

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

{% highlight UWP %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a header and draw the image.

RectangleF bounds = new RectangleF(0, 0, pdfDocument.Pages[0].GetClientSize().Width, 50);

PdfPageTemplateElement header = new PdfPageTemplateElement(bounds);

//Load the image as stream

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.L

PdfImage image = new PdfBitmap(imageStream);

//Draw the image in the header.

header.Graphics.DrawImage(image, new PointF(0, 0), new SizeF(100, 50));

//Add the header at the top.

pdfDocument.Template.Top = header;

//Create a Page template that can be used as footer.

PdfPageTemplateElement footer = new PdfPageTemplateElement(bounds);

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 7);

PdfBrush brush = new PdfSolidBrush(Color.FromArgb(128, 0, 0, 0));

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

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await pdfDocument.SaveAsync(stream);

//Close the document

pdfDocument.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a header and draw the image.

RectangleF bounds = new RectangleF(0, 0, pdfDocument.Pages[0].GetClientSize().Width, 50);

PdfPageTemplateElement header = new PdfPageTemplateElement(bounds);

//Load the image file

FileStream imageStream = new FileStream("Logo.png", FileMode.Open, FileAccess.Read);

PdfImage image = new PdfBitmap(imageStream);

//Draw the image in the header.

header.Graphics.DrawImage(image, new Syncfusion.Drawing.PointF(0, 0), new SizeF(100, 50));

//Add the header at the top.

pdfDocument.Template.Top = header;

//Create a Page template that can be used as footer.

PdfPageTemplateElement footer = new PdfPageTemplateElement(bounds);

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 7);

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Create page number field.

PdfPageNumberField pageNumber = new PdfPageNumberField(font, brush);

//Create page count field.

PdfPageCountField count = new PdfPageCountField(font, brush);

//Add the fields in composite fields.

PdfCompositeField compositeField = new PdfCompositeField(font, brush, "Page {0} of {1}", pageNumber, count);

compositeField.Bounds = footer.Bounds;

//Draw the composite field in footer.

compositeField.Draw(footer.Graphics, new Syncfusion.Drawing.PointF(470, 40));

//Add the footer template at the bottom.

pdfDocument.Template.Bottom = footer;

//Save the document into stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

stream.Position = 0;

//Closes the document

pdfDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a header and draw the image.

RectangleF bounds = new RectangleF(0, 0, pdfDocument.Pages[0].GetClientSize().Width, 50);

PdfPageTemplateElement header = new PdfPageTemplateElement(bounds);

//Load the image as stream

Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Logo.png");

PdfImage image = new PdfBitmap(imageStream);

//Draw the image in the header.

header.Graphics.DrawImage(image, new PointF(0, 0), new SizeF(100, 50));

//Add the header at the top.

pdfDocument.Template.Top = header;

//Create a Page template that can be used as footer.

PdfPageTemplateElement footer = new PdfPageTemplateElement(bounds);

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 7);

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

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

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

//Closes the document

pdfDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}



{% endtabs %}  

## Creating Document Overlays 

Multiple templates can be drawn over a PDF page, to create a document-overlay. The below code illustrates how to overlay the documents.

{% tabs %} 

{% highlight c# %}


//Load the existing documents

PdfLoadedDocument loadedDocument1 = new PdfLoadedDocument(fileName1);

PdfLoadedDocument loadedDocument2 = new PdfLoadedDocument(fileName2);

//Create the new document

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

//Create a template from the first document

PdfPageBase loadedPage = loadedDocument1.Pages[0];

PdfTemplate template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(0, 0), new SizeF(500, 700));

// Create a template from the second document

loadedPage = loadedDocument2.Pages[0];

template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(10, 10), new SizeF(400, 500));

//Save the new document.

document.Save("output.pdf");

//Close the documents

loadedDocument1.Close(true);

loadedDocument2.Close(true);

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing documents

Dim loadedDocument1 As New PdfLoadedDocument(fileName1)

Dim loadedDocument2 As New PdfLoadedDocument(fileName2)

'Create the new document

Dim document As New PdfDocument()

Dim page As PdfPage = document.Pages.Add()

'Create a template from the first document 

Dim loadedPage As PdfPageBase = loadedDocument1.Pages(0)

Dim template As PdfTemplate = loadedPage.CreateTemplate()

'Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, New PointF(0, 0), New SizeF(500, 700))

'Create a template from the first document 

loadedPage = loadedDocument2.Pages(0)

template = loadedPage.CreateTemplate()

'Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, New PointF(10, 10), New SizeF(400, 500))

'Save the new document.

document.Save("output.pdf")

'Close the documents

loadedDocument1.Close(True)

loadedDocument2.Close(True)

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Load the existing documents.

Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Sample1.pdf");

PdfLoadedDocument loadedDocument1 = new PdfLoadedDocument();

await loadedDocument1.OpenAsync(pdfStream);

Stream pdfStream1 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Sample2.pdf");

PdfLoadedDocument loadedDocument2 = new PdfLoadedDocument();

await loadedDocument2.OpenAsync(pdfStream1);

//Create the new document

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

//Create a template from the first document

PdfPageBase loadedPage = loadedDocument1.Pages[0];

PdfTemplate template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(0, 0), new SizeF(500, 700));

// Create a template from the second document

loadedPage = loadedDocument2.Pages[0];

template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(10, 10), new SizeF(400, 500));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the documents

document.Close(true);

loadedDocument1.Close(true);

loadedDocument2.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream1 = new FileStream(fileName1, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument1 = new PdfLoadedDocument(docStream1);

//Load the PDF document

FileStream docStream2 = new FileStream(fileName2, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument2 = new PdfLoadedDocument(docStream2);

//Create the new document

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

//Create a template from the first document

PdfPageBase loadedPage = loadedDocument1.Pages[0];

PdfTemplate template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(0, 0), new SizeF(500, 700));

// Create a template from the second document

loadedPage = loadedDocument2.Pages[0];

template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(10, 10), new SizeF(400, 500));

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the documents

document.Close(true);

loadedDocument1.Close(true);

loadedDocument2.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the existing document

Stream docStream1 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample1.pdf");

PdfLoadedDocument loadedDocument1 = new PdfLoadedDocument(docStream1);

Stream docStream2 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample2.pdf");

PdfLoadedDocument loadedDocument2 = new PdfLoadedDocument(docStream2);

//Create the new document

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

//Create a template from the first document

PdfPageBase loadedPage = loadedDocument1.Pages[0];

PdfTemplate template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(0, 0), new SizeF(500, 700));

// Create a template from the second document

loadedPage = loadedDocument2.Pages[0];

template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(10, 10), new SizeF(400, 500));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the documents

document.Close(true);

loadedDocument1.Close(true);

loadedDocument2.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("output.pdf", "application/pdf", stream);
}

{% endhighlight %}

 {% endtabs %}  

## Adding a PdfPageTemplate in the PDF document

The following code sample shows how to add a PdfPageTemplate from an existing PDF document.

{% tabs %}  

{% highlight c# %}

// Loads an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Get the first page of the document.
PdfPageBase page = loadedDocument.Pages[0];

//Create a page template.
PdfPageTemplate pageTemplate = new PdfPageTemplate(page);

//Sets the PdfPageTemplate name.
pageTemplate.Name = "pageTemplate";

//Sets the PdfPageTemplate is visible.
pageTemplate.IsVisible = true;

//Adds the page template.
loadedDocument.PdfPageTemplates.Add(pageTemplate);

//Save the PDF document.
loadedDocument.Save("output.pdf");

//Close the PDF document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

' Loads an existing PDF document.
Dim loadedDocument As PdfLoadedDocument =  New PdfLoadedDocument("input.pdf") 

'Get the first page of the document.
Dim page As PdfPageBase =  loadedDocument.Pages(0) 

'Create a page template.
Dim pageTemplate As PdfPageTemplate =  New PdfPageTemplate(page) 

'Sets the PdfPageTemplate name.
pageTemplate.Name = "pageTemplate"

'Sets the PdfPageTemplate is visible.
pageTemplate.IsVisible = True

'Adds the page template.
loadedDocument.PdfPageTemplates.Add(pageTemplate)

'Save the PDF document.
loadedDocument.Save("output.pdf")

'Close the PDF document.
loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf"); 

// Loads an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the first page of the document.
PdfPageBase page = loadedDocument.Pages[0];

//Create a page template.
PdfPageTemplate pageTemplate = new PdfPageTemplate(page);

//Sets the PdfPageTemplate name.
pageTemplate.Name = "pageTemplate";

//Sets the PdfPageTemplate is visible.
pageTemplate.IsVisible = true;

//Adds the page template.
loadedDocument.PdfPageTemplates.Add(pageTemplate);

//Save the document.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Close the PDF document.
loadedDocument.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

// Loads an existing PDF document.

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the first page of the document.
PdfPageBase page = loadedDocument.Pages[0];

//Create a page template.
PdfPageTemplate pageTemplate = new PdfPageTemplate(page);

//Sets the PdfPageTemplate name.
pageTemplate.Name = "pageTemplate";

//Sets the PdfPageTemplate is visible.
pageTemplate.IsVisible = true;

//Adds the page template.
loadedDocument.PdfPageTemplates.Add(pageTemplate);

//Creating the stream object.
MemoryStream stream = new MemoryStream();

//Save the document into stream.
loadedDocument.Save(stream);

//If the position is not set to '0,' then the PDF will be empty.
stream.Position = 0;

//Close the document.
loadedDocument.Close(true);

//Defining the ContentType for a PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf"); 

// Loads an existing PDF Document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the first page of the document.
PdfPageBase page = loadedDocument.Pages[0];

//Create a page template.
PdfPageTemplate pageTemplate = new PdfPageTemplate(page);

//Sets the PdfPageTemplate name.
pageTemplate.Name = "pageTemplate";

//Sets the PdfPageTemplate is visible.
pageTemplate.IsVisible = true;

//Adds the page template.
loadedDocument.PdfPageTemplates.Add(pageTemplate);

//Save the document to the stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Close the document.
loadedDocument.Close(true);

stream.Position = 0;

//Save the stream into a PDF file.

//The operation in save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer to the PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  
