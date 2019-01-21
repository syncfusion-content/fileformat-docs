---
title: Add Worksheets to Workbook | Syncfusion
description: This page shows how to add worksheets to workbook when working with template Excel document.
platform: file-formats
control: XlsIO
documentation: UG
---

# Add Worksheets to Workbook

While handling Excel templates, we may need to add worksheets to workbook to fill certain data and manipulate it.

The following code shows how to add 5 worksheets within a workbook with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void AddWorksheet()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Specify the template excel file path.
    string myPath = @"d:\test\Sample.xlsx";

    //Open the excel file.
    Workbook workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value);

    //Declare a Worksheet object.
    Worksheet newWorksheet;

    //Add 5 new worksheets to the workbook and fill some data into the cells.
    for (int i = 1; i <= 5; i++)
    {
        //Add a worksheet to the workbook.
        newWorksheet = excelApp.Worksheets.Add(Missing.Value, Missing.Value, Missing.Value, Missing.Value);

        //Name the sheet.
        newWorksheet.Name = "New_Sheet" + i.ToString();

        //Get the Cells collection.
        Range cells = newWorksheet.Cells;

        //Input a string value to a cell of the sheet.
        cells.set_Item(i, i, "New_Sheet" + i.ToString());
    }

    //Save as excel file.
    workbook.SaveCopyAs(@"d:\test\InteropOutput_AddWorksheet.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub AddWorksheet()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Specify the template excel file path.
    Dim myPath As String = "d:\test1\Sample.xlsx"

    'Open the excel file.
    Dim workbook As Workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value)

    'Declare a Worksheet object.
    Dim newWorksheet As Worksheet

    'Add 5 New worksheets to the workbook And fill some data into the cells.
    For i As Integer = 1 To 5
        'Add a worksheet to the workbook.
        newWorksheet = excelApp.Worksheets.Add(Missing.Value, Missing.Value, Missing.Value, Missing.Value)

        'Name the sheet.
        newWorksheet.Name = "New_Sheet" & i.ToString()

        'Get the Cells collection.
        Dim cells As Range = newWorksheet.Cells

        'Input a string value to a cell of the sheet.
        cells.Item(i, i) = "New_Sheet" & i.ToString()
    Next

    'Save as excel file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_AddWorksheet.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void AddWorksheet()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.                
        IApplication application = excelEngine.Excel;

        //Specify the template excel file path.
        string myPath = @"d:\test\Sample.xlsx";

        //Instantiate a new Workbook.
        //Open the excel file.
        IWorkbook workbook = application.Workbooks.Open(myPath);

        //Declare a Worksheet object.
        IWorksheet newWorksheet;

        //Add 5 new worksheets to the workbook and fill some data into the cells.
        for (int i = 1; i <= 5; i++)
        {
            //Add a worksheet to the workbook.
            newWorksheet = workbook.Worksheets.Create("New_Sheet" + (i).ToString());

            //Get the Cells collection.
            IRange cells = newWorksheet.Range;

            //Input a string value to a cell of the sheet.
            cells[i, i].Value = "New_Sheet" + (i).ToString();
        }

        //Save as excel file.
        workbook.SaveAs(@"d:\test\XlsIOOutput_AddWorksheet.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub AddWorksheet()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Specify the template excel file path.
        Dim myPath As String = "d:\test\Sample.xlsx"

        'Instantiate a New Workbook.
        'Open the excel file.
        Dim workbook As IWorkbook = application.Workbooks.Open(myPath)

        'Declare a Worksheet object.
        Dim newWorksheet As IWorksheet

        'Add 5 new worksheets to the workbook and fill some data into the cells.
        For i As Integer = 1 To 5
            'Add a worksheet to the workbook.
            newWorksheet = workbook.Worksheets.Create("New_Sheet" & (i).ToString())

            'Get the Cells collection.
            Dim cells As IRange = newWorksheet.Range

            'Input a string value to a cell of the sheet.
            cells(i, i).Value = "New_Sheet" & (i).ToString()
        Next

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_AddWorksheet.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
