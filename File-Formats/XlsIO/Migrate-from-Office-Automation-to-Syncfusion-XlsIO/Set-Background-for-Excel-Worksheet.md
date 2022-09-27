---
title: Set Background for Excel Worksheet | Syncfusion
description: Explains with an example on how to set background for Excel Worksheet with a single image to be tiled to fill the whole screen using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Set Background for Excel Worksheet

Adding a picture to the background either as a watermark of company's logo or a relevant image will improve the appearance of the document. When you set background picture to a worksheet, the picture is tiled so that it fills the whole screen over and again.

The following code shows how to set Excel worksheet background image with Interop and XlsIO for .NET. The process will assume that you already have the picture on your computer to use as a background image.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void SetWorksheetBackground()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a workbook
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the first sheet
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Set a background picture for the sheet
    worksheet.SetBackgroundPicture(@"d:\test\Syncfusion.png");

    //Save the Excel file
    workbook.SaveCopyAs(@"d:\test\InteropOutput_BackgroundPicture.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub SetWorksheetBackground()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a workbook
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the first sheet
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Set a background picture for the sheet
    worksheet.SetBackgroundPicture("d:\test\Syncfusion.png")

    'Save the file
    workbook.SaveCopyAs("d:\test1\InteropOutput_BackgroundPicture.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void SetWorksheetBackground()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the first sheet
        IWorksheet worksheet = workbook.Worksheets[0];

        //Set a background picture for the sheet
        worksheet.PageSetup.BackgoundImage = new Bitmap(@"d:\test\Syncfusion.png");

        //Save the workbook
        workbook.SaveAs(@"d:\test\XlsIOOutput_BackgroundPicture.xlsx");
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub SetWorksheetBackground()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Create a workbook
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the first sheet
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Set a background picture for the sheet
        worksheet.PageSetup.BackgoundImage = New Bitmap("d:\test\Syncfusion.png")

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_BackgroundPicture.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
