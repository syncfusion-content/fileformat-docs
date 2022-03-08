---
title: Apply Borders in Excel | Syncfusion
description: Explains with an example on how to programmatically apply borders in Excel with different line styles using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Apply Borders in Excel

Applying borders around specific cells makes those cells stand out to people who view the document. For example, this is used when calling attention to totals, other specific numbers, or words in the file. Alternatively, as the borders are thicker and more pronounceable than the default grid lines, you can add border lines around all the cells to define each to prevent from blending together when users view the document. You can also use different line styles for borders.

The following code shows how to apply borders in Excel with different line styles to cells using Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void ApplyBorders()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a workbook
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the first sheet
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Put some text into different cells (A2, A4, A6, and A8)
    worksheet.Cells[2, 1] = "Hair Lines";
    worksheet.Cells[4, 1] = "Thin Lines";
    worksheet.Cells[6, 1] = "Medium Lines";
    worksheet.Cells[8, 1] = "Thick Lines";

    //Define a range object (A2)
    Range range;
    range = worksheet.get_Range("A2", "A2");
    //Get the borders collection
    Borders borders = range.Borders;
    //Set the hair lines style
    borders.LineStyle = XlLineStyle.xlContinuous;
    borders.Weight = 1d;

    //Define a range object (A4)
    range = worksheet.get_Range("A4", "A4");
    //Get the borders collection
    borders = range.Borders;
    //Set the thin lines style
    borders.LineStyle = XlLineStyle.xlContinuous;
    borders.Weight = 2d;

    //Define a range object (A6)
    range = worksheet.get_Range("A6", "A6");
    //Get the borders collection
    borders = range.Borders;
    //Set the medium lines style
    borders.LineStyle = XlLineStyle.xlContinuous;
    borders.Weight = 3d;

    //Define a range object (A8)
    range = worksheet.get_Range("A8", "A8");
    //Get the borders collection
    borders = range.Borders;
    //Set the thick lines style
    borders.LineStyle = XlLineStyle.xlContinuous;
    borders.Weight = 4d;

    //Autofit column A
    worksheet.get_Range("A2", "A2").EntireColumn.AutoFit();

    //Save the file
    workbook.SaveAs(@"d:\test\InteropOutput_Borders.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub ApplyBorders()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a workbook
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the first sheet
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Put some text into different cells (A2, A4, A6, and A8)
    worksheet.Cells(2, 1) = "Hair Lines"
    worksheet.Cells(4, 1) = "Thin Lines"
    worksheet.Cells(6, 1) = "Medium Lines"
    worksheet.Cells(8, 1) = "Thick Lines"

    'Define a range object (A2)
    Dim range As Range
    range = worksheet.Range("A2", "A2")
    'Get the borders collection
    Dim borders As Borders = range.Borders
    'Set the hair lines style
    borders.LineStyle = XlLineStyle.xlContinuous
    borders.Weight = 1.0R

    'Define a range object (A4)
    range = worksheet.Range("A4", "A4")
    'Get the borders collection
    borders = range.Borders
    'Set the thin lines style
    borders.LineStyle = XlLineStyle.xlContinuous
    borders.Weight = 2.0R

    'Define a range object (A6)
    range = worksheet.Range("A6", "A6")
    'Get the borders collection
    borders = range.Borders
    'Set the medium lines style
    borders.LineStyle = XlLineStyle.xlContinuous
    borders.Weight = 3.0R

    'Define a range object (A8)
    range = worksheet.Range("A8", "A8")
    'Get the borders collection
    borders = range.Borders
    'Set the thick lines style
    borders.LineStyle = XlLineStyle.xlContinuous
    borders.Weight = 4.0R

    'Autofit column A
    worksheet.Range("A2", "A2").EntireColumn.AutoFit()

    'Save the file
    workbook.SaveCopyAs("d:\test1\InteropOutput_Borders.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void ApplyBorders()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the first sheet
        IWorksheet worksheet = workbook.Worksheets[0];

        //Put some text into different cells (A2, A4, A6, and A8)
        worksheet.Range[2, 1].Value = "Hair Lines";
        worksheet.Range[4, 1].Value = "Thin Lines";
        worksheet.Range[6, 1].Value = "Medium Lines";
        worksheet.Range[8, 1].Value = "Thick Lines";

        //Define a range object (A2)
        IRange range;
        range = worksheet.Range["A2"];
        //Set the borders with hair lines style
        range.BorderAround(ExcelLineStyle.Hair);

        //Define a range object (A4)
        range = worksheet.Range["A4"];
        //Set the borders with thin lines style
        range.BorderAround(ExcelLineStyle.Thin);

        //Define a range object (A6)
        range = worksheet.Range["A6"];
        //Set the borders with medium lines style
        range.BorderAround(ExcelLineStyle.Medium);

        //Define a range object (A8)
        range = worksheet.Range["A8"];
        //Set the borders with thick lines style
        range.BorderAround(ExcelLineStyle.Thick);

        //Autofit column A
        worksheet.AutofitColumn(1);

        //Save the workbook
        workbook.SaveAs(@"d:\test\XlsIOOutput_Borders.xlsx");
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub ApplyBorders()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Create a workbook
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the first sheet
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Put some text into different cells (A2, A4, A6, and A8)
        worksheet.Range(2, 1).Value = "Hair Lines"
        worksheet.Range(4, 1).Value = "Thin Lines"
        worksheet.Range(6, 1).Value = "Medium Lines"
        worksheet.Range(8, 1).Value = "Thick Lines"

        'Define a range object (A2)
        Dim range As IRange
        range = worksheet.Range("A2")
        'Set the borders with hair lines style
        range.BorderAround(ExcelLineStyle.Hair)

        'Define a range object (A4)
        range = worksheet.Range("A4")
        'Set the borders with thin lines style
        range.BorderAround(ExcelLineStyle.Thin)

        'Define a range object (A6)
        range = worksheet.Range("A6")
        'Set the borders with medium lines style
        range.BorderAround(ExcelLineStyle.Medium)

        'Define a range object (A8)
        range = worksheet.Range("A8")
        'Set the borders with thick lines style
        range.BorderAround(ExcelLineStyle.Thick)

        'Autofit column A
        worksheet.AutofitColumn(1)

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_Borders.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
