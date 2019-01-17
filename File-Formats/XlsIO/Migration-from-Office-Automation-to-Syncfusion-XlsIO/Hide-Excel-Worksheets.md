---
title: Hide Excel Worksheets
description: We can hide Excel worksheets so that a user cannot see them when opening the workbook.
platform: file-formats
control: XlsIO
documentation: UG
---

# Hide Excel Worksheets

We can hide any type of sheet in a workbook so that a user cannot see them when opening the workbook, but we must always leave at least one sheet visible.
A sheet can be Visible, Hidden or Very Hidden.

* A visible sheet’s tab appears in the bottom of the Excel window, enabling the user to click the tab for navigation into the sheet. By default, all new sheets are visible.
* If a sheet is hidden, the sheet’s tab is gone. The sheet itself however, is not gone. Formulas can still retrieve values stored on a hidden sheet. It just disappears from the user interface.
* The difference between a hidden sheet and a very hidden sheet is simply this: very hidden sheets do not appear in the Unhide dialog box.

The following code shows how to hide Excel worksheets with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void HideWorksheet()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a Workbook.
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Add a worksheet to the workbook.
    Worksheet newWorksheet = excelApp.Worksheets.Add(Missing.Value, Missing.Value, Missing.Value, Missing.Value);

    //Get the First sheet.
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Hide the worksheet.
    worksheet.Visible = XlSheetVisibility.xlSheetHidden;

    //Save the file.
    workbook.SaveCopyAs(@"d:\test\InteropOutput_HiddenWorksheet.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub HideWorksheet()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a Workbook.
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Add a worksheet to the workbook.
    Dim newWorksheet As Worksheet = excelApp.Worksheets.Add(Missing.Value, Missing.Value, Missing.Value, Missing.Value)

    'Get the First sheet.
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Hide the worksheet.
    worksheet.Visible = XlSheetVisibility.xlSheetHidden

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_HiddenWorksheet.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void HideWorksheet()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Create a Workbook.
        IWorkbook workbook = application.Workbooks.Create(1);

        //Add a worksheet to the workbook.
        IWorksheet newWorksheet = workbook.Worksheets.Create();

        //Get the First sheet.
        IWorksheet worksheet = workbook.Worksheets[0];

        //Hide the worksheet.
        worksheet.Visibility = WorksheetVisibility.Hidden;

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_HiddenWorksheet.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub HideWorksheet()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Create a Workbook.
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Add a worksheet to the workbook.
        Dim newWorksheet As IWorksheet = workbook.Worksheets.Create()

        'Get the First sheet.
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Hide the worksheet.
        worksheet.Visibility = WorksheetVisibility.Hidden

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_HiddenWorksheet.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
