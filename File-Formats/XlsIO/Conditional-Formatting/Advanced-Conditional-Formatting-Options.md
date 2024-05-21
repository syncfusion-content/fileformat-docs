---
title: Advanced Conditional Formatting Options| Excel library | Syncfusion
description: In this section, you can learn how to use advanced conditional formatting options in Excel using XlsIO
platform: file-formats
control: XlsIO
documentation: UG
---
# Advanced Conditional Formatting Options

The various types of advanced conditional formatting options are:

* Formatting unique and duplicate values
* Format top or bottom values
* Format above or below average values

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

![unique and duplicate conditional Formatting](Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img3.jpg)

## Format Top or Bottom Values

Top/Bottom rule in conditional formatting is used to highlight the top or bottom ranked cells in a data range. Top/Bottom conditional formatting rule can be created and customized using the [ITopBottom](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITopBottom.html) interface in XlsIO.

The properties of **ITopBottom** interface are:

* **Type** - Specifies whether the rank is evaluated from the top or bottom.
* **Percent** - Specifies whether the rank is determined by a percentage value.
* **Rank** - Specifies the maximum number or percentage of cells to be highlighted.

The following screenshot represents the input template of conditional formatting.

![Conditional formatting input template](/Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img4.png)

### Top/Bottom ‘n’ rank values

