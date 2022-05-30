---
title: Working with Pictures | Syncfusion
description: Briefs about inserting pictures in Essential XlsIO. It provides various simple and interactive options to insert Pictures into a worksheet.
platform: file-Formats
control: XlsIO
documentation: UG
---
# Working with Pictures 

XlsIO allows to insert Pictures into a worksheet. Refer to the following code snippet. 

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding a picture
  IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, "Image.png");

  workbook.SaveAs("AddingImage.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Adding a picture
  Dim shape As IPictureShape = worksheet.Pictures.AddPicture(1, 1, "Image.png")

  workbook.SaveAs("AddingImage.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding a picture
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream imageStream = assembly.GetManifestResourceStream("UWP.Data.Image.png");
  IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, imageStream);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "AddingImage";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding a picture
  FileStream imageStream = new FileStream("Image.png", FileMode.Open, FileAccess.Read);
  IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, imageStream);

  //Saving the workbook as stream
  FileStream stream = new FileStream("AddingImage.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding a picture
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream imageStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Image.png");
  IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, imageStream);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("AddingImage.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("AddingImage.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to insert picture in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pictures%20in%20Excel/Add%20Picture).   

## Positioning and Re-Sizing Pictures

Pictures can be re-sized, positioned, and formatted using various properties of **IPictureShape** interface. Refer to the following code snippet.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding a Picture
  IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, "Image.png");

  //Positioning a Picture
  shape.Top = 100;
  shape.Left = 100;

  //Re-sizing a Picture
  shape.Height = 100;
  shape.Width = 100;

  workbook.SaveAs("AddingImage.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Adding a Picture
  Dim shape As IPictureShape = worksheet.Pictures.AddPicture(1, 1, "Image.png")

  'Positioning a Picture
  shape.Top = 100
  shape.Left = 100

  'Re-sizing a Picture
  shape.Height = 100
  shape.Width = 100

  workbook.SaveAs("AddingImage.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding a picture
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream imageStream = assembly.GetManifestResourceStream("UWP.Data.Image.png");
  IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, imageStream);

  //Positioning a Picture
  shape.Top = 100;
  shape.Left = 100;

  //Re-sizing a Picture
  shape.Height = 100;
  shape.Width = 100;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "AddingImage";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding a picture
  FileStream imageStream = new FileStream("Image.png", FileMode.Open, FileAccess.Read);
  IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, imageStream);

  //Positioning a Picture
  shape.Top = 100;
  shape.Left = 100;

  //Re-sizing a Picture
  shape.Height = 100;
  shape.Width = 100;

  //Saving the workbook as stream
  FileStream stream = new FileStream("AddingImage.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding a picture
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream imageStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Image.png");
  IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, imageStream);

  //Positioning a Picture
  shape.Top = 100;
  shape.Left = 100;

  //Re-sizing a Picture
  shape.Height = 100;
  shape.Width = 100;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("AddingImage.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("AddingImage.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to position and resize picture in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pictures%20in%20Excel/Position%20and%20Resize%20Picture).   

## Image into Merged Region

