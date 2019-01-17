---
title: Activate a Worksheet
description: We can activate a worksheet in workbooks containing more than one worksheet.
platform: file-formats
control: XlsIO
documentation: UG
---

# Activate a Worksheet

If there are more worksheets in a workbook, we may need to have certain worksheet to be active while opening the workbook in Microsoft Excel.

The following code shows how to activate a worksheet in workbook containing 3 worksheets, with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void ActivateWorksheet()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Specify the template excel file path.
    string myPath = @"d:\test\Sample.xlsx";

    //Open the excel file.
    Workbook workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value);

    //Activate the first worksheet by default.
    workbook.Sheets[1].Activate();

    //Save as excel file.
    workbook.SaveCopyAs(@"d:\test\InteropOutput_ActivateWorksheet.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub ActivateWorksheet()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Specify the template excel file path.
    Dim myPath As String = "d:\test1\Sample.xlsx"

    'Open the excel file.
    Dim workbook As Workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value)

    'Activate the first worksheet by default.
    workbook.Sheets(1).Activate()

    'Save as excel file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_ActivateWorksheet.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void ActivateWorksheet()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.                
        IApplication application = excelEngine.Excel;

        //Specify the template excel file path.
        string myPath = @"d:\test\Sample.xlsx";

        //Instantiate a new Workbook.
        //Open the excel file.
        IWorkbook workbook = application.Workbooks.Open(myPath);

        //Activate the first worksheet by default.
        workbook.Worksheets[0].Activate();

        //Save as excel file.
        workbook.SaveAs(@"d:\test\XlsIOOutput_ActivateWorksheet.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub ActivateWorksheet()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Specify the template excel file path.
        Dim myPath As String = "d:\test\Sample.xlsx"

        'Instantiate a New Workbook.
        'Open the excel file.
        Dim workbook As IWorkbook = application.Workbooks.Open(myPath)

        'Activate the first worksheet by default.
        workbook.Worksheets(0).Activate()

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_ActivateWorksheet.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
