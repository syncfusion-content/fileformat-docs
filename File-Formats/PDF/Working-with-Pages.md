---
title: Working with pages | Syncfusion
description: This section explains how to add, rearrange and remove pages from the PDF document
platform: file-formats
control: PDF
documentation: UG
---
# Working with Pages

## Adding a new page to the document

The following code sample explains you on how to add a [PdfPage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPage.html) in a PDF document. When multiple pages are added, the new page is always added to the end of the document.

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//Save the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

'Draw the text.

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'Save the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(new PdfColor(0, 0, 0));

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//Save the document as stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new Syncfusion.Drawing.PointF(20, 20));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new Syncfusion.Drawing.PointF(20, 20));

//Save the document as stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

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

## Inserting pages in a document

You can insert an empty page at any location in the existing PDF document using [Insert](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedPageCollection.html#Syncfusion_Pdf_Parsing_PdfLoadedPageCollection_Insert_System_Int32_) method. The below code snippet explains the same.

{% tabs %} 

{% highlight c# %}


//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Insert a new page in the beginning of the document

loadedDocument.Pages.Insert(0);

//Save and close the document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Insert a new page in the beginning of the document

loadedDocument.Pages.Insert(0)

'Save and close the document

loadedDocument.Save("Output.pdf")

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

//Insert a new page in the beginning of the document

loadedDocument.Pages.Insert(0);

//Save the document as stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Insert a new page in the beginning of the document

loadedDocument.Pages.Insert(0);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Insert a new page in the beginning of the document

loadedDocument.Pages.Insert(0);

//Save the document as stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

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

## Adding margin to the PDF pages

You can add margin to all the PDF pages of the PDF document using the [PageSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html#Syncfusion_Pdf_PdfDocument_PageSettings) property. The following code snippet illustrates the same.

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set margin for all the pages

document.PageSettings.Margins.All = 10;

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Creates a solid brush.

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//Save and close the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim document As New PdfDocument()

'Set margin for all the pages

document.PageSettings.Margins.All = 10

'Add a page.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

'Draw the text.

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'Save the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set margin for all the pages

document.PageSettings.Margins.All = 10;

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Creates a solid brush.

PdfBrush brush = new PdfSolidBrush(new PdfColor(0, 0, 0));

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//Save the document as stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set margin for all the pages

document.PageSettings.Margins.All = 10;

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Creates a solid brush.

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new Syncfusion.Drawing.PointF(20, 20));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set margin for all the pages

document.PageSettings.Margins.All = 10;

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Creates a solid brush.

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new Syncfusion.Drawing.PointF(20, 20));

//Save the document as stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

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

## Adding sections with different page settings

Essential PDF supports adding sections with different page settings like [Height](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageSettings.html#Syncfusion_Pdf_PdfPageSettings_Height), [Margins](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageSettings.html#Syncfusion_Pdf_PdfPageSettings_Margins), [Orientation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageSettings.html#Syncfusion_Pdf_PdfPageSettings_Orientation), [Rotate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageSettings.html#Syncfusion_Pdf_PdfPageSettings_Rotate), [Size](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageSettings.html#Syncfusion_Pdf_PdfPageSettings_Size), [Transition](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageSettings.html#Syncfusion_Pdf_PdfPageSettings_Transition) and [Width](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageSettings.html#Syncfusion_Pdf_PdfPageSettings_Width). You can add sections to a PDF document by using the [PdfSection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfSection.html) available in [PdfDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html) instance and create page settings to the ``PdfSection`` using the [PageSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfSection.html#Syncfusion_Pdf_PdfSection_PageSettings) property. 

The following code snippet explains how to add more sections to a PDF document with different page settings.

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create a solid brush and standard font
PdfBrush brush = new PdfSolidBrush(Color.Black);
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Section - 1
//Add new section to the document
PdfSection section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle0;
section.PageSettings.Size = PdfPageSize.A5;
section.PageSettings.Width = 300;
section.PageSettings.Height = 400;

//Add page to the section and initialize graphics for the page
PdfPage page = section.Pages.Add();
PdfGraphics graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 0 degrees", font, brush, new PointF(20, 20));

//Section - 2
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;
section.PageSettings.Width = 300;
section.PageSettings.Height = 400;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 90 degrees", font, brush, new PointF(20, 20));

//Section - 3
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle180;
section.PageSettings.Width = 500;
section.PageSettings.Height = 200;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 180 degrees", font, brush, new PointF(20, 20));

//Section - 4
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle270;
section.PageSettings.Width = 300;
section.PageSettings.Height = 200;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 270 degrees", font, brush, new PointF(20, 20));

//Save the document
document.Save("Output.pdf");

//Close the instance of PdfDocument
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Create a solid brush and standard font
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

'Section - 1
'Add new section to the document
Dim section As PdfSection = document.Sections.Add

'Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle0
section.PageSettings.Size = PdfPageSize.A5
section.PageSettings.Width = 300
section.PageSettings.Height = 400

'Add page to the section and initialize graphics for the page
Dim page As PdfPage = section.Pages.Add
Dim graphics As PdfGraphics = page.Graphics

'Draw simple text on the page
graphics.DrawString("Rotated by 0 degrees", font, brush, New PointF(20, 20))

'Section - 2
'Add new section to the document
section = document.Sections.Add

'Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90
section.PageSettings.Width = 300
section.PageSettings.Height = 400

'Add page to the section and initialize graphics for the page
page = section.Pages.Add
graphics = page.Graphics

'Draw simple text on the page
graphics.DrawString("Rotated by 90 degrees", font, brush, New PointF(20, 20))

'Section - 3
'Add new section to the document
section = document.Sections.Add

'Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle180
section.PageSettings.Width = 500
section.PageSettings.Height = 200

'Add page to the section and initialize graphics for the page
page = section.Pages.Add
graphics = page.Graphics

'Draw simple text on the page
graphics.DrawString("Rotated by 180 degrees", font, brush, New PointF(20, 20))

'Section - 4
'Add new section to the document
section = document.Sections.Add

'Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle270
section.PageSettings.Width = 300
section.PageSettings.Height = 200

'Add page to the section and initialize graphics for the page
page = section.Pages.Add
graphics = page.Graphics

'Draw simple text on the page
graphics.DrawString("Rotated by 270 degrees", font, brush, New PointF(20, 20))

'Save the document
document.Save("Output.pdf")

'Close the instance of PdfDocument
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create a solid brush and standard font
PdfBrush brush = new PdfSolidBrush(Color.FromArgb(255, 0, 0, 0));
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Section - 1
//Add new section to the document
PdfSection section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle0;
section.PageSettings.Size = PdfPageSize.A5;
section.PageSettings.Width = 300;
section.PageSettings.Height = 400;

//Add page to the section and initialize graphics for the page
PdfPage page = section.Pages.Add();
PdfGraphics graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 0 degrees", font, brush, new PointF(20, 20));

//Section - 2
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;
section.PageSettings.Width = 300;
section.PageSettings.Height = 400;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 90 degrees", font, brush, new PointF(20, 20));

//Section - 3
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle180;
section.PageSettings.Width = 500;
section.PageSettings.Height = 200;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 180 degrees", font, brush, new PointF(20, 20));

//Section - 4
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle270;
section.PageSettings.Width = 300;
section.PageSettings.Height = 200;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 270 degrees", font, brush, new PointF(20, 20));

//Create memory stream
MemoryStream stream = new MemoryStream();

//Open the document in browser after saving it
document.Save(stream);

//Close the document
document.Close(true);
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create a solid brush and standard font
PdfBrush brush = new PdfSolidBrush(Color.Black);
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Section - 1
//Add new section to the document
PdfSection section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle0;
section.PageSettings.Size = PdfPageSize.A5;
section.PageSettings.Width = 300;
section.PageSettings.Height = 400;

//Add page to the section and initialize graphics for the page
PdfPage page = section.Pages.Add();
PdfGraphics graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 0 degrees", font, brush, new PointF(20, 20));

//Section - 2
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;
section.PageSettings.Width = 300;
section.PageSettings.Height = 400;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 90 degrees", font, brush, new PointF(20, 20));

//Section - 3
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle180;
section.PageSettings.Width = 500;
section.PageSettings.Height = 200;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 180 degrees", font, brush, new PointF(20, 20));

//Section - 4
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle270;
section.PageSettings.Width = 300;
section.PageSettings.Height = 200;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 270 degrees", font, brush, new PointF(20, 20));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create a solid brush and standard font
PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.FromArgb(255, 0, 0, 0));
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Section - 1
//Add new section to the document
PdfSection section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle0;
section.PageSettings.Size = PdfPageSize.A5;
section.PageSettings.Width = 300;
section.PageSettings.Height = 400;

//Add page to the section and initialize graphics for the page
PdfPage page = section.Pages.Add();
PdfGraphics graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 0 degrees", font, brush, new PointF(20, 20));

//Section - 2
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;
section.PageSettings.Width = 300;
section.PageSettings.Height = 400;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 90 degrees", font, brush, new PointF(20, 20));

//Section - 3
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle180;
section.PageSettings.Width = 500;
section.PageSettings.Height = 200;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 180 degrees", font, brush, new PointF(20, 20));

//Section - 4
//Add new section to the document
section = document.Sections.Add();

//Create page settings to the section
section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle270;
section.PageSettings.Width = 300;
section.PageSettings.Height = 200;

//Add page to the section and initialize graphics for the page
page = section.Pages.Add();
graphics = page.Graphics;

//Draw simple text on the page
graphics.DrawString("Rotated by 270 degrees", font, brush, new PointF(20, 20));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
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

## Get number of pages from a PDF document 

You can get page count from the existing PDF document as shown in the following code snippet.

{% tabs %}  

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Get the page count.

int pageCount = loadedDocument.Pages.Count;

//Close the document.   
                     
loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the page count.

Dim pageCount As Integer = loadedDocument.Pages.Count

'Close the document.

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

//Get the page count.

int pageCount = loadedDocument.Pages.Count;

//Close the document.

loadedDocument.Close(true);


{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the page count.

int pageCount = loadedDocument.Pages.Count;

//Close the document.

loadedDocument.Close(true);


{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf ");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the page count.

int pageCount = loadedDocument.Pages.Count;

//Close the document.

loadedDocument.Close(true);


{% endhighlight %}

{% endtabs %}  


## Importing pages from an existing document.

Essential PDF allows you to import a page or import a range of pages from one document to the other. The following code sample illustrates how to import a range of pages from an existing document using [ImportPageRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_ImportPageRange_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_Int32_System_Int32_) method.

{% tabs %}   

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Create a new PDF document.

PdfDocument document = new PdfDocument();

int startIndex = 0;

int endIndex = loadedDocument.Pages.Count - 1;

//Import all the pages to the new PDF document.

document.ImportPageRange(loadedDocument, startIndex, endIndex);

//Save the document.

document.Save("Output.pdf");

//Close both document instances.

loadedDocument.Close(true);

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Create a new PDF document.

Dim document As New PdfDocument()

Dim startIndex As Integer = 0

Dim endIndex As Integer = loadedDocument.Pages.Count - 1

'Import all the pages to the new PDF document.

document.ImportPageRange(loadedDocument, startIndex, endIndex)

'Save the document.

document.Save("Output.pdf")

'Close both document instances.

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

//Create a new PDF document.

PdfDocument document = new PdfDocument();

int startIndex = 0;

int endIndex = loadedDocument.Pages.Count - 1;

//Import all the pages to the new PDF document.

document.ImportPageRange(loadedDocument, startIndex, endIndex);

//Save the document as stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document instances.

loadedDocument.Close(true);

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create a new PDF document.

PdfDocument document = new PdfDocument();

int startIndex = 0;

int endIndex = loadedDocument.Pages.Count - 1;

//Import all the pages to the new PDF document.

document.ImportPageRange(loadedDocument, startIndex, endIndex);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document instances.

document.Close(true);

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}


{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create a new PDF document.

PdfDocument document = new PdfDocument();

int startIndex = 0;

int endIndex = loadedDocument.Pages.Count - 1;

//Import all the pages to the new PDF document.

document.ImportPageRange(loadedDocument, startIndex, endIndex);

//Save the document as stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document instances.

document.Close(true);

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

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

## Importing pages from an existing document without bookmarks.

You can import a page or range of pages from one document to other without bookmarks. Refer to the following code sample. 

N> Performance will be effective only in the large PDF document.

{% tabs %}   

{% highlight c# %}


//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Create the new PDF document

PdfDocument document = new PdfDocument();

int startIndex = 0;

int endIndex = loadedDocument.Pages.Count - 1;

//Import all the pages to the new PDF document without bookmarks

document.ImportPageRange(loadedDocument, startIndex, endIndex,false);

//Save the document

document.Save("Output.pdf");

//Close both document instances

loadedDocument.Close(true);

document.Close(true);

System.Diagnostics.Process.Start("Output.pdf");


{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document

Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Create the new PDF document

Dim document As PdfDocument = New PdfDocument()

Dim startIndex As Integer = 0

Dim endIndex As Integer = loadedDocument.Pages.Count - 1

'Import all the pages to the new PDF document without bookmarks

document.ImportPageRange(loadedDocument, startIndex, endIndex, False)

'Save the document

document.Save("Output.pdf")

'Close both the document instances

loadedDocument.Close(True)

document.Close(True)


{% endhighlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Create the new PDF document

PdfDocument document = new PdfDocument();

int startIndex = 0;

int endIndex = loadedDocument.Pages.Count - 1;

//Import all the pages to the new PDF document

document.ImportPageRange(loadedDocument, startIndex, endIndex, false);

//Save the document as stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document instances

loadedDocument.Close(true);

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the new PDF document

PdfDocument document = new PdfDocument();

int startIndex = 0;

int endIndex = loadedDocument.Pages.Count - 1;

//Import all the pages to the new PDF document

document.ImportPageRange(loadedDocument, startIndex, endIndex, false);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0', then the PDF will be empty

stream.Position = 0;

//Close the document instances

document.Close(true);

loadedDocument.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}


{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the new PDF document

PdfDocument document = new PdfDocument();

int startIndex = 0;

int endIndex = loadedDocument.Pages.Count - 1;

//Import all the pages to the new PDF document

document.ImportPageRange(loadedDocument, startIndex, endIndex, false);

//Save the document as stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document instances

document.Close(true);

loadedDocument.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

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

## Rearranging pages in an existing document

You can rearrange the pages in an existing PDF document using [ReArrange](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedPageCollection.html#Syncfusion_Pdf_Parsing_PdfLoadedPageCollection_ReArrange_System_Int32___) method. This method uses zero based start index. The following code snippet illustrates the same.

{% tabs %}  

{% highlight c# %}


//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Rearrange the page by index

loadedDocument.Pages.ReArrange(new int[] {1, 0});

//Save and close the document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Rearrange the page by index

loadedDocument.Pages.ReArrange(New Integer() {1, 0})

'Save and close the document

loadedDocument.Save("Output.pdf")

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

//Rearrange the page by index

loadedDocument.Pages.ReArrange(new int[] { 1, 0 });

//Save the document as stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Rearrange the page by index

loadedDocument.Pages.ReArrange(new int[] { 1, 0 });

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Rearrange the page by index

loadedDocument.Pages.ReArrange(new int[] { 1, 0 });

//Save the document as stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);
            
//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

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


## Changing the page numbers in a PDF document

You can alter the page label for the existing PDF document using [PdfPageLabel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageLabel.html) class. Refer to the following code snippet. 

{% tabs %}  

{% highlight c# %}

//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Create a page label

PdfPageLabel pageLabel = new PdfPageLabel();

//Set the number style with upper case roman letters

pageLabel.NumberStyle = PdfNumberStyle.UpperRoman;

//Set the staring number as 1

pageLabel.StartNumber = 1;

loadedDocument.LoadedPageLabel = pageLabel;

//Save the document

loadedDocument.Save("Output.pdf");

//Close the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load the PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Create a page label

Dim pageLabel As New PdfPageLabel()

'Set the number style with upper case roman letters

pageLabel.NumberStyle = PdfNumberStyle.UpperRoman

'Set the staring number as 1

pageLabel.StartNumber = 1

loadedDocument.LoadedPageLabel = pageLabel

'Save the document

loadedDocument.Save("Output.pdf")

'Close the document

loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose a file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of the PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

// Create a page label

PdfPageLabel pageLabel = new PdfPageLabel();

//Set the number style with upper case roman letters

pageLabel.NumberStyle = PdfNumberStyle.UpperRoman;

//Set the staring number as 1

pageLabel.StartNumber = 1;

loadedDocument.LoadedPageLabel = pageLabel;

//Save the document as stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document instances

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

// Create a page label

PdfPageLabel pageLabel = new PdfPageLabel();

//Set the number style with upper case roman letters

pageLabel.NumberStyle = PdfNumberStyle.UpperRoman;

//Set the staring number as 1

pageLabel.StartNumber = 1;

loadedDocument.LoadedPageLabel = pageLabel;

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

loadedDocument.Save(stream);

//If the position is not set to '0', then the PDF will be empty.

stream.Position = 0;

//Close the document

loadedDocument.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

// Create a page label

PdfPageLabel pageLabel = new PdfPageLabel();

//Set the number style with upper case roman letters

pageLabel.NumberStyle = PdfNumberStyle.UpperRoman;

//Set the staring number as 1

pageLabel.StartNumber = 1;

loadedDocument.LoadedPageLabel = pageLabel;

//Save the document as stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document instances

loadedDocument.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

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


## Removing pages from a document

You can remove the pages from the existing PDF document using [RemoveAt](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedPageCollection.html#Syncfusion_Pdf_Parsing_PdfLoadedPageCollection_RemoveAt_System_Int32_) method as shown in the below code snippet. 

{% tabs %}  

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");



//Remove the first page in the PDF document

loadedDocument.Pages.RemoveAt(0);

//Save the document.

loadedDocument.Save("Output.pdf");

//Close the document.            
loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Remove the first page in the PDF document

loadedDocument.Pages.RemoveAt(0)

'Save the document.

loadedDocument.Save("Output.pdf")

'Close the document.

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

//Remove the first page in the PDF document

loadedDocument.Pages.RemoveAt(0);

//Save the document as stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

 //Load the PDF document.

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Remove the first page in the PDF document

loadedDocument.Pages.RemoveAt(0);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Remove the first page in the PDF document

loadedDocument.Pages.RemoveAt(0);

//Save the document as stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);
            
//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

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

## Rotating a PDF page

You can rotate a particular PDF page in the PDF document using [PdfPageRotateAngle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageRotateAngle.html) Enum as shown the following code snippet. 

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section.

PdfSection section = document.Sections.Add();

//Rotate a section/page

section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draws the text.

graphics.DrawString("Rotated by 90 degree", font, brush, new PointF(20, 20));

//Save the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim document As New PdfDocument()

'Add a section.

Dim section As PdfSection = document.Sections.Add()

'Rotate a section/page

section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90

Dim page As PdfPage = section.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

'Draw the text.

graphics.DrawString("Rotated by 90 degree", font, brush, New PointF(20, 20))

'Save the document.

document.Save("Output.pdf")

document.Close(True)





{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section.

PdfSection section = document.Sections.Add();

//Rotate a section/page

section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(new PdfColor(0, 0, 0));

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draws the text.

graphics.DrawString("Rotated by 90 degree", font, brush, new PointF(20, 20));

//Save the document as stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section.

PdfSection section = document.Sections.Add();

//Rotate a section/page

section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draws the text.

graphics.DrawString("Rotated by 90 degree", font, brush, new Syncfusion.Drawing.PointF(20, 20));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section.

PdfSection section = document.Sections.Add();

//Rotate a section/page

section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draws the text.

graphics.DrawString("Rotated by 90 degree", font, brush, new Syncfusion.Drawing.PointF(20, 20));

//Save the document as stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);
            
//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

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

## Rotating an existing PDF page

You can also rotate a PDF page in the existing PDF document using PdfPageRotateAngle(https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageRotateAngle.html) as shown in the following code snippet.

{% tabs %}  

{% highlight c# %}

//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Gets the page.

PdfPageBase loadedPage = loadedDocument.Pages[0] as PdfPageBase;
 
//Set the rotation for loaded page.

loadedPage.Rotation = PdfPageRotateAngle.RotateAngle90;
             
// Save the Document

loadedDocument.Save("Output.pdf");

// Close the Document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load the PDF document. 

Dim loadedDocument As New PdfLoadedDocument("input.pdf")

'Gets the page.

Dim page As PdfPageBase = TryCast(loadedDocument.Pages(0), PdfPageBase)

'Set the rotation for loaded page.

page.Rotation = PdfPageRotateAngle.RotateAngle90

'Save the document. 

loadedDocument.Save("Output.pdf")

'Closes the document.

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

//Gets the page

PdfPageBase loadedPage = loadedDocument.Pages[0] as PdfPageBase;

//Set the rotation for loaded page.

loadedPage.Rotation = PdfPageRotateAngle.RotateAngle90;

//Save the document as stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document. 

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples. 

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Gets the page

PdfPageBase loadedPage = loadedDocument.Pages[0] as PdfPageBase;

//Set the rotation for loaded page.

loadedPage.Rotation = PdfPageRotateAngle.RotateAngle90;            

//Save the document into stream 

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty. 

stream.Position = 0;

//Close the document 

loadedDocument.Close(true);

//Defining the ContentType for pdf file. 

string contentType = "application/pdf";

//Define the file name. 

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name. 

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf ");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream); 

//Gets the page

PdfPageBase loadedPage = loadedDocument.Pages[0] as PdfPageBase;

//Set the rotation for loaded page.

loadedPage.Rotation = PdfPageRotateAngle.RotateAngle90;

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

loadedDocument.Save(memoryStream);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

## Detect empty pages from a PDF document

You can find the empty pages from the PDF document using the[Isblank](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html#Syncfusion_Pdf_PdfPageBase_Isblank) property as shown in the following code sample.  

{% tabs %}  

{% highlight c# %}

//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Gets the page.

PdfPageBase loadedPage = loadedDocument.Pages[0] as PdfPageBase;

//Get the page is blank or not

bool isEmpty = loadedPage.Isblank;

// Save the Document

loadedDocument.Save("Output.pdf");

// Close the Document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load the PDF document.

 Dim loadedDocument As New PdfLoadedDocument("input.pdf")
 
'Gets the page.

 Dim page As PdfPageBase = TryCast(loadedDocument.Pages(0), PdfPageBase)
 
'Get the page is blank or not.

 bool isEmpty = loadedPage.Isblank
 
 'Save the document.
 
loadedDocument.Save("Output.pdf")
 
'Closes the document.

 loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create the file open picker 

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file 

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document using the Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Gets the page

PdfPageBase loadedPage = loadedDocument.Pages[0] as PdfPageBase;

//get the page is blank or not.

bool isEmpty = loadedPage.Isblank;

//Save the document as a stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document. 

loadedDocument.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respected code samples. 

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Gets the page

PdfPageBase loadedPage = loadedDocument.Pages[0] as PdfPageBase;

//get the page is blank or not.

bool isEmpty = loadedPage.Isblank;

//Save the document into a stream 

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty. 

stream.Position = 0;

//Close the document 

loadedDocument.Close(true);

//Defining the ContentType for pdf file. 

string contentType = "application/pdf";

//Define the file name. 

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name. 

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as a stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf ");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream); 

//Gets the page

PdfPageBase loadedPage = loadedDocument.Pages[0] as PdfPageBase;

//Get the page is blank or not.

bool isEmpty = loadedPage.Isblank;

//Save the document into a stream

MemoryStream memoryStream = new MemoryStream();

loadedDocument.Save(memoryStream);

//Save the stream into a PDF file

//The operation saves under the Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer to the PDF or Xamarin section for the respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

## Splitting a PDF file to individual pages

Essential PDF allows to split the pages of an existing PDF document into multiple individual PDF documents using [Split](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_Split_System_String_) method of [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class. The following code snippet explains the same.

{% tabs %}  

{% highlight c# %}


//Load document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("OutputE.pdf");

//Sets pattern.

const string destinationFilePattern = "Output" + "{0}.pdf";

//Split the pages into separate documents.

loadedDocument.Split(destinationFilePattern);

//close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load document.

Dim loadedDocument As New PdfLoadedDocument("OutputE.pdf")

'Sets pattern.

Const destinationFilePattern As String = "Output" + "{0}.pdf"

'Split the pages into separate documents.

loadedDocument.Split(destinationFilePattern)

'close the document

loadedDocument.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Due to platform limitations, Essential PDF supports splitting a PDF file into individual pages only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. However this can be achieved by using the following code snippet. 

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

for (int i = 0; i < loadedDocument.PageCount; i++)
{

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the loaded document page index to the current document

document.ImportPage(loadedDocument, i);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output" +i +".pdf");

}


{% endhighlight %}

{% highlight ASP.NET Core %}

//Due to platform limitations, Essential PDF supports splitting a PDF file into individual pages only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. However this can be achieved by using the following code snippet. 

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

for (int i=0;i<loadedDocument.PageCount;i++)
{

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the pages from the loaded document

document.ImportPage(loadedDocument, i);

//Create a memory stream 

MemoryStream stream = new MemoryStream();

//Save the document to stream

document.Save(stream);

stream.Position = 0;

//Close the document

document.Close(true);

//Create a file stream

FileStream fileStream = new FileStream("Output" + i + ".pdf", FileMode.Create, FileAccess.Write);

byte[] bytes = stream.ToArray();

//Write bytes to file

fileStream.Write(bytes, 0, (int)bytes.Length);

//Dispose the streams

stream.Dispose();

fileStream.Dispose();

}

{% endhighlight %}

{% highlight Xamarin %}

//Due to platform limitations, Essential PDF supports splitting a PDF file into individual pages only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. However this can be achieved by using the following code snippet. 

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

for (int i = 0; i < loadedDocument.Pages.Count; i++)
{

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the pages from the loaded document

document.ImportPage(loadedDocument, i);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output"+ i+ ".pdf", "application/pdf", stream;
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output" + i + ".pdf", "application/pdf", stream);
}
}


{% endhighlight %}

{% endtabs %}  
