---
title: Filter Excel Data | Syncfusion
description: We can filter Excel data with specific conditions to show or hide certain rows.
platform: file-formats
control: XlsIO
documentation: UG
---

# Filter Excel Data

Auto filtering data allows to view specific rows in a worksheet, while hiding the other rows. When an AutoFilter is added to the header row, a drop-down menu appears in each cell of the header row which provides filter options that can be used to specify the rows to be displayed. We can achieve it programmatically by specifying conditions.

The following code shows how to auto filter Excel data with specific conditions using Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void FilterData()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a Workbook.
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the First sheet.
    Worksheet sheet = workbook.Sheets["Sheet1"];

    //Add data into A1 and B1 Cells as headers.
    sheet.Cells[1, 1] = "Product ID";
    sheet.Cells[1, 2] = "Product Name";

    //Add data into cells.
    sheet.Cells[2, 1] = 1;
    sheet.Cells[3, 1] = 2;
    sheet.Cells[4, 1] = 3;
    sheet.Cells[5, 1] = 4;
    sheet.Cells[2, 2] = "Apples";
    sheet.Cells[3, 2] = "Bananas";
    sheet.Cells[4, 2] = "Grapes";
    sheet.Cells[5, 2] = "Oranges";

    //Enable Auto-filter.
    sheet.EnableAutoFilter = true;

    //Create the range.
    Range range = sheet.get_Range("A1", "B5");

    //Auto-filter the range.
    range.AutoFilter("1", "<>", XlAutoFilterOperator.xlOr, "", true);

    //Auto-fit the second column.
    sheet.get_Range("B1", "B5").EntireColumn.AutoFit();

    //Save the excel file.
    workbook.SaveCopyAs(@"d:\test\InteropOutput_AutoFilter.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub FilterData()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a Workbook.
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the First sheet.
    Dim sheet As Worksheet = workbook.Sheets("Sheet1")

    'Add data into A1 and B1 Cells as headers.
    sheet.Cells(1, 1) = "Product ID"
    sheet.Cells(1, 2) = "Product Name"

    'Add data into cells.
    sheet.Cells(2, 1) = 1
    sheet.Cells(3, 1) = 2
    sheet.Cells(4, 1) = 3
    sheet.Cells(5, 1) = 4
    sheet.Cells(2, 2) = "Apples"
    sheet.Cells(3, 2) = "Bananas"
    sheet.Cells(4, 2) = "Grapes"
    sheet.Cells(5, 2) = "Oranges"

    'Enable Auto-filter.
    sheet.EnableAutoFilter = True

    'Create the range.
    Dim range As Range = sheet.Range("A1", "B5")

    'Auto-filter the range.
    range.AutoFilter("1", "<>", XlAutoFilterOperator.xlOr, "", True)

    'Auto-fit the second column.
    sheet.Range("B1", "B5").EntireColumn.AutoFit()

    'Save the excel file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_AutoFilter.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void FilterData()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Create a Workbook.
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the First sheet.
        IWorksheet worksheet = workbook.Worksheets[0];

        //Add data into A1 and B1 Cells as headers.
        worksheet[1, 1].Value = "Product ID";
        worksheet[1, 2].Value = "Product Name";

        //Add data into cells.
        worksheet[2, 1].Value2 = 1;
        worksheet[3, 1].Value2 = 2;
        worksheet[4, 1].Value2 = 3;
        worksheet[5, 1].Value2 = 4;
        worksheet[2, 2].Value = "Apples";
        worksheet[3, 2].Value = "Bananas";
        worksheet[4, 2].Value = "Grapes";
        worksheet[5, 2].Value = "Oranges";

        //Create an AutoFilter in the first worksheet. Specify the AutoFilter range.
        worksheet.AutoFilters.FilterRange = worksheet.Range["A1:B5"];

        //Column index to which AutoFilter must be applied.
        IAutoFilter filter = worksheet.AutoFilters[0];

        //Specify first condition.
        IAutoFilterCondition firstCondition = filter.FirstCondition;
        firstCondition.ConditionOperator = ExcelFilterCondition.Contains;
        firstCondition.String = "";

        //Auto-fit the second column.
        worksheet.Range["B1:B5"].EntireColumn.AutofitColumns();

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_AutoFilter.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub FilterData()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Create a Workbook.
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the First sheet.
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Add data into A1 and B1 Cells as headers.
        worksheet(1, 1).Value = "Product ID"
        worksheet(1, 2).Value = "Product Name"

        'Add data into cells.
        worksheet(2, 1).Value2 = 1
        worksheet(3, 1).Value2 = 2
        worksheet(4, 1).Value2 = 3
        worksheet(5, 1).Value2 = 4
        worksheet(2, 2).Value = "Apples"
        worksheet(3, 2).Value = "Bananas"
        worksheet(4, 2).Value = "Grapes"
        worksheet(5, 2).Value = "Oranges"

        'Create an AutoFilter in the first worksheet. Specify the AutoFilter range.
        worksheet.AutoFilters.FilterRange = worksheet.Range("A1:B5")

        'Column index to which AutoFilter must be applied.
        Dim filter As IAutoFilter = worksheet.AutoFilters(0)

        'Specify first condition.
        Dim firstCondition As IAutoFilterCondition = filter.FirstCondition
        firstCondition.ConditionOperator = ExcelFilterCondition.Contains
        firstCondition.String = ""

        'Auto-fit the second column.
        worksheet.Range("B1:B5").EntireColumn.AutofitColumns()

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_AutoFilter.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
