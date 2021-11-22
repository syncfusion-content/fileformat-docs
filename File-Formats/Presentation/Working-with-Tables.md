---
title: Create, edit and format table in PowerPoint slide | Syncfusion |
description: Code examples to create, edit and format PowerPoint tables in .NET, C#, web, ASP.NET, UWP, MVC, Xamarin and .NET Core
platform: file-formats
control: Syncfusion PowerPoint presentation
documentation: 
keywords: PowerPoint, slide, table, format-table, rows, columns, pptx
---
# Working with PowerPoint Tables

A [table](https://www.syncfusion.com/powerpoint-framework/net/powerpoint-library/powerpoint-tables) in PowerPoint presentation is used to arrange document content in rows and columns. `ITable` instance represents a table in PowerPoint presentation. A table must contain at least one row.

N> Adding more than 75 rows/columns not supported in the PowerPoint presentation using Microsoft PowerPoint application. It shows alert when you attempt to insert a table with more than 75 rows/columns, which is one of the behaviors of Microsoft PowerPoint and Essential Presentation does the same.

## Create a table by adding rows

Essential Presentation supports creating and editing tables in PowerPoint slides by adding rows. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells
int rowIndex = 0, colIndex;

//Iterate row-wise cells and add text to it
foreach (IRow rows in table.Rows)
{
	colIndex = 0;
	
	foreach (ICell cell in rows.Cells)	
	{
	
		cell.TextBody.AddParagraph("(" + rowIndex.ToString() + " , " + colIndex.ToString() + ")");
		
		colIndex++;
		
	}
	
	rowIndex++;

}

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Create a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()

'Add slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

'Add a table to the slide
Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Initialize index values to add text to table cells
Dim rowIndex As Integer = 0, colIndex As Integer

'Iterate row-wise cells and add text to it
For Each rows As IRow In table.Rows
	colIndex = 0
	
	For Each cell As ICell In rows.Cells
	
		cell.TextBody.AddParagraph("(" + rowIndex.ToString() + " , " + colIndex.ToString() + ")")
		
		colIndex += 1
		
	Next
	
	rowIndex += 1
	
Next

'Save the presentation
pptxDoc.Save("Sample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells
int rowIndex = 0, colIndex;

//Iterate row-wise cells and add text to it

foreach (IRow rows in table.Rows)
{
	colIndex = 0;	
	foreach (ICell cell in rows.Cells)	
	{	
		cell.TextBody.AddParagraph("(" + rowIndex.ToString() + " , " + colIndex.ToString() + ")");
		colIndex++;
	}
	rowIndex++;
}

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells
int rowIndex = 0, colIndex;

//Iterate row-wise cells and add text to it
foreach (IRow rows in table.Rows)
{
	colIndex = 0;
	
	foreach (ICell cell in rows.Cells)	
	{
	
		cell.TextBody.AddParagraph("(" + rowIndex.ToString() + " , " + colIndex.ToString() + ")");
		
		colIndex++;
		
	}
	
	rowIndex++;

}

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells
int rowIndex = 0, colIndex;

//Iterate row-wise cells and add text to it
foreach (IRow rows in table.Rows)
{
	colIndex = 0;
	
	foreach (ICell cell in rows.Cells)	
	{
	
		cell.TextBody.AddParagraph("(" + rowIndex.ToString() + " , " + colIndex.ToString() + ")");
		
		colIndex++;
		
	}
	
	rowIndex++;

}

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Create a table by adding columns

The following code example demonstrates how to create a simple table in a PowerPoint slide by adding columns.

{% tabs %}
{% highlight c# %}

//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells
int row = 0, col;

//Iterate row-wise cells and add text to it
foreach (IColumn columns in table.Columns)
{
	col = 0;
	
	foreach (ICell cell in columns.Cells)
	{
	
		cell.TextBody.AddParagraph("(" + row.ToString() + " , " + col.ToString() + ")");
		
		col++;
		
	}
	
	row++;
}

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()

'Add slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

'Add a table to the slide
Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Initialize index values to add text to the table cells
Dim row As Integer = 0, col As Integer

'Iterate row-wise cells and add text to it
For Each columns As IColumn In table.Columns
	col = 0
	
	For Each cell As ICell In columns.Cells
	
		cell.TextBody.AddParagraph("(" + row.ToString() + " , " + col.ToString() + ")")
		
		col += 1
		
	Next
	
	row += 1
	
Next

'Save the presentation
pptxDoc.Save("Sample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells
int row = 0, col;

//Iterate row-wise cells and add text to it

foreach (IColumn columns in table.Columns)
{
	col = 0;	
	foreach (ICell cell in columns.Cells)
	{	
		cell.TextBody.AddParagraph("(" + row.ToString() + " , " + col.ToString() + ")");		
		col++;		
	}	
	row++;
}

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight ASP.NET CORE %}

//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells
int row = 0, col;

//Iterate row-wise cells and add text to it
foreach (IColumn columns in table.Columns)
{
	col = 0;
	
	foreach (ICell cell in columns.Cells)
	{
	
		cell.TextBody.AddParagraph("(" + row.ToString() + " , " + col.ToString() + ")");
		
		col++;
		
	}
	
	row++;
}

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight XAMARIN %}

//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells
int row = 0, col;

//Iterate row-wise cells and add text to it
foreach (IColumn columns in table.Columns)
{
	col = 0;
	
	foreach (ICell cell in columns.Cells)
	{
	
		cell.TextBody.AddParagraph("(" + row.ToString() + " , " + col.ToString() + ")");
		
		col++;
		
	}
	
	row++;
}

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Append a new row at the end of table

You can append new rows at the end of an existing PowerPoint table. Refer to the following code sample.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new row at the end of table
IRow row = table.Rows.Add();

//Iterate row-wise cells and add text to it
foreach (ICell cell in row.Cells)
{
    cell.TextBody.AddParagraph(table.Rows.IndexOf(row).ToString());
	
}

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get a table in the slide
Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Add a new row at the end of table
Dim row As IRow = table.Rows.Add()

'Iterate row-wise cells and add text to it
For Each cell As ICell In row.Cells

	cell.TextBody.AddParagraph(table.Rows.IndexOf(row).ToString())
	
Next

'Save the presentation
pptxDoc.Save("Sample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new row at the end of table
IRow row = table.Rows.Add();

//Iterate row-wise cells and add text to it

foreach (ICell cell in row.Cells)
{
    cell.TextBody.AddParagraph(table.Rows.IndexOf(row).ToString());	
}

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new row at the end of table
IRow row = table.Rows.Add();

//Iterate row-wise cells and add text to it
foreach (ICell cell in row.Cells)
{
    cell.TextBody.AddParagraph(table.Rows.IndexOf(row).ToString());

}

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Table.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new row at the end of table
IRow row = table.Rows.Add();

//Iterate row-wise cells and add text to it
foreach (ICell cell in row.Cells)
{
	cell.TextBody.AddParagraph(table.Rows.IndexOf(row).ToString());

}

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Copy an existing row to the end of table

You can copy an existing row to the end of a table. Refer to the following code example.

{% tabs %}

{% highlight c# %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the first row to the end of table
table.Rows.Add(table.Rows[0].Clone());

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get the table in the slide
Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Copy the first row to the end of table
table.Rows.Add(table.Rows(0).Clone())

'Save the presentation
pptxDoc.Save("Sample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the first row to the end of table
table.Rows.Add(table.Rows[0].Clone());

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the first row to the end of table
table.Rows.Add(table.Rows[0].Clone());

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Table.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the first row to the end of table
table.Rows.Add(table.Rows[0].Clone());

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Insert a row in table

You can insert a row at the specified index position of a table. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a row at the specified index. Here, the existing first row at index 0 is copied and inserted at row index 1
table.Rows.Insert(1, table.Rows[0].Clone());

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get a table in the slide
Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Insert a row at the specified index. Here, the existing first row at index 0 is copied and inserted at row index 1.
table.Rows.Insert(1, table.Rows(0).Clone())

'Save the presentation
pptxDoc.Save("Sample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a row at the specified index. Here, the existing first row at index 0 is copied and inserted at row index 1
table.Rows.Insert(1, table.Rows[0].Clone());

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a row at the specified index. Here, the existing first row at index 0 is copied and inserted at row index 1
table.Rows.Insert(1, table.Rows[0].Clone());

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Table.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a row at the specified index. Here, the existing first row at index 0 is copied and inserted at row index 1
table.Rows.Insert(1, table.Rows[0].Clone());

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Append a new column at the end table

You can append new column to a table. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new column at the end of table
IColumn column = table.Columns.Add();

//Iterate row-wise cells and add text to it
foreach (ICell cell in column.Cells)
{
    cell.TextBody.AddParagraph(table.Columns.IndexOf(column).ToString());
}

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get a table in the slide
Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Add or append a new column at the end of table
Dim column As IColumn = table.Columns.Add()

'Iterate row-wise cells and add text to it
For Each cell As ICell In column.Cells

	cell.TextBody.AddParagraph(table.Columns.IndexOf(column).ToString())

Next

'Save the presentation
pptxDoc.Save("Sample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new column at the end of table
IColumn column = table.Columns.Add();

//Iterate row-wise cells and add text to it
foreach (ICell cell in column.Cells)
{
    cell.TextBody.AddParagraph(table.Columns.IndexOf(column).ToString());
}

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new column at the end of table
IColumn column = table.Columns.Add();

//Iterate row-wise cells and add text to it
foreach (ICell cell in column.Cells)
{
    cell.TextBody.AddParagraph(table.Columns.IndexOf(column).ToString());
}

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Table.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new column at the end of table
IColumn column = table.Columns.Add();

//Iterate row-wise cells and add text to it
foreach (ICell cell in column.Cells)
{
    cell.TextBody.AddParagraph(table.Columns.IndexOf(column).ToString());
}

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Copy an existing column to the end of table

You can copy an existing column and append it to the end of table. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table from the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the column and append it to the end of table
table.Columns.Add(table.Columns[0].Clone());

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get a table from the slide
Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Copy the column and append it to the end of table
table.Columns.Add(table.Columns(0).Clone())

'Save the presentation
pptxDoc.Save("Sample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get a table from the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the column and append it to the end of table
table.Columns.Add(table.Columns[0].Clone());

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the column and append it to the end of table
table.Columns.Add(table.Columns[0].Clone());

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Table.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the column and append it to the end of table
table.Columns.Add(table.Columns[0].Clone());

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Insert a column to a table

You can insert a column at the specified index position of a table. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get the table from the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a column at the specified index. Here, the existing first column at index 0 is copied and inserted at column index 1
table.Columns.Insert(1, table.Columns[0].Clone());

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get the table from the slide
Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Insert a column at the specified index. Here, the existing first column at index 0 is copied and inserted at column index 1.
table.Columns.Insert(1, table.Columns(0).Clone())

'Save the presentation
pptxDoc.Save("Sample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get the table from the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a column at the specified index. Here, the existing first column at index 0 is copied and inserted at column index 1
table.Columns.Insert(1, table.Columns[0].Clone());

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a column at the specified index. Here, the existing first column at index 0 is copied and inserted at column index 1
table.Columns.Insert(1, table.Columns[0].Clone());

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Table.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a column at the specified index. Here, the existing first column at index 0 is copied and inserted at column index 1
table.Columns.Insert(1, table.Columns[0].Clone());

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Get the actual height of the table

The table height expands with the content added to it. The Essential Presentation library allows you to get this actual height or rendered height of the table. This property is a calculated value based on the content added to the table cells.

The following code example demonstrates how to get the actual height of a PowerPoint table.

{% tabs %}

{% highlight c# %}

//Opens existing PowerPoint file
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Opens slide in the presentation
ISlide slide = pptxDoc.Slides[0];

//Open Table in the slide to make changes
ITable table = slide.Shapes[0] as ITable;

//Changing the paragraph content in the table
table.Rows[0].Cells[0].TextBody.AddParagraph("Hello World");

//Get the dynamic height of the table
float height=table.GetActualHeight();

//Save the presentation
pptxDoc.Save("Table.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint file
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

'Get the table from the slide
Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

‘Changing the paragraph content in the table
table.Rows[0].Cells[0].TextBody.AddParagraph("Hello World");

‘Get the dynamic height of table
Dim height As float = table.GetActualHeight()

'Save the presentation
pptxDoc.Save("Table.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Initialize Presentation renderer
pptxDoc.PresentationRenderer = new PresentationRenderer();

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Changing the paragraph content in the table
table.Rows[0].Cells[0].TextBody.AddParagraph("Hello World");

//Get the dynamic height of the table
float height=table.GetActualHeight();

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Table.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Initialize Presentation renderer
pptxDoc.PresentationRenderer = new PresentationRenderer();

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Changing the paragraph content in the table
table.Rows[0].Cells[0].TextBody.AddParagraph("Hello World");

//Get the dynamic height of the table
float height=table.GetActualHeight();

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

N> Getting the actual height of the table is not supported in UWP platform.

## Applying table formatting

You can format a table to change its appearance by customizing the table border, cell background, cell margins etc. The following code example demonstrates how to apply the custom table formatting.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves each cell and fills text content to the cell.
ICell cell = table[0, 0];

//Sets the column width for a cell; this sets the width for entire column
cell.ColumnWidth = 400;

//Sets the margin for the cell.
cell.TextBody.MarginBottom = 0;
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color.SystemColor = Color.Orange;
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

//Sets the margin for the cell.
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color.SystemColor = Color.BlueViolet;
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

//Sets the margin for the cell.
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color.SystemColor = Color.SandyBrown;
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

//Sets the margin for the cell.
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color.SystemColor = Color.Silver;
cell.TextBody.AddParagraph("Second Row and Second Column");

//Saves the Presentation
pptxDoc.Save("Table.pptx");

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()

'Adds slide to the Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

'Adds table to the slide
Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Retrieves each cell and fills text content to the cell.
Dim cell As ICell = table(0, 0)

'Sets the column width for a cell; this sets the width for entire column
cell.ColumnWidth = 400

'Sets the margin for the cell.
cell.TextBody.MarginBottom = 0
cell.TextBody.MarginLeft = 58
cell.TextBody.MarginRight = 29
cell.TextBody.MarginTop = 65

'Sets the back color for the cell.
cell.Fill.SolidFill.Color.SystemColor = Color.Orange
cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)

'Sets the margin for the cell.
cell.TextBody.MarginLeft = 58
cell.TextBody.MarginRight = 29
cell.TextBody.MarginTop = 65

'Sets the back color for the cell.
cell.Fill.SolidFill.Color.SystemColor = Color.BlueViolet
cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(1, 0)

'Sets the margin for the cell.
cell.TextBody.MarginLeft = 58
cell.TextBody.MarginRight = 29
cell.TextBody.MarginTop = 65

'Sets the back color for the cell.
cell.Fill.SolidFill.Color.SystemColor = Color.SandyBrown
cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)

'Sets the margin for the cell.
cell.TextBody.MarginLeft = 58
cell.TextBody.MarginRight = 29
cell.TextBody.MarginTop = 65

'Sets the back color for the cell.
cell.Fill.SolidFill.Color.SystemColor = Color.Silver
cell.TextBody.AddParagraph("Second Row and Second Column")

'Saves the Presentation
pptxDoc.Save("Table.pptx")

'Closes the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves each cell and fills text content to the cell.
ICell cell = table[0, 0];

//Sets the column width for a cell; this sets the width for entire column
cell.ColumnWidth = 400;

//Sets the margin for the cell.

cell.TextBody.MarginBottom = 0;
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color = ColorObject.Orange;

cell.TextBody.AddParagraph("First Row and First Column");
cell = table[0, 1];

//Sets the margin for the cell.

cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color = ColorObject.BlueViolet;

cell.TextBody.AddParagraph("First Row and Second Column");
cell = table[1, 0];

//Sets the margin for the cell.

cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color = ColorObject.SandyBrown;

cell.TextBody.AddParagraph("Second Row and First Column");
cell = table[1, 1];

//Sets the margin for the cell.

cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color = ColorObject.Silver;

cell.TextBody.AddParagraph("Second Row and Second Column");

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Table";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves each cell and fills text content to the cell.
ICell cell = table[0, 0];

//Sets the column width for a cell; this sets the width for entire column
cell.ColumnWidth = 400;

//Sets the margin for the cell.
cell.TextBody.MarginBottom = 0;
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color = ColorObject.Orange;
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

//Sets the margin for the cell.
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color = ColorObject.BlueViolet;
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

//Sets the margin for the cell.
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color= ColorObject.SandyBrown;
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

//Sets the margin for the cell.
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color  = ColorObject.Silver;
cell.TextBody.AddParagraph("Second Row and Second Column");

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Table.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves each cell and fills text content to the cell.
ICell cell = table[0, 0];

//Sets the column width for a cell; this sets the width for entire column
cell.ColumnWidth = 400;

//Sets the margin for the cell.
cell.TextBody.MarginBottom = 0;
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color = ColorObject.Orange;
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

//Sets the margin for the cell.
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color = ColorObject.BlueViolet;
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

//Sets the margin for the cell.
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color= ColorObject.SandyBrown;
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

//Sets the margin for the cell.
cell.TextBody.MarginLeft = 58;
cell.TextBody.MarginRight = 29;
cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.
cell.Fill.SolidFill.Color  = ColorObject.Silver;
cell.TextBody.AddParagraph("Second Row and Second Column");

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Applying table styles

You can format a table by applying pre-defined table styles. The following code example demonstrates how to apply predefined styles to a table.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(3, 3, 100, 120, 300, 200);

table.BuiltInStyle = BuiltInTableStyle.ThemedStyle2Accent4;
table.HasBandedRows = false;
table.HasHeaderRow = false;
table.HasBandedColumns = true;
table.HasFirstColumn = true;
table.HasLastColumn = true;
table.HasTotalRow = true;

//Retrieves each cell and fills text content to the cell.
ICell cell = table[0, 0];
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[0, 2];
cell.TextBody.AddParagraph("First Row and Third Column");

cell = table[1, 0];
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];
cell.TextBody.AddParagraph("Second Row and Second Column");

cell = table[1, 2];
cell.TextBody.AddParagraph("Second Row and Third Column");

cell = table[2, 0];
cell.TextBody.AddParagraph("Third Row and First Column");

cell = table[2, 1];
cell.TextBody.AddParagraph("Third Row and Second Column");

cell = table[2, 2];
cell.TextBody.AddParagraph("Third Row and Third Column");

//Adds description to table shape
table.Description = "Table arrangement";

//Saves the Presentation
pptxDoc.Save("Table.pptx");

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation
Dim  pptxDoc As IPresentation = Presentation.Create()

'Adds slide to the Presentation
Dim slide As ISlide =  pptxDoc .Slides.Add(SlideLayoutType.Blank)

'Adds table to the slide
Dim table As ITable = slide.Shapes.AddTable(3, 3, 100, 120, 300, 200)

table.BuiltInStyle = BuiltInTableStyle.ThemedStyle2Accent4
table.HasBandedRows = False
table.HasHeaderRow = False
table.HasBandedColumns = True
table.HasFirstColumn = True
table.HasLastColumn = True
table.HasTotalRow = True

'Retrieves each cell and fills text content to the cell.
Dim cell As ICell = table(0, 0)
cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)
cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(0, 2)
cell.TextBody.AddParagraph("First Row and Third Column")

cell = table(1, 0)
cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)
cell.TextBody.AddParagraph("Second Row and Second Column")

cell = table(1, 2)
cell.TextBody.AddParagraph("Second Row and Third Column")

cell = table(2, 0)
cell.TextBody.AddParagraph("Third Row and First Column")

cell = table(2, 1)
cell.TextBody.AddParagraph("Third Row and Second Column")

cell = table(2, 2)
cell.TextBody.AddParagraph("Third Row and Third Column")

'Adds description to table shape
table.Description = "Table arrangement"

'Saves the Presentation
pptxDoc.Save("Table.pptx")

'Closes the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide

ITable table = slide.Shapes.AddTable(3, 3, 100, 120, 300, 200);
table.BuiltInStyle = BuiltInTableStyle.ThemedStyle2Accent4;
table.HasBandedRows = false;
table.HasHeaderRow = false;
table.HasBandedColumns = true;
table.HasFirstColumn = true;
table.HasLastColumn = true;
table.HasTotalRow = true;

//Retrieves each cell and fills text content to the cell.

ICell cell = table[0, 0];
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[0, 2];
cell.TextBody.AddParagraph("First Row and Third Column");

cell = table[1, 0];
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];
cell.TextBody.AddParagraph("Second Row and Second Column");

cell = table[1, 2];
cell.TextBody.AddParagraph("Second Row and Third Column");

cell = table[2, 0];
cell.TextBody.AddParagraph("Third Row and First Column");

cell = table[2, 1];
cell.TextBody.AddParagraph("Third Row and Second Column");

cell = table[2, 2];
cell.TextBody.AddParagraph("Third Row and Third Column");

//Adds description to table shape
table.Description = "Table arrangement";

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Table";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(3, 3, 100, 120, 300, 200);

table.BuiltInStyle = BuiltInTableStyle.ThemedStyle2Accent4;
table.HasBandedRows = false;
table.HasHeaderRow = false;
table.HasBandedColumns = true;
table.HasFirstColumn = true;
table.HasLastColumn = true;
table.HasTotalRow = true;

//Retrieves each cell and fills text content to the cell.
ICell cell = table[0, 0];
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[0, 2];
cell.TextBody.AddParagraph("First Row and Third Column");

cell = table[1, 0];
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];
cell.TextBody.AddParagraph("Second Row and Second Column");

cell = table[1, 2];
cell.TextBody.AddParagraph("Second Row and Third Column");

cell = table[2, 0];
cell.TextBody.AddParagraph("Third Row and First Column");

cell = table[2, 1];
cell.TextBody.AddParagraph("Third Row and Second Column");

cell = table[2, 2];
cell.TextBody.AddParagraph("Third Row and Third Column");

//Adds description to table shape
table.Description = "Table arrangement";

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Table.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(3, 3, 100, 120, 300, 200);

table.BuiltInStyle = BuiltInTableStyle.ThemedStyle2Accent4;
table.HasBandedRows = false;
table.HasHeaderRow = false;
table.HasBandedColumns = true;
table.HasFirstColumn = true;
table.HasLastColumn = true;
table.HasTotalRow = true;

//Retrieves each cell and fills text content to the cell.
ICell cell = table[0, 0];
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[0, 2];
cell.TextBody.AddParagraph("First Row and Third Column");

cell = table[1, 0];
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];
cell.TextBody.AddParagraph("Second Row and Second Column");

cell = table[1, 2];
cell.TextBody.AddParagraph("Second Row and Third Column");

cell = table[2, 0];
cell.TextBody.AddParagraph("Third Row and First Column");

cell = table[2, 1];
cell.TextBody.AddParagraph("Third Row and Second Column");

cell = table[2, 2];
cell.TextBody.AddParagraph("Third Row and Third Column");

//Adds description to table shape
table.Description = "Table arrangement";

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Modifying the table

The following code example demonstrates how to modify the table in existing PowerPoint Presentation

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Gets slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Gets table from slide
ITable table = slide.Shapes[0] as ITable;

//Modifies the table width
table.Width = 450;

//Changes the built in style of the table
table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2;

//Sets text content to the cell
table.Rows[0].Cells[0].TextBody.AddParagraph("Row1 Cell1");           

//Saves the Presentation
pptxDoc.Save("TableModified.pptx");

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Gets slide from the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)

'Gets table from slide
Dim table As ITable = TryCast(slide.Shapes(0), ITable)

'Modifies the table width
table.Width = 450

'Changes the built in style of the table
table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2

'Sets text content to the cell
table.Rows(0).Cells(0).TextBody.AddParagraph("Row1 Cell1")

'Saves the Presentation
pptxDoc.Save("TableModified.pptx")

'Closes the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Gets slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Gets table from slide
ITable table = slide.Shapes[0] as ITable;

//Modifies the table width
table.Width = 450;

//Changes the built in style of the table
table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2;

//Sets text content to the cell
table.Rows[0].Cells[0].TextBody.AddParagraph("Row1 Cell1");

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "TableModified";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Gets slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Gets table from slide
ITable table = slide.Shapes[0] as ITable;

//Modifies the table width
table.Width = 450;

//Changes the built in style of the table
table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2;

//Sets text content to the cell
table.Rows[0].Cells[0].TextBody.AddParagraph("Row1 Cell1");          

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("TableModified.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Gets slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Gets table from slide
ITable table = slide.Shapes[0] as ITable;

//Modifies the table width
table.Width = 450;

//Changes the built in style of the table
table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2;

//Sets text content to the cell
table.Rows[0].Cells[0].TextBody.AddParagraph("Row1 Cell1");          

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Merging the cells

The following code example shows how to merge cells in a table.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves first cell.
ICell cell = table[0, 0];

//Sets the column span value to merge the cell.
cell.ColumnSpan = 2;

//Retrieves each cell and fills text content to the cell.
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];
cell.TextBody.AddParagraph("Second Row and Second Column");

//Gives simple description to table shape
table.Description = "Table arrangement";

//Saves the Presentation
pptxDoc.Save("Table.pptx");

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()

'Adds slide to the Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

'Adds table to the slide
Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Retrieves first cell.
Dim cell As ICell = table(0, 0)

'Sets the column span value to merge the cell.
cell.ColumnSpan = 2

'Retrieves each cell and fills text content to the cell.
cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)
cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(1, 0)
cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)
cell.TextBody.AddParagraph("Second Row and Second Column")

'Gives simple description to table shape
table.Description = "Table arrangement"

'Saves the Presentation
pptxDoc.Save("Table.pptx")

'Closes the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves first cell.
ICell cell = table[0, 0];

//Sets the column span value to merge the cell.
cell.ColumnSpan = 2;

//Retrieves each cell and fills text content to the cell.

cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

cell.TextBody.AddParagraph("Second Row and Second Column");

//Gives simple description to table shape
table.Description = "Table arrangement";

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Table";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves first cell.
ICell cell = table[0, 0];

//Sets the column span value to merge the cell.
cell.ColumnSpan = 2;

//Retrieves each cell and fills text content to the cell.
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];
cell.TextBody.AddParagraph("Second Row and Second Column");

