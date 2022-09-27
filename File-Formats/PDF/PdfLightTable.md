---
title: Working with Tables using PdfLightTable | Syncfusion
description: Learn how to create a table to PDF, apply cell & built-in table styles, automatic pagination, customize the rows and columns, and more using the PdfLightTable.  
platform: File-formats
control: PDF
documentation: UG
---

# Working with .NET PDF Tables using PdfLightTable model

The Syncfusion .NET PDF library supports creating PDF tables or grids. The PDF table displays data from data sources or directly binding data in a tabular format. Here, you will see the creation of a PDF table using the Table** model.  

## Creating a simple table 

The Syncfusion .NET PDF library allows you to create the table with [DataSource](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html#Syncfusion_Pdf_Tables_PdfLightTable_DataSource) from DataSet, DataTable, arrays and IEnumerable objects using [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) class. It allows you to perform simple formatting. 

N> In Silverlight, Windows store apps and Xamarin only strongly typed IEnumerable objects are supported.

### Create a simple table from a data source 

The following code sample illustrates how to create a simple table from a data source.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Initialize DataTable to assign as DateSource to the light table.
DataTable table = new DataTable();

//Include columns in the DataTable.
table.Columns.Add("Name");
table.Columns.Add("Age");
table.Columns.Add("Sex");

//Include rows to the DataTable.
table.Rows.Add(new string[] { "abc", "21", "Male" });

//Assign data source.
pdfLightTable.DataSource = table;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, new PointF(0, 0));

//Save the document.
doc.Save("Output.pdf");

//Close the document.
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Initialize DataTable to assign as DateSource to the light table.
Dim table As New DataTable()

'Include columns to the DataTable.
table.Columns.Add("Name")
table.Columns.Add("Age")
table.Columns.Add("Sex")

'Include rows to the DataTable.
table.Rows.Add(New String() {"abc", "21", "Male"})

'Assign data source.
pdfLightTable.DataSource = table

'Draw the PdfLightTable.
pdfLightTable.Draw(page, New PointF(0, 0))

'Save the document.
doc.Save("Output.pdf")

'Close the document.
doc.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to the IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, new PointF(0, 0));

//Save the PDF document to the stream.
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to the IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Draw PdfLightTable.
pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(0, 0));

//Create the stream object.
MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.
doc.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Define the ContentType for PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to the IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(0, 0));

//Save the PDF document to the stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into a PDF file.
//The operation in the Save under Xamarin varies between the Windows Phone, Android, and iOS platforms. Please refer to the PDF or Xamarin section for the respective code samples.

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Create-simple-table-from-data-source).

### Create a simple table directly without setting any data source 

Directly add rows and columns instead of a data source, by setting the [DataSourceType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html#Syncfusion_Pdf_Tables_PdfLightTable_DataSourceType) property to **TableDirect** of [PdfLightTableDataSourceType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableDataSourceType.html) Enum. 

The following code illustrates how to add the data directly into the [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html). 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Acquire the page's graphics.
PdfGraphics graphics = page.Graphics;

//Declare a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the Data source as direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the document.
doc.Save("Output.pdf");

//Close the document.
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Acquire page's graphics.
Dim graphics As PdfGraphics = page.Graphics

'Declare a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Set the Data source type as direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.
pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))
pdfLightTable.Columns.Add(New PdfColumn("Name"))
pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add rows.
pdfLightTable.Rows.Add(New Object() {"111", "Maxim", "III"})

'Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty)

'Save the document.
doc.Save("Output.pdf")

'Close the document.
doc.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Acquire the page's graphics.
PdfGraphics graphics = page.Graphics;

//Declare a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the Data source as direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into the stream
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Acquire page's graphics.
PdfGraphics graphics = page.Graphics;

//Declare a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the Data source as direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object
MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.
doc.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Define the ContentType for PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Acquire page's graphics.
PdfGraphics graphics = page.Graphics;

//Declare a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the Data source as direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into a PDF file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer PDF or Xamarin section for respective code samples.

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Add-the-data-directly-into-the-PDF-table).

### Creating a simple table in an existing PDF document 

Create a table using the [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) in the existing PDF document by using the following code sample. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load a PDF document.
PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");

//Get the first page from document.
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;
            
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
            
// Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

// Initialize DataTable to assign as DateSource to the light table.
DataTable table = new DataTable();

//Include columns in the DataTable.
table.Columns.Add("Name");
table.Columns.Add("Age");
table.Columns.Add("Sex");

//Include rows to the DataTable.
table.Rows.Add(new string[] { "abc", "21", "Male" });

//Assign data source.
pdfLightTable.DataSource = table;

//Draw PdfLightTable.
pdfLightTable.Draw(graphics, new PointF(0, 0));

//Save the document.
doc.Save("Output.pdf");

//Close the document.
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load a PDF document.
Dim doc As New PdfLoadedDocument("input.pdf")

'Get the first page from document.
Dim page As PdfLoadedPage = TryCast(doc.Pages(0), PdfLoadedPage)

'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics

'Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Initialize DataTable to assign as DateSource to the light table.
Dim table As New DataTable()

'Include columns to the DataTable.
table.Columns.Add("Name")
table.Columns.Add("Age")
table.Columns.Add("Sex")

