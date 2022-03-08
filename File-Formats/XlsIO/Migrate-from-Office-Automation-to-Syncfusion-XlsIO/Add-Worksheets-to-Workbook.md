---
title: Add Worksheets to Workbook | Syncfusion
description: Explains with an example on how to programmatically add worksheets to a workbook when working with template Excel document using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Add Worksheets to Workbook

While handling Excel templates, you should add worksheets to workbook to fill certain data and manipulate it.

The following code shows how to add five worksheets within a workbook with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight C# %}
private void AddWorksheet()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Specify the template Excel file path
    string myPath = @"d:\test\Sample.xlsx";

    //Open the Excel file
    Workbook workbook = excelApp.Workbooks.Open(myPath);

    //Declare a worksheet object
    Worksheet newWorksheet;

    //Add five new worksheets to the workbook and fill some data into the cells
    for (int i = 1; i <= 5; i++)
    {
        //Add a worksheet to the workbook
        newWorksheet = excelApp.Worksheets.Add(Missing.Value, Missing.Value, Missing.Value, Missing.Value);

        //Name the sheet
        newWorksheet.Name = "New_Sheet" + i.ToString();

        //Get the cells collection
        Range cells = newWorksheet.Cells;

        //Input a string value to a cell of the sheet
        cells.set_Item(i, i, "New_Sheet" + i.ToString());
    }

    //Save as Excel file
    workbook.SaveCopyAs(@"d:\test\InteropOutput_AddWorksheet.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight VB.NET %}
Private Sub AddWorksheet()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Specify the template Excel file path
    Dim myPath As String = "d:\test1\Sample.xlsx"

    'Open the Excel file
    Dim workbook As Workbook = excelApp.Workbooks.Open(myPath)

    'Declare a worksheet object
    Dim newWorksheet As Worksheet

    'Add five new worksheets to the workbook And fill some data into the cells
    For i As Integer = 1 To 5
        'Add a worksheet to the workbook
        newWorksheet = excelApp.Worksheets.Add(Missing.Value, Missing.Value, Missing.Value, Missing.Value)

        'Name the sheet
        newWorksheet.Name = "New_Sheet" & i.ToString()

        'Get the cells collection
        Dim cells As Range = newWorksheet.Cells

        'Input a string value to a cell of the sheet
        cells.Item(i, i) = "New_Sheet" & i.ToString()
    Next

    'Save as Excel file
    workbook.SaveCopyAs("d:\test1\InteropOutput_AddWorksheet.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight C# %}
private void AddWorksheet()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object                
        IApplication application = excelEngine.Excel;

        //Specify the template Excel file path
        string myPath = @"d:\test\Sample.xlsx";

        //Instantiate a new workbook
        //Open the Excel file
        IWorkbook workbook = application.Workbooks.Open(myPath);

        //Declare a worksheet object
        IWorksheet newWorksheet;

        //Add five new worksheets to the workbook and fill some data into the cells
        for (int i = 1; i <= 5; i++)
        {
            //Add a worksheet to the workbook
            newWorksheet = workbook.Worksheets.Create("New_Sheet" + (i).ToString());

            //Get the cells collection
            IRange cells = newWorksheet.Range;

            //Input a string value to a cell of the sheet
            cells[i, i].Value = "New_Sheet" + (i).ToString();
        }

        //Save as Excel file
        workbook.SaveAs(@"d:\test\XlsIOOutput_AddWorksheet.xlsx");
    }
}
{% endhighlight %}

{% highlight VB.NET %}
Private Sub AddWorksheet()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Specify the template Excel file path
        Dim myPath As String = "d:\test\Sample.xlsx"

        'Instantiate a new workbook
        'Open the Excel file
        Dim workbook As IWorkbook = application.Workbooks.Open(myPath)

        'Declare a worksheet object
        Dim newWorksheet As IWorksheet

        'Add five new worksheets to the workbook and fill some data into the cells
        For i As Integer = 1 To 5
            'Add a worksheet to the workbook
            newWorksheet = workbook.Worksheets.Create("New_Sheet" & (i).ToString())

            'Get the cells collection
            Dim cells As IRange = newWorksheet.Range

            'Input a string value to a cell of the sheet
            cells(i, i).Value = "New_Sheet" & (i).ToString()
        Next

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_AddWorksheet.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
