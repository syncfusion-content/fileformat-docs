---
title: Rotate Text in Cells | Syncfusion
description: Text in cells can be rotated to add visual impact to a spreadsheet or a presentation.
platform: file-formats
control: XlsIO
documentation: UG
---

# Rotate Text in Cells

When a text is entered, it is positioned horizontally by default. However, we may want to rotate text in cells to add visual impact to a spreadsheet or a presentation. Orientation or Rotation allows to rotate text in a variety of ways.

The following code shows how to change the formatting of a cell to rotate text in the desired direction with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void RotateText()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a Workbook.
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the First sheet.
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Put some text into cell B2.
    worksheet.Cells[2, 2] = "Syncfusion Software";

    //Define a range object(B2).
    Range range;
    range = worksheet.get_Range("B2", "B2");

    //Specify the angle of rotation of the text.
    range.Orientation = 45;

    //Set the background color.
    range.Interior.Color = System.Drawing.ColorTranslator.ToWin32(Color.FromArgb(0, 51, 105));

    //Set the font color of cell text.
    range.Font.Color = System.Drawing.ColorTranslator.ToOle(System.Drawing.Color.White);

    //Save the excel file.
    workbook.SaveCopyAs(@"d:\test\InteropOutput_RotateText.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub RotateText()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a Workbook.
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the First sheet.
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Put some text into cell B2.
    worksheet.Cells(2, 2) = "Syncfusion Software"

    'Define a range object(B2).
    Dim range As Range
    range = worksheet.Range("B2", "B2")

    'Specify the angle of rotation of the text.
    range.Orientation = 45

    'Set the background color.
    range.Interior.Color = System.Drawing.ColorTranslator.ToWin32(Color.FromArgb(0, 51, 105))

    'Set the font color of cell text.
    range.Font.Color = System.Drawing.ColorTranslator.ToOle(System.Drawing.Color.White)

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_RotateText.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void RotateText()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Create a Workbook.
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the First sheet.
        IWorksheet worksheet = workbook.Worksheets[0];

        //Get a particular Cell.
        IRange range = worksheet.Range["B2"];

        //Put some text value.
        range.Value = "Syncfusion Software";

        //Specify the angle of rotation of the text.
        range.CellStyle.Rotation = 45;

        //Set the background color.
        range.CellStyle.Color = Color.FromArgb(0, 51, 105);

        //Set the font color of cell text.
        range.CellStyle.Font.Color = ExcelKnownColors.White;

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_RotateText.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub RotateText()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Create a Workbook.
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the First sheet.
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Get a particular Cell.
        Dim range As IRange = worksheet.Range("B2")

        'Put some text value.
        range.Value = "Syncfusion Software"

        'Specify the angle of rotation of the text.
        range.CellStyle.Rotation = 45

        'Set the background color.
        range.CellStyle.Color = Color.FromArgb(0, 51, 105)

        'Set the font color of cell text.
        range.CellStyle.Font.Color = ExcelKnownColors.White

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_RotateText.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
