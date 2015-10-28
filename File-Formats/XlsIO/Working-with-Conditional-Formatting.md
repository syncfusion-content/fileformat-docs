---
layout: Post
title: Conditional Formatting
description: Briefs about conditional formatting operations
platform: XlsIO
control: File-formats
documentation: UG
---
# Working with Conditional Formatting

Conditional formatting allows the contents of a cell to be dynamically formatted. This can be defined and applied in XlsIO through [IConditionalFormats](IConditionalFormat interface# "") interface.

## Create a Conditional Format 

IConditionalFormats represents a collection of conditional formats for a single IRange. One or more conditional formats can be added to the range as below.

{% tabs %}  
{% highlight c# %}
// Applying conditional formatting to "A1"

IConditionalFormats condition = worksheet.Range["A1"].ConditionalFormats;

IConditionalFormat condition1 = condition.AddCondition();



{% endhighlight %}

{% highlight vb %}
' Applying conditional formatting to "A1"

Dim condition As IConditionalFormats = worksheet.Range("A1").ConditionalFormats

Dim condition1 As IConditionalFormat = condition.AddCondition()



{% endhighlight %}
{% endtabs %}  

The criteria or rules that the target range should meet is set through [IConditionalFormat](go to IConditionalFormat# "") interface. The  desired format type is set through [ExcelCFType](ExcelCFType enumerator# "") enumerator, which are the supported conditional format types in XlsIO. The below piece of code sets a basic conditional formatting rule.

{% tabs %}  
{% highlight c# %}
// Represents conditional format rule that the value in target range should be between 10 and 20

condition1.FormatType = ExcelCFType.CellValue;

condition1.Operator = ExcelComparisonOperator.Between;

condition1.FirstFormula = "10";

condition1.SecondFormula = "20";

worksheet.Range["A1"].Text = "Enter a number between 10 and 20";



{% endhighlight %}

{% highlight vb %}
' Represents conditional format rule that the value in target range should be between 10 and 20

condition1.FormatType = ExcelCFType.CellValue

condition1.Operator = ExcelComparisonOperator.Between

condition1.FirstFormula = "10"

condition1.SecondFormula = "20"

worksheet.Range("A1").Text = "Enter a number between 10 and 20"



{% endhighlight %}
{% endtabs %}  

When the criteria set for the target range is satisfied, the defined formats (like the one below) are applied in the order of priority. For more details on conditional format priority, see [Manage conditional formatting rule precedence](https://support.office.com/en-us/article/Manage-conditional-formatting-rule-precedence-063cde21-516e-45ca-83f5-8e8126076249# "").

{% tabs %}  
{% highlight c# %}
// Setting format properties to be applied when the above condition is met

condition1.BackColor = ExcelKnownColors.Light_orange;

condition1.IsBold = true;

condition1.IsItalic = true;



{% endhighlight %}

{% highlight vb %}
' Setting format properties to be applied when the above condition is met

condition1.BackColor = ExcelKnownColors.Light_orange

condition1.IsBold = True

condition1.IsItalic = True



{% endhighlight %}
{% endtabs %}  

The following code creates and applies various different conditional formats for different ranges in XlsIO.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

// Applying conditional formatting to "A1"

IConditionalFormats condition = worksheet.Range["A1"].ConditionalFormats;

IConditionalFormat condition1 = condition.AddCondition();

// Represents conditional format rule that the value in target range should be between 10 and 20

condition1.FormatType = ExcelCFType.CellValue;

condition1.Operator = ExcelComparisonOperator.Between;

condition1.FirstFormula = "10";

condition1.SecondFormula = "20";

worksheet.Range["A1"].Text = "Enter a number between 10 and 20";

// Setting back color and font style to be applied for target range

condition1.BackColor = ExcelKnownColors.Light_orange;

condition1.IsBold = true;

condition1.IsItalic = true;

// Applying conditional formatting to "A3"

condition = worksheet.Range["A3"].ConditionalFormats;

IConditionalFormat condition2 = condition.AddCondition();

// Represents conditional format rule that the cell value should be 1000

condition2.FormatType = ExcelCFType.CellValue;

condition2.Operator = ExcelComparisonOperator.Equal;

condition2.FirstFormula = "1000";

worksheet.Range["A3"].Text = "Enter the Number as 1000";

// Setting fill pattern and back color to target range

condition2.FillPattern = ExcelPattern.LightUpwardDiagonal;

condition2.BackColor = ExcelKnownColors.Yellow;

// Applying conditional formatting to "A5"

condition = worksheet.Range["A5"].ConditionalFormats;

IConditionalFormat condition3 = condition.AddCondition();

// Setting conditional format rule that the cell value for target range should be less than or equal to 1000

condition3.FormatType = ExcelCFType.CellValue;

condition3.Operator = ExcelComparisonOperator.LessOrEqual;

condition3.FirstFormula = "1000";

worksheet.Range["A5"].Text = "Enter a Number which is less than or equal to 1000";

// Setting back color to target range

condition3.BackColor = ExcelKnownColors.Light_green;

workbook.SaveAs("ConditionalFormatting.xlsx");

workbook.Close();

excelEngine.Dispoe();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

' Applying conditional formatting to "A1"

Dim condition As IConditionalFormats = worksheet.Range("A1").ConditionalFormats

Dim condition1 As IConditionalFormat = condition.AddCondition()

' Represents conditional format rule that the value in target range should be between 10 and 20

condition1.FormatType = ExcelCFType.CellValue

condition1.Operator = ExcelComparisonOperator.Between

condition1.FirstFormula = "10"

condition1.SecondFormula = "20"

worksheet.Range("A1").Text = "Enter a number between 10 and 20"

' Setting back color and font style to be applied for target range

condition1.BackColor = ExcelKnownColors.Light_orange

condition1.IsBold = True

condition1.IsItalic = True

' Applying conditional formatting to "A3"

condition = worksheet.Range("A3").ConditionalFormats

Dim condition2 As IConditionalFormat = condition.AddCondition()

' Represents conditional format rule that the cell value should be 1000

condition2.FormatType = ExcelCFType.CellValue

condition2.Operator = ExcelComparisonOperator.Equal

condition2.FirstFormula = "1000"

worksheet.Range("A3").Text = "Enter the Number as 1000"

' Setting fill pattern and back color to target range

condition2.FillPattern = ExcelPattern.LightUpwardDiagonal

condition2.BackColor = ExcelKnownColors.Yellow

' Applying conditional formatting to "A5"

condition = worksheet.Range("A5").ConditionalFormats

Dim condition3 As IConditionalFormat = condition.AddCondition()

' Setting conditional format rule that the cell value for target range should be less than or equal to 1000

condition3.FormatType = ExcelCFType.CellValue

condition3.[Operator] = ExcelComparisonOperator.LessOrEqual

condition3.FirstFormula = "1000"

worksheet.Range("A5").Text = "Enter a Number which is less than or equal to 1000"

' Setting back color to target range

condition3.BackColor = ExcelKnownColors.Light_green

workbook.SaveAs("ConditionalFormatting.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

I> Excel allows the addition of a maximum of three conditions for the same cell in the Biff8 format and hence XlsIO. However, this restriction is removed from Excel 2007 formats.

I> The conditional formats for a single range should be added in descending order of priority in XlsIO.

When proper criteria are met, the output file looks like the below one.

![](Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img1.jpeg)


## Reading Conditional Formats in XlsIO

XlsIO also provides support for reading conditional formats from existing excel workbook. Following code example illustrates this.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];



// Read conditional formatting settings 

string formatType = worksheet.Range["A1"].ConditionalFormats[0].FormatType.ToString();

string cfOperator = worksheet.Range["A1"].ConditionalFormats[0].Operator.ToString();

string backColor = worksheet.Range["A1"].ConditionalFormats[0].BackColor.ToString(); 

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks. Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

' Read conditional formatting settings

Dim formatType As String = worksheet.Range("A1").ConditionalFormats(0).FormatType.ToString()

Dim cfOperator As String = worksheet.Range("A1").ConditionalFormats(0).Operator.ToString()

Dim backColor As String = worksheet.Range("A1").ConditionalFormats(0).BackColor.ToString()

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Removing Conditional Formats

All the conditional format for a specified range can be removed through [Remove](Go to Remove# "") method. This is illustrated below.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Removing conditional format for a specified range worksheet.Range["E5"].ConditionalFormats.Remove();

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

' Removing conditional format for a specified range worksheet.Range["E5"].ConditionalFormats.Remove()

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Removing Conditional Formats at specified index value

A particular conditional format at the specified range can be removed by using **RemoveAt** Method, as below.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

// Removing first conditional Format at the specified Range worksheet.Range["E5"].ConditionalFormats.RemoveAt(0);

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngineDispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

' Removing first conditional Format at the specified Range worksheet.Range["E5"].ConditionalFormats.RemoveAt(0)

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Removing Conditional Formats from entire sheet

The entire conditional formats from the worksheet can be removed as below.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Removing Conditional Formatting Settings From Entire Sheet worksheet.UsedRange.Clear(ExcelClearOptions.ClearConditionalFormats);

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}



{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

' Removing Conditional Formatting Settings From Entire Sheet worksheet.UsedRange.Clear(ExcelClearOptions.ClearConditionalFormats)

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Using FormulaR1C1 property in Conditional Formats

Moreover XlsIO supports setting the formula for the conditional format in R1C1-style notation. Following code example illustrates this.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

// Using FormulaR1C1 property in Conditional Formatting 

IConditionalFormats condition = worksheet.Range["E5:E18"].ConditionalFormats;

IConditionalFormat condition1 = condition.AddCondition();



condition1.FirstFormulaR1C1 = "=R[1]C[0]" ;

condition1.SecondFormulaR1C1 = "=R[1]C[1]" ;

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

' Using FormulaR1C1 property in Conditional Formatting

Dim condition As IConditionalFormats = worksheet.Range("E5:E18").ConditionalFormats

Dim condition1 As IConditionalFormat = condition.AddCondition()           

condition1.FirstFormulaR1C1 = "=R[1]C[0]" 

condition1.SecondFormulaR1C1 = "=R[1]C[1]" 

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Advanced Conditional Format Types 

In conjunction with basic conditional formatting, the new formatting visualizations such as **Data** **Bars**, **Color** **Scales**, and **Icon** **Sets** are supported in XlsIO.

### Data Bars

Here, the values in each of the selected cells are compared, and a data bar is drawn in each cell representing the value of that cell relative to the other cells in the selected range. This bar provides a clear visual cue for users, making it easier to pick out larger and smaller values in a range.

This can be set and manipulated through IDataBar interface as below.

{% tabs %}  
{% highlight c# %}
// Create data bars for the data in specified range
IConditionalFormats conditionalFormats = worksheet.Range["C7:C46"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();

conditionalFormat.FormatType = ExcelCFType.DataBar;
IDataBar dataBar = conditionalFormat.DataBar;

// Set the constraints
dataBar.MinPoint.Type = ConditionValueType.LowestValue;
dataBar.MaxPoint.Type = ConditionValueType.HighestValue;


// Set color for DataBar
dataBar.BarColor = Color.FromArgb(156, 208, 243);

//Hide the data bar values
dataBar.ShowValue = false;
dataBar.BarColor = Color.Aqua;



{% endhighlight %}

{% highlight vb %}
' Create data bars for the data in specified range
Dim formats As IConditionalFormats = worksheet.Range("C7:C46").ConditionalFormats
Dim format As IConditionalFormat = formats.AddCondition()

format.FormatType = ExcelCFType.DataBar
Dim dataBar As IDataBar = format.DataBar


' Set the constraints
dataBar.MinPoint.Type = ConditionValueType.LowestValue
dataBar.MaxPoint.Type = ConditionValueType.HighestValue


' Set color for DataBar
dataBar.BarColor = System.Drawing.Color.FromArgb(156, 208, 243)


' Hide the data bar values
dataBar.ShowValue = False

dataBar.BarColor = Color.Aqua





{% endhighlight %}
{% endtabs %}  

### Color Scales

Color Scales let you create visual effects in your data, to see how the value of a cell is compared with the values in a range of cells. A color scale uses cell shading, as opposed to bars, to communicate relative values, beyond the relative size of the value of a cell.

Creation of color scales and its formatting rules through [IColorScale](Go to IColorScale# "") interface in XlsIO is illustrated below.

{% tabs %}  
{% highlight c# %}
// Create color scale for the data in specified range
conditionalFormats = worksheet.Range["D7:D46"].ConditionalFormats;
conditionalFormat = conditionalFormats.AddCondition();


conditionalFormat.FormatType = ExcelCFType.ColorScale;
IColorScale colorScale = conditionalFormat.ColorScale;

// Sets 3 - color scale and its constarints
colorScale.SetConditionCount(3);
colorScale.Criteria[0].FormatColorRGB = Color.FromArgb(230, 197, 218);
colorScale.Criteria[0].Type = ConditionValueType.LowestValue;
colorScale.Criteria[0].Value = "0";
colorScale.Criteria[1].FormatColorRGB = Color.FromArgb(244, 210, 178);
colorScale.Criteria[1].Type = ConditionValueType.Percentile;
colorScale.Criteria[1].Value = "50";

colorScale.Criteria[2].FormatColorRGB = Color.FromArgb(245, 247, 171);
colorScale.Criteria[2].Type = ConditionValueType.HighestValue;
colorScale.Criteria[2].Value = "0";           

conditionalFormat.FirstFormulaR1C1 = "=R[1]C[0]" ;

conditionalFormat.SecondFormulaR1C1 = "=R[1]C[1]" ;



{% endhighlight %}

{% highlight vb %}
' Create color scale for the data in specified range
formats = worksheet.Range("D7:D46").ConditionalFormats
format = formats.AddCondition()
format.FormatType = ExcelCFType.ColorScale
Dim colorScale As IColorScale = format.ColorScale

' Sets 3 - color scale and its constraints
colorScale.SetConditionCount(3)
colorScale.Criteria(0).FormatColorRGB = System.Drawing.Color.FromArgb(230, 197, 218)
colorScale.Criteria(0).Type = ConditionValueType.LowestValue
colorScale.Criteria(0).Value = "0"
colorScale.Criteria(1).FormatColorRGB = System.Drawing.Color.FromArgb(244, 210, 178)
colorScale.Criteria(1).Type = ConditionValueType.Percentile
colorScale.Criteria(1).Value = "50"
colorScale.Criteria(2).FormatColorRGB = System.Drawing.Color.FromArgb(245, 247, 171)
colorScale.Criteria(2).Type = ConditionValueType.HighestValue
colorScale.Criteria(2).Value = "0"



{% endhighlight %}
{% endtabs %}  

### Icon Sets

Icon sets present data in three to five categories that are distinguished by a threshold value. Each icon represents a range of values and each cell is annotated with the icon that represents that range.

Icon sets can be created and customized in XlsIO as follows.

{% tabs %}  
{% highlight c# %}
// Create icon sets for the data in specified range
conditionalFormats = worksheet.Range["E7:E46"].ConditionalFormats;
conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.IconSet;
IIconSet iconSet = conditionalFormat.IconSet;


// Apply three symbols icon and hide the data in the specified range

iconSet.IconSet = ExcelIconSetType.ThreeSymbols;
iconSet.IconCriteria[0].Type = ConditionValueType.Percent;

iconSet.IconCriteria[0].Value = "50";

iconSet.IconCriteria[1].Type = ConditionValueType.Percent;

iconSet.IconCriteria[1].Value = "50";
iconSet.ShowIconOnly = true;



{% endhighlight %}

{% highlight vb %}
' Create icon sets for the data in specified range
formats = worksheet.Range("E7:E46").ConditionalFormats
format = formats.AddCondition()
format.FormatType = ExcelCFType.IconSet
Dim iconSet As IIconSet = format.IconSet

' Apply three symbols icon and hide the data in the specified range
iconSet.IconSet = ExcelIconSetType.ThreeSymbols
iconSet.IconCriteria(0).Type = ConditionValueType.Percent

iconSet.IconCriteria(0).Value = "50"

iconSet.IconCriteria(1).Type = ConditionValueType.Percent

iconSet.IconCriteria(1).Value = "50"
iconSet.ShowIconOnly = True



{% endhighlight %}
{% endtabs %}  

The application of these visualizations to a sample data and its output file are represented in the below code example.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create.Open("SampleTemplate.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

// Create data bars for the data in specified range

IConditionalFormats conditionalFormats = worksheet.Range["C7:C46"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();

conditionalFormat.FormatType = ExcelCFType.DataBar;
IDataBar dataBar = conditionalFormat.DataBar;

// Set the constraints
dataBar.MinPoint.Type = ConditionValueType.LowestValue;
dataBar.MaxPoint.Type = ConditionValueType.HighestValue;

// Set color for Bar
dataBar.BarColor = Color.FromArgb(156, 208, 243);

//Hide the values in data bar
dataBar.ShowValue = false;
dataBar.BarColor = Color.Aqua;


// Create color scales for the data in specified range
conditionalFormats = worksheet.Range["D7:D46"].ConditionalFormats;
conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.ColorScale;
IColorScale colorScale = conditionalFormat.ColorScale;

// Sets 3 - color scale
colorScale.SetConditionCount(3);
colorScale.Criteria[0].FormatColorRGB = Color.FromArgb(230, 197, 218);
colorScale.Criteria[0].Type = ConditionValueType.LowestValue;
colorScale.Criteria[0].Value = "0";
colorScale.Criteria[1].FormatColorRGB = Color.FromArgb(244, 210, 178);
colorScale.Criteria[1].Type = ConditionValueType.Percentile;
colorScale.Criteria[1].Value = "50";

colorScale.Criteria[2].FormatColorRGB = Color.FromArgb(245, 247, 171);
colorScale.Criteria[2].Type = ConditionValueType.HighestValue;
colorScale.Criteria[2].Value = "0";           

conditionalFormat.FirstFormulaR1C1 = "=R[1]C[0]" ;

conditionalFormat.SecondFormulaR1C1 = "=R[1]C[1]" ;

// Create icon sets for the data in specified range
conditionalFormats = worksheet.Range["E7:E46"].ConditionalFormats;
conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.IconSet;
IIconSet iconSet = conditionalFormat.IconSet;

// Apply three symbols icon and hide the data in the specified range

iconSet.IconSet = ExcelIconSetType.ThreeSymbols;
iconSet.IconCriteria[0].Type = ConditionValueType.Percent;

iconSet.IconCriteria[0].Value = "50";

iconSet.IconCriteria[1].Type = ConditionValueType.Percent;

iconSet.IconCriteria[1].Value = "50";
iconSet.ShowIconOnly = true;

string fileName = "ConditionalFormatting.xlsx";

workbook.SaveAs(fileName);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("SampleTemplate.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

' Create data bars for the data in specified range

Dim formats As IConditionalFormats = worksheet.Range("C7:C46").ConditionalFormats
Dim format As IConditionalFormat = formats.AddCondition()

format.FormatType = ExcelCFType.DataBar
Dim dataBar As IDataBar = format.DataBar


' Set the constraints
dataBar.MinPoint.Type = ConditionValueType.LowestValue
dataBar.MaxPoint.Type = ConditionValueType.HighestValue

' Set color for Bar
dataBar.BarColor = System.Drawing.Color.FromArgb(156, 208, 243)


' Hide the value in data bar
dataBar.ShowValue = False

dataBar.BarColor = Color.Aqua

' Create color scales for the data in specified range
formats = worksheet.Range("D7:D46").ConditionalFormats
format = formats.AddCondition()
format.FormatType = ExcelCFType.ColorScale
Dim colorScale As IColorScale = format.ColorScale

' Sets 3 - color scale
colorScale.SetConditionCount(3)
colorScale.Criteria(0).FormatColorRGB = System.Drawing.Color.FromArgb(230, 197, 218)
colorScale.Criteria(0).Type = ConditionValueType.LowestValue
colorScale.Criteria(0).Value = "0"
colorScale.Criteria(1).FormatColorRGB = System.Drawing.Color.FromArgb(244, 210, 178)
colorScale.Criteria(1).Type = ConditionValueType.Percentile
colorScale.Criteria(1).Value = "50"
colorScale.Criteria(2).FormatColorRGB = System.Drawing.Color.FromArgb(245, 247, 171)
colorScale.Criteria(2).Type = ConditionValueType.HighestValue
colorScale.Criteria(2).Value = "0"

' Create icon sets for the data in specified range
formats = worksheet.Range("E7:E46").ConditionalFormats
format = formats.AddCondition()
format.FormatType = ExcelCFType.IconSet
Dim iconSet As IIconSet = format.IconSet

' Apply three symbols icon and hide the data in the specified range

iconSet.IconSet = ExcelIconSetType.ThreeSymbols
iconSet.IconCriteria(0).Type = ConditionValueType.Percent

iconSet.IconCriteria(0).Value = "50"

iconSet.IconCriteria(1).Type = ConditionValueType.Percent

iconSet.IconCriteria(1).Value = "50"
iconSet.ShowIconOnly = True

Dim fileName As String = "ConditionalFormatting.xlsx"

workbook.SaveAs(fileName)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

![](Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img2.jpeg)


__Excel__ __with__ __Conditional__ __Formatting__

I> XlsIO visualization has been enhanced with backward compatibility for Advanced Conditional Formatting.

