---
title: How to create a sparkline from a named range | XlsIO | Syncfusion
description: This page demonstrates to create a sparkline from a named range using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to create a sparkline from a named range?

You can create a [sparkline](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#sparkline) from a [named range](https://help.syncfusion.com/file-formats/xlsio/faq#how-to-use-named-ranges-with-xlsio) with the help of the following code.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add sample data
  worksheet["A1"].Number = 6911;
  worksheet["B1"].Number = 8261;
  worksheet["C1"].Number = 812;
  worksheet["D1"].Number = 166;

  //Add SparklineGroups
  ISparklineGroup sparklineGroup = worksheet.SparklineGroups.Add();

  //Add SparkLineType
  sparklineGroup.SparklineType = SparklineType.Line;
  sparklineGroup.MarkersColor = Color.BlueViolet;

  //Add sparklines
  ISparklines sparklines = sparklineGroup.Add();

  //Create named ranges
  IName name1 = workbook.Names.Add("Data_Range");
  name1.RefersToRange = worksheet.Range["A1:D1"];
  IRange dataRange = worksheet.Range["Data_Range"];

  IName name2 = workbook.Names.Add("Sparkline_Range");
  name2.RefersToRange = worksheet.Range["E1"];                
  IRange referenceRange = worksheet.Range["Sparkline_Range"];

  //Add a sparkline
  sparklines.Add(dataRange, referenceRange);

  workbook.SaveAs("SparklineFromNamedRange.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Add sample data
  worksheet("A1").Number = 6911
  worksheet("B1").Number = 8261
  worksheet("C1").Number = 812
  worksheet("D1").Number = 166

  'Add SparklineGroups
  Dim sparklineGroup As ISparklineGroup = worksheet.SparklineGroups.Add()

  'Add SparkLineType
  sparklineGroup.SparklineType = SparklineType.Line
  sparklineGroup.MarkersColor = Color.BlueViolet

  'Add sparklines
  Dim sparklines As ISparklines = sparklineGroup.Add()

  'Create named ranges
  Dim name1 As IName = workbook.Names.Add("Data_Range")
  name1.RefersToRange = worksheet.Range("A1:D1")
  Dim dataRange As IRange = worksheet.Range("Data_Range")

  Dim name2 As IName = workbook.Names.Add("Sparkline_Range")
  name2.RefersToRange = worksheet.Range("E1")
  Dim referenceRange As IRange = worksheet.Range("Sparkline_Range")

  'Add a sparkline
  sparklines.Add(dataRange, referenceRange)

  workbook.SaveAs("SparklineFromNamedRange.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add sample data
  worksheet["A1"].Number = 6911;
  worksheet["B1"].Number = 8261;
  worksheet["C1"].Number = 812;
  worksheet["D1"].Number = 166;

  //Add SparklineGroups
  ISparklineGroup sparklineGroup = worksheet.SparklineGroups.Add();

  //Add SparkLineType
  sparklineGroup.SparklineType = SparklineType.Line;
  sparklineGroup.MarkersColor = Color.FromArgb(255, 138, 43, 226);

  //Add sparklines
  ISparklines sparklines = sparklineGroup.Add();

  //Create named ranges
  IName name1 = workbook.Names.Add("Data_Range");
  name1.RefersToRange = worksheet.Range["A1:D1"];
  IRange dataRange = worksheet.Range["Data_Range"];

  IName name2 = workbook.Names.Add("Sparkline_Range");
  name2.RefersToRange = worksheet.Range["E1"];
  IRange referenceRange = worksheet.Range["Sparkline_Range"];

  //Add a sparkline
  sparklines.Add(dataRange, referenceRange);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "SparklineFromNamedRange";
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
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add sample data
  worksheet["A1"].Number = 6911;
  worksheet["B1"].Number = 8261;
  worksheet["C1"].Number = 812;
  worksheet["D1"].Number = 166;

  //Add SparklineGroups
  ISparklineGroup sparklineGroup = worksheet.SparklineGroups.Add();

  //Add SparkLineType
  sparklineGroup.SparklineType = SparklineType.Line;
  sparklineGroup.MarkersColor = Color.BlueViolet;

  //Add sparklines
  ISparklines sparklines = sparklineGroup.Add();

  //Create named ranges
  IName name1 = workbook.Names.Add("Data_Range");
  name1.RefersToRange = worksheet.Range["A1:D1"];
  IRange dataRange = worksheet.Range["Data_Range"];

  IName name2 = workbook.Names.Add("Sparkline_Range");
  name2.RefersToRange = worksheet.Range["E1"];
  IRange referenceRange = worksheet.Range["Sparkline_Range"];

  //Add a sparkline
  sparklines.Add(dataRange, referenceRange);

  FileStream stream = new FileStream("SparklineFromNamedRange.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  workbook.Close();
  excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add sample data
  worksheet["A1"].Number = 6911;
  worksheet["B1"].Number = 8261;
  worksheet["C1"].Number = 812;
  worksheet["D1"].Number = 166;

  //Add SparklineGroups
  ISparklineGroup sparklineGroup = worksheet.SparklineGroups.Add();

  //Add SparkLineType
  sparklineGroup.SparklineType = SparklineType.Line;
  sparklineGroup.MarkersColor = Color.BlueViolet;

  //Add sparklines
  ISparklines sparklines = sparklineGroup.Add();

  //Create named ranges
  IName name1 = workbook.Names.Add("Data_Range");
  name1.RefersToRange = worksheet.Range["A1:D1"];
  IRange dataRange = worksheet.Range["Data_Range"];

  IName name2 = workbook.Names.Add("Sparkline_Range");
  name2.RefersToRange = worksheet.Range["E1"];
  IRange referenceRange = worksheet.Range["Sparkline_Range"];

  //Add a sparkline
  sparklines.Add(dataRange, referenceRange);

  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the stream as a file in the device and invoke it for viewing
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("SparklineFromNamedRange.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

## See Also

* [How to create a Chart with a discontinuous range?](how-to-create-a-chart-with-a-discontinuous-range)
* [How to create and open Excel Template files by using XlsIO?](how-to-create-and-open-excel-template-files-by-using-xlsio)
* [How to create sparkline?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#sparkline)
* [How to create named range in Excel?](https://help.syncfusion.com/file-formats/xlsio/migrate-from-office-automation-to-syncfusion-xlsio/create-named-range-in-excel)
* [How to define names?](https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#defined-names)
* [How to use named ranges in formulas?](https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#named-ranges-in-formulas)
