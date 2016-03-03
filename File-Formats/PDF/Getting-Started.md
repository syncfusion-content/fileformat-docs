---
title: Getting Started
description: This section explains creating a simple PDF document with basic elements
platform: file-formats
control: PDF
documentation: UG
---
# Getting Started

To create a PDF document from scratch and saving it to disk or stream, the following assemblies have to be added as reference to the project.

<table>
  <tr>
    <th>Assembly Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>Syncfusion.Pdf.Base</td>
    <td>This assembly contains the core feature for creating, manipulating and saving PDF documents.</td>
  </tr>
  <tr>
    <td>Syncfusion.Compression.Base</td>
    <td>This assembly is required for compressing the internal contents of a PDF document.</td>
  </tr>
</table>

Include the following namespaces in your .cs or .vb file as shown below.
{% tabs %}
{% highlight c# %}
using Syncfusion.Pdf;
using Syncfusion.Pdf.Parsing;
using Syncfusion.Pdf.Graphics;
using Syncfusion.Pdf.Grid;
{% endhighlight %}

{% highlight vb.net %}
Imports Syncfusion.Pdf
Imports Syncfusion.Pdf.Parsing
Imports Syncfusion.Pdf.Graphics
Imports Syncfusion.Pdf.Grid
{% endhighlight %}
{% endtabs %}

## Creating a PDF document with simple text

The following code example shows how to create a PDF document with simple text.
{% tabs %}
{% highlight c# %}
//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the standard font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
//Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));
//Save the document.
document.Save("Output.pdf");
//Close the document.
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document.
Dim document As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics
'Set the standard font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)
'Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))
'Save the document.
document.Save("Output.pdf")
'Close the document.
document.Close(True)
{% endhighlight %}
{% endtabs %}

## Creating a PDF document with image

The following code example shows how to create a PDF document with an image.
{% tabs %}
{% highlight c# %}
//Create a new PDF document.
PdfDocument doc = new PdfDocument();
//Add a page to the document.
PdfPage page = doc.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the image from the disk.
PdfBitmap image = new PdfBitmap("Autumn Leaves.jpg");
//Draw the image
graphics.DrawImage(image, 0, 0);
//Save the document.
doc.Save("Output.pdf");
//Close the document.
doc.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document.
Dim doc As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = doc.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Load the image from the disk.
Dim image As New PdfBitmap("Autumn Leaves.jpg")
'Draw the image
graphics.DrawImage(image, 0, 0)
'Save the document.
doc.Save("Output.pdf")
'Close the document.
doc.Close(True)
{% endhighlight %}
{% endtabs %}

## Creating a PDF document with table

The following code example shows how to create a PDF document with a simple table.
{% tabs %}
{% highlight c# %}
//Create a new PDF document.
PdfDocument doc = new PdfDocument();
//Add a page.
PdfPage page = doc.Pages.Add();
//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();
//Create a DataTable.
DataTable dataTable = new DataTable();
//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");
//Add rows to the DataTable.
dataTable.Rows.Add(new object[] { "E01", "Clay" });
dataTable.Rows.Add(new object[] { "E02", "Thomas" });
dataTable.Rows.Add(new object[] { "E03", "Andrew" });
dataTable.Rows.Add(new object[] { "E04", "Paul" });
dataTable.Rows.Add(new object[] { "E05", "Gary" });
//Assign data source.
pdfGrid.DataSource = dataTable;
//Draw grid to the page of PDF document.
pdfGrid.Draw(page, new PointF(10, 10));
//Save the document.
doc.Save("Output.pdf");
//close the document
doc.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document.
Dim doc As New PdfDocument()
'Add a page.
Dim page As PdfPage = doc.Pages.Add()
'Create a PdfGrid.
Dim pdfGrid As New PdfGrid()
'Create a DataTable.
Dim dataTable As New DataTable()
'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")
'Add rows to the DataTable.
dataTable.Rows.Add(New Object() {"E01", "Clay"})
dataTable.Rows.Add(New Object() {"E02", "Thomas"})
dataTable.Rows.Add(New Object() {"E03", "Andrew"})
dataTable.Rows.Add(New Object() {"E04", "Paul"})
dataTable.Rows.Add(New Object() {"E05", "Gary"})
'Assign data source.
pdfGrid.DataSource = dataTable
'Draw grid to the page of PDF document.
pdfGrid.Draw(page, New PointF(10, 10))
'Save the document.
doc.Save("Output.pdf")
'close the document
doc.Close(True)
{% endhighlight %}
{% endtabs %}

## Creating a simple PDF document with basic elements
The PdfDocument object represents an entire PDF document that is being created. The following code example shows how to create a PDF document and add a page to it along with the page settings.

{% tabs %}
{% highlight c# %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds page settings
document.PageSettings.Orientation = PdfPageOrientation.Landscape;
document.PageSettings.Margins.All = 50;
//Adds a page to the document
PdfPage page = document.Pages.Add();
{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document
Dim document As New PdfDocument()
'Adds page settings
document.PageSettings.Orientation = PdfPageOrientation.Landscape
document.PageSettings.Margins.All = 50
'Adds a page to the document
Dim page As PdfPage = document.Pages.Add()


{% endhighlight %}
{% endtabs %}
1. Essential PDF has APIs similar to the .NET GDI plus which helps to draw elements to the PDF page just like 2D drawing in .NET. 
2. Unlike System.Drawing APIs all the units are measured in point instead of pixel. 
3. In PDF, all the elements are placed in absolute positions and has the possibility for content overlapping if misplaced. 
4. Essential PDF provides the rendered bounds for each and every elements added through PdfLayoutResult objects. This can be used to add successive elements and prevent content overlap.

The following code example explains how to add an image from disk to a PDF document, by providing the rectangle coordinates. 

{% tabs %}
{% highlight c# %}

//Loads the image from disk
PdfImage img = PdfImage.FromFile("AdventureCycle.jpg");
//Draws the image to the PDF page
page.Graphics.DrawImage(img, new RectangleF(176, 0, 390, 130));

{% endhighlight %}

{% highlight vb.net %}

'Loads the image from disk 
Dim img As PdfImage = PdfImage.FromFile("AdventureCycle.jpg")
'Draws the image to the PDF page
page.Graphics.DrawImage(img, New RectangleF(176, 0, 390, 130))


{% endhighlight %}
{% endtabs %}

The following methods can be used to add text to a PDF document.

1. DrawString() method of the PdfGraphics
2. PdfTextElement class.

The PdfTextElement provides the layout result of the added text by using the location of the next element that decides to prevent content overlapping. This is not available in the DrawString method. 

The following code example adds the necessary text such as address, invoice number and date to create a basic invoice application. 
{% tabs %}

{% highlight c# %}

PdfBrush solidBrush = new PdfSolidBrush(new PdfColor(126, 151, 173));
RectangleF bounds = new RectangleF(0, result.Bounds.Bottom + 90, graphics.ClientSize.Width, 30);
//Draws a rectangle to place the heading in that region.
graphics.DrawRectangle(solidBrush, bounds);
//Creates a font for adding the heading in the page
PdfFont subHeadingFont = new PdfStandardFont(PdfFontFamily.TimesRoman, 14);
//Creates a text element to add the invoice number
PdfTextElement element = new PdfTextElement("INVOICE " + id.ToString(), subHeadingFont);
element.Brush = PdfBrushes.White;

//Draws the heading on the page
result = element.Draw(page, new PointF(10, result.Bounds.Bottom + 98));
string currentDate = "DATE " + DateTime.Now.ToString("MM/dd/yyyy");
//Measures the width of the text to place it in the correct location
SizeF textSize = subHeadingFont.MeasureString(currentDate);
PointF textPosition = new PointF(graphics.ClientSize.Width - textSize.Width - 10, result.Bounds.Y);
//Draws the date by using DrawString method
graphics.DrawString(currentDate, subHeadingFont, element.Brush, textPosition);
PdfFont timesRoman = new PdfStandardFont(PdfFontFamily.TimesRoman, 10);
//Creates text elements to add the address and draw it to the page.
element = new PdfTextElement("BILL TO ", timesRoman);
element.Brush = new PdfSolidBrush(new PdfColor(126, 155, 203));
result = element.Draw(page, new PointF(10, result.Bounds.Bottom + 25));
PdfPen linePen = new PdfPen(new PdfColor(126, 151, 173), 0.70f);
PointF startPoint = new PointF(0, result.Bounds.Bottom + 3);
PointF endPoint = new PointF(graphics.ClientSize.Width, result.Bounds.Bottom + 3);
//Draws a line at the bottom of the address
graphics.DrawLine(linePen, startPoint, endPoint);

{% endhighlight %}

{% highlight vb.net %}


Dim solidBrush As PdfBrush = New PdfSolidBrush(New PdfColor(126, 151, 173))
Dim bounds As New RectangleF(0, result.Bounds.Bottom + 90, graphics.ClientSize.Width, 30)
'Draws a rectangle to place the heading in that region.
graphics.DrawRectangle(solidBrush, bounds)
'Create a font for adding the heading in the page
Dim subHeadingFont As PdfFont = New PdfStandardFont(PdfFontFamily.TimesRoman, 14)
'Creates a text element to add the invoice number
Dim element As New PdfTextElement("INVOICE " + id.ToString(), subHeadingFont)
element.Brush = PdfBrushes.White

'Draws the heading on the page
result = element.Draw(page, New PointF(10, result.Bounds.Bottom + 98))
Dim currentDate As String = "DATE " + DateTime.Now.ToString("MM/dd/yyyy")
'Measures the width of the text to place it in the correct location
Dim textSize As SizeF = subHeadingFont.MeasureString(currentDate)
Dim textPosition As New PointF(graphics.ClientSize.Width - textSize.Width - 10, result.Bounds.Y)
'Draws the date by using DrawString method
graphics.DrawString(currentDate, subHeadingFont, element.Brush, textPosition)
Dim timesRoman As PdfFont = New PdfStandardFont(PdfFontFamily.TimesRoman, 10)
'Creates text elements to add the address and draw it to the page.
element = New PdfTextElement("BILL TO ", timesRoman)
element.Brush = New PdfSolidBrush(New PdfColor(126, 155, 203))
result = element.Draw(page, New PointF(10, result.Bounds.Bottom + 25))
Dim linePen As New PdfPen(New PdfColor(126, 151, 173), 0.7F)
Dim startPoint As New PointF(0, result.Bounds.Bottom + 3)
Dim endPoint As New PointF(graphics.ClientSize.Width, result.Bounds.Bottom + 3)
'Draws a line at the bottom of the address
graphics.DrawLine(linePen, startPoint, endPoint)



{% endhighlight %}
{% endtabs %}
Essential PDF provides two types of table models. The difference between both the table models can be referred from the link 
[Difference between PdfLightTable and PdfGrid](/file-formats/pdf/working-with-tables#difference-between-pdflighttable-and-pdfgrid "difference-between-pdflighttable-and-pdfgrid")

Since the invoice document requires only simple cell customizations, the given code example explains how to create a simple invoice table by using PdfGrid.

{% tabs %}
{% highlight c# %}


//Creates the datasource for the table
DataTable invoiceDetails = GetProductDetailsAsDataTable();
//Creates a PDF grid
PdfGrid grid = new PdfGrid();
//Adds the data source
grid.DataSource = invoiceDetails;
//Creates the grid cell styles
PdfGridCellStyle cellStyle = new PdfGridCellStyle();
cellStyle.Borders.All = PdfPens.White;
PdfGridRow header = grid.Headers[0];
//Creates the header style
PdfGridCellStyle headerStyle = new PdfGridCellStyle();
headerStyle.Borders.All = new PdfPen(new PdfColor(126, 151, 173));
headerStyle.BackgroundBrush = new PdfSolidBrush(new PdfColor(126, 151, 173));
headerStyle.TextBrush = PdfBrushes.White;
headerStyle.Font = new PdfStandardFont(PdfFontFamily.TimesRoman, 14f, PdfFontStyle.Regular);

//Adds cell customizations
for (int i = 0; i < header.Cells.Count; i++)
{
if (i == 0 || i == 1)
header.Cells[i].StringFormat = new PdfStringFormat(PdfTextAlignment.Left, PdfVerticalAlignment.Middle);
else
header.Cells[i].StringFormat = new PdfStringFormat(PdfTextAlignment.Right, PdfVerticalAlignment.Middle);
}

//Applies the header style
header.ApplyStyle(headerStyle);
cellStyle.Borders.Bottom = new PdfPen(new PdfColor(217, 217, 217), 0.70f);
cellStyle.Font = new PdfStandardFont(PdfFontFamily.TimesRoman, 12f);
cellStyle.TextBrush = new PdfSolidBrush(new PdfColor(131, 130, 136));
//Creates the layout format for grid
PdfGridLayoutFormat layoutFormat = new PdfGridLayoutFormat();
// Creates layout format settings to allow the table pagination
layoutFormat.Layout = PdfLayoutType.Paginate;
//Draws the grid to the PDF page.
PdfGridLayoutResult gridResult = grid.Draw(page, new RectangleF(new PointF(0, result.Bounds.Bottom + 40), new SizeF(g.ClientSize.Width, g.ClientSize.Height - 100)), layoutFormat);

{% endhighlight %}

{% highlight vb.net %}

'Creates the datasource for the table
Dim invoiceDetails As DataTable = GetProductDetails(Integer.Parse(invoiceNumber))
'Create a PDF grid
Dim grid As New PdfGrid()
'Adds the data source
grid.DataSource = invoiceDetails
'creates the grid cell stlyes
Dim cellStyle As New PdfGridCellStyle()
cellStyle.Borders.All = PdfPens.White
Dim header As PdfGridRow = grid.Headers(0)
'Creates the header style
Dim headerStyle As New PdfGridCellStyle()
headerStyle.Borders.All = New PdfPen(New PdfColor(126, 151, 173))
headerStyle.BackgroundBrush = New PdfSolidBrush(New PdfColor(126, 151, 173))
headerStyle.TextBrush = PdfBrushes.White
headerStyle.Font = New PdfStandardFont(PdfFontFamily.TimesRoman, 14.0F, PdfFontStyle.Regular)
'Adds cell customizations
For i As Integer = 0 To header.Cells.Count - 1
If i = 0 OrElse i = 1 Then
header.Cells(i).StringFormat = New PdfStringFormat(PdfTextAlignment.Left, PdfVerticalAlignment.Middle)
Else
header.Cells(i).StringFormat = New PdfStringFormat(PdfTextAlignment.Right, PdfVerticalAlignment.Middle)
End If
Next
'Applies the header style
header.ApplyStyle(headerStyle)
cellStyle.Borders.Bottom = New PdfPen(New PdfColor(217, 217, 217), 0.7F)
cellStyle.Font = New PdfStandardFont(PdfFontFamily.TimesRoman, 12.0F)
cellStyle.TextBrush = New PdfSolidBrush(New PdfColor(131, 130, 136))
'Creates the layout format for grid
Dim layoutFormat As New PdfGridLayoutFormat()
'Layout format settings to allow the table pagination
layoutFormat.Layout = PdfLayoutType.Paginate
'Draws the grid to the PDF page.
Dim gridResult As PdfGridLayoutResult = grid.Draw(page, New RectangleF(New PointF(0, result.Bounds.Bottom + 40), New SizeF(g.ClientSize.Width, g.ClientSize.Height - 100)), layoutFormat)

{% endhighlight %}
{% endtabs %}

The following code example shows how to save the invoice document to disk and dispose the PdfDocument object.

{% tabs %}
{% highlight c# %}

//Saves and closes the document.
document.Save("Sample.pdf");
document.Close(true);


{% endhighlight %}

{% highlight vb.net %}

'Saves and closes the document.
document.Save("Sample.pdf")
document.Close(True)

{% endhighlight %}
{% endtabs %}

The following screenshot shows the invoice PDF document created by using Essential PDF.

![](GettingStarted_images/GettingStarted_img1.jpeg)


## Filling forms

An interactive form, sometimes referred to as an AcroForm is a collection of fields for gathering information interactively from the user. A PDF document can contain any number of fields appearing in any combination of pages, all of that make a single, globally interactive form spanning the entire document.

Essential PDF allows you to create and manipulate existing form in PDF document. To work with existing form documents, the following namespaces are required.

1. Syncfusion.Pdf
2. Syncfusion.Pdf.Parsing

The following guide shows how to fill a sample PDF form as shown.

![](GettingStarted_images/GettingStarted_img2.jpeg)


Essential PDF allows you to fill the form fields by using PdfLoadedField class. You can get the form field either by using its field name or field index.

{% tabs %}
{% highlight c# %}

//Loads the PDF form.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(@"JobApplication.pdf");
//Loads the form
PdfLoadedForm form = loadedDocument.Form;
//Fills the textbox field by using index
(form.Fields[0] as PdfLoadedTextBoxField).Text = "John";
//Fills the textbox fields by using field name
(form.Fields["LastName"] as PdfLoadedTextBoxField).Text = "Doe";
(form.Fields["Address"] as PdfLoadedTextBoxField).Text = " John Doe \n 123 Main St \n Anytown, USA";
//Loads the radion button group
PdfLoadedRadioButtonItemCollection radioButtoncollection = (form.Fields["Gender"] as PdfLoadedRadioButtonListField).Items;
//Checks the 'Male' option
radioButtoncollection[0].Checked = true;
//Checks the 'business' checkbox field
(form.Fields["Business"] as PdfLoadedCheckBoxField).Checked = true;
//Checks the 'retiree' checkbox field
(form.Fields["Retiree"] as PdfLoadedCheckBoxField).Checked = true;
//Saves and closes the document
loadedDocument.Save("filledform.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Loads the PDF form.
Dim loadedDocument As New PdfLoadedDocument("JobApplication.pdf")
'Load the form
Dim form As PdfLoadedForm = loadedDocument.Form
'Fills the textbox field by using index
TryCast(form.Fields(0), PdfLoadedTextBoxField).Text = "John"
'Fills the textbox fields by using field name
TryCast(form.Fields("LastName"), PdfLoadedTextBoxField).Text = "Doe"
TryCast(form.Fields("Address"), PdfLoadedTextBoxField).Text = " John Doe " & vbLf & " 123 Main St " & vbLf & " Anytown, USA"
'Load the radion button group
Dim radioButtoncollection As PdfLoadedRadioButtonItemCollection = TryCast(form.Fields("Gender"), PdfLoadedRadioButtonListField).Items
'Checks the 'Male' option
radioButtoncollection(0).Checked = True
'Checks the 'business' checkbox field
TryCast(form.Fields("Business"), PdfLoadedCheckBoxField).Checked = True
'Checks the 'retiree' checkbox field
TryCast(form.Fields("Retiree"), PdfLoadedCheckBoxField).Checked = True
'Saves and closes the document
loadedDocument.Save("filledform.pdf")
loadedDocument.Close(True)

{% endhighlight %}
{% endtabs %}

The filled form is shown in adobe reader application as follows.

![](GettingStarted_images/GettingStarted_img3.jpeg)

## Converting HTML contents to PDF

Essential PDF supports converting HTML contents to PDF. To add the HTML to PDF conversion functionality by using WebKit rendering engine, the following assemblies need to be added as reference to the project.

<table>
  <tr>
    <th>Assembly Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>Syncfusion.Pdf.Base</td>
    <td>This assembly contains the core feature for creating, manipulating and saving PDF documents.</td>
  </tr>
  <tr>
    <td>Syncfusion.Compression.Base</td>
    <td>This assembly is required for compressing the internal contents of a PDF document.</td>
  </tr>
  <tr>
    <td>Syncfusion.HtmlConverter.Base.dll</td>
    <td>This assembly is required for converting the HTML to PDF</td>
  </tr>
</table>

The QtBinaries available in the WebKitHTMLConverter installed location __**($Systemdrive\Program Files(x86)\Syncfusion\WebKitHTMLConverter\xx.x.x.xx\QtBinaries)**__ should be placed in the local machine where the conversion takes place. The physical path of this folder has been set to the **WebKitPath** property of the **WebKitConverterSettings** class, as shown. By default it will search for WebKit assemblies in bin folder.

{% tabs %}
{% highlight c# %}
//Create a WebKitConverterSettings instance
WebKitConverterSettings webKitSettings = new WebKitConverterSettings();
//Set WebKit path
webKitSettings.WebKitPath = @"/QtBinaries/";
{% endhighlight %}

{% highlight vb.net %}
'Create a WebKitConverterSettings instance
Dim webKitSettings As New WebKitConverterSettings()
'Set WebKit path
webKitSettings.WebKitPath = "/QtBinaries/"
{% endhighlight %}
{% endtabs %}

For converting HTTPS sites, it requires OPENSSL libraries to be installed in the machine. You can install the OPENSSL library by downloading its setup from the following link,

[OpenSSL](http://www.syncfusion.com/downloads/support/directtrac/general/ze/Win32OpenSSL-1_0_1h1593443064 )

WebKit conversion also requires VC++ 2010 redistributable to be installed in the machine. You can use the below mentioned download link,

X86 - [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)

X64 - [https://www.microsoft.com/en-in/download/details.aspx?id=14632](https://www.microsoft.com/en-in/download/details.aspx?id=14632)

To convert website URL or local HTML file to PDF by using WebKit rendering engine, refer to the following code example.

{% tabs %}
{% highlight c# %}
//Create an instance of HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);
//Create a WebKitConverterSettings instance
WebKitConverterSettings webKitSettings = new WebKitConverterSettings();
//Set WebKit path
webKitSettings.WebKitPath = @"/QtBinaries/";
//Assign the WebKit settings to converter
htmlConverter.ConverterSettings = webKitSettings;
//Convert the URL to PDF
PdfDocument document = htmlConverter.Convert("http://www.google.com");
//Save and close the document.
document.Save("Sample.pdf");
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create an instance of HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)
'Create a WebKitConverterSettings instance
Dim webKitSettings As New WebKitConverterSettings()
'Set WebKit path
webKitSettings.WebKitPath = "/QtBinaries/"
'Assign the WebKit settings to converter
htmlConverter.ConverterSettings = webKitSettings
'Convert the URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("http://www.google.com")
'Save and close the document.
document.Save("Sample.pdf")
document.Close(True)
{% endhighlight %}
{% endtabs %}

To convert the HTML string to PDF, use the following code example.
{% tabs %}
{% highlight c# %}
//Create an instance of HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);
//Create a WebKitConverterSettings instance
WebKitConverterSettings webKitSettings = new WebKitConverterSettings();
//Set WebKit path
webKitSettings.WebKitPath = @"/QtBinaries/";
//Assign the WebKit settings to converter
htmlConverter.ConverterSettings = webKitSettings;
//Convert the HTML string to PDF
PdfDocument document = htmlConverter.Convert("<html><head><title></title></head><body><div>Hello World!!!</div></body></html>","");
//Save and close the document.
document.Save("Sample.pdf");
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create an instance of HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)
'Create a WebKitConverterSettings instance
Dim webKitSettings As New WebKitConverterSettings()
'Set WebKit path
webKitSettings.WebKitPath = "/QtBinaries/"
'Assign the WebKit settings to converter
htmlConverter.ConverterSettings = webKitSettings
'Convert the HTML string to PDF
Dim document As PdfDocument = htmlConverter.Convert("<html><head><title></title></head><body><div>Hello World!!!</div></body></html>", "")
'Save and close the document.
document.Save("Sample.pdf")
document.Close(True)
{% endhighlight %}
{% endtabs %}
## Merge PDF Documents

Essential PDF supports merging multiple PDF documents from disk and stream. You can merge the multiple PDF document from disk by specifying the path of the documents in a string array.

Refer to the following code example to merge multiple documents from disk.
{% tabs %}
{% highlight c# %}

//Creates the new PDF document
PdfDocument finalDoc = new PdfDocument();
// Creates a string array of source files to be merged.
string[] source = { "file1.pdf, file2.pdf" };
// Merges PDFDocument.
PdfDocument.Merge(finalDoc, source);
//Saves the final document
finalDoc.Save("Sample.pdf");
//closes the document
finalDoc.Close(true);

{% endhighlight %}



{% highlight vb.net %}

'Creates the new PDF document
Dim finalDoc As New PdfDocument()
' Creates a string array of source files to be merged.
Dim source As String() = {"file1.pdf, file2.pdf"}
' Merges PDFDocument.
PdfDocument.Merge(finalDoc, source)
'Saves the final document
finalDoc.Save("Sample.pdf")
'closes the document
finalDoc.Close(True)

{% endhighlight %}
{% endtabs %}
You can merge the PDF document streams by using the following code example.

{% tabs %}
{% highlight c# %}

//Creates the detination document
PdfDocument finalDoc = new PdfDocument();
Stream stream1 = File.OpenRead("file1.pdf");
Stream stream2 = File.OpenRead("file2.pdf");
// Creates a PDF stream for merging.
Stream[] streams = { stream1, stream2 };
// Merges PDFDocument.
PdfDocumentBase.Merge(finalDoc, streams);
//Saves the document
finalDoc.Save("sample.pdf");
//closes the document
finalDoc.Close(true);

{% endhighlight %}



{% highlight vb.net %}

'creates the detination document
Dim finalDoc As New PdfDocument()
Dim stream1 As Stream = File.OpenRead("file1.pdf")
Dim stream2 As Stream = File.OpenRead("file2.pdf")
' Creates a PDF stream for merging.
Dim streams As Stream() = {stream1, stream2}
' Merges PDFDocument.
PdfDocumentBase.Merge(finalDoc, streams)
'Saves the document
finalDoc.Save("sample.pdf")
'closes the document
finalDoc.Close(True)

{% endhighlight %}

{% endtabs %}