//Gives simple description to table shape
table.Description = "Table arrangement";

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide
ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves first cell.
ICell cell = table[0, 0];

//Sets the column span value to merge the cell.
cell.ColumnSpan = 2;

//Retrieves each cell and fills text content to the cell.
cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];
cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];
cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];
cell.TextBody.AddParagraph("Second Row and Second Column");

//Gives simple description to table shape
table.Description = "Table arrangement";

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Removing the table

You can remove a table from a slide by its instance or by its index position in the shape collection. The following code example demonstrates removing a table in a slide.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Gets slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Gets the table from slide
ITable table = slide.Shapes[0] as ITable;

//Removes table from shape collection
slide.Shapes.Remove(table);

//Saves the Presentation
pptxDoc.Save("TableRemoved.pptx");

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Gets slide from the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)

'Gets the table from slide
Dim table As ITable = TryCast(slide.Shapes(0), ITable)

'Removes table from shape collection
slide.Shapes.Remove(table)

'Saves the Presentation
pptxDoc.Save("TableRemoved.pptx")

'Closes the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Gets slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Gets the table from slide
ITable table = slide.Shapes[0] as ITable;

//Removes table from shape collection
slide.Shapes.Remove(table);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "TableRemoved";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Gets slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Gets the table from slide
ITable table = slide.Shapes[0] as ITable;

