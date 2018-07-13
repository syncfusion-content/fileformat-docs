---
title: Worksheet to Image conversion
description: Briefs about Worksheet to Image conversion in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Worksheet to Image conversion

## Convert as bitmap

The following code shows how to convert the specified range of rows and columns in the worksheet to bitmap.

{% tabs %}
{% highlight c# %}
// Convert as bitmap
Image image = sheet.ConvertToImage(1, 1, 10, 20);
image.Save("Sample.png", ImageFormat.Png);
{% endhighlight %}

{% highlight vb %}
'Convert as bitmap
Dim image As Image = sheet.ConvertToImage(1, 1, 10, 20)
image.Save("Sample.png", ImageFormat.Png)
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET, ASP.NET MVC and .NET Core (from 2.0) platforms.
{% endhighlight %}

{% highlight asp.net core %}
// Convert as bitmap
Image image = sheet.ConvertToImage(1, 1, 10, 20);
image.Save("Sample.png", ImageFormat.Png);
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET, ASP.NET MVC and .NET Core (from 2.0) platforms.
{% endhighlight %}
{% endtabs %}  

## Save as stream

The following code snippet shows how to save a sheet as stream.

{% tabs %}
{% highlight c# %}
// Converts and save as stream
MemoryStream stream = new MemoryStream();
sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);
{% endhighlight %}

{% highlight vb %}
'Converts and save as stream
Dim stream As MemoryStream = New MemoryStream()
sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream)
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET, ASP.NET MVC and .NET Core (from 2.0) platforms.
{% endhighlight %}

{% highlight asp.net core %}
// Converts and save as stream
MemoryStream stream = new MemoryStream();
sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET, ASP.NET MVC and .NET Core (from 2.0) platforms.
{% endhighlight %}
{% endtabs %}  

The complete code snippet of the previous options is shown as follows.

{% tabs %}
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Convert as bitmap
  Image image = sheet.ConvertToImage(1, 1, 10, 20);

  image.Save("Sample.png", ImageFormat.Png);

  //Converts and save as stream
  MemoryStream stream = new MemoryStream();
  sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);

  //Save the workbook to disk
  workbook.SaveAs("Sample.xlsx");

  //No exception will be thrown if there are unsaved workbooks
  excelEngine.ThrowNotSavedOnDestroy = false;
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Convert as bitmap
  Dim image As Image = worksheet.ConvertToImage(1, 1, 10, 20)

  image.Save("Sample.png", ImageFormat.Png)

  'Converts and save as stream
  Dim stream As MemoryStream = New MemoryStream()
  worksheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream)

  'Save the workbook to disk
  workbook.SaveAs("Sample.xlsx")

  'No exception will be thrown if there are unsaved workbooks.
  excelEngine.ThrowNotSavedOnDestroy = False
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET, ASP.NET MVC and .NET Core (from 2.0) platforms.
{% endhighlight %}

{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Convert as bitmap
  Image image = sheet.ConvertToImage(1, 1, 10, 20);

  image.Save("Sample.png", ImageFormat.Png);

  //Converts and save as stream
  MemoryStream stream = new MemoryStream();
  sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Sample.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET, ASP.NET MVC and .NET Core (from 2.0) platforms.
{% endhighlight %}
{% endtabs %}  

**Non****-****Supported** **Features****:**

* Subscript/Superscript
* Shrink to fit
* Shapes (except TextBox shape and Image)
* Complex conditional formatting
* Gradient fill is partially supported