'Include rows to the DataTable.
table.Rows.Add(New String() {"abc", "21", "Male"})

'Assign data source.
pdfLightTable.DataSource = table

'Draw PdfLightTable.
pdfLightTable.Draw(graphics, New PointF(0, 0))

'Save the document.
doc.Save("Output.pdf")

'Close the document.
doc.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create the open file picker.
var picker = new FileOpenPicker();
picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file.
StorageFile file = await picker.PickSingleFileAsync();

//Create an empty PDF loaded document instance.
PdfLoadedDocument doc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through the Open method of PdfLoadedDocument class.
await doc.OpenAsync(file);

//Get the first page from document.
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Draw PdfLightTable.
pdfLightTable.Draw(graphics, new PointF(0, 0));

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Get stream from an existing PDF document. 
FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document. 
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

//Get the first page from the document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Draw PdfLightTable.
pdfLightTable.Draw(graphics, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object.
MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.
doc.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Define the ContentType for PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

 //Get stream from an existing PDF document. 
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the PDF document. 
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

//Get the first page from document.
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Draw PdfLightTable.
pdfLightTable.Draw(graphics, new Syncfusion.Drawing.PointF(0, 0));

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into a PDF file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer PDF or Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Creating-the-table-in-an-existing-PDF-document).

## Support for cell customization 

[PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) allows users to customize cell font, background, border, etc. using [PdfCellStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfCellStyle.html).

The following code sample illustrates how to customize the cell properties in ``PdfLightTable``.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add Rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Create the font for setting the style.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Declare and define the alternate style.
PdfCellStyle altStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Green);
altStyle.BackgroundBrush = PdfBrushes.DarkGray;

//Declare and define the header style.
PdfCellStyle headerStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown);
headerStyle.BackgroundBrush = PdfBrushes.Red;

//Set the alternate style and header style to table. 
pdfLightTable.Style.AlternateStyle = altStyle;
pdfLightTable.Style.HeaderStyle = headerStyle;

//Show header in the table.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the document.
doc.Save("Output.pdf");

//Close the document.
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.
pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))
pdfLightTable.Columns.Add(New PdfColumn("Name"))
pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add Rows.
pdfLightTable.Rows.Add(New Object() {"111", "Maxim", "III"})
pdfLightTable.Rows.Add(New Object() {"112", "Minim", "III"})

'Create the font for setting the style.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

'Declare and define the alternate style.
Dim altStyle As New PdfCellStyle(font, PdfBrushes.White, PdfPens.Green)
altStyle.BackgroundBrush = PdfBrushes.DarkGray

'Declare and define the header style.
Dim headerStyle As New PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown)
headerStyle.BackgroundBrush = PdfBrushes.Red

'Set the alternate and header style to table. 
pdfLightTable.Style.AlternateStyle = altStyle
pdfLightTable.Style.HeaderStyle = headerStyle

'Show the header in the table.
pdfLightTable.Style.ShowHeader = True

'Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty)

'Save the document.
doc.Save("Output.pdf")

'Close the document.
doc.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add Rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Create the font for setting the style.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Declare and define the alternate style.
PdfCellStyle altStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Green);
altStyle.BackgroundBrush = PdfBrushes.DarkGray;

//Declare and define the header style.
PdfCellStyle headerStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown);
headerStyle.BackgroundBrush = PdfBrushes.Red;

//Set the alternate and header style to table. 
pdfLightTable.Style.AlternateStyle = altStyle;
pdfLightTable.Style.HeaderStyle = headerStyle;

//Show header in the table.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add Rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Create the font for setting the style.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Declare and define the alternate style.
PdfCellStyle altStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Green);
altStyle.BackgroundBrush = PdfBrushes.DarkGray;

//Declare and define the header style.
PdfCellStyle headerStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown);
headerStyle.BackgroundBrush = PdfBrushes.Red;

//Set the alternate and header style to table. 
pdfLightTable.Style.AlternateStyle = altStyle;
pdfLightTable.Style.HeaderStyle = headerStyle;

//Show header in the table.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object.
MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.
doc.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Define the ContentType for PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add Rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Create the font for setting the style.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Declare and define the alternate style.
PdfCellStyle altStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Green);
altStyle.BackgroundBrush = PdfBrushes.DarkGray;

//Declare and define the header style.
PdfCellStyle headerStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown);
headerStyle.BackgroundBrush = PdfBrushes.Red;

//Set the alternate and header style to table. 
pdfLightTable.Style.AlternateStyle = altStyle;
pdfLightTable.Style.HeaderStyle = headerStyle;

//Show header in the table.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into a PDF file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer PDF or Xamarin section for respective code samples.

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Customize-the-table-cell-in-PDF-document).

### Draw graphics elements in a particular cell 

You can set different styles for particular cell using [BeginCellLayout](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) and [EndCellLayout](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) events in [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) class. 

The following code example illustrates how to draw the graphics elements in the particular cell using these event handlers. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Subscribe to events.
pdfLightTable.BeginCellLayout += pdfLightTable_BeginCellLayout;
pdfLightTable.EndCellLayout+=pdfLightTable_EndCellLayout;

