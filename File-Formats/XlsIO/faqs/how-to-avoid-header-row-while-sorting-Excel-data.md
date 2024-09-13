---
title: How to avoid header row while sorting Excel data | XlsIO | Syncfusion
description: Code example to avoid header row while sorting Excel data using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to avoid header row while sorting Excel data?

Syncfusion XlsIO considers first row in the sort range as header. In order to disable this behavior and consider the first row in sorting, the [HasHeader](https://help.syncfusion.com/cr/document-processing/Syncfusion.XlsIO.IDataSort.html#Syncfusion_XlsIO_IDataSort_HasHeader) property of [IDataSort](https://help.syncfusion.com/cr/document-processing/Syncfusion.XlsIO.IDataSort.html) interface should be disabled. Please find the code snippet below.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Load data
  worksheet["A2"].Text = "banana";
  worksheet["A3"].Text = "Cherry";
  worksheet["A4"].Text = "Banana";
  worksheet["A5"].Text = "Apple";
  worksheet["A6"].Text = "cherry";
  worksheet["A7"].Text = "apple";

  worksheet["B2"].Number = 744;
  worksheet["B3"].Number = 5079;
  worksheet["B4"].Number = 1267;
  worksheet["B5"].Number = 1418;
  worksheet["B6"].Number = 4728;
  worksheet["B7"].Number = 943;

  worksheet["C2"].Number = 162;
  worksheet["C3"].Number = 1249;
  worksheet["C4"].Number = 1062;
  worksheet["C5"].Number = 756;
  worksheet["C6"].Number = 4547;
  worksheet["C7"].Number = 349;

  IDataSort sorter = workbook.CreateDataSorter();
  sorter.SortRange = worksheet["A2:C7"];
  ISortField sortField = sorter.SortFields.Add(0, SortOn.Values, OrderBy.Ascending);

  //Disable HasHeader
  sorter.HasHeader = false;

  sorter.Sort();
  worksheet.UsedRange.AutofitColumns();

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Load data
  worksheet["A2"].Text = "banana";
  worksheet["A3"].Text = "Cherry";
  worksheet["A4"].Text = "Banana";
  worksheet["A5"].Text = "Apple";
  worksheet["A6"].Text = "cherry";
  worksheet["A7"].Text = "apple";

  worksheet["B2"].Number = 744;
  worksheet["B3"].Number = 5079;
  worksheet["B4"].Number = 1267;
  worksheet["B5"].Number = 1418;
  worksheet["B6"].Number = 4728;
  worksheet["B7"].Number = 943;

  worksheet["C2"].Number = 162;
  worksheet["C3"].Number = 1249;
  worksheet["C4"].Number = 1062;
  worksheet["C5"].Number = 756;
  worksheet["C6"].Number = 4547;
  worksheet["C7"].Number = 349;

  IDataSort sorter = workbook.CreateDataSorter();
  sorter.SortRange = worksheet["A2:C7"];
  ISortField sortField = sorter.SortFields.Add(0, SortOn.Values, OrderBy.Ascending);

  //Disable HasHeader
  sorter.HasHeader = false;

  sorter.Sort();
  worksheet.UsedRange.AutofitColumns();
  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Load data
  worksheet("A2").Text = "banana"
  worksheet("A3").Text = "Cherry"
  worksheet("A4").Text = "Banana"
  worksheet("A5").Text = "Apple"
  worksheet("A6").Text = "cherry"
  worksheet("A7").Text = "apple"

  worksheet("B2").Number = 744
  worksheet("B3").Number = 5079
  worksheet("B4").Number = 1267
  worksheet("B5").Number = 1418
  worksheet("B6").Number = 4728
  worksheet("B7").Number = 943

  worksheet("C2").Number = 162
  worksheet("C3").Number = 1249
  worksheet("C4").Number = 1062
  worksheet("C5").Number = 756
  worksheet("C6").Number = 4547
  worksheet("C7").Number = 349

  Dim sorter As IDataSort = workbook.CreateDataSorter
  sorter.SortRange = worksheet("A2:C7")
  Dim sortField As ISortField = sorter.SortFields.Add(0, SortOn.Values, OrderBy.Ascending)

  'Disable HasHeader
  sorter.HasHeader = False

  sorter.Sort()
  worksheet.UsedRange.AutofitColumns()

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %} 
