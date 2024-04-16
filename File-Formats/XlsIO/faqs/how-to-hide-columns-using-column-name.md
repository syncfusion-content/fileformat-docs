---
title: How to hide columns using column name |Syncfusion.
description: This page explains how to hide columns using column name using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to hide columns using column name?

The following code illustrates how to hide columns using column name.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Loads an existing file
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream);
    IWorksheet worksheet = workbook.Worksheets[0];

    List<string> columnsToHide = new List<string> { "column1", "column2", "column3" };

    foreach (string columnName in columnsToHide)
    {
        IRange headerCell = worksheet.UsedRange.FindFirst(columnName, ExcelFindType.Text);
        if (headerCell != null)
        {
            int columnIndex = headerCell.Column;

            // Hide the column
            worksheet.ShowColumn(columnIndex, false);
        }
    }

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
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Loads an existing file
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx");
    IWorksheet worksheet = workbook.Worksheets[0];

    List<string> columnsToHide = new List<string> { "column1", "column2", "column3" };

    foreach (string columnName in columnsToHide)
    {
        IRange headerCell = worksheet.UsedRange.FindFirst(columnName, ExcelFindType.Text);
        if (headerCell != null)
        {
            int columnIndex = headerCell.Column;

            // Hide the column
            worksheet.ShowColumn(columnIndex, false);
        }
    }

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx

    ' Loads an existing file
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx")
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim columnsToHide As List(Of String) = New List(Of String) From {"column1", "column2", "column3"}

    For Each columnName As String In columnsToHide
        Dim headerCell As IRange = worksheet.UsedRange.FindFirst(columnName, ExcelFindType.Text)
        If headerCell IsNot Nothing Then
            Dim columnIndex As Integer = headerCell.Column

            ' Hide the column
            worksheet.ShowColumn(columnIndex, False)
        End If
    Next

    ' Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}