//Show the header.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the document.
doc.Save("Output.pdf");

//Close the document.
doc.Close(true);

private void pdfLightTable_EndCellLayout(object sender, EndCellLayoutEventArgs args)
{
if(args.RowIndex==0 &&args.CellIndex==0)
{
args.Graphics.DrawImage(new PdfBitmap(imageFileName), args.Bounds);
}
}

private void pdfLightTable_BeginCellLayout(object sender, BeginCellLayoutEventArgs args)
{
if (args.RowIndex == 0 && args.CellIndex == 1)
{
args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds);
}
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Declare a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.
pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))
pdfLightTable.Columns.Add(New PdfColumn("Name"))
pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add rows.
pdfLightTable.Rows.Add(New Object() {"111", "Maxim", "III"})
pdfLightTable.Rows.Add(New Object() {"112", "Minim", "III"})

'Subscribe to events.
AddHandler pdfLightTable.BeginCellLayout, AddressOf pdfLightTable_BeginCellLayout
AddHandler pdfLightTable.EndCellLayout, AddressOf pdfLightTable_EndCellLayout

'Show the header.
pdfLightTable.Style.ShowHeader = True

'Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty)

'Save the document.
doc.Save("Output.pdf")

'Close the document.
doc.Close(True)

Private Sub pdfLightTable_EndCellLayout(ByVal sender As Object, ByVal args As EndCellLayoutEventArgs)

If args.RowIndex = 0 AndAlso args.CellIndex = 0 Then

args.Graphics.DrawImage(New PdfBitmap(imageFileName), args.Bounds)

End If

End Sub

Private Sub pdfLightTable_BeginCellLayout(ByVal sender As Object, ByVal args As BeginCellLayoutEventArgs)

If args.RowIndex = 0 AndAlso args.CellIndex = 1 Then

args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds)

End If

End Sub

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Subscribe to events.
pdfLightTable.BeginCellLayout += pdfLightTable_BeginCellLayout;
pdfLightTable.EndCellLayout += pdfLightTable_EndCellLayout;

//Show the header.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

private void pdfLightTable_EndCellLayout(object sender, EndCellLayoutEventArgs args)
{
    if (args.RowIndex == 0 && args.CellIndex == 0)
    {
        //Load the PDF document as a stream.
        Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Image.jpg");

        args.Graphics.DrawImage(new PdfBitmap(imageStream), args.Bounds);
    }
}

private void pdfLightTable_BeginCellLayout(object sender, BeginCellLayoutEventArgs args)
{
    if (args.RowIndex == 0 && args.CellIndex == 1)
    {
        args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds);
    }
}


{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Subscribe to events.
pdfLightTable.BeginCellLayout += pdfLightTable_BeginCellLayout;
pdfLightTable.EndCellLayout += pdfLightTable_EndCellLayout;

//Show the header.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object.
MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.
doc.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Define the ContentType for PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

private void pdfLightTable_EndCellLayout(object sender, EndCellLayoutEventArgs args)
{
    if (args.RowIndex == 0 && args.CellIndex == 0)
    {
        //Load the image as a stream.
        FileStream imageStream = new FileStream("Image.jpg", FileMode.Open, FileAccess.Read);

        args.Graphics.DrawImage(new PdfBitmap(imageStream), args.Bounds);
    }
}

private void pdfLightTable_BeginCellLayout(object sender, BeginCellLayoutEventArgs args)
{
    if (args.RowIndex == 0 && args.CellIndex == 1)
    {
        args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds);
    }
}


{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Subscribe to events.
pdfLightTable.BeginCellLayout += pdfLightTable_BeginCellLayout;
pdfLightTable.EndCellLayout += pdfLightTable_EndCellLayout;

//Show the header.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into a PDF file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer PDF or Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

private void pdfLightTable_EndCellLayout(object sender, EndCellLayoutEventArgs args)
{
    if (args.RowIndex == 0 && args.CellIndex == 0)
    {
        //Load the image as a stream.

        Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Image.jpg");

        args.Graphics.DrawImage(new PdfBitmap(imageStream), args.Bounds);
    }
}

private void pdfLightTable_BeginCellLayout(object sender, BeginCellLayoutEventArgs args)
{
    if (args.RowIndex == 0 && args.CellIndex == 1)
    {
        args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds);
    }
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Draw-graphics-element-in-particular-cell).

## Support for rows and columns customization 

### Row customization 

[PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) doesn't provide direct support for row customization. However, this can be done through the event handlers. The following code sample illustrates how to customize the row in ``PdfLightTable`` using [BeginRowLayout](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html#Syncfusion_Pdf_Tables_PdfLightTable_BeginRowLayout) and [EndRowLayout](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html#Syncfusion_Pdf_Tables_PdfLightTable_EndRowLayout) event handlers.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });
pdfLightTable.Rows.Add(new object[] { "113", "john", "III" });
pdfLightTable.Rows.Add(new object[] { "114", "peter", "III" });

//Subscribe to events.
pdfLightTable.BeginRowLayout+=pdfLightTable_BeginRowLayout;
pdfLightTable.EndRowLayout+=pdfLightTable_EndRowLayout;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the document.
doc.Save("Output.pdf");

