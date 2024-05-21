---
title: Conditional Formatting | Excel library | Syncfusion
description: In this section, you can learn how to create and use conditional formatting operations in an Excel document using XlsIO
platform: file-formats
control: XlsIO
documentation: UG
---
# Working with Conditional Formatting

Conditional formatting allows to format the contents of a cell dynamically. This can be defined and applied in XlsIO through the [IConditionalFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IConditionalFormat.html) interface.

## Create a Conditional Format 

The [IConditionalFormats](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IConditionalFormats.html) represents a collection of conditional formats for a single [IRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html). One or more conditional formats can be added to the range as follows.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Applying conditional formatting to "A1"
IConditionalFormats condition = worksheet.Range["A1"].ConditionalFormats;
IConditionalFormat condition1 = condition.AddCondition();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Applying conditional formatting to "A1"
IConditionalFormats condition = worksheet.Range["A1"].ConditionalFormats;
IConditionalFormat condition1 = condition.AddCondition();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Applying conditional formatting to "A1"
Dim condition As IConditionalFormats = worksheet.Range("A1").ConditionalFormats
Dim condition1 As IConditionalFormat = condition.AddCondition()
{% endhighlight %}
{% endtabs %}

The target range should meet the criteria, which is set using the **IConditionalFormat** interface. The  desired format type is set through the [ExcelCFType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelCFType.html) enumerator, which are the supported conditional format types in XlsIO. Refer to the following code.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Represents conditional format rule that the value in target range should be between 10 and 20
condition1.FormatType = ExcelCFType.CellValue;
condition1.Operator = ExcelComparisonOperator.Between;
condition1.FirstFormula = "10";
condition1.SecondFormula = "20";
worksheet.Range["A1"].Text = "Enter a number between 10 and 20";
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Represents conditional format rule that the value in target range should be between 10 and 20
condition1.FormatType = ExcelCFType.CellValue;
condition1.Operator = ExcelComparisonOperator.Between;
condition1.FirstFormula = "10";
condition1.SecondFormula = "20";
worksheet.Range["A1"].Text = "Enter a number between 10 and 20";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Represents conditional format rule that the value in target range should be between 10 and 20
condition1.FormatType = ExcelCFType.CellValue
condition1.Operator = ExcelComparisonOperator.Between
condition1.FirstFormula = "10"
condition1.SecondFormula = "20"
worksheet.Range("A1").Text = "Enter a number between 10 and 20"
{% endhighlight %}
{% endtabs %}