The following code example illustrates how to format top 10 rank values from the given data range using [ITopBottom](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITopBottom.html) [Type](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITopBottom.html#Syncfusion_XlsIO_ITopBottom_Type) and [Rank](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITopBottom.html#Syncfusion_XlsIO_ITopBottom_Rank) properties in XlsIO.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("CFTemplate.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  
  //Applying conditional formatting to "N6:N35".
  IConditionalFormats formats = worksheet.Range["N6:N35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();
  
  //Applying top or bottom rule in the conditional formatting.
  format.FormatType = ExcelCFType.TopBottom;
  ITopBottom topBottom = format.TopBottom;
  
  //Set type as Top for TopBottom rule.
  topBottom.Type = ExcelCFTopBottomType.Top;
  
  //Set rank value for the TopBottom rule.
  topBottom.Rank = 10;
  
  //Set color for Conditional Formattting.
  format.BackColorRGB = System.Drawing.Color.FromArgb(51, 153, 102);
  
  //Saves the excel document to MemoryStream
  FileStream stream = new FileStream("TopBottom.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = workbook = application.Workbooks.Open("CFTemplate.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];
  
  //Applying conditional formatting to "N6:N35".
  IConditionalFormats formats = worksheet.Range["N6:N35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();
  
  //Applying top or bottom rule in the conditional formatting.
  format.FormatType = ExcelCFType.TopBottom;
  ITopBottom topBottom = format.TopBottom;
  
  //Set type as Top for TopBottom rule.
  topBottom.Type = ExcelCFTopBottomType.Top;
  
  //Set rank value for the TopBottom rule.
  topBottom.Rank = 10;
  
  //Set color for Conditional Formattting.
  format.BackColorRGB = System.Drawing.Color.FromArgb(51, 153, 102);
  
  //Saves the Excel
  workbook.SaveAs("TopBottom.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("CFTemplate.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Applying conditional formatting to "N6:N35".
  Dim formats As IConditionalFormats = worksheet.Range("N6:N35").ConditionalFormats
  Dim format As IConditionalFormat = formats.AddCondition()

  'Set type as Top for TopBottom rule.
  format.FormatType = ExcelCFType.TopBottom
  Dim topBottom As ITopBottom = format.TopBottom

  'Set rank value for the TopBottom rule.
  topBottom.Type = ExcelCFTopBottomType.Top

  'Set rank value for the TopBottom rule.
  topBottom.Rank = 10

  'Set color for Conditional Formattting.
  format.BackColorRGB = System.Drawing.Color.FromArgb(51, 153, 102)

  'Saves the Excel
  workbook.SaveAs("TopBottom.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format top and bottom rank values in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Conditional%20Formatting/Top%20to%20Bottom%20Rank).

By executing the program, you will get the Excel file as below

![Top or Bottom conditional format](/Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img6.png)

N> **ITopBottom** **Rank** value should be in a range between 1 and 1000.

### Top/Bottom ‘n’% rank values

The following code example illustrates how to format top 50 percentage rank values from the given data range using [ITopBottom](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITopBottom.html) [Type](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITopBottom.html#Syncfusion_XlsIO_ITopBottom_Type), [Rank](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITopBottom.html#Syncfusion_XlsIO_ITopBottom_Rank) and [Percent](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITopBottom.html#Syncfusion_XlsIO_ITopBottom_Percent) properties in XlsIO

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("CFTemplate.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Applying conditional formatting to "N6:N35".
  IConditionalFormats formats = worksheet.Range["N6:N35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();

  //Applying top or bottom rule in the conditional formatting.
  format.FormatType = ExcelCFType.TopBottom;
  ITopBottom topBottom = format.TopBottom;

  //Set type as Bottom for TopBottom rule.
  topBottom.Type = ExcelCFTopBottomType.Bottom;

  //Set true to Percent property for TopBottom rule.
  topBottom.Percent = true;

  //Set rank value for the TopBottom rule.
  topBottom.Rank = 50;

  //Set color for Conditional Formattting.
  format.BackColorRGB = System.Drawing.Color.FromArgb(51, 153, 102);

  //Saves the excel document to MemoryStream
  FileStream stream = new FileStream("TopBottom.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = workbook = application.Workbooks.Open("CFTemplate.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Applying conditional formatting to "N6:N35".
  IConditionalFormats formats = worksheet.Range["N6:N35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();

  //Applying top or bottom rule in the conditional formatting.
  format.FormatType = ExcelCFType.TopBottom;
  ITopBottom topBottom = format.TopBottom;

  //Set type as Bottom for TopBottom rule.
  topBottom.Type = ExcelCFTopBottomType.Bottom;

  //Set true to Percent property for TopBottom rule.
  topBottom.Percent = true;

  //Set rank value for the TopBottom rule.
  topBottom.Rank = 50;

  //Set color for Conditional Formattting.
  format.BackColorRGB = System.Drawing.Color.FromArgb(51, 153, 102);

  //Saves the Excel
  workbook.SaveAs("TopBottom.xlsx");   
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("CFTemplate.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Applying conditional formatting to "N6:N35".
  Dim formats As IConditionalFormats = worksheet.Range("N6:N35").ConditionalFormats
  Dim format As IConditionalFormat = formats.AddCondition()

  'Set type as Top for TopBottom rule.
  format.FormatType = ExcelCFType.TopBottom
  Dim topBottom As ITopBottom = format.TopBottom

  'Set type as Bottom for TopBottom rule.
  topBottom.Type = ExcelCFTopBottomType.Bottom

  'Set true to Percent property for TopBottom rule.
  topBottom.Percent = true

  Set rank value for the TopBottom rule.
  topBottom.Rank = 50

  'Set color for Conditional Formattting.
  format.BackColorRGB = System.Drawing.Color.FromArgb(51, 153, 102)

  'Saves the Excel
  workbook.SaveAs("TopBottom.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format top and bottom rank percentage in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Conditional%20Formatting/Top%20To%20Bottom%20Percent).

By executing the program, you will get the Excel file as below

![Top or Bottom conditional format](/Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img6.png)

N> **ITopBottom** **Rank** value should be in a range between 1 and 100 when set true to **Percent** property.

## Format Above or Below Average Values

Above/Below average rule in conditional formatting is used to highlight the cells which contains above/below the average values in a data range. Top/Bottom conditional formatting rule can be created and customized using the [IAboveBelowAverage](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IAboveBelowAverage.html) interface in XlsIO.

The properties of **IAboveBelowAverage** are:

* **AverageType** - Specifies whether the conditional formatting rule looks for cell values that are above average or below average or standard deviation.
* **StdDevValue** - Specifies standard deviation number for **AboveBelowAverage** conditional formatting rule.

The following code example illustrates shows how to format a range with values that are below average using **IAboveBelowAverage** [AverageType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IAboveBelowAverage.html#Syncfusion_XlsIO_IAboveBelowAverage_AverageType) property in XlsIO.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("CFTemplate.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Applying conditional formatting to "M6:M35"
  IConditionalFormats formats = worksheet.Range["M6:M35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();

  //Applying above or below average rule in the conditional formatting
  format.FormatType = ExcelCFType.AboveBelowAverage;
  IAboveBelowAverage aboveBelowAverage = format.AboveBelowAverage;

  //Set AverageType as Below for AboveBelowAverage rule.
  aboveBelowAverage.AverageType = ExcelCFAverageType.Below;

  //Set color for Conditional Formattting.
  format.FontColorRGB = System.Drawing.Color.FromArgb(255, 255, 255);
  format.BackColorRGB = System.Drawing.Color.FromArgb(166, 59, 38);

  //Saves the excel document to MemoryStream
  FileStream stream = new FileStream("AboveBelowAverage.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = workbook = application.Workbooks.Open("CFTemplate.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Applying conditional formatting to "M6:M35"
  IConditionalFormats formats = worksheet.Range["M6:M35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();

  //Applying above or below average rule in the conditional formatting
  format.FormatType = ExcelCFType.AboveBelowAverage;
  IAboveBelowAverage aboveBelowAverage = format.AboveBelowAverage;

  //Set AverageType as Below for AboveBelowAverage rule.
  aboveBelowAverage.AverageType = ExcelCFAverageType.Below;

  //Set color for Conditional Formattting.
  format.FontColorRGB = System.Drawing.Color.FromArgb(255, 255, 255);
  format.BackColorRGB = System.Drawing.Color.FromArgb(166, 59, 38);

  //Saves the Excel
  workbook.SaveAs("AboveBelowAverage.xlsx");   
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("CFTemplate.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Applying conditional formatting to "M6:M35"
  IConditionalFormats formats = worksheet.Range["M6:M35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();

  'Applying above or below average rule in the conditional formatting
  format.FormatType = ExcelCFType.AboveBelowAverage;
  IAboveBelowAverage aboveBelowAverage = format.AboveBelowAverage;

  'Set AverageType as Below for AboveBelowAverage rule.
  aboveBelowAverage.AverageType = ExcelCFAverageType.Below;

  'Set color for Conditional Formattting.
  format.FontColorRGB = System.Drawing.Color.FromArgb(255, 255, 255);
  format.BackColorRGB = System.Drawing.Color.FromArgb(166, 59, 38);

  'Saves the Excel
  workbook.SaveAs("AboveBelowAverage.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format above and below average values in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Conditional%20Formatting/Above%20and%20Below%20Average).

By executing the program, you will get the Excel file as below

![Above or Below Average conditional format](/Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img7.png)

### Above or Below Standard Deviation values

The following code example illustrates how to format a range with values above standard deviation, using [IAboveBelowAverage](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IAboveBelowAverage.html) [AverageType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IAboveBelowAverage.html#Syncfusion_XlsIO_IAboveBelowAverage_AverageType) and [StdDevValue](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IAboveBelowAverage.html#Syncfusion_XlsIO_IAboveBelowAverage_StdDevValue) properties in XlsIO.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("CFTemplate.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Applying conditional formatting to "M6:M35"
  IConditionalFormats formats = worksheet.Range["M6:M35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();

  //Applying above or below average rule in the conditional formatting
  format.FormatType = ExcelCFType.AboveBelowAverage;
  IAboveBelowAverage aboveBelowAverage = format.AboveBelowAverage;

  //Set AverageType as AboveStdDev for AboveBelowAverage rule.
  aboveBelowAverage.AverageType = ExcelCFAverageType.AboveStdDev;

  //Set value to StdDevValue property for AboveBelowAverage rule.
  aboveBelowAverage.StdDevValue = 1;

  //Set color for Conditional Formattting.
  format.FontColorRGB = System.Drawing.Color.FromArgb(255, 255, 255);
  format.BackColorRGB = System.Drawing.Color.FromArgb(166, 59, 38);

  //Saves the excel document to MemoryStream
  FileStream stream = new FileStream("AboveBelowAverage.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = workbook = application.Workbooks.Open("CFTemplate.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Applying conditional formatting to "M6:M35"
  IConditionalFormats formats = worksheet.Range["M6:M35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();

  //Applying above or below average rule in the conditional formatting
  format.FormatType = ExcelCFType.AboveBelowAverage;
  IAboveBelowAverage aboveBelowAverage = format.AboveBelowAverage;

  //Set AverageType as AboveStdDev for AboveBelowAverage rule.
  aboveBelowAverage.AverageType = ExcelCFAverageType.AboveStdDev;

  //Set value to StdDevValue property for AboveBelowAverage rule.
  aboveBelowAverage.StdDevValue = 1;

  //Set color for Conditional Formattting.
  format.FontColorRGB = System.Drawing.Color.FromArgb(255, 255, 255);
  format.BackColorRGB = System.Drawing.Color.FromArgb(166, 59, 38);

  //Saves the Excel
  workbook.SaveAs("AboveBelowAverage.xlsx");   
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("CFTemplate.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)
	
  'Applying conditional formatting to "M6:M35"
  IConditionalFormats formats = worksheet.Range["M6:M35"].ConditionalFormats;
  IConditionalFormat format = formats.AddCondition();

  'Applying above or below average rule in the conditional formatting
  format.FormatType = ExcelCFType.AboveBelowAverage;
  IAboveBelowAverage aboveBelowAverage = format.AboveBelowAverage;

  'Set AverageType as AboveStdDev for AboveBelowAverage rule.
  aboveBelowAverage.AverageType = ExcelCFAverageType.AboveStdDev

  'Set value to StdDevValue property for AboveBelowAverage rule.
  aboveBelowAverage.StdDevValue = 1

  'Set color for Conditional Formattting.
  format.FontColorRGB = System.Drawing.Color.FromArgb(255, 255, 255);
  format.BackColorRGB = System.Drawing.Color.FromArgb(166, 59, 38);

  'Saves the Excel
  workbook.SaveAs("AboveBelowAverage.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format above and below standard deviation values in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Conditional%20Formatting/Above%20and%20Below%20Standard%20Deviation).

By executing the program, you will get the Excel file as below

![Above or Below Average conditional format](/Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img8.png)

N> **IAboveBelowAverage** **StdDevValue** can be applied only if the **AverageType** is **AboveStdDev** or **BelowStdDev**. The **StdDevValue** value should be in a range between 1 and 3.