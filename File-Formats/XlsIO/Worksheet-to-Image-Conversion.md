---
title: Worksheet to Image conversion
description: Briefs about Worksheet to Image conversion in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Worksheet to Image conversion

## Convert as Bitmap

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
N> XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight asp.netcore %}
N> XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight Xamarin %}
N> XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
  {% endtabs %}  

## Save as Stream

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
N> XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight asp.netcore %}
N> XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight Xamarin %}
N> XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}

  {% endtabs %}  

The complete code snippet of the above options is shown below.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
IWorksheet sheet = workbook.Worksheets[0];

// Convert as bitmap
Image image = sheet.ConvertToImage(1, 1, 10, 20);

image.Save("Sample.png", ImageFormat.Png);

// Converts and save as stream
MemoryStream stream = new MemoryStream();
sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);

//Save the workbook to disk
workbook.SaveAs("Sample.xlsx");

//Close the workbook
workbook.Close();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = false;

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("sample.xlsx", ExcelOpenType.Automatic)
Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Convert as bitmap
Dim image As Image = sheet.ConvertToImage(1, 1, 10, 20)

image.Save("Sample.png", ImageFormat.Png)

'Converts and save as stream
Dim stream As MemoryStream = New MemoryStream()
sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream)

'Save the workbook to disk
workbook.SaveAs("Sample.xlsx")

'Close the workbook
workbook.Close()

'No exception will be thrown if there are unsaved workbooks.
excelEngine.ThrowNotSavedOnDestroy = False

excelEngine.Dispose()



{% endhighlight %}
{% highlight UWP %}
N> XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight asp.netcore %}
N> XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight Xamarin %}
N> XlsIO supports worksheet to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}

  {% endtabs %}  

**Non****-****Supported** **Features****:**

* Subscript/Superscript
* RTF
* Shrink to fit
* Shapes (except TextBox shape and Image)
* Charts and Chart Worksheet
* Complex conditional formatting
* Gradient fill is partially supported