//Close the document.
doc.Close(true);

private void pdfLightTable_EndRowLayout(object sender, EndRowLayoutEventArgs args)
{
//Customize the rows when the row layout ends.
if (args.RowIndex == 3)
args.Cancel = true;
}

private void pdfLightTable_BeginRowLayout(object sender, BeginRowLayoutEventArgs args)
{
//Apply column span.
if(args.RowIndex==1)
{
PdfLightTable table = (PdfLightTable)sender;
int count = table.Columns.Count;
int[] spanMap = new int[count];

//Set just spanned cells. Negative values are not allowed.
spanMap[0] = 2;
spanMap[1] = 3;
args.ColumnSpanMap = spanMap;
}
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.
pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))
pdfLightTable.Columns.Add(New PdfColumn("Name"))
pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add rows.
pdfLightTable.Rows.Add(New Object() { "111", "Maxim", "III" })
pdfLightTable.Rows.Add(New Object() { "112", "Minim", "III" })
pdfLightTable.Rows.Add(New Object() { "113", "john", "III" })
pdfLightTable.Rows.Add(New Object() { "114", "peter", "III" })

'Subscribe to events.
AddHandler pdfLightTable.BeginRowLayout, AddressOf pdfLightTable_BeginRowLayout
AddHandler pdfLightTable.EndRowLayout, AddressOf pdfLightTable_EndRowLayout

'Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty)

'Save the document.
doc.Save("Output.pdf")

'Close the document.
doc.Close(True)

Private Sub pdfLightTable_EndRowLayout(ByVal sender As Object, ByVal args As EndRowLayoutEventArgs)

'Customize the rows when the row layout ends.

If args.RowIndex = 3 Then
args.Cancel = True
End If

End Sub

Private Sub pdfLightTable_BeginRowLayout(ByVal sender As Object, ByVal args As BeginRowLayoutEventArgs)

'Apply column span.

If args.RowIndex=1 Then

Dim table As PdfLightTable = CType(sender, PdfLightTable)

Dim count As Integer = table.Columns.Count

Dim spanMap(count - 1) As Integer

' Set just spanned cells. Negative values are not allowed.

spanMap(0) = 2

spanMap(1) = 3

args.ColumnSpanMap = spanMap

End If

End Sub

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });
pdfLightTable.Rows.Add(new object[] { "113", "john", "III" });
pdfLightTable.Rows.Add(new object[] { "114", "peter", "III" });

//Subscribe to events.
pdfLightTable.BeginRowLayout += pdfLightTable_BeginRowLayout;
pdfLightTable.EndRowLayout += pdfLightTable_EndRowLayout;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF OR UWP section for the respective code samples.
Save(stream, "Output.pdf");

private void pdfLightTable_EndRowLayout(object sender, EndRowLayoutEventArgs args)
{

   //Customize the rows when the row layout ends.
    if (args.RowIndex == 3)
    args.Cancel = true;
}

private void pdfLightTable_BeginRowLayout(object sender, BeginRowLayoutEventArgs args)
{
    //Apply column span.
    if (args.RowIndex == 1)
    {
        PdfLightTable table = (PdfLightTable)sender;
        int count = table.Columns.Count;
        int[] spanMap = new int[count];

        //Set just spanned cells. Negative values are not allowed.
        spanMap[0] = 2;
        spanMap[1] = 3;
        args.ColumnSpanMap = spanMap;
    }
}

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });
pdfLightTable.Rows.Add(new object[] { "113", "john", "III" });
pdfLightTable.Rows.Add(new object[] { "114", "peter", "III" });

//Subscribe to events.
pdfLightTable.BeginRowLayout += pdfLightTable_BeginRowLayout;
pdfLightTable.EndRowLayout += pdfLightTable_EndRowLayout;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Create the stream object.
MemoryStream stream = new MemoryStream();

//Save the PDF document to the stream.
doc.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Define the ContentType for a PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

private void pdfLightTable_EndRowLayout(object sender, EndRowLayoutEventArgs args)
{

    //Customize the rows when the row layout ends.
    if (args.RowIndex == 3)
    args.Cancel = true;

}

private void pdfLightTable_BeginRowLayout(object sender, BeginRowLayoutEventArgs args)
{
    //Apply the column span.
    if (args.RowIndex == 1)
    {
        PdfLightTable table = (PdfLightTable)sender;
        int count = table.Columns.Count;
        int[] spanMap = new int[count];

        //Set just spanned cells. Negative values are not allowed.
        spanMap[0] = 2;
        spanMap[1] = 3;
        args.ColumnSpanMap = spanMap;
    }
}


{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });
pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });
pdfLightTable.Rows.Add(new object[] { "113", "john", "III" });
pdfLightTable.Rows.Add(new object[] { "114", "peter", "III" });

//Subscribe to events.
pdfLightTable.BeginRowLayout += pdfLightTable_BeginRowLayout;
pdfLightTable.EndRowLayout += pdfLightTable_EndRowLayout;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into a PDF file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer PDF or Xamarin section for respective code samples.

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Row-customization-of-the-table-in-PDF-document).

### Column customization 

The following code sample illustrates how to customize the column in [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) using the [PdfStringFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStringFormat.html) class. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Acquire the page's graphics.
PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "john", "III" });

