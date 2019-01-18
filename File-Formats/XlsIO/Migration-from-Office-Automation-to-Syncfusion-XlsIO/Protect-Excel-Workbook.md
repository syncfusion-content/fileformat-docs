---
title: Protect Excel Workbook | Syncfusion
description: This page shows how to protect Excel workbook with password.
platform: file-formats
control: XlsIO
documentation: UG
---

# Protect Excel Workbook

Workbooks are protected by its structure and its window. 

* Workbook structure prevents from moving, deleting, hiding, unhiding, renaming and inserting worksheets. 
* Protecting window will retain the size and position of a workbook whenever opened.

The following code shows how to protect Excel workbook with password using Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void ProtectWorkbook()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a Workbook.
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Protect the workbook specifying a password with Boolean attributes for Structure and Windows Protection.
    workbook.Protect("007", true, true);

    //Save the file.
    workbook.SaveAs(@"d:\test\InteropOutput_ProtectedWorkbook.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub ProtectWorkbook()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a Workbook.
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Protect the workbook specifying a password with Boolean attributes for Structure and Windows Protection.
    workbook.Protect("007", True, True)

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_ProtectedWorkbook.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void ProtectWorkbook()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Create a Workbook.
        IWorkbook workbook = application.Workbooks.Create(1);

        //Protect the workbook specifying a password with Boolean attributes for Structure and Windows Protection.
        bool isProtectWindow = true;
        bool isProtectContent = true;
        workbook.Protect(isProtectWindow, isProtectContent, "password");

        //Save the excel file
        workbook.SaveAs(@"d:\test\XlsIOOutput_ProtectedWorkbook.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub ProtectWorkbook()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Create a Workbook.
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Protect the workbook specifying a password with Boolean attributes for Structure and Windows Protection.
        Dim isProtectWindow As Boolean = True
        Dim isProtectContent As Boolean = True
        workbook.Protect(isProtectWindow, isProtectContent, "password")

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_ProtectedWorkbook.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
