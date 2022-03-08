---
title: Hide Excel Worksheets | Syncfusion
description: This documentation explains with an example on how to hide Excel worksheets programmatically using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Hide Excel Worksheets

You can hide any type of sheet in a workbook so that, users cannot see that when opening the workbook, but, you must always leave at least one sheet visible.
A sheet can be visible, hidden, or very hidden.

* A visible sheets tab appears in the bottom of the Excel window enabling users to click the tab for navigating to the sheet. By default, all new sheets are visible.
* If a sheet is hidden, the sheets tab will only disappear. Formulas can still retrieve values stored on a hidden sheet. It just disappears from the user interface.
* The difference between a hidden sheet and a very hidden sheet is, very hidden sheets do not appear in the unhide dialog box.

The following code shows how to hide Excel worksheets with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void HideWorksheet()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a workbook
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Add a worksheet to the workbook
    Worksheet newWorksheet = excelApp.Worksheets.Add(Missing.Value, Missing.Value, Missing.Value, Missing.Value);

    //Get the first sheet
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Hide the worksheet
    worksheet.Visible = XlSheetVisibility.xlSheetHidden;

    //Save the file
    workbook.SaveCopyAs(@"d:\test\InteropOutput_HiddenWorksheet.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub HideWorksheet()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a workbook
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Add a worksheet to the workbook
    Dim newWorksheet As Worksheet = excelApp.Worksheets.Add(Missing.Value, Missing.Value, Missing.Value, Missing.Value)

    'Get the first sheet
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Hide the worksheet
    worksheet.Visible = XlSheetVisibility.xlSheetHidden

    'Save the file
    workbook.SaveCopyAs("d:\test1\InteropOutput_HiddenWorksheet.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void HideWorksheet()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);

        //Add a worksheet to the workbook
        IWorksheet newWorksheet = workbook.Worksheets.Create();

        //Get the first sheet
        IWorksheet worksheet = workbook.Worksheets[0];

        //Hide the worksheet
        worksheet.Visibility = WorksheetVisibility.Hidden;

        //Save the workbook
        workbook.SaveAs(@"d:\test\XlsIOOutput_HiddenWorksheet.xlsx");
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub HideWorksheet()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Create a workbook
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Add a worksheet to the workbook
        Dim newWorksheet As IWorksheet = workbook.Worksheets.Create()

        'Get the first sheet
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Hide the worksheet
        worksheet.Visibility = WorksheetVisibility.Hidden

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_HiddenWorksheet.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
