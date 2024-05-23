---
title: Icon Sets | Excel library | Syncfusion
description: In this section, you can learn how to apply Icon sets uisng conditional formatting in an Excel document with XlsIO
platform: file-formats
control: XlsIO
documentation: UG
---

# Icon Sets in Conditional Formatting

Icon sets present data in three to five categories that are distinguished by a threshold value. Each icon represents a range of values and each cell is annotated with the icon that represents that range.

The following code example illustrates how to apply Icon sets using [IconSet](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IIconSet.html) interface in XlsIO.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("../../../Data/InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream);
    IWorksheet worksheet = workbook.Worksheets[0];

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

    //Saving the workbook
    FileStream outputStream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.Write);
    workbook.SaveAs(outputStream);

    //Dispose streams
    outputStream.Dispose();
    inputStream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx");
    IWorksheet worksheet = workbook.Worksheets[0];

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

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx")
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    ' Create icon sets for the data in specified range
    Dim conditionalFormats As IConditionalFormats = worksheet.Range("E7:E46").ConditionalFormats
    Dim conditionalFormat As IConditionalFormat = conditionalFormats.AddCondition()
    conditionalFormat.FormatType = ExcelCFType.IconSet
    Dim iconSet As IIconSet = conditionalFormat.IconSet

    ' Apply three symbols icon and hide the data in the specified range
    iconSet.IconSet = ExcelIconSetType.ThreeSymbols
    iconSet.IconCriteria(1).Type = ConditionValueType.Percent
    iconSet.IconCriteria(1).Value = "50"
    iconSet.IconCriteria(2).Type = ConditionValueType.Percent
    iconSet.IconCriteria(2).Value = "50"
    iconSet.ShowIconOnly = True

    ' Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to apply Icon sets in C# is present on [this GitHub page]().

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

N> XlsIO visualization has been enhanced with backward compatibility for Advanced Conditional Formatting.