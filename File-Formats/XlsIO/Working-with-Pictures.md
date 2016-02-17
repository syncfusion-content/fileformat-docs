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

