---
title: Convert hidden worksheets alone to image | Syncfusion
description: This page shows how to convert hidden worksheets alone to image using the Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to convert hidden worksheets alone to image?

Worksheet hiding and unhiding can be achieved easily through [Visibility](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITabSheet.html#Syncfusion_XlsIO_ITabSheet_Visibility) property of IWorksheet interface. Essential XlsIO also supports strong hidden, which makes the worksheet very hidden and cannot be unhidden easily. To know more about strong hidden, please see [documentation](https://www.syncfusion.com/kb/4878/how-to-set-worksheet-visibility-to-very-hidden).

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Opening workbook with hidden worksheets
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Converting only hidden worksheets to image
  foreach (IWorksheet worksheet in workbook.Worksheets)
  {
    if (worksheet.Visibility == WorksheetVisibility.Hidden)
    {
      Image image = worksheet.ConvertToImage(1, 1, 5, 5);
      image.Save(worksheet.Name + ".png", ImageFormat.Png);
    }
  }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013

  'Opening workbook with hidden worksheets
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Converting only hidden worksheets to image
  For Each worksheet As IWorksheet In workbook.Worksheets
    If (worksheet.Visibility = WorksheetVisibility.Hidden) Then
      Dim image As Image = worksheet.ConvertToImage(1, 1, 5, 5)
      image.Save((worksheet.Name + ".png"), ImageFormat.Png)
    End If
  Next
End Using
{% endhighlight %}
{% endtabs %}  

