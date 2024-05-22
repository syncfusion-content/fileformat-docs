---
title: Highlight Cells| Excel library | Syncfusion
description: In this section, you can learn how to apply highlight cells using conditional formatting in an Excel document with XlsIO
platform: file-formats
control: XlsIO
documentation: UG
---

# Highlight Cells

Highlight cell rules are powerful tools for data analysis and presentation, enhancing the ability to quickly interpret and act upon data within worksheets.

## Format Unique and Duplicate Values

Format unique and duplicate values of an Excel range using conditional formatting. The values, **Unique** and **Duplicate** of the enumeration [ExcelCFType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelCFType.html) helps to achieve the requirement.

The following code example illustrates how to format unique and duplicate values using conditional formatting.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];
  
  //Fill worksheet with data
  worksheet.Range["A1:B1"].Merge();
  worksheet.Range["A1:B1"].CellStyle.Font.RGBColor = Color.FromArgb(255, 102, 102, 255);
  worksheet.Range["A1:B1"].CellStyle.Font.Size = 14;
  worksheet.Range["A1:B1"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter;
  worksheet.Range["A1"].Text = "Global Internet Usage";
  worksheet.Range["A1:B1"].CellStyle.Font.Bold = true;
  
  worksheet.Range["A3:B21"].CellStyle.Font.RGBColor = Color.FromArgb(255, 64, 64, 64);
  worksheet.Range["A3:B3"].CellStyle.Font.Bold = true;
  worksheet.Range["B3"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignRight;
  
  worksheet.Range["A3"].Text = "Country";
  worksheet.Range["A4"].Text = "Northern America";
  worksheet.Range["A5"].Text = "Central America";
  worksheet.Range["A6"].Text = "The Caribbean";
  worksheet.Range["A7"].Text = "South America";
  worksheet.Range["A8"].Text = "Northern Europe";
  worksheet.Range["A9"].Text = "Eastern Europe";
  worksheet.Range["A10"].Text = "Western Europe";
  worksheet.Range["A11"].Text = "Southern Europe";
  worksheet.Range["A12"].Text = "Northern Africa";
  worksheet.Range["A13"].Text = "Eastern Africa";
  worksheet.Range["A14"].Text = "Middle Africa";
  worksheet.Range["A15"].Text = "Western Africa";
  worksheet.Range["A16"].Text = "Southern Africa";
  worksheet.Range["A17"].Text = "Central Asia";
  worksheet.Range["A18"].Text = "Eastern Asia";
  worksheet.Range["A19"].Text = "Southern Asia";
  worksheet.Range["A20"].Text = "SouthEast Asia";
  worksheet.Range["A21"].Text = "Oceania";    
  
  worksheet.Range["B3"].Text = "Usage";
  worksheet.Range["B4"].Value = "88%";
  worksheet.Range["B5"].Value = "61%";
  worksheet.Range["B6"].Value = "49%";
  worksheet.Range["B7"].Value = "68%";
  worksheet.Range["B8"].Value = "94%";
  worksheet.Range["B9"].Value = "74%";
  worksheet.Range["B10"].Value = "90%";
  worksheet.Range["B11"].Value = "77%";
  worksheet.Range["B12"].Value = "49%";
  worksheet.Range["B13"].Value = "27%";
  worksheet.Range["B14"].Value = "12%";
  worksheet.Range["B15"].Value = "39%";
  worksheet.Range["B16"].Value = "51%";
  worksheet.Range["B17"].Value = "50%";
  worksheet.Range["B18"].Value = "58%";
  worksheet.Range["B19"].Value = "36%";
  worksheet.Range["B20"].Value = "58%";
  worksheet.Range["B21"].Value = "69%";
  
  worksheet.SetColumnWidth(1, 23.45);
  worksheet.SetColumnWidth(2, 8.09);
  
  IConditionalFormats conditionalFormats =
  worksheet.Range["A4:B21"].ConditionalFormats;
  IConditionalFormat condition = conditionalFormats.AddCondition();
  
  //conditional format to set duplicate format type
  condition.FormatType = ExcelCFType.Duplicate;
  condition.BackColorRGB = Color.FromArgb(255, 255, 199, 206);
  
  //Saves the excel document to MemoryStream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];
  
  //Fill worksheet with data
  worksheet.Range["A1:B1"].Merge();
  worksheet.Range["A1:B1"].CellStyle.Font.RGBColor = Color.FromArgb(255, 102, 102, 255);
  worksheet.Range["A1:B1"].CellStyle.Font.Size = 14;
  worksheet.Range["A1:B1"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter;
  worksheet.Range["A1"].Text = "Global Internet Usage";
  worksheet.Range["A1:B1"].CellStyle.Font.Bold = true;
  
  worksheet.Range["A3:B21"].CellStyle.Font.RGBColor = Color.FromArgb(255, 64, 64, 64);
  worksheet.Range["A3:B3"].CellStyle.Font.Bold = true;
  worksheet.Range["B3"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignRight;
  
  worksheet.Range["A3"].Text = "Country";
  worksheet.Range["A4"].Text = "Northern America";
  worksheet.Range["A5"].Text = "Central America";
  worksheet.Range["A6"].Text = "The Caribbean";
  worksheet.Range["A7"].Text = "South America";
  worksheet.Range["A8"].Text = "Northern Europe";
  worksheet.Range["A9"].Text = "Eastern Europe";
  worksheet.Range["A10"].Text = "Western Europe";
  worksheet.Range["A11"].Text = "Southern Europe";
  worksheet.Range["A12"].Text = "Northern Africa";
  worksheet.Range["A13"].Text = "Eastern Africa";
  worksheet.Range["A14"].Text = "Middle Africa";
  worksheet.Range["A15"].Text = "Western Africa";
  worksheet.Range["A16"].Text = "Southern Africa";
  worksheet.Range["A17"].Text = "Central Asia";
  worksheet.Range["A18"].Text = "Eastern Asia";
  worksheet.Range["A19"].Text = "Southern Asia";
  worksheet.Range["A20"].Text = "SouthEast Asia";
  worksheet.Range["A21"].Text = "Oceania";    
  
  worksheet.Range["B3"].Text = "Usage";
  worksheet.Range["B4"].Value = "88%";
  worksheet.Range["B5"].Value = "61%";
  worksheet.Range["B6"].Value = "49%";
  worksheet.Range["B7"].Value = "68%";
  worksheet.Range["B8"].Value = "94%";
  worksheet.Range["B9"].Value = "74%";
  worksheet.Range["B10"].Value = "90%";
  worksheet.Range["B11"].Value = "77%";
  worksheet.Range["B12"].Value = "49%";
  worksheet.Range["B13"].Value = "27%";
  worksheet.Range["B14"].Value = "12%";
  worksheet.Range["B15"].Value = "39%";
  worksheet.Range["B16"].Value = "51%";
  worksheet.Range["B17"].Value = "50%";
  worksheet.Range["B18"].Value = "58%";
  worksheet.Range["B19"].Value = "36%";
  worksheet.Range["B20"].Value = "58%";
  worksheet.Range["B21"].Value = "69%";
  
  worksheet.SetColumnWidth(1, 23.45);
  worksheet.SetColumnWidth(2, 8.09);
  
  IConditionalFormats conditionalFormats =
  worksheet.Range["A4:B21"].ConditionalFormats;
  IConditionalFormat condition = conditionalFormats.AddCondition();
  
  //conditional format to set duplicate format type
  condition.FormatType = ExcelCFType.Duplicate;
  condition.BackColorRGB = Color.FromArgb(255, 255, 199, 206);
  
  //Saves the Excel
  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)
  
  'Fill worksheet with data
  worksheet.Range("A1:B1").Merge()
  worksheet.Range("A1:B1").CellStyle.Font.RGBColor = Color.FromArgb(255, 102, 102, 255)
  worksheet.Range("A1:B1").CellStyle.Font.Size = 14
  worksheet.Range("A1:B1").CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter
  worksheet.Range("A1").Text = "Global Internet Usage"
  
  worksheet.Range("A1:B1").CellStyle.Font.Bold = True
  worksheet.Range("A3:B21").CellStyle.Font.RGBColor = Color.FromArgb(255, 64, 64, 64)
  worksheet.Range("A3:B3").CellStyle.Font.Bold = True
  worksheet.Range("B3").CellStyle.HorizontalAlignment = ExcelHAlign.HAlignRight
  
  worksheet.Range("A3").Text = "Country"
  worksheet.Range("A4").Text = "Northern America"
  worksheet.Range("A5").Text = "Central America"
  worksheet.Range("A6").Text = "The Caribbean"
  worksheet.Range("A7").Text = "South America"
  worksheet.Range("A8").Text = "Northern Europe"
  worksheet.Range("A9").Text = "Eastern Europe"
  worksheet.Range("A10").Text = "Western Europe"
  worksheet.Range("A11").Text = "Southern Europe"
  worksheet.Range("A12").Text = "Northern Africa"
  worksheet.Range("A13").Text = "Eastern Africa"
  worksheet.Range("A14").Text = "Middle Africa"
  worksheet.Range("A15").Text = "Western Africa"
  worksheet.Range("A16").Text = "Southern Africa"
  worksheet.Range("A17").Text = "Central Asia"
  worksheet.Range("A18").Text = "Eastern Asia"
  worksheet.Range("A19").Text = "Southern Asia"
  worksheet.Range("A20").Text = "SouthEast Asia"
  worksheet.Range("A21").Text = "Oceania"
  
  worksheet.Range("B3").Text = "Usage"
  worksheet.Range("B4").Value = "88%"
  worksheet.Range("B5").Value = "61%"
  worksheet.Range("B6").Value = "49%"
  worksheet.Range("B7").Value = "68%"
  worksheet.Range("B8").Value = "94%"
  worksheet.Range("B9").Value = "74%"
  worksheet.Range("B10").Value = "90%"
  worksheet.Range("B11").Value = "77%"
  worksheet.Range("B12").Value = "49%"
  worksheet.Range("B13").Value = "27%"
  worksheet.Range("B14").Value = "12%"
  worksheet.Range("B15").Value = "39%"
  worksheet.Range("B16").Value = "51%"
  worksheet.Range("B17").Value = "50%"
  worksheet.Range("B18").Value = "58%"
  worksheet.Range("B19").Value = "36%"
  worksheet.Range("B20").Value = "58%"
  worksheet.Range("B21").Value = "69%"
  
  worksheet.SetColumnWidth(1, 23.45)
  worksheet.SetColumnWidth(2, 8.09)
  
  'conditional format to set duplicate format type
  Dim conditionalFormats As IConditionalFormats =
  worksheet.Range("A4:B21").ConditionalFormats
  Dim condition As IConditionalFormat = conditionalFormats.AddCondition()
  condition.FormatType = ExcelCFType.Duplicate
  condition.BackColorRGB = Color.FromArgb(255, 255, 199, 206)
  
  'Saves the Excel
  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format unique and duplicate values in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Conditional%20Formatting/Unique%20and%20Duplicate).

By executing the program, you will get the Excel file as below

![unique and duplicate conditional Formatting](../Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img3.jpg).