The following code snippet explains how to add images into merged regions.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open(InputTemplate.xlsx);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Get the merged cells
    IRange[] range = new IRange[3];
    range[0] = worksheet.MergedCells[0];
    range[1] = worksheet.MergedCells[1];
    range[2] = worksheet.MergedCells[2];

    //Get the images
    string[] image = new string[3];
    image[0] = "Picture1.png";
    image[1] = "Picture2.png";
    image[2] = "Picture3.png";

    //Insert images
    int count = 0;
    foreach (IRange cell in range)
    {
        FileStream imageStream = new FileStream(image[count], FileMode.Open, FileAccess.Read);
        IPictureShape shape = worksheet.Pictures.AddPicture(cell.Row, cell.Column, imageStream);
        (shape as ShapeImpl).BottomRow = cell.MergeArea.LastRow;
        (shape as ShapeImpl).RightColumn = cell.MergeArea.LastColumn;
        count++;
        imageStream.Dispose();
    }

    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx")
    Dim worksheet As IWorksheet = workbook.Worksheets(0)
    Dim range() As IRange = New IRange((3) - 1) {}
    range(0) = worksheet.MergedCells(0)
    range(1) = worksheet.MergedCells(1)
    range(2) = worksheet.MergedCells(2)
    Dim image() As String = New String((3) - 1) {}
    image(0) = "Picture1.png"
    image(1) = "Picture2.png"
    image(2) = "Picture3.png"
    Dim count As Integer = 0
    For Each cell As IRange In range
        Dim imageStream As FileStream = New FileStream(image(count), FileMode.Open, FileAccess.Read)
        Dim shape As IPictureShape = worksheet.Pictures.AddPicture(cell.Row, cell.Column, imageStream)
        CType(shape, ShapeImpl).BottomRow = cell.MergeArea.LastRow
        CType(shape, ShapeImpl).RightColumn = cell.MergeArea.LastColumn
        count = (count + 1)
        imageStream.Dispose
    Next
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

	//Instantiates the File Picker
    FileOpenPicker openPicker = new FileOpenPicker();
    openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
    openPicker.FileTypeFilter.Add(".xlsx");
    openPicker.FileTypeFilter.Add(".xls");
    StorageFile file = await openPicker.PickSingleFileAsync();
    IWorkbook workbook = application.Workbooks.Open(file);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Get the merged cells
    IRange[] range = new IRange[3];
    range[0] = worksheet.MergedCells[0];
    range[1] = worksheet.MergedCells[1];
    range[2] = worksheet.MergedCells[2];

    //Get the images
    string[] image = new string[3];
    image[0] = "Picture1.png";
    image[1] = "Picture2.png";
    image[2] = "Picture3.png";

    //Insert images
    int count = 0;
    foreach (IRange cell in range)
    {
        FileStream imageStream = new FileStream(image[count], FileMode.Open, FileAccess.Read);
        IPictureShape shape = worksheet.Pictures.AddPicture(cell.Row, cell.Column, imageStream);
        (shape as ShapeImpl).BottomRow = cell.MergeArea.LastRow;
        (shape as ShapeImpl).RightColumn = cell.MergeArea.LastColumn;
        count++;
        imageStream.Dispose();
    }

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

    //Creates a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();

    //Saves changes to the specified storage file
    await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
	FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Get the merged cells
    IRange[] range = new IRange[3];
    range[0] = worksheet.MergedCells[0];
    range[1] = worksheet.MergedCells[1];
    range[2] = worksheet.MergedCells[2];

    //Get the images
    string[] image = new string[3];
    image[0] = "Picture1.png";
    image[1] = "Picture2.png";
    image[2] = "Picture3.png";

    //Insert images
    int count = 0;
    foreach (IRange cell in range)
    {
        FileStream imageStream = new FileStream(image[count], FileMode.Open, FileAccess.Read);
        IPictureShape shape = worksheet.Pictures.AddPicture(cell.Row, cell.Column, imageStream);
        (shape as ShapeImpl).BottomRow = cell.MergeArea.LastRow;
        (shape as ShapeImpl).RightColumn = cell.MergeArea.LastColumn;
        count++;
        imageStream.Dispose();
    }

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
	//"App" is the class of Portable project
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream inputStream = assembly.GetManifestResourceStream("Pictures.InputTemplate.xlsx");
    IWorkbook workbook = application.Workbooks.Open(inputStream);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Get the merged cells
    IRange[] range = new IRange[3];
    range[0] = worksheet.MergedCells[0];
    range[1] = worksheet.MergedCells[1];
    range[2] = worksheet.MergedCells[2];

    //Get the images
    string[] image = new string[3];
    image[0] = "Picture1.png";
    image[1] = "Picture2.png";
    image[2] = "Picture3.png";

    //Insert images
    int count = 0;
    foreach (IRange cell in range)
    {
        FileStream imageStream = new FileStream(image[count], FileMode.Open, FileAccess.Read);
        IPictureShape shape = worksheet.Pictures.AddPicture(cell.Row, cell.Column, imageStream);
        (shape as ShapeImpl).BottomRow = cell.MergeArea.LastRow;
        (shape as ShapeImpl).RightColumn = cell.MergeArea.LastColumn;
        count++;
        imageStream.Dispose();
    }

    //Saving the workbook as stream
    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);
	
    stream.Position = 0;

    //Save the document as file and view the saved document
    //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

    if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    {
	    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
    }
    else
    {
	    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
    }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add picture into merged region in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pictures%20in%20Excel/ImageInMergedRegion).   

