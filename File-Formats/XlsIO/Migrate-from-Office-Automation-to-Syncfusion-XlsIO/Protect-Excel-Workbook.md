---
title: Protect Excel Workbook | Syncfusion
description: Explains with an example on how to protect Excel workbook with password programmatically, using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Protect Excel Workbook

Workbooks are protected by its structure and window. 

* Workbook structure prevents from moving, deleting, hiding, unhiding, renaming, and inserting worksheets. 
* Protecting window will retain the size and position of a workbook whenever opened.

The following code shows how to protect Excel workbook with password using Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void ProtectWorkbook()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a workbook
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Protect the workbook specifying a password with Boolean attributes for structure and windows protection
    workbook.Protect("007", true, true);

    //Save the file
    workbook.SaveAs(@"d:\test\InteropOutput_ProtectedWorkbook.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub ProtectWorkbook()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a workbook
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Protect the workbook specifying a password with Boolean attributes for structure and windows protection
    workbook.Protect("007", True, True)

    'Save the file
    workbook.SaveCopyAs("d:\test1\InteropOutput_ProtectedWorkbook.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void ProtectWorkbook()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);

        //Protect the workbook specifying a password with Boolean attributes for structure and windows protection
        bool isProtectWindow = true;
        bool isProtectContent = true;
        workbook.Protect(isProtectWindow, isProtectContent, "password");

        //Save the Excel file
        workbook.SaveAs(@"d:\test\XlsIOOutput_ProtectedWorkbook.xlsx");
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub ProtectWorkbook()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Create a workbook
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Protect the workbook specifying a password with Boolean attributes for structure and windows protection
        Dim isProtectWindow As Boolean = True
        Dim isProtectContent As Boolean = True
        workbook.Protect(isProtectWindow, isProtectContent, "password")

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_ProtectedWorkbook.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
