---
title: Color Scales | Excel library | Syncfusion
description: In this section, you can learn how to apply color scales using conditional formatting in an Excel document with XlsIO
platform: file-formats
control: XlsIO
documentation: UG
---

# Color Scales in Conditional Formatting

Color Scales let you create visual effects in your data to see how the value of a cell is compared with the values in a range of cells. A color scale uses cell shading, as opposed to bars, to communicate relative values, beyond the relative size of the value of a cell.

The following code example illustrates how to apply color scales using [IColorScale](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IColorScale.html) interface in XlsIO.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("../../../Data/InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Create color scales for the data in specified range
    IConditionalFormats conditionalFormats = worksheet.Range["D7:D46"].ConditionalFormats;
    IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
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

    //Create color scales for the data in specified range
    IConditionalFormats conditionalFormats = worksheet.Range["D7:D46"].ConditionalFormats;
    IConditionalFormat conditionalFormat = conditionalFormats.AddCondition();
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

    ' Create color scales for the data in specified range
    Dim conditionalFormats As IConditionalFormats = worksheet.Range("D7:D46").ConditionalFormats
    Dim conditionalFormat As IConditionalFormat = conditionalFormats.AddCondition()
    conditionalFormat.FormatType = ExcelCFType.ColorScale
    Dim colorScale As IColorScale = conditionalFormat.ColorScale

    ' Sets 3 - color scale
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

    conditionalFormat.FirstFormulaR1C1 = "=R[1]C[0]"
    conditionalFormat.SecondFormulaR1C1 = "=R[1]C[1]"

    ' Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to apply color scales in C# is present on [this GitHub page]().