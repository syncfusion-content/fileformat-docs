---
title: Delete Comments in Excel | Syncfusion
description: This page shows how to delete comments in Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Delete Comments in Excel

We can also delete comments in Excel which removes the red triangle in the cell.

The following code shows how to delete a comment from a cell with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void DeleteComment()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Specify the template excel file path.
    string myPath = @"d:\test\InteropOutput_AddComment.xlsx";

    //Open the excel file containing comment.
    Workbook workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value);

    //Get the A1 cell.
    Range rng1 = excelApp.get_Range("A1", Missing.Value);

    //Remove the comment.
    rng1.Comment.Delete();

    //Save the file.
    workbook.SaveAs(@"d:\test\InteropOutput_DeleteComment.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub DeleteComment()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Specify the template excel file path.
    Dim myPath As String = "d:\test\InteropOutput_AddComment.xlsx"

    'Open the excel file.
    Dim workbook As Workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value)

    'Get the A1 cell.
    Dim rng1 As Range = excelApp.Range("A1")

    'Remove the comment.
    rng1.Comment.Delete()

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_DeleteComment.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void DeleteComment()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Open the excel file containing comment.
        IWorkbook workbook = application.Workbooks.Open(@"d:\test\XlsIOOutput_AddComment.xlsx");
        IWorksheet worksheet = workbook.Worksheets[0];

        //Remove the comment.
        worksheet.Range["A1"].Comment.Remove();

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_DeleteComment.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub DeleteComment()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Open the excel file containing comment.
        Dim workbook As IWorkbook = application.Workbooks.Open("d:\test1\XlsIOOutput_AddComment.xlsx")
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Remove the comment.
        worksheet.Range("A1").Comment.Remove()

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_DeleteComment.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
