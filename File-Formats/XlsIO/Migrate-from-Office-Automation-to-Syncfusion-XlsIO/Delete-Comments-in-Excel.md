---
title: Delete Comments in Excel | Syncfusion
description: Explains with an example on how to programmatically delete Excel comments using Interop and Essential XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Delete Comments in Excel

You can also delete comments in Excel, which removes the red triangle in a cell.

The following code shows how to delete a comment from a cell with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void DeleteComment()
{
  //Instantiate the application object
  var excelApp = new Microsoft.Office.Interop.Excel.Application();

  //Specify the template Excel file path
  string myPath = "InteropOutput_AddComment.xlsx";

  //Open the Excel file containing comment
  Workbook workbook = excelApp.Workbooks.Open(myPath);

  //Get the A1 cell
  Range rng1 = excelApp.get_Range("A1", Missing.Value);

  //Remove the comment
  rng1.Comment.Delete();

  //Save the file
  workbook.SaveAs("InteropOutput_DeleteComment.xlsx");

  //Quit the application
  excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub DeleteComment()
  'Instantiate the application object
  Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

  'Specify the template Excel file path
  Dim myPath As String = "InteropOutput_AddComment.xlsx"

  'Open the Excel file
  Dim workbook As Workbook = excelApp.Workbooks.Open(myPath)

  'Get the A1 cell
  Dim rng1 As Range = excelApp.Range("A1")

  'Remove the comment
  rng1.Comment.Delete()

  'Save the file
  workbook.SaveCopyAs("InteropOutput_DeleteComment.xlsx")

  'Quit the application
  excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void DeleteComment()
{
  using (ExcelEngine excelEngine = new ExcelEngine())
  {
    //Instantiate the application object
    IApplication application = excelEngine.Excel;

    //Open the Excel file containing comment
    IWorkbook workbook = application.Workbooks.Open("XlsIOOutput_AddComment.xlsx");
    IWorksheet worksheet = workbook.Worksheets[0];

    //Remove the comment
    worksheet.Range["A1"].Comment.Remove();

    //Save the workbook
    workbook.SaveAs("XlsIOOutput_DeleteComment.xlsx");
  }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub DeleteComment()
  Using excelEngine As ExcelEngine = New ExcelEngine()
    'Instantiate the application object
    Dim application As IApplication = excelEngine.Excel

    'Open the Excel file containing comment
    Dim workbook As IWorkbook = application.Workbooks.Open("XlsIOOutput_AddComment.xlsx")
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Remove the comment.
    worksheet.Range("A1").Comment.Remove()

    'Save as Excel file
    workbook.SaveAs("XlsIOOutput_DeleteComment.xlsx")
  End Using
End Sub
{% endhighlight %}
{% endtabs %}
