---
title: Set Background for Excel Worksheet | Syncfusion
description: We can set background for Excel Worksheet with a single image to be tiled to fill the whole screen.
platform: file-formats
control: XlsIO
documentation: UG
---

# Set Background for Excel Worksheet

Adding a picture to the background, either as a watermark of company’s logo, or a relevant image improves the appearance of the document. When we set a background picture of a worksheet, the picture is tiled so that it fills the whole screen, over and again.

The following code shows how to set image background for Excel worksheet with Interop and XlsIO for .NET. The process will assume that we already have the picture on our computer that we want to use as background image.

## Interop

{% tabs %}
{% highlight c# %}
private void SetWorksheetBackground()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a Workbook.
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the First sheet.
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Set a background picture for the sheet.
    worksheet.SetBackgroundPicture(@"d:\test\Syncfusion.png");

    //Save the excel file.
    workbook.SaveCopyAs(@"d:\test\InteropOutput_BackgroundPicture.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub SetWorksheetBackground()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a Workbook.
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the First sheet.
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Set a background picture for the sheet.
    worksheet.SetBackgroundPicture("d:\test\Syncfusion.png")

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_BackgroundPicture.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void SetWorksheetBackground()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Create a Workbook.
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the First sheet.
        IWorksheet worksheet = workbook.Worksheets[0];

        //Set a background picture for the sheet.
        worksheet.PageSetup.BackgoundImage = new Bitmap(@"d:\test\Syncfusion.png");

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_BackgroundPicture.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub SetWorksheetBackground()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Create a Workbook.
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the First sheet.
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Set a background picture for the sheet.
        worksheet.PageSetup.BackgoundImage = New Bitmap("d:\test\Syncfusion.png")

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_BackgroundPicture.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