//Specify the column name.
pdfLightTable.Columns[1].ColumnName = "Student Name";

//Create and customize the string formats.
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Bottom;

//Apply the string format.
pdfLightTable.Columns[0].StringFormat = format;

//Style to display header.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the document.
doc.Save("Output.pdf");

//Close the document.
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Acquire page's graphics.
Dim graphics As PdfGraphics = page.Graphics

'Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.
pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))
pdfLightTable.Columns.Add(New PdfColumn("Name"))
pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add rows.
pdfLightTable.Rows.Add(New Object() { "111", "john", "III" })

'Specify the column name.
pdfLightTable.Columns(1).ColumnName = "Student Name"

'Create and customize the string format.
Dim format As New PdfStringFormat()
format.Alignment = PdfTextAlignment.Center
format.LineAlignment = PdfVerticalAlignment.Bottom

'Apply the string format.
pdfLightTable.Columns(0).StringFormat = format

'Style to display the header.
pdfLightTable.Style.ShowHeader = True

'Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty)

'Save the document.
doc.Save("Output.pdf")

'Close the document.
doc.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Acquire the page's graphics.
PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "john", "III" });

//Specify the column name.
pdfLightTable.Columns[1].ColumnName = "Student Name";

//Create and customize the string formats.
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Bottom;

//Apply the string format.
pdfLightTable.Columns[0].StringFormat = format;

//Style to display the header.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page
PdfPage page = doc.Pages.Add();

//Acquire the page's graphics.
PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "john", "III" });

//Specify the column name.
pdfLightTable.Columns[1].ColumnName = "Student Name";

//Create and customize the string formats.
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Bottom;

//Apply the string format.
pdfLightTable.Columns[0].StringFormat = format;

//Style to display the header.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object.
MemoryStream stream = new MemoryStream();

//Save the PDF document to the stream.
doc.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Define the ContentType for PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Acquire page's graphics.
PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));
pdfLightTable.Columns.Add(new PdfColumn("Name"));
pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.
pdfLightTable.Rows.Add(new object[] { "111", "john", "III" });

//Specify the column name.
pdfLightTable.Columns[1].ColumnName = "Student Name";

//Create and customize the string formats.
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Bottom;

//Apply the string format.
pdfLightTable.Columns[0].StringFormat = format;

//Style to display header.
pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into the stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into a PDF file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer PDF or Xamarin section for respective code samples.

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Column-customization-of-the-table-in-PDF-document).

## Table customization 

The Syncfusion .NET PDF library supports users to create a customizable PDF table like [CellSpacing](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html#Syncfusion_Pdf_Tables_PdfLightTableStyle_CellSpacing), [CellPadding](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html#Syncfusion_Pdf_Tables_PdfLightTableStyle_CellPadding), [RepeatHeader](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html#Syncfusion_Pdf_Tables_PdfLightTableStyle_RepeatHeader), [ShowHeader](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html#Syncfusion_Pdf_Tables_PdfLightTableStyle_ShowHeader), etc. This can be achieved by using the [PdfLightTableStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html) class. 

The following code sample illustrates how to customize the table using [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html).

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Initialize DataTable to assign as DateSource to the light table.
DataTable table = new DataTable();

//Include columns in the DataTable.
table.Columns.Add("Name");
table.Columns.Add("Age");
table.Columns.Add("Sex");

//Include rows to the DataTable.
table.Rows.Add(new string[] { "abc", "21", "Male" });

//Assign data source.
pdfLightTable.DataSource = table;

//Declare and define light table style.
PdfLightTableStyle lightTableStyle = new PdfLightTableStyle();

//Set cell padding, which specifies the space between the border and content of the cell.
lightTableStyle.CellPadding = 2;

//Set cell spacing, which specifies the space between the adjacent cells.
lightTableStyle.CellSpacing = 2;

//Sets to show header in the table.
lightTableStyle.ShowHeader = true;

//Sets to repeat the header on each page.
lightTableStyle.RepeatHeader = true;

//Apply the style.
pdfLightTable.Style = lightTableStyle;

//Draw PdfLightTable.
pdfLightTable.Draw(page, new PointF(0, 0));

//Save the document.
document.Save("Output.pdf");

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()

'Add a page.
Dim page As PdfPage = document.Pages.Add()

'Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Initialize DataTable to assign as DateSource to the light table.
Dim table As New DataTable()

'Include columns to the DataTable.
table.Columns.Add("Name")
table.Columns.Add("Age")
table.Columns.Add("Sex")

'Include rows to the DataTable.
table.Rows.Add(New String() {"abc", "21", "Male"})

'Assign data source.
pdfLightTable.DataSource = table

'Declare and define light table style.
Dim lightTableStyle As New PdfLightTableStyle()

'Set cell padding, which specifies the space between the border and content of the cell.
lightTableStyle.CellPadding = 2

'Set cell spacing, which specifies the space between the adjacent cells.
lightTableStyle.CellSpacing = 2

'Sets to show header in the table.
lightTableStyle.ShowHeader = True

'Sets to repeat the header on each page.
lightTableStyle.RepeatHeader = True

'Apply the style.
pdfLightTable.Style = lightTableStyle

'Draw PdfLightTable.
pdfLightTable.Draw(page, New PointF(0, 0))

'Save the document.
document.Save("Output.pdf")

'Close the document.
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Declare and define light table style.
PdfLightTableStyle lightTableStyle = new PdfLightTableStyle();

//Set cell padding, which specifies the space between the border and content of the cell.
lightTableStyle.CellPadding = 2;

//Set cell spacing, which specifies the space between the adjacent cells.
lightTableStyle.CellSpacing = 2;

//Sets to show header in the table.
lightTableStyle.ShowHeader = true;

//Sets to repeat the header on each page.
lightTableStyle.RepeatHeader = true;

//Apply style.
pdfLightTable.Style = lightTableStyle;

//Draw PdfLightTable.
pdfLightTable.Draw(page, new PointF(0, 0));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);