## Adding Images from External Link

An image can be added to a worksheet as an external link without downloading the original image. The picture will be downloaded every time the spreadsheet is opened in Microsoft Excel. The image is not physically embedded into the Excel document, but points to a web resource. Refer to the following code snippet.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add image from the specified url at the specified location in the worksheet
  worksheet.Pictures.AddPictureAsLink(1, 1, 5, 7, "https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png");

  //Save workbook
  workbook.SaveAs("ExternalImage.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Add image from the specified url at the specified location in the worksheet
  worksheet.Pictures.AddPictureAsLink(1, 1, 5, 7, "https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png")

  'Save workbook
  workbook.SaveAs("ExternalImage.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add image from the specified url at the specified location in the worksheet
  worksheet.Pictures.AddPictureAsLink(1, 1, 5, 7, "https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png");

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "ExternalImage";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add image from the specified url at the specified location in the worksheet
  worksheet.Pictures.AddPictureAsLink(1, 1, 5, 7, "https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png");

  //Saving the workbook as stream
  FileStream stream = new FileStream("ExternalImage.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add image from the specified url at the specified location in the worksheet
  worksheet.Pictures.AddPictureAsLink(1, 1, 5, 7, "https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png");

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("ExternalImage.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ExternalImage.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add picture from external link in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pictures%20in%20Excel/External%20Image).   

## Adding SVG Images

SVG images can be inserted in Excel documents for displaying images with accuracy when scaling or zooming page. Adding SVG images is now supported in XlsIO with SVG and its fallback raster image data as parameters as in the following code snippet.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  FileStream svgStream = new FileStream("Sample.svg", FileMode.Open);
  FileStream pngStream = new FileStream("Sample.png", FileMode.Open);

  //Add svg image with given svg and png streams
  worksheet.Pictures.AddPicture(1, 1, svgStream, pngStream);

  //Save workbook
  workbook.SaveAs("Svg.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  Dim svgStream As New FileStream("Sample.svg", FileMode.Open)
  Dim pngStream As New FileStream("Sample.png", FileMode.Open)

  'Add svg image with given svg and png streams
  worksheet.Pictures.AddPicture(1, 1, svgStream, pngStream)

  'Save workbook
  workbook.SaveAs("Svg.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream svgStream = assembly.GetManifestResourceStream("UWP.Data.Sample.svg");
  Stream pngStream = assembly.GetManifestResourceStream("UWP.Data.Sample.png");

  //Add svg image with given svg and png streams
  worksheet.Pictures.AddPicture(1, 1, svgStream, pngStream);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Svg";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  FileStream svgStream = new FileStream("Sample.svg", FileMode.Open);
  FileStream pngStream = new FileStream("Sample.png", FileMode.Open);

  //Add svg image with given svg and png streams
  worksheet.Pictures.AddPicture(1, 1, svgStream, pngStream);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Svg.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream svgStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.svg");
  Stream pngStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.png");

  //Add svg image with given svg and png streams
  worksheet.Pictures.AddPicture(1, 1, svgStream, pngStream);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Svg.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Svg.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add SVG images in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pictures%20in%20Excel/Add%20SVG%20Picture).

