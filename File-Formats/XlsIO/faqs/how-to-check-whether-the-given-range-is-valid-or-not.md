---
title: How to check whether the given range is valid or not | Syncfusion
description: This page tells how to check whether given range is valid or not using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to check whether the given range is valid or not?

In the given range, if the first row and first column are less than or equal to last row and last column respectively, then the range is valid. XlsIO do not have direct support to check whether the given range is valid or not. But this can be achieved with a simple workaround. Please find the code snippet below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  string[] ranges = { "D1:A14", "A14:D1", "E1:F3", "G5", "AA10", "A1:A1" };
  foreach (string range in ranges)
  {
    try
    {
      IRange temp_range = worksheet.Range[range];
      Debug.WriteLine(range + " - is valid worksheet range");
    }
    catch (Exception ex)
    {
      Debug.WriteLine(range + " - is invalid worksheet range");
    }
  }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  string[] ranges = { "D1:A14", "A14:D1", "E1:F3", "G5", "AA10", "A1:A1" };
  foreach(string range in ranges)
  {
    try
    {
      IRange temp_range = worksheet.Range[range];
      Console.WriteLine(range + " - is valid worksheet range");
    }
    catch(Exception ex)
    {
      Console.WriteLine(range + " - is invalid worksheet range");
    }
  }
  Console.ReadLine();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  Dim ranges() As String = {"D1:A14", "A14:D1", "E1:F3", "G5", "AA10", "A1:A1"}
  For Each range As String In ranges
    Try
      Dim temp_range As IRange = worksheet.Range(range)
      Console.WriteLine((range + " - is valid worksheet range"))
    Catch ex As Exception
      Console.WriteLine((range + " - is invalid worksheet range"))
    End Try
  Next
  Console.ReadLine()
End Using
{% endhighlight %}
{% endtabs %}