//Close the document.
document.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Declare and define light table style.
PdfLightTableStyle lightTableStyle = new PdfLightTableStyle();

//Set cell padding, which specifies the space between the border and content of the cell.
lightTableStyle.CellPadding = 2;

//Set cell spacing, which specifies the space between the adjacent cells.
lightTableStyle.CellSpacing = 2;

//Sets to show header in the table.
lightTableStyle.ShowHeader = true;

//Sets to repeat the header on each page.
lightTableStyle.RepeatHeader = true;

//Apply style.
pdfLightTable.Style = lightTableStyle;

//Draw PdfLightTable.
pdfLightTable.Draw(page, new PointF(0, 0));

//Creating the stream object.
MemoryStream stream = new MemoryStream();

//Save the document as a stream.
document.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
document.Close(true);

//Define the ContentType for a PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Declare and define light table style.
PdfLightTableStyle lightTableStyle = new PdfLightTableStyle();	

//Set cell padding, which specifies the space between the border and content of the cell.
lightTableStyle.CellPadding = 2;

//Set cell spacing, which specifies the space between the adjacent cells.
lightTableStyle.CellSpacing = 2;

//Set to show header in the table.
lightTableStyle.ShowHeader = true;

//Set the repeat header on each page.
lightTableStyle.RepeatHeader = true;

//Apply style.
pdfLightTable.Style = lightTableStyle;

//Draw PdfLightTable.
pdfLightTable.Draw(page, new PointF(0, 0));

//Save the document as a stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document instances.
document.Close(true);

//Save the stream into a PDF file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF or Xamarin section for the respective code samples.

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Customize-the-table-in-a-PDF-document).

## Built-in table styles 

In-built table styles can be applied to [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html), and the appearance is made similar to Microsoft Word’s built-in table styles. You can also apply in-built table styles with the following additional table style options.

* Banded columns
* Banded rows
* First column
* Last column
* Header row
* Last row

The following code example illustrates how to apply built-in table style using [ApplyBuiltinStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html#Syncfusion_Pdf_Tables_PdfLightTable_ApplyBuiltinStyle_Syncfusion_Pdf_PdfLightTableBuiltinStyle_) method of the ``PdfLightTable`` with styles from [PdfLightTableBuiltinStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfLightTableBuiltinStyle.html) Enum.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Create a DataTable.
DataTable dataTable = new DataTable();

//Add columns to the DataTable.
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");

//Add rows to the DataTable.
dataTable.Rows.Add(new object[] { "E01", "Clay" });
dataTable.Rows.Add(new object[] { "E02", "Thomas" });
dataTable.Rows.Add(new object[] { "E03", "George" });
dataTable.Rows.Add(new object[] { "E04", "Stefan" });
dataTable.Rows.Add(new object[] { "E05", "Mathew" });

//Assign data source.
pdfLightTable.DataSource = dataTable;

//Apply built-in table style.
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2);

//Draw the grid to the page of PDF document.
pdfLightTable.Draw(page, new PointF(10, 10));

//Save the document.
doc.Save("Output.pdf");

//Close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Create a DataTable.
Dim dataTable As New DataTable()

'Add columns to the DataTable.
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")

'Add rows to the DataTable.
dataTable.Rows.Add(New Object() {"E01", "Clay"})
dataTable.Rows.Add(New Object() {"E02", "Thomas"})
dataTable.Rows.Add(New Object() {"E03", "George"})
dataTable.Rows.Add(new object() { "E04", "Stefan"})
dataTable.Rows.Add(new object() { "E05", "Mathew"})

'Assign data source.
pdfLightTable.DataSource = dataTable

'Apply built-in table style.
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2)

'Draw grid to the page of PDF document.
pdfLightTable.Draw(page, New PointF(10, 10))

'Save the document.
doc.Save("Output.pdf")

'Close the document
doc.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable.
IEnumerable<object> dataTable = data;

//Assign data source.
pdfLightTable.DataSource = dataTable;

//Apply built-in table style.
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2);

//Draw the grid to the page of PDF document.
pdfLightTable.Draw(page, new PointF(10, 10));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable.
IEnumerable<object> dataTable = data;

//Assign data source.
pdfLightTable.DataSource = dataTable;

//Apply built-in table style.
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2);

//Draw the grid to the page of a PDF document.
pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Creating the stream object.
MemoryStream stream = new MemoryStream();