//Removes table from shape collection
slide.Shapes.Remove(table);        

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("TableModified.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Gets slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Gets the table from slide
ITable table = slide.Shapes[0] as ITable;

//Removes table from shape collection
slide.Shapes.Remove(table);        

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Table.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Editing the table content

The following code example demonstrates how to edit the content in a table.

{% tabs %}

{% highlight c# %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Iterates through the rows of the table
foreach (IRow row in table.Rows)
{
    //Iterates through the cells of the rows
    foreach (ICell cell in row.Cells)
    {
        //Iterates through the paragraphs of the cell
        foreach (IParagraph paragraph in cell.TextBody.Paragraphs)
        {
            //Iterates through the TextPart of the paragraph
            foreach (ITextPart textPart in paragraph.TextParts)
            {
                //When the TextPart contains text Panda, then modifies the text content of the TextPart.
                if (textPart.Text.Contains("Panda"))
                    textPart.Text = "Hello Presentation";
            }
        }
    }
}

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get a table in the slide
Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Iterates through the rows of the table
For Each row As IRow In table.Rows
    'Iterates through the cells of the rows
    For Each cell As ICell In row.Cells
        'Iterates through the paragraphs of the cell
        For Each paragraph As IParagraph In cell.TextBody.Paragraphs
            'Iterates through the TextPart of the paragraph
            For Each textPart As ITextPart In paragraph.TextParts
                'When the TextPart contains text Panda, then modifies the text content of the TextPart.
                If textPart.Text.Contains("Panda") Then
                    textPart.Text = "Hello Presentation"
                End If
            Next
        Next
    Next
Next

'Save the presentation
pptxDoc.Save("Sample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Iterates through the rows of the table
foreach (IRow row in table.Rows)
{
    //Iterates through the cells of the rows
    foreach (ICell cell in row.Cells)
    {
        //Iterates through the paragraphs of the cell
        foreach (IParagraph paragraph in cell.TextBody.Paragraphs)
        {
            //Iterates through the TextPart of the paragraph
            foreach (ITextPart textPart in paragraph.TextParts)
            {
                //When the TextPart contains text Panda, then modifies the text content of the TextPart.
                if (textPart.Text.Contains("Panda"))
                    textPart.Text = "Hello Presentation";
            }
        }
    }
}

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Table.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Iterates through the rows of the table
foreach (IRow row in table.Rows)
{
    //Iterates through the cells of the rows
    foreach (ICell cell in row.Cells)
    {
        //Iterates through the paragraphs of the cell
        foreach (IParagraph paragraph in cell.TextBody.Paragraphs)
        {
            //Iterates through the TextPart of the paragraph
            foreach (ITextPart textPart in paragraph.TextParts)
            {
                //When the TextPart contains text Panda, then modifies the text content of the TextPart.
                if (textPart.Text.Contains("Panda"))
                    textPart.Text = "Hello Presentation";
            }
        }
    }
}

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Table.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get a table in the slide
ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Iterates through the rows of the table
foreach (IRow row in table.Rows)
{
    //Iterates through the cells of the rows
    foreach (ICell cell in row.Cells)
    {
        //Iterates through the paragraphs of the cell
        foreach (IParagraph paragraph in cell.TextBody.Paragraphs)
        {
            //Iterates through the TextPart of the paragraph
            foreach (ITextPart textPart in paragraph.TextParts)
            {
                //When the TextPart contains text Panda then modifies the text content of the TextPart.
                if (textPart.Text.Contains("Panda"))
                    textPart.Text = "Hello Presentation";
            }
        }
    }
}

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();

stream.Position = 0;

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}