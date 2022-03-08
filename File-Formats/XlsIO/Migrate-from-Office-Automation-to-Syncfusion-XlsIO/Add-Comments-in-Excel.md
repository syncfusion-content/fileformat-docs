---
title: Add Comments in Excel | Syncfusion
description: Explains with an example on how to add Excel comments programmatically using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Add Comments in Excel

You can add comments in Excel to give feedback about the content of a cell. A red triangle in the upper-right corner of a cell indicates comment. By default, a comment can be seen only when you hover over the cell that contains the comment.

The following code shows how to add a comment with text to a cell using Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight C# %}
private void AddComment()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a workbook
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the A1 cell
    Range rng1 = excelApp.get_Range("A1", Missing.Value);

    //Add the comment with text
    rng1.AddComment("This is my comment");

    //Save the file
    workbook.SaveAs(@"d:\test\InteropOutput_AddComment.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight VB.NET %}
Private Sub AddComment()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a workbook
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the A1 cell
    Dim rng1 As Range = excelApp.Range("A1")

    'Add the comment with text
    rng1.AddComment("This is my comment")

    'Save the file
    workbook.SaveCopyAs("d:\test1\InteropOutput_AddComment.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight C# %}
private void AddComment()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);
        IWorksheet worksheet = workbook.Worksheets[0];

        //Add comments to a cell
        IComment comment = worksheet.Range["A1"].AddComment();
        comment.Text = "This is my comment";

        //Save the workbook
        workbook.SaveAs(@"d:\test\XlsIOOutput_AddComment.xlsx");
    }
}
{% endhighlight %}

{% highlight VB.NET %}
Private Sub AddComment()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Create a workbook
        Dim workbook As IWorkbook = application.Workbooks.Create(1)
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Add comments to a cell
        Dim comment As IComment = worksheet.Range("A1").AddComment()
        comment.Text = "This is my comment"

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_AddComment.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