//Save the document as a stream.
doc.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Define the ContentType for PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable.
IEnumerable<object> dataTable = data;

//Assign data source.
pdfLightTable.DataSource = dataTable;

//Apply built-in table style.
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2);

//Draw the grid to the page of PDF document.
pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into a PDF file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer PDF or Xamarin section for respective code samples.

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Create-table-with-built-in-style).

The following image shows the PDF document with ```PdfGridBuiltinStyle.Gridtable4Accent2```.
![Gridtable4Accent2 image](Table_images/Gridtable4Accent2.png)

## Pagination 

The Syncfusion .NET PDF library provides support to paginate the [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) using [PdfLightTableLayoutFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableLayoutFormat.html) class. 

The following sample illustrates how to allow the ``PdfLightTable`` to flow across pages. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Initialize DataTable to assign as Date Source to the light table.
DataTable table = new DataTable();

//Include columns in the Data Table.
table.Columns.Add("Name");
table.Columns.Add("Age");
table.Columns.Add("Sex");

//Include rows to the Data Table.
//Add multiple rows.
table.Rows.Add(new string[] { "abc", "21", "Male" });

//Assign data source.
pdfLightTable.DataSource = table;

//Set properties to paginate the table.
PdfLightTableLayoutFormat layoutFormat = new PdfLightTableLayoutFormat();
layoutFormat.Break = PdfLayoutBreakType.FitPage;
layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw PdfLightTable.
pdfLightTable.Draw(page, new PointF(0, 0), layoutFormat);

//Save the document.
document.Save("Output.pdf");

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()

'Add a page.
Dim page As PdfPage = document.Pages.Add()

'Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

'Initialize DataTable to assign as Date Source to the light table.
Dim table As New DataTable()

'Include columns to the Data Table.
table.Columns.Add("Name")
table.Columns.Add("Age")
table.Columns.Add("Sex")

'Include rows to the Data Table.//you can add multiple rows.
table.Rows.Add(New String() {"abc", "21", "Male"})

'Assign data source.
pdfLightTable.DataSource = table

'Set properties to paginate the table.
Dim layoutFormat As New PdfLightTableLayoutFormat()
layoutFormat.Break = PdfLayoutBreakType.FitPage
layoutFormat.Layout = PdfLayoutType.Paginate

'Draw PdfLightTable.
pdfLightTable.Draw(page, New PointF(0, 0), layoutFormat)

'Save the document.
document.Save("Output.pdf")

'Close the document.
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();

//You can add multiple rows.
Object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Set properties to paginate the table.
PdfLightTableLayoutFormat layoutFormat = new PdfLightTableLayoutFormat();
layoutFormat.Break = PdfLayoutBreakType.FitPage;
layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw PdfLightTable.
pdfLightTable.Draw(page, new PointF(0, 0), layoutFormat);

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);

//Close the document.
document.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();

//You can add multiple rows.
Object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Set properties to paginate the table.
PdfLightTableLayoutFormat layoutFormat = new PdfLightTableLayoutFormat();
layoutFormat.Break = PdfLayoutBreakType.FitPage;
layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw PdfLightTable.
pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(0, 0), layoutFormat);

//Creating the stream object.
MemoryStream stream = new MemoryStream();

//Save the document as a stream.
document.Save(stream);

//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;

//Close the document.
document.Close(true);

//Define the ContentType for a PDF file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to the list.
List<object> data = new List<object>();

//Add multiple rows.
Object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to the IEnumerable.
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Set properties to paginate the table.
PdfLightTableLayoutFormat layoutFormat = new PdfLightTableLayoutFormat();
layoutFormat.Break = PdfLayoutBreakType.FitPage;
layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw the PdfLightTable.
pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(0, 0), layoutFormat);

//Save the PDF document to the stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document.
document.Close(true);

//Save the stream into a PDF file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer PDF or Xamarin section for respective code samples.

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Paginate-table-in-a-PDF-document).

## String formatting 

The Syncfusion .NET PDF library supports applying string formatting for a whole table, a column in the table, a row in a table, and a cell in a table using the [PdfStringFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStringFormat.html) class. 

### String formatting for whole table in PdfLightTable

The following code sample explains how to add string formatting for the whole table in [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html).

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add page to the document.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows.
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Enable the ShowHeader.
lightTable.Style.ShowHeader = true;

//Create and customize the string formats.
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for the whole table.
for (int i = 0; i < lightTable.Columns.Count; i++)
{
    lightTable.Columns[i].StringFormat = stringFormat;
}

//Draw the PdfLightTable on page.
lightTable.Draw(page, new PointF(10, 10));

//Save the document and close the instance of PdfDocument.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As PdfDocument = New PdfDocument

'Add page to the document.
Dim page As PdfPage = document.Pages.Add

'Create a PdfLightTable.
Dim lightTable As PdfLightTable = New PdfLightTable

'Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.
lightTable.Columns.Add(New PdfColumn("ID"))
lightTable.Columns.Add(New PdfColumn("Name"))
lightTable.Columns.Add(New PdfColumn("Salary"))

'Add rows.
lightTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
lightTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
lightTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Enable the ShowHeader.
lightTable.Style.ShowHeader = True

