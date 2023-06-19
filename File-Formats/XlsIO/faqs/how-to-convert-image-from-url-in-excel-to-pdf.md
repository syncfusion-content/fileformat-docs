---
title: Convert image from URL in Excel to PDF | Syncfusion
description: This page shows how to image from URL in Excel to PDF using the Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to convert image from URL in Excel to PDF?

The image added from an URL/external link will be downloaded every time the spreadsheet is opened in Microsoft Excel. The image is not physically embedded into the Excel document but points to a web resource. As the image is not present, it would not be rendered in the converted PDF document.

But, this can be achieved by downloading the image prior and adding it into Excel. Please find the code snippet below.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  WebClient client = new WebClient();
  byte[] imageData = client.DownloadData("https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png");

  worksheet.Pictures.AddPicture(1, 1, 5, 7, Image.FromStream(new MemoryStream(imageData)));

  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert Excel document into PDF document 
  PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

  FileStream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  WebClient client = new WebClient();
  byte[] imageData = client.DownloadData("https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png");

  worksheet.Pictures.AddPicture(1, 1, 5, 7, Image.FromStream(new MemoryStream(imageData)));

  //Initialize XlsIO renderer.
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert Excel document into PDF document 
  PdfDocument pdfDocument = converter.Convert();

  FileStream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)
  Dim client As WebClient = New WebClient
  Dim imageData() As Byte = client.DownloadData("https://cdn.syncfusion.com/content/images/company-logos/Syncfusion_Logo_Image.png")
  worksheet.Pictures.AddPicture(1, 1, 5, 7, Image.FromStream(New MemoryStream(imageData)))
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)
  Dim pdfDocument As PdfDocument = converter.Convert
  Dim stream As FileStream = New FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite)
  pdfDocument.Save(stream)
  stream.Dispose
End Using
{% endhighlight %}
{% endtabs %}  

