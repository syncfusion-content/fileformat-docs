---
title: Resolve performance issue when deleting a large number of rows | Syncfusion
description: This page explains how to resolve performance issue when deleting a large number of rows using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to resolve performance issue when deleting a large number of rows?

To address the performance issue, rather than deleting the large number of blank rows using the DeleteRow method, copy the row containing values to a new worksheet and then delete the previous worksheet.

The following code illustrates how to resolve performance issue when deleting a large number of rows.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Loads an existing file
    FileStream fileStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(fileStream);
    IWorksheet worksheet = workbook.Worksheets[0];
    IWorksheet newWorksheet = workbook.Worksheets[1];

    IRange usedRange = worksheet.UsedRange;
    int rowIndexSheet1 = 1;
    int rowIndexSheet2 = 1;
    foreach (IRange row in  usedRange.Rows)
    {
        RowStorage rowStorage = WorksheetHelper.GetOrCreateRow(worksheet as IInternalWorksheet, rowIndexSheet1 - 1, false);
        if (rowStorage != null)
        {
            // Copy the Entire row to the next sheet
            IRange destinationRow = newWorksheet.Range[rowIndexSheet2, 1];
            row.EntireRow.CopyTo(destinationRow);
            rowIndexSheet2++;
        }
        rowIndexSheet1++;
    }

    //Remove the worksheet
    workbook.Worksheets[0].Remove();

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Loads an existing file
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx");
    IWorksheet worksheet = workbook.Worksheets[0];
    IWorksheet newWorksheet = workbook.Worksheets[1];

    IRange usedRange = worksheet.UsedRange;
    int rowIndexSheet1 = 1;
    int rowIndexSheet2 = 1;
    foreach (IRange row in  usedRange.Rows)
    {
        RowStorage rowStorage = WorksheetHelper.GetOrCreateRow(worksheet as IInternalWorksheet, rowIndexSheet1 - 1, false);
        if (rowStorage != null)
        {
            // Copy the Entire row to the next sheet
            IRange destinationRow = newWorksheet.Range[rowIndexSheet2, 1];
            row.EntireRow.CopyTo(destinationRow);
            rowIndexSheet2++;
        }
        rowIndexSheet1++;
    }

    //Remove the worksheet
    workbook.Worksheets[0].Remove();

    //Saving the workbook as stream
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx

    ' Loads an existing file
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx")
    Dim worksheet As IWorksheet = workbook.Worksheets(0)
    Dim newWorksheet As IWorksheet = workbook.Worksheets(1)

    Dim usedRange As IRange = worksheet.UsedRange
    Dim rowIndexSheet1 As Integer = 1
    Dim rowIndexSheet2 As Integer = 1
    For Each row As IRange In usedRange.Rows
        Dim rowStorage As RowStorage = WorksheetHelper.GetOrCreateRow(TryCast(worksheet, IInternalWorksheet), rowIndexSheet1 - 1, False)
        If rowStorage IsNot Nothing Then
            ' Copy the Entire row to the next sheet
            Dim destinationRow As IRange = newWorksheet.Range(rowIndexSheet2, 1)
            row.EntireRow.CopyTo(destinationRow)
            rowIndexSheet2 += 1
        End If
        rowIndexSheet1 += 1
    Next

    ' Remove the worksheet
    workbook.Worksheets(0).Remove()

    ' Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}