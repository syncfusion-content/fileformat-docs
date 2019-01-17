---
title: Apply Borders in Excel
description: This page shows how to apply borders in Excel with different line styles.
platform: file-formats
control: XlsIO
documentation: UG
---

# Apply Borders in Excel

Applying borders around specific cells makes those cells stand out to people viewing the document. For example, this could be useful when calling attention to totals or to other specific numbers or words in the file. Alternatively, because borders are thicker and more pronounced than the default grid lines, you can put border lines around all cells to further define each one to prevent them from blending together when someone views the document. We can also use different line styles for borders.

The following code shows how to apply borders in Excel with different line styles to cells using Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void ApplyBorders()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a Workbook.
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the First sheet.
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Put some text into different cells (A2, A4, A6, A8).
    worksheet.Cells[2, 1] = "Hair Lines";
    worksheet.Cells[4, 1] = "Thin Lines";
    worksheet.Cells[6, 1] = "Medium Lines";
    worksheet.Cells[8, 1] = "Thick Lines";

    //Define a range object(A2).
    Range range;
    range = worksheet.get_Range("A2", "A2");
    //Get the borders collection.
    Borders borders = range.Borders;
    //Set the hair lines style.
    borders.LineStyle = XlLineStyle.xlContinuous;
    borders.Weight = 1d;

    //Define a range object(A4).
    range = worksheet.get_Range("A4", "A4");
    //Get the borders collection.
    borders = range.Borders;
    //Set the thin lines style.
    borders.LineStyle = XlLineStyle.xlContinuous;
    borders.Weight = 2d;

    //Define a range object(A6).
    range = worksheet.get_Range("A6", "A6");
    //Get the borders collection.
    borders = range.Borders;
    //Set the medium lines style.
    borders.LineStyle = XlLineStyle.xlContinuous;
    borders.Weight = 3d;

    //Define a range object(A8).
    range = worksheet.get_Range("A8", "A8");
    //Get the borders collection.
    borders = range.Borders;
    //Set the thick lines style.
    borders.LineStyle = XlLineStyle.xlContinuous;
    borders.Weight = 4d;

    //Auto-fit Column A.
    worksheet.get_Range("A2", "A2").EntireColumn.AutoFit();

    //Save the file.
    workbook.SaveAs(@"d:\test\InteropOutput_Borders.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub ApplyBorders()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a Workbook.
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the First sheet.
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Put some text into different cells (A2, A4, A6, A8).
    worksheet.Cells(2, 1) = "Hair Lines"
    worksheet.Cells(4, 1) = "Thin Lines"
    worksheet.Cells(6, 1) = "Medium Lines"
    worksheet.Cells(8, 1) = "Thick Lines"

    'Define a range object(A2).
    Dim range As Range
    range = worksheet.Range("A2", "A2")
    'Get the borders collection.
    Dim borders As Borders = range.Borders
    'Set the hair lines style.
    borders.LineStyle = XlLineStyle.xlContinuous
    borders.Weight = 1.0R

    'Define a range object(A4).
    range = worksheet.Range("A4", "A4")
    'Get the borders collection.
    borders = range.Borders
    'Set the thin lines style.
    borders.LineStyle = XlLineStyle.xlContinuous
    borders.Weight = 2.0R

    'Define a range object(A6).
    range = worksheet.Range("A6", "A6")
    'Get the borders collection.
    borders = range.Borders
    'Set the medium lines style.
    borders.LineStyle = XlLineStyle.xlContinuous
    borders.Weight = 3.0R

    'Define a range object(A8).
    range = worksheet.Range("A8", "A8")
    'Get the borders collection.
    borders = range.Borders
    'Set the thick lines style.
    borders.LineStyle = XlLineStyle.xlContinuous
    borders.Weight = 4.0R

    'Auto-fit Column A.
    worksheet.Range("A2", "A2").EntireColumn.AutoFit()

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_Borders.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void ApplyBorders()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Create a Workbook.
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the First sheet.
        IWorksheet worksheet = workbook.Worksheets[0];

        //Put some text into different cells (A2, A4, A6, A8).
        worksheet.Range[2, 1].Value = "Hair Lines";
        worksheet.Range[4, 1].Value = "Thin Lines";
        worksheet.Range[6, 1].Value = "Medium Lines";
        worksheet.Range[8, 1].Value = "Thick Lines";

        //Define a range object(A2).
        IRange range;
        range = worksheet.Range["A2"];
        //Set the borders with hair lines style.
        range.BorderAround(ExcelLineStyle.Hair);

        //Define a range object(A4).
        range = worksheet.Range["A4"];
        //Set the borders with thin lines style.
        range.BorderAround(ExcelLineStyle.Thin);

        //Define a range object(A6).
        range = worksheet.Range["A6"];
        //Set the borders with medium lines style.
        range.BorderAround(ExcelLineStyle.Medium);

        //Define a range object(A8).
        range = worksheet.Range["A8"];
        //Set the borders with thick lines style.
        range.BorderAround(ExcelLineStyle.Thick);

        //Auto-fit Column A.
        worksheet.AutofitColumn(1);

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_Borders.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub ApplyBorders()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Create a Workbook.
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the First sheet.
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Put some text into different cells (A2, A4, A6, A8).
        worksheet.Range(2, 1).Value = "Hair Lines"
        worksheet.Range(4, 1).Value = "Thin Lines"
        worksheet.Range(6, 1).Value = "Medium Lines"
        worksheet.Range(8, 1).Value = "Thick Lines"

        'Define a range object(A2).
        Dim range As IRange
        range = worksheet.Range("A2")
        'Set the borders with hair lines style.
        range.BorderAround(ExcelLineStyle.Hair)

        'Define a range object(A4).
        range = worksheet.Range("A4")
        'Set the borders with thin lines style.
        range.BorderAround(ExcelLineStyle.Thin)

        'Define a range object(A6).
        range = worksheet.Range("A6")
        'Set the borders with medium lines style.
        range.BorderAround(ExcelLineStyle.Medium)

        'Define a range object(A8).
        range = worksheet.Range("A8")
        'Set the borders with thick lines style.
        range.BorderAround(ExcelLineStyle.Thick)

        'Auto-fit Column A.
        worksheet.AutofitColumn(1)

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_Borders.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
