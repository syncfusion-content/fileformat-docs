---
title: Font settings for shape text | Syncfusion
description: This page explains the font settings for the shape text using the Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to apply font to shape text?

The following code snippet shows how to apply or change the shape text font.  

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  IFont font = workbook.CreateFont();
  font.FontName = "Arial";
  font.Size = 9; 

  IShape shape = worksheet.Shapes[0];
  shape.TextFrame.TextRange.RichText.SetFont(1, 3, font);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  IFont font = workbook.CreateFont();
  font.FontName = "Arial";
  font.Size = 9; 

  IShape shape = worksheet.Shapes[0];
  shape.TextFrame.TextRange.RichText.SetFont(1, 3, font);

  //Saving the workbook
  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  Dim font As IFont = workbook.CreateFont
  font.FontName = "Arial"
  font.Size = 9
  
  Dim shape As IShape = worksheet.Shapes(0)
  shape.TextFrame.TextRange.RichText.SetFont(1, 3, font)

  'Saving the workbook
  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

