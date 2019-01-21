---
title: Unhide Excel Worksheets | Syncfusion
description: We can unhide Excel worksheets which are in hidden state.
platform: file-formats
control: XlsIO
documentation: UG
---

# Unhide Excel Worksheets

Hidden sheets can be unhidden and made visible.

The following code shows how to unhide Excel worksheets with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void UnhideWorksheet()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Open the workbook with hidden worksheets.
    Workbook workbook = excelApp.Workbooks.Open(@"d:\test\InteropOutput_HiddenWorksheet.xlsx", Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value);

    //Get the First sheet.
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Unhide the worksheet.
    worksheet.Visible = XlSheetVisibility.xlSheetVisible;

    //Save the file.
    workbook.SaveCopyAs(@"d:\test\InteropOutput_UnhiddenWorksheet.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub UnhideWorksheet()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Open the workbook with hidden worksheets.
    Dim workbook As Workbook = excelApp.Workbooks.Open("d:\test\InteropOutput_HiddenWorksheet.xlsx", Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value)

    'Get the First sheet.
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Unhide the worksheet.
    worksheet.Visible = XlSheetVisibility.xlSheetVisible

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_UnhiddenWorksheet.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void UnhideWorksheet()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Open the workbook with hidden worksheets.
        IWorkbook workbook = application.Workbooks.Open(@"d:\test\XlsIOOutput_HiddenWorksheet.xlsx");

        //Get the First sheet.
        IWorksheet worksheet = workbook.Worksheets[0];

        //Unhide the worksheet.
        worksheet.Visibility = WorksheetVisibility.Visible;

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_UnhiddenWorksheet.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub UnhideWorksheet()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Open the excel file.
        Dim workbook As IWorkbook = application.Workbooks.Open("d:\test1\XlsIOOutput_HiddenWorksheet.xlsx")

        'Get the First sheet.
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Unhide the worksheet.
        worksheet.Visibility = WorksheetVisibility.Visible

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_UnhiddenWorksheet.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