'Create and customize the string formats.
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle
stringFormat.CharacterSpacing = 2.0F

'Apply string formatting for the whole table.
Dim i As Integer = 0
For i = 0 To lightTable.Columns.Count - 1 Step 1
    lightTable.Columns(i).StringFormat = stringFormat
Next

'Draw the PdfLightTable on the page.
lightTable.Draw(page, New PointF(10, 10))

'Save the document and close the instance of PdfDocument.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add page to the document.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows.
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Enable ShowHeader.
lightTable.Style.ShowHeader = true;

//Create and customize the string formats.
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for the whole table.
for (int i = 0; i < lightTable.Columns.Count; i++)
{
    lightTable.Columns[i].StringFormat = stringFormat;
}

//Draw the PdfLightTable on page.
lightTable.Draw(page, new PointF(10, 10));

//Create a memory stream.
MemoryStream ms = new MemoryStream();

//Open the document in the browser after saving it.
document.Save(ms);

//Close the document.
document.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(ms, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add page to the document.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows.
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Enable the ShowHeader.
lightTable.Style.ShowHeader = true;

//Create and customize the string formats.
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for the whole table.
for (int i = 0; i < lightTable.Columns.Count; i++)
{
    lightTable.Columns[i].StringFormat = stringFormat;
}

//Draw the PdfLightTable on the page.
lightTable.Draw(page, new PointF(10, 10));

//Save a PDF to the MemoryStream.
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0.'
stream.Position = 0;

//Download a PDF document in the browser.
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows.
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Enable the ShowHeader.
lightTable.Style.ShowHeader = true;

//Create and customize the string formats.
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for the whole table.
for (int i = 0; i < lightTable.Columns.Count; i++)
{
    lightTable.Columns[i].StringFormat = stringFormat;
}

//Draw the PdfLightTable on the page.
lightTable.Draw(page, new PointF(10, 10));

//Save the document to the stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document.
document.Close(true);

//Save the stream into a PDF file.
//The operation in the Save under Xamarin varies between the Windows Phone, Android, and iOS platforms. Refer to the PDF or Xamarin section for the respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Add-string-formatting-for-whole-table-in-a-PDF).

### String formatting to a column in PdfGrid

The following code sample explains how to add string formatting to a column in the [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html).

The following code sample explains how to add string formatting to a column in the [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html).

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows.
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//create and customize the string formats.
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Enable the ShowHeader.
lightTable.Style.ShowHeader = true;

//Apply string format to a column.
lightTable.Columns[1].StringFormat = stringFormat;

//Draw the PdfLightTable on the page.
lightTable.Draw(page, new PointF(10, 10));

//Save the document and close the instance of the PdfDocument.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As PdfDocument = New PdfDocument

'Add a page to the document.
Dim page As PdfPage = document.Pages.Add

'Create a PdfLightTable.
Dim lightTable As PdfLightTable = New PdfLightTable

'Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.
lightTable.Columns.Add(New PdfColumn("ID"))
lightTable.Columns.Add(New PdfColumn("Name"))
lightTable.Columns.Add(New PdfColumn("Salary"))

'Add rows.
lightTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
lightTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
lightTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Create and customize the string formats.
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle
stringFormat.CharacterSpacing = 2.0F

'Enable the ShowHeader.
lightTable.Style.ShowHeader = True

'Apply string format to a column.
lightTable.Columns(1).StringFormat = stringFormat

'Draw the PdfLightTable on the page.
lightTable.Draw(page, New PointF(10, 10))

'Save the document and close the instance of the PdfDocument.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add page to the document.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows.
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//create and customize the string formats.
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Enable the ShowHeader.
lightTable.Style.ShowHeader = true;

//Apply string format to a column.
lightTable.Columns[1].StringFormat = stringFormat;

//Draw the PdfLightTable on the page.
lightTable.Draw(page, new PointF(10, 10));

//Create a memory stream.
MemoryStream ms = new MemoryStream();

//Open the document in the browser after saving it.
document.Save(ms);

//Close the document.
document.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(ms, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add page to the document.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows.
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//create and customize the string formats.
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Enable the ShowHeader.
lightTable.Style.ShowHeader = true;

//Apply string format to a column.
lightTable.Columns[1].StringFormat = stringFormat;

//Draw the PdfLightTable on the page.
lightTable.Draw(page, new PointF(10, 10));

//Save the PDF to the MemoryStream.
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0.'
stream.Position = 0;

//Download the PDF document in the browser.
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add page to the document.
PdfPage page = document.Pages.Add();

//Create a PdfLightTable.
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct.
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows.
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//create and customize the string formats.
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Enable the ShowHeader.
lightTable.Style.ShowHeader = true;

//Apply string format to a column.
lightTable.Columns[1].StringFormat = stringFormat;

//Draw the PdfLightTable on the page.
lightTable.Draw(page, new PointF(10, 10));

//Save the document to the stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document.
document.Close(true);

//Save the stream into a PDF file.
//The operation in the Save under Xamarin varies between the Windows Phone, Android, and iOS platforms. Refer to the PDF or Xamarin section for the respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Table/PdfLightTable/Add-string-formatting-to-a-column-in-table).

