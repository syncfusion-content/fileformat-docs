---
title: Add Hyperlinks in Excel | Syncfusion
description: This page shows how to add hyperlinks in Excel, programmatically.
platform: file-formats
control: XlsIO
documentation: UG
---

# Add Hyperlinks in Excel

A hyperlink is a reference to a specific location, document or web-page that the user can jump to by clicking the link in a cell. Hyperlinks are easily recognizable because this is a text highlighted with underlined blue color.

The following code shows how to add hyperlinks in Excel with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void AddHyperlinks()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a Workbook.
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the First sheet.
    Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

    //Define a range object(A1).
    Range range;
    range = worksheet.get_Range("A1", "A1");

    //Add a hyperlink to it.
    worksheet.Hyperlinks.Add(range, "https://www.syncfusion.com/", Type.Missing, "Click to go to Syncfusion site", "Syncfusion Site!");

    //Save the file.
    workbook.SaveCopyAs(@"d:\test\InteropOutput_Hyperlinks.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub AddHyperlinks()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a Workbook.
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the First sheet.
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Define a range object(A1).
    Dim range As Range
    range = worksheet.Range("A1", "A1")

    'Add a hyperlink to it.
    worksheet.Hyperlinks.Add(range, "https://www.syncfusion.com/", Type.Missing, "Click to go to Syncfusion site", "Syncfusion Site!")

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_Hyperlinks.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void AddHyperlinks()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Create a Workbook.
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the First sheet.
        IWorksheet worksheet = workbook.Worksheets[0];

        //Create a Hyperlink for a Website.
        IHyperLink hyperlink = worksheet.HyperLinks.Add(worksheet.Range["A1"]);
        hyperlink.Type = ExcelHyperLinkType.Url;
        hyperlink.Address = "http://www.syncfusion.com";
        hyperlink.ScreenTip = "To know more about Syncfusion products, go through this link.";
        hyperlink.TextToDisplay = "Syncfusion Site!";

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_Hyperlinks.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub AddHyperlinks()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Create a Workbook.
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the First sheet.
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Create a Hyperlink for a Website.
        Dim hyperlink As IHyperLink = worksheet.HyperLinks.Add(worksheet.Range("A1"))
        hyperlink.Type = ExcelHyperLinkType.Url
        hyperlink.Address = "http://www.syncfusion.com"
        hyperlink.ScreenTip = "To know more about Syncfusion products, go through this link."
        hyperlink.TextToDisplay = "Syncfusion Site!"

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_Hyperlinks.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