When the criteria set for the target range is satisfied, the defined formats (like the one below) are applied in the order of priority. For more details about conditional format priority, see [Manage conditional formatting rule precedence](https://support.microsoft.com/en-us/office/video-manage-conditional-formatting-6b69364e-dc79-4fe4-bd94-1883e40848f9).

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Setting format properties to be applied when the above condition is met
condition1.BackColor = ExcelKnownColors.Light_orange;
condition1.IsBold = true;
condition1.IsItalic = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Setting format properties to be applied when the above condition is met
condition1.BackColor = ExcelKnownColors.Light_orange;
condition1.IsBold = true;
condition1.IsItalic = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Setting format properties to be applied when the above condition is met
condition1.BackColor = ExcelKnownColors.Light_orange
condition1.IsBold = True
condition1.IsItalic = True
{% endhighlight %}
{% endtabs %}

The following code example illustrates how to create and applies various different conditional formats for different ranges in XlsIO.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Applying conditional formatting to "A1"
  IConditionalFormats condition = worksheet.Range["A1"].ConditionalFormats;
  IConditionalFormat condition1 = condition.AddCondition();

  //Represents conditional format rule that the value in target range should be between 10 and 20
  condition1.FormatType = ExcelCFType.CellValue;
  condition1.Operator = ExcelComparisonOperator.Between;
  condition1.FirstFormula = "10";
  condition1.SecondFormula = "20";
  worksheet.Range["A1"].Text = "Enter a number between 10 and 20";

  //Setting back color and font style to be applied for target range
  condition1.BackColor = ExcelKnownColors.Light_orange;
  condition1.IsBold = true;
  condition1.IsItalic = true;

  //Applying conditional formatting to "A3"
  condition = worksheet.Range["A3"].ConditionalFormats;
  IConditionalFormat condition2 = condition.AddCondition();

  //Represents conditional format rule that the cell value should be 1000
  condition2.FormatType = ExcelCFType.CellValue;
  condition2.Operator = ExcelComparisonOperator.Equal;
  condition2.FirstFormula = "1000";
  worksheet.Range["A3"].Text = "Enter the Number as 1000";

  //Setting fill pattern and back color to target range
  condition2.FillPattern = ExcelPattern.LightUpwardDiagonal;
  condition2.BackColor = ExcelKnownColors.Yellow;

  //Applying conditional formatting to "A5"
  condition = worksheet.Range["A5"].ConditionalFormats;
  IConditionalFormat condition3 = condition.AddCondition();

  //Setting conditional format rule that the cell value for target range should be less than or equal to 1000
  condition3.FormatType = ExcelCFType.CellValue;
  condition3.Operator = ExcelComparisonOperator.LessOrEqual;
  condition3.FirstFormula = "1000";
  worksheet.Range["A5"].Text = "Enter a Number which is less than or equal to 1000";

  //Setting back color to target range
  condition3.BackColor = ExcelKnownColors.Light_green;

  //Saving the workbook as stream
  FileStream stream = new FileStream("ConditionalFormatting.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Applying conditional formatting to "A1"
  IConditionalFormats condition = worksheet.Range["A1"].ConditionalFormats;
  IConditionalFormat condition1 = condition.AddCondition();

  //Represents conditional format rule that the value in target range should be between 10 and 20
  condition1.FormatType = ExcelCFType.CellValue;
  condition1.Operator = ExcelComparisonOperator.Between;
  condition1.FirstFormula = "10";
  condition1.SecondFormula = "20";
  worksheet.Range["A1"].Text = "Enter a number between 10 and 20";

  //Setting back color and font style to be applied for target range
  condition1.BackColor = ExcelKnownColors.Light_orange;
  condition1.IsBold = true;
  condition1.IsItalic = true;

  //Applying conditional formatting to "A3"
  condition = worksheet.Range["A3"].ConditionalFormats;
  IConditionalFormat condition2 = condition.AddCondition();

  //Represents conditional format rule that the cell value should be 1000
  condition2.FormatType = ExcelCFType.CellValue;
  condition2.Operator = ExcelComparisonOperator.Equal;
  condition2.FirstFormula = "1000";
  worksheet.Range["A3"].Text = "Enter the Number as 1000";

  //Setting fill pattern and back color to target range
  condition2.FillPattern = ExcelPattern.LightUpwardDiagonal;
  condition2.BackColor = ExcelKnownColors.Yellow;

  //Applying conditional formatting to "A5"
  condition = worksheet.Range["A5"].ConditionalFormats;
  IConditionalFormat condition3 = condition.AddCondition();

  //Setting conditional format rule that the cell value for target range should be less than or equal to 1000
  condition3.FormatType = ExcelCFType.CellValue;
  condition3.Operator = ExcelComparisonOperator.LessOrEqual;
  condition3.FirstFormula = "1000";
  worksheet.Range["A5"].Text = "Enter a Number which is less than or equal to 1000";

  //Setting back color to target range
  condition3.BackColor = ExcelKnownColors.Light_green;

  workbook.SaveAs("ConditionalFormatting.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Applying conditional formatting to "A1"
  Dim condition As IConditionalFormats = worksheet.Range("A1").ConditionalFormats
  Dim condition1 As IConditionalFormat = condition.AddCondition()

  'Represents conditional format rule that the value in target range should be between 10 and 20
  condition1.FormatType = ExcelCFType.CellValue
  condition1.Operator = ExcelComparisonOperator.Between
  condition1.FirstFormula = "10"
  condition1.SecondFormula = "20"
  worksheet.Range("A1").Text = "Enter a number between 10 and 20"

  'Setting back color and font style to be applied for target range
  condition1.BackColor = ExcelKnownColors.Light_orange
  condition1.IsBold = True
  condition1.IsItalic = True

  'Applying conditional formatting to "A3"
  condition = worksheet.Range("A3").ConditionalFormats
  Dim condition2 As IConditionalFormat = condition.AddCondition()

  'Represents conditional format rule that the cell value should be 1000
  condition2.FormatType = ExcelCFType.CellValue
  condition2.Operator = ExcelComparisonOperator.Equal
  condition2.FirstFormula = "1000"
  worksheet.Range("A3").Text = "Enter the Number as 1000"

  'Setting fill pattern and back color to target range
  condition2.FillPattern = ExcelPattern.LightUpwardDiagonal
  condition2.BackColor = ExcelKnownColors.Yellow

  'Applying conditional formatting to "A5"
  condition = worksheet.Range("A5").ConditionalFormats
  Dim condition3 As IConditionalFormat = condition.AddCondition()

  'Setting conditional format rule that the cell value for target range should be less than or equal to 1000
  condition3.FormatType = ExcelCFType.CellValue
  condition3.Operator = ExcelComparisonOperator.LessOrEqual
  condition3.FirstFormula = "1000"
  worksheet.Range("A5").Text = "Enter a Number which is less than or equal to 1000"

  'Setting back color to target range
  condition3.BackColor = ExcelKnownColors.Light_green

  workbook.SaveAs("ConditionalFormatting.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to create conditional formatting in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Conditional%20Formatting/Create%20Conditional%20Format).

N> Excel allows the addition of a maximum of three conditions for the same cell in the Biff8 format and XlsIO. However, this restriction is removed from the Excel 2007 formats.

N> The conditional formats for a single range should be added in descending order in XlsIO.

By executing the program, you will get the Excel file as below

![working with conditional format](Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img1.jpeg)

## Reading an Existing Conditional Format

XlsIO also reads conditional formats from an existing Excel workbook. 

The following code example illustrates how to read existing conditional formatting.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Read conditional formatting settings 
  string formatType = worksheet.Range["A1"].ConditionalFormats[0].FormatType.ToString();
  string cfOperator = worksheet.Range["A1"].ConditionalFormats[0].Operator.ToString();
  string backColor = worksheet.Range["A1"].ConditionalFormats[0].BackColor.ToString();

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
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Read conditional formatting settings 
  string formatType = worksheet.Range["A1"].ConditionalFormats[0].FormatType.ToString();
  string cfOperator = worksheet.Range["A1"].ConditionalFormats[0].Operator.ToString();
  string backColor = worksheet.Range["A1"].ConditionalFormats[0].BackColor.ToString();

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Read conditional formatting settings
  Dim formatType As String = worksheet.Range("A1").ConditionalFormats(0).FormatType.ToString()
  Dim cfOperator As String = worksheet.Range("A1").ConditionalFormats(0).Operator.ToString()
  Dim backColor As String = worksheet.Range("A1").ConditionalFormats(0).BackColor.ToString()

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to read conditional formatting in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Conditional%20Formatting/Read%20Conditional%20Format).

## Advanced Conditional Formatting Options

Advanced conditional formatting options encompass techniques beyond basic color or font changes, such as formatting **unique/duplicate values**, **top/bottom ranked values**, and values **above or below standard deviation**, to visually highlight specific data patterns or outliers based on user-defined criteria.

These methods make it easier to understand data by using custom formatting to highlight important patterns or unusual values, like unique numbers, top or bottom rankings, and deviations from the norm.

### Formatting unique and duplicating values

This involves applying formatting styles to cells or data entries that are either unique (occurring only once in the dataset) or duplicate (repeating multiple times). It helps in visually distinguishing between unique and repetitive information. For further information, click [here]().

### Format top and bottom values

#### Top/Bottom n rank values

This refers to formatting the cells containing the highest or lowest n values in the dataset, based on their rank.

#### Top/Bottom n% rank values

This refers to formatting cells containing the top or bottom n% of values, similar to the previous point.

For further information, click [here]().

### Format above or below values

This involves applying formatting to cells that contain values either above or below a specified threshold. This helps in visually identifying data points that exceed or fall short of certain benchmarks.

#### Format above or below standard deviation values
This refers to applying formatting to cells containing values that are either above or below a certain number of standard deviations from the mean (average) of the dataset. Formatting cells based on standard deviation helps highlight data points that significantly deviate from the average, which can be useful in identifying outliers or understanding the distribution of data.

For further information, click [here]().

## Formula usage in conditional formatting

### Using FormulaR1C1 Property in Conditional Formats

This involves using custom formulas with the R1C1 reference style for conditional formatting, allowing for complex and flexible rules that adapt to different data ranges and criteria.

For further information, click [here]().

## Removing Conditional Formatting

### Removing Conditional Formats at specified index value

This involves deleting a specific conditional formatting rule from a cell or range based on its index value. This allows users to precisely manage and update their formatting rules without affecting others.

### Removing Conditional Formats from entire sheet

This refers to clearing all conditional formatting rules from an entire worksheet. This action removes any custom formatting applied to data, returning the sheet to its default formatting state.

For further information, click [here]().

## Advanced Conditional Format Types

### Data Bars

These are horizontal bars added to cells that visually represent the value of each cell relative to others in the range. The length of the bar corresponds to the cell's value, making it easy to compare values at a glance.

### Color Scales

This type of formatting applies a gradient of colors to a range of cells based on their values. Each color represents a different value range, helping to visualize data distribution and trends.

### Icon Sets

These are collections of icons that can be applied to cells based on their values. Icons can represent different data levels, such as arrows for growth or decline, traffic lights for performance indicators, or other symbols.

### Custom Icon Sets 

Similar to standard icon sets, but users can define their own icons and the value ranges that trigger each icon. This allows for highly tailored visual representations of data according to specific criteria.

For further information, click [here]().

## See Also

* [How to set criteria for icon set conditional formats in Excel using XlsIO?](https://support.syncfusion.com/kb/article/7422/how-to-set-criteria-for-icon-set-conditional-formats-in-excel-using-xlsio)
* [Can we set multiple conditional formatting using XlsIO?](https://support.syncfusion.com/kb/article/2610/can-we-set-multiple-conditional-formatting-using-xlsio)
* [Set conditional formatting for text in C#, VB.NET](https://support.syncfusion.com/kb/article/2611/set-conditional-formatting-for-text-in-c-vb-net)
* [How to set conditional formatting for numbers?](https://support.syncfusion.com/kb/article/2621/how-to-set-conditional-formatting-for-numbers)
* [Blog: Excel conditional formatting in C# and VB.NET](https://www.syncfusion.com/document-processing/excel-framework/net/excel-library/conditional-formatting)