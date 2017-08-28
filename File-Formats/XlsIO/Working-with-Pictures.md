---
title: Working with Pictures
description: Briefs about inserting pictures in XlsIO
platform: File-Formats
control: XlsIO
documentation: UG
---
# Working with Pictures 

XlsIO allows to insert Pictures into a worksheet. The following code snippet shows how to insert picture using XlsIO. 

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Adding a picture

IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, "Image.png");

workbook.SaveAs("AddingImage.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Adding a picture 

Dim shape As IPictureShape = worksheet.Pictures.AddPicture(1, 1, "Image.png")

workbook.SaveAs("AddingImage.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## Positioning and Re-Sizing Pictures

Pictures can be re-sized, positioned and formatted using various properties of **IPictureShape** interface. The following code snippet shows how to apply picture settings.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

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

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

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

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## Adding images from external link

An image can be added to a worksheet as an external link without downloading the original image. The picture will be downloaded every time the spreadsheet is opened in Microsoft Excel. The image is not physically embedded into the Excel document, but points to a web resource. 
The following code snippet illustrates adding linked images to a worksheet.

{% tabs %}
{% highlight c# %}
ExcelEngine engine = new ExcelEngine();
IApplication application = engine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;
IWorkbook workbook = application.Workbooks.Create(1);
IWorksheet worksheet = workbook.Worksheets[0];

// The first worksheet object in the worksheets collection is accessed.
IWorksheet worksheet = workbook.Worksheets[0];
 
// Add image from the specified url at the specified location in the worksheet.
worksheet.Pictures.AddPictureAsLink(1, 1, 5, 7, https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png);

// Save workbook
workbook.SaveAs("ExternalImage.xlsx");      

workbook.Close();
engine.Dispose();
{% endhighlight %}
{% highlight vb %}
Dim engine As New ExcelEngine()
Dim application As IApplication = engine.Excel
application.DefaultVersion = ExcelVersion.Excel2013
Dim workbook As IWorkbook = application.Workbooks.Create(1)
Dim worksheet As IWorksheet = workbook.Worksheets(0)
 
' The first worksheet object in the worksheets collection is accessed.
Dim worksheet As IWorksheet = workbook.Worksheets(0)
 
' Add image from the specified url at the specified location in the worksheet.
worksheet.Pictures.AddPictureAsLink(1, 1, 5, 7, https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png)
 
' Save workbook
workbook.SaveAs("ExternalImage.xlsx")
 
workbook.Close()
engine.Dispose()

{% endhighlight %}
{% endtabs %}

## Adding SVG images

SVG images can be inserted in Excel documents for displaying images with accuracy while scaling/zooming page. Adding SVG images is now supported in XlsIO with SVG and its fallback raster image data as parameters as in the below code snippet.

{% tabs %}
{% highlight c# %}
ExcelEngine engine = new ExcelEngine();
IApplication application = engine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;
IWorkbook workbook = application.Workbooks.Create(1);
IWorksheet worksheet = workbook.Worksheets[0];

FileStream svgStream = new FileStream("Sample.svg", FileMode.Open);
FileStream pngStream = new FileStream("Sample.png", FileMode.Open);
 
// Add svg image with given svg and png streams
worksheet.Pictures.AddPicture(1, 1, svgStream, imageStream);

// Save workbook
workbook.SaveAs("Svg.xlsx");      

workbook.Close();
engine.Dispose();
{% endhighlight %}
{% endtabs %}
{% tabs %}
{% highlight vb %}
Dim engine As New ExcelEngine()
Dim application As IApplication = engine.Excel
application.DefaultVersion = ExcelVersion.Excel2013
Dim workbook As IWorkbook = application.Workbooks.Create(1)
Dim worksheet As IWorksheet = workbook.Worksheets(0)
 
Dim svgStream As New FileStream("Sample.svg", FileMode.Open)
Dim pngStream As New FileStream("Sample.png", FileMode.Open)
 
' Add svg image with given svg and png streams
worksheet.Pictures.AddPicture(1, 1, svgStream, imageStream)
 
' Save workbook
workbook.SaveAs("Svg.xlsx")
 
workbook.Close()
engine.Dispose()

{% endhighlight %}
{% endtabs %}
