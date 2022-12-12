---
title: Rotate Text in Cells | Syncfusion
description: Explains with an example on how to rotate text in cells programmatically, to add visual impact to a spreadsheet or a presentation using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Rotate Text in Cells

When a text is entered, it is placed horizontally by default. However, you may need to rotate text in cells to add visual impact to a spreadsheet or presentation. Orientation or rotation allows rotating text in various ways.

The following code shows how to change the formatting of a cell to rotate text in the desired direction with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void RotateText()
{
  //Instantiate the application object
  var excelApp = new Microsoft.Office.Interop.Excel.Application();

  //Add a workbook
  Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

  //Get the first sheet
  Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

  //Put some text into cell B2
  worksheet.Cells[2, 2] = "Syncfusion Software";

  //Define a range object (B2)
  Range range;
  range = worksheet.get_Range("B2", "B2");

  //Specify the angle of rotation of the text
  range.Orientation = 45;

  //Set the background color
  range.Interior.Color = System.Drawing.ColorTranslator.ToWin32(Color.FromArgb(0, 51, 105));

  //Set the font color of cell text
  range.Font.Color = System.Drawing.ColorTranslator.ToOle(System.Drawing.Color.White);

  //Save the Excel file
  workbook.SaveCopyAs("InteropOutput_RotateText.xlsx");

  //Quit the application
  excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub RotateText()
  'Instantiate the application object
  Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

  'Add a workbook
  Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

  'Get the first sheet
  Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

  'Put some text into cell B2
  worksheet.Cells(2, 2) = "Syncfusion Software"

  'Define a range object (B2)
  Dim range As Range
  range = worksheet.Range("B2", "B2")

  'Specify the angle of rotation of the text
  range.Orientation = 45

  'Set the background color
  range.Interior.Color = System.Drawing.ColorTranslator.ToWin32(Color.FromArgb(0, 51, 105))

  'Set the font color of cell text
  range.Font.Color = System.Drawing.ColorTranslator.ToOle(System.Drawing.Color.White)

  'Save the file
  workbook.SaveCopyAs("InteropOutput_RotateText.xlsx")

  'Quit the application
  excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void RotateText()
{
  using (ExcelEngine excelEngine = new ExcelEngine())
  {
    //Instantiate the application object
    IApplication application = excelEngine.Excel;

    //Create a workbook
    IWorkbook workbook = application.Workbooks.Create(1);

    //Get the first sheet
    IWorksheet worksheet = workbook.Worksheets[0];

    //Get a particular cell
    IRange range = worksheet.Range["B2"];

    //Put some text value
    range.Value = "Syncfusion Software";

    //Specify the angle of rotation of the text
    range.CellStyle.Rotation = 45;

    //Set the background color
    range.CellStyle.Color = Color.FromArgb(0, 51, 105);

    //Set the font color of cell text
    range.CellStyle.Font.Color = ExcelKnownColors.White;

    //Save the workbook
    workbook.SaveAs("XlsIOOutput_RotateText.xlsx");
  }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub RotateText()
  Using excelEngine As ExcelEngine = New ExcelEngine()
    'Instantiate the application object
    Dim application As IApplication = excelEngine.Excel

    'Create a workbook
    Dim workbook As IWorkbook = application.Workbooks.Create(1)

    'Get the first sheet
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Get a particular cell
    Dim range As IRange = worksheet.Range("B2")

    'Put some text value
    range.Value = "Syncfusion Software"

    'Specify the angle of rotation of the text
    range.CellStyle.Rotation = 45

    'Set the background color
    range.CellStyle.Color = Color.FromArgb(0, 51, 105)

    'Set the font color of cell text
    range.CellStyle.Font.Color = ExcelKnownColors.White

    'Save as Excel file
    workbook.SaveAs("XlsIOOutput_RotateText.xlsx")
  End Using
End Sub
{% endhighlight %}
{% endtabs %}
