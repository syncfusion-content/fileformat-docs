---
title: Advanced Conditional Format Types| Excel library | Syncfusion
description: In this section, you can learn how to apply advanced conditional format types in Excel using XlsIO
platform: file-formats
control: XlsIO
documentation: UG
---
# Advanced Conditional Format Types 

In conjunction with basic conditional formatting, the new formatting visualizations such as **Data** **Bars**, **Color** **Scales**, and **Icon** **Sets** are supported in XlsIO.

## Data Bars

Here, the values in each of the selected cells are compared, and a data bar is drawn in each cell representing the value of that cell relative to the other cells in the selected range. This bar provides a clear visual cue for users, making it easier to pick out larger and smaller values in a range.

This can be set and manipulated using the [IDataBar](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IDataBar.html) interface as follows.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create data bars for the data in specified range
IConditionalFormats conditionalFormats = worksheet.Range["C7:C46"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.DataBar;
IDataBar dataBar = conditionalFormat.DataBar;

//Set the constraints
dataBar.MinPoint.Type = ConditionValueType.LowestValue;
dataBar.MaxPoint.Type = ConditionValueType.HighestValue;

//Set color for DataBar
dataBar.BarColor = Color.FromArgb(156, 208, 243);

//Hide the data bar values
dataBar.ShowValue = false;
dataBar.BarColor = Color.Aqua;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create data bars for the data in specified range
IConditionalFormats conditionalFormats = worksheet.Range["C7:C46"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.DataBar;
IDataBar dataBar = conditionalFormat.DataBar;

//Set the constraints
dataBar.MinPoint.Type = ConditionValueType.LowestValue;
dataBar.MaxPoint.Type = ConditionValueType.HighestValue;

//Set color for DataBar
dataBar.BarColor = Color.FromArgb(156, 208, 243);

//Hide the data bar values
dataBar.ShowValue = false;
dataBar.BarColor = Color.Aqua;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create data bars for the data in specified range
Dim formats As IConditionalFormats = worksheet.Range("C7:C46").ConditionalFormats
Dim format As IConditionalFormat = formats.AddCondition()
format.FormatType = ExcelCFType.DataBar
Dim dataBar As IDataBar = format.DataBar

'Set the constraints
dataBar.MinPoint.Type = ConditionValueType.LowestValue
dataBar.MaxPoint.Type = ConditionValueType.HighestValue

'Set color for DataBar
dataBar.BarColor = System.Drawing.Color.FromArgb(156, 208, 243)

'Hide the data bar values
dataBar.ShowValue = False
dataBar.BarColor = Color.Aqua
{% endhighlight %}
{% endtabs %}  

## Color Scales

Color Scales let you create visual effects in your data to see how the value of a cell is compared with the values in a range of cells. A color scale uses cell shading, as opposed to bars, to communicate relative values, beyond the relative size of the value of a cell.

Creation of color scales and its formatting rules using the [IColorScale](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IColorScale.html) interface in XlsIO is illustrated as follows.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create color scale for the data in specified range
IConditionalFormats conditionalFormats = worksheet.Range["D7:D46"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.ColorScale;
IColorScale colorScale = conditionalFormat.ColorScale;

//Sets 3 - color scale and its constraints
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

conditionalFormat.FirstFormulaR1C1 = "=R[1]C[0]";
conditionalFormat.SecondFormulaR1C1 = "=R[1]C[1]";
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create color scale for the data in specified range
IConditionalFormats conditionalFormats = worksheet.Range["D7:D46"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.ColorScale;
IColorScale colorScale = conditionalFormat.ColorScale;

//Sets 3 - color scale and its constraints
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create color scale for the data in specified range
Dim conditionalFormats As IConditionalFormats = worksheet.Range("D7:D46").ConditionalFormats
Dim conditionalFormat As IConditionalFormat = conditionalFormats.AddCondition()
conditionalFormat.FormatType = ExcelCFType.ColorScale
Dim colorScale As IColorScale = conditionalFormat.ColorScale

'Sets 3 - color scale and its constraints
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

## Icon Sets

Icon sets present data in three to five categories that are distinguished by a threshold value. Each icon represents a range of values and each cell is annotated with the icon that represents that range.

Icon sets can be created and customized in XlsIO as follows.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create icon sets for the data in specified range
IConditionalFormats conditionalFormats = worksheet.Range["E7:E46"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.IconSet;
IIconSet iconSet = conditionalFormat.IconSet;

//Apply three symbols icon and hide the data in the specified range
iconSet.IconSet = ExcelIconSetType.ThreeSymbols;
iconSet.IconCriteria[1].Type = ConditionValueType.Percent;
iconSet.IconCriteria[1].Value = "50";
iconSet.IconCriteria[2].Type = ConditionValueType.Percent;
iconSet.IconCriteria[2].Value = "50";
iconSet.ShowIconOnly = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create icon sets for the data in specified range
IConditionalFormats conditionalFormats = worksheet.Range["E7:E46"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.IconSet;
IIconSet iconSet = conditionalFormat.IconSet;

//Apply three symbols icon and hide the data in the specified range
iconSet.IconSet = ExcelIconSetType.ThreeSymbols;
iconSet.IconCriteria[1].Type = ConditionValueType.Percent;
iconSet.IconCriteria[1].Value = "50";
iconSet.IconCriteria[2].Type = ConditionValueType.Percent;
iconSet.IconCriteria[2].Value = "50";
iconSet.ShowIconOnly = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create icon sets for the data in specified range
Dim conditionalFormats As IConditionalFormats = worksheet.Range("E7:E46").ConditionalFormats
Dim conditionalFormat As IConditionalFormat = formats.AddCondition()
format.FormatType = ExcelCFType.IconSet
Dim iconSet As IIconSet = format.IconSet

'Apply three symbols icon and hide the data in the specified range
iconSet.IconSet = ExcelIconSetType.ThreeSymbols
iconSet.IconCriteria(1).Type = ConditionValueType.Percent
iconSet.IconCriteria(1).Value = "50"
iconSet.IconCriteria(2).Type = ConditionValueType.Percent
iconSet.IconCriteria(2).Value = "50"
iconSet.ShowIconOnly = True
{% endhighlight %}
{% endtabs %}

## Custom Icon Sets

You can customize the icon set by changing the [IconSet](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IIconConditionValue.html#Syncfusion_XlsIO_IIconConditionValue_IconSet) and [Index](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IIconConditionValue.html#Syncfusion_XlsIO_IIconConditionValue_Index) properties for each icon criteria.

Custom Icon sets can be created and customized in XlsIO as follows.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
// Create icon sets for the data in specified range
IConditionalFormats conditionalFormats = sheet.Range["H1:K6"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.IconSet;
IIconSet iconSet = conditionalFormat.IconSet;
iconSet.IconSet = ExcelIconSetType.ThreeFlags;

IIconConditionValue iconValue1 = iconSet.IconCriteria[0] as IIconConditionValue;
iconValue1.IconSet = ExcelIconSetType.FiveBoxes;
iconValue1.Index = 3;
iconValue1.Type = ConditionValueType.Percent;
iconValue1.Value = "25";
iconValue1.Operator = ConditionalFormatOperator.GreaterThan;

IIconConditionValue iconValue2 = iconSet.IconCriteria[1] as IIconConditionValue;
iconValue2.IconSet = ExcelIconSetType.ThreeSigns;
iconValue2.Index = 2;
iconValue2.Type = ConditionValueType.Percent;
iconValue2.Value = "50";
iconValue2.Operator = ConditionalFormatOperator.GreaterThan;

IIconConditionValue iconValue3 = iconSet.IconCriteria[2] as IIconConditionValue;
iconValue3.IconSet = ExcelIconSetType.FourRating;
iconValue3.Index = 0;
iconValue3.Type = ConditionValueType.Percent;
iconValue3.Value = "75";
iconValue3.Operator = ConditionalFormatOperator.GreaterThan;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
// Create icon sets for the data in specified range
IConditionalFormats conditionalFormats = sheet.Range["H1:K6"].ConditionalFormats;
IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
conditionalFormat.FormatType = ExcelCFType.IconSet;
IIconSet iconSet = conditionalFormat.IconSet;
iconSet.IconSet = ExcelIconSetType.ThreeFlags;

IIconConditionValue iconValue1 = iconSet.IconCriteria[0] as IIconConditionValue;
iconValue1.IconSet = ExcelIconSetType.FiveBoxes;
iconValue1.Index = 3;
iconValue1.Type = ConditionValueType.Percent;
iconValue1.Value = "25";
iconValue1.Operator = ConditionalFormatOperator.GreaterThan;

IIconConditionValue iconValue2 = iconSet.IconCriteria[1] as IIconConditionValue;
iconValue2.IconSet = ExcelIconSetType.ThreeSigns;
iconValue2.Index = 2;
iconValue2.Type = ConditionValueType.Percent;
iconValue2.Value = "50";
iconValue2.Operator = ConditionalFormatOperator.GreaterThan;

IIconConditionValue iconValue3 = iconSet.IconCriteria[2] as IIconConditionValue;
iconValue3.IconSet = ExcelIconSetType.FourRating;
iconValue3.Index = 0;
iconValue3.Type = ConditionValueType.Percent;
iconValue3.Value = "75";
iconValue3.Operator = ConditionalFormatOperator.GreaterThan;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim conditionalFormats As IConditionalFormats = sheet.Range("H1:K6").ConditionalFormats
Dim conditionalFormat As IConditionalFormat = conditionalFormats.AddCondition
conditionalFormat.FormatType = ExcelCFType.IconSet
Dim iconSet As IIconSet = conditionalFormat.IconSet
iconSet.IconSet = ExcelIconSetType.ThreeFlags

Dim iconValue1 As IIconConditionValue = CType(iconSet.IconCriteria(0),IIconConditionValue)
iconValue1.IconSet = ExcelIconSetType.FiveBoxes
iconValue1.Index = 3
iconValue1.Type = ConditionValueType.Percent
iconValue1.Value = "25"
iconValue1.Operator = ConditionalFormatOperator.GreaterThan

Dim iconValue2 As IIconConditionValue = CType(iconSet.IconCriteria(1),IIconConditionValue)
iconValue2.IconSet = ExcelIconSetType.ThreeSigns
iconValue2.Index = 2
iconValue2.Type = ConditionValueType.Percent
iconValue2.Value = "50"
iconValue2.Operator = ConditionalFormatOperator.GreaterThan

Dim iconValue3 As IIconConditionValue = CType(iconSet.IconCriteria(2),IIconConditionValue)
iconValue3.IconSet = ExcelIconSetType.FourRating
iconValue3.Index = 0
iconValue3.Type = ConditionValueType.Percent
iconValue3.Value = "75"
iconValue3.Operator = ConditionalFormatOperator.GreaterThan
{% endhighlight %}
{% endtabs %}  

The following code example illustrates how to apply advanced conditional formatting options like data bars, color scales and icon sets.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  FileStream fileStream = new FileStream("SampleTemplate.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create data bars for the data in specified range
  IConditionalFormats conditionalFormats = worksheet.Range["C7:C46"].ConditionalFormats;
  IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
  conditionalFormat.FormatType = ExcelCFType.DataBar;
  IDataBar dataBar = conditionalFormat.DataBar;

  //Set the constraints
  dataBar.MinPoint.Type = ConditionValueType.LowestValue;
  dataBar.MaxPoint.Type = ConditionValueType.HighestValue;

  //Set color for Bar
  dataBar.BarColor = Color.FromArgb(156, 208, 243);

  //Hide the values in data bar
  dataBar.ShowValue = false;
  dataBar.BarColor = Color.Aqua;

  //Create color scales for the data in specified range
  conditionalFormats = worksheet.Range["D7:D46"].ConditionalFormats;
  conditionalFormat = conditionalFormats.AddCondition();
  conditionalFormat.FormatType = ExcelCFType.ColorScale;
  IColorScale colorScale = conditionalFormat.ColorScale;

  //Sets 3 - color scale
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

  conditionalFormat.FirstFormulaR1C1 = "=R[1]C[0]";
  conditionalFormat.SecondFormulaR1C1 = "=R[1]C[1]";

  //Create icon sets for the data in specified range
  conditionalFormats = worksheet.Range["E7:E46"].ConditionalFormats;
  conditionalFormat = conditionalFormats.AddCondition();
  conditionalFormat.FormatType = ExcelCFType.IconSet;
  IIconSet iconSet = conditionalFormat.IconSet;

  //Apply three symbols icon and hide the data in the specified range
  iconSet.IconSet = ExcelIconSetType.ThreeSymbols;
  iconSet.IconCriteria[1].Type = ConditionValueType.Percent;
  iconSet.IconCriteria[1].Value = "50";
  iconSet.IconCriteria[2].Type = ConditionValueType.Percent;
  iconSet.IconCriteria[2].Value = "50";
  iconSet.ShowIconOnly = true;

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
  IWorkbook workbook = application.Workbooks.Open("SampleTemplate.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create data bars for the data in specified range
  IConditionalFormats conditionalFormats = worksheet.Range["C7:C46"].ConditionalFormats;
  IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
  conditionalFormat.FormatType = ExcelCFType.DataBar;
  IDataBar dataBar = conditionalFormat.DataBar;

  //Set the constraints
  dataBar.MinPoint.Type = ConditionValueType.LowestValue;
  dataBar.MaxPoint.Type = ConditionValueType.HighestValue;

  //Set color for Bar
  dataBar.BarColor = Color.FromArgb(156, 208, 243);

  //Hide the values in data bar
  dataBar.ShowValue = false;
  dataBar.BarColor = Color.Aqua;

  //Create color scales for the data in specified range
  conditionalFormats = worksheet.Range["D7:D46"].ConditionalFormats;
  conditionalFormat = conditionalFormats.AddCondition();
  conditionalFormat.FormatType = ExcelCFType.ColorScale;
  IColorScale colorScale = conditionalFormat.ColorScale;

  //Sets 3 - color scale
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

  conditionalFormat.FirstFormulaR1C1 = "=R[1]C[0]";
  conditionalFormat.SecondFormulaR1C1 = "=R[1]C[1]";

  //Create icon sets for the data in specified range
  conditionalFormats = worksheet.Range["E7:E46"].ConditionalFormats;
  conditionalFormat = conditionalFormats.AddCondition();
  conditionalFormat.FormatType = ExcelCFType.IconSet;
  IIconSet iconSet = conditionalFormat.IconSet;

  //Apply three symbols icon and hide the data in the specified range
  iconSet.IconSet = ExcelIconSetType.ThreeSymbols;
  iconSet.IconCriteria[1].Type = ConditionValueType.Percent;
  iconSet.IconCriteria[1].Value = "50";
  iconSet.IconCriteria[2].Type = ConditionValueType.Percent;
  iconSet.IconCriteria[2].Value = "50";
  iconSet.ShowIconOnly = true;

  string fileName = "ConditionalFormatting.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("SampleTemplate.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Create data bars for the data in specified range
  Dim formats As IConditionalFormats = worksheet.Range("C7:C46").ConditionalFormats
  Dim format As IConditionalFormat = formats.AddCondition()
  format.FormatType = ExcelCFType.DataBar
  Dim dataBar As IDataBar = format.DataBar

  'Set the constraints
  dataBar.MinPoint.Type = ConditionValueType.LowestValue
  dataBar.MaxPoint.Type = ConditionValueType.HighestValue

  'Set color for Bar
  dataBar.BarColor = System.Drawing.Color.FromArgb(156, 208, 243)

  'Hide the value in data bar
  dataBar.ShowValue = False
  dataBar.BarColor = Color.Aqua

  'Create color scales for the data in specified range
  formats = worksheet.Range("D7:D46").ConditionalFormats
  format = formats.AddCondition()
  format.FormatType = ExcelCFType.ColorScale
  Dim colorScale As IColorScale = format.ColorScale

  'Sets 3 - color scale
  colorScale.SetConditionCount(3)
  colorScale.Criteria(0).FormatColorRGB = Color.FromArgb(230, 197, 218)
  colorScale.Criteria(0).Type = ConditionValueType.LowestValue
  colorScale.Criteria(0).Value = "0"

  colorScale.Criteria(1).FormatColorRGB = Color.FromArgb(244, 210, 178)
  colorScale.Criteria(1).Type = ConditionValueType.Percentile
  colorScale.Criteria(1).Value = "50"

  colorScale.Criteria(2).FormatColorRGB = Color.FromArgb(245, 247, 171)
  colorScale.Criteria(2).Type = ConditionValueType.HighestValue
  colorScale.Criteria(2).Value = "0"

  'Create icon sets for the data in specified range
  formats = worksheet.Range("E7:E46").ConditionalFormats
  format = formats.AddCondition()
  format.FormatType = ExcelCFType.IconSet
  Dim iconSet As IIconSet = format.IconSet

  'Apply three symbols icon and hide the data in the specified range
  iconSet.IconSet = ExcelIconSetType.ThreeSymbols
  iconSet.IconCriteria(1).Type = ConditionValueType.Percent
  iconSet.IconCriteria(1).Value = "50"
  iconSet.IconCriteria(2).Type = ConditionValueType.Percent
  iconSet.IconCriteria(2).Value = "50"
  iconSet.ShowIconOnly = True

  Dim fileName As String = "ConditionalFormatting.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format values with advanced conditional formatting options like data bars, color scales, icon sets in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Conditional%20Formatting/Advanced%20Conditional%20Formats).

![Advanced conditional Formatting](../Working-with-Conditional-Formatting_images/Working-with-Conditional-Formatting_img2.jpeg)

N> XlsIO visualization has been enhanced with backward compatibility for Advanced Conditional Formatting.