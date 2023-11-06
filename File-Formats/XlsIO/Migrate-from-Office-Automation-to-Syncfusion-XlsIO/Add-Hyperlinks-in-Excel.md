---
title: Add Hyperlinks in Excel | Syncfusion
description: Explains with an example on how to programmatically add hyperlinks in Excel using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Add Hyperlinks in Excel

A hyperlink is a reference to a specific location, document, or webpage that the user can jump to by clicking the link in a cell. Hyperlinks are easily recognizable because this is a text highlighted with underlined blue color.

The following code shows how to add hyperlinks in Excel with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void AddHyperlinks()
{
  //Instantiate the application object
  var excelApp = new Microsoft.Office.Interop.Excel.Application();

  //Add a workbook
  Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

  //Get the first sheet
  Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

  //Define a range object (A1)
  Range range;
  range = worksheet.get_Range("A1", "A1");

  //Add a hyperlink to it
  worksheet.Hyperlinks.Add(range, "https://www.syncfusion.com/", Type.Missing, "Click to go to Syncfusion site", "Syncfusion Site!");

  //Save the file
  workbook.SaveCopyAs("InteropOutput_Hyperlinks.xlsx");

  //Quit the application
  excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub AddHyperlinks()
  'Instantiate the application object
  Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

  'Add a workbook
  Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

  'Get the first sheet
  Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

  'Define a range object (A1)
  Dim range As Range
  range = worksheet.Range("A1", "A1")

  'Add a hyperlink to it
  worksheet.Hyperlinks.Add(range, "https://www.syncfusion.com/", Type.Missing, "Click to go to Syncfusion site", "Syncfusion Site!")

  'Save the file
  workbook.SaveCopyAs("InteropOutput_Hyperlinks.xlsx")

  'Quit the application
  excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void AddHyperlinks()
{
  using (ExcelEngine excelEngine = new ExcelEngine())
  {
    //Instantiate the application object
    IApplication application = excelEngine.Excel;

    //Create a workbook
    IWorkbook workbook = application.Workbooks.Create(1);

    //Get the first sheet
    IWorksheet worksheet = workbook.Worksheets[0];

    //Create a hyperlink for a website
    IHyperLink hyperlink = worksheet.HyperLinks.Add(worksheet.Range["A1"]);
    hyperlink.Type = ExcelHyperLinkType.Url;
    hyperlink.Address = "http://www.syncfusion.com";
    hyperlink.ScreenTip = "To know more about Syncfusion products, go through this link.";
    hyperlink.TextToDisplay = "Syncfusion Site!";

    //Save the workbook
    workbook.SaveAs(@"XlsIOOutput_Hyperlinks.xlsx");
  }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub AddHyperlinks()
  Using excelEngine As ExcelEngine = New ExcelEngine()
    'Instantiate the application object
    Dim application As IApplication = excelEngine.Excel

    'Create a workbook
    Dim workbook As IWorkbook = application.Workbooks.Create(1)

    'Get the first sheet
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Create a hyperlink for a website
    Dim hyperlink As IHyperLink = worksheet.HyperLinks.Add(worksheet.Range("A1"))
    hyperlink.Type = ExcelHyperLinkType.Url
    hyperlink.Address = "http://www.syncfusion.com"
    hyperlink.ScreenTip = "To know more about Syncfusion products, go through this link."
    hyperlink.TextToDisplay = "Syncfusion Site!"

    'Save as Excel file
    workbook.SaveAs("XlsIOOutput_Hyperlinks.xlsx")
  End Using
End Sub
{% endhighlight %}
{% endtabs %}
