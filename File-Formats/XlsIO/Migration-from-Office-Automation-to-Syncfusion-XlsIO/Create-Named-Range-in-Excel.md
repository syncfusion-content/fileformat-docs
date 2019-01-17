---
title: Create Named Range in Excel
description: Named range can be created by giving unique name to one or more cells which makes us to call the range using their name instead of using the cell reference.
platform: file-formats
control: XlsIO
documentation: UG
---

# Create Named Range in Excel

Users can have a privilege to provide names to a specific cell, a range of cells, function, constant or table. Instead of using the cell reference, we can simply use the name assigned to the cell. By using names, we can make our formulas much easier to understand and maintain.

The following code shows how to create named range in Excel with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void CreateNamedRange()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a Workbook.
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the First sheet.
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Create a named range.
    Range range = (Range)worksheet.get_Range("A1:B4", Type.Missing);
    range.Name = "Test_Range";
    worksheet.Range["Test_Range"].Value = "Test";

    //Save the file.
    workbook.SaveCopyAs(@"d:\test\InteropOutput_NamedRange.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub CreateNamedRange()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a Workbook.
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the First sheet.
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Create a named range.
    Dim range As Range = CType(worksheet.Range("A1:B4"), Range)
    range.Name = "Test_Range"
    worksheet.Range("Test_Range").Value = "Test"

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_NamedRange.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void CreateNamedRange()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Create a Workbook.
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the First sheet.
        IWorksheet worksheet = workbook.Worksheets[0];

        //Create a named range.
        IName name = workbook.Names.Add("Test_Range");
        name.RefersToRange = worksheet.Range["A1:B4"];
        worksheet.Range["Test_Range"].Text = "Test";

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_NamedRange.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub CreateNamedRange()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Create a Workbook.
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the First sheet.
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Create a named range.
        Dim name As IName = workbook.Names.Add("Test_Range")
        name.RefersToRange = worksheet.Range("A1:B4")
        worksheet.Range("Test_Range").Text = "Test"

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_NamedRange.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
