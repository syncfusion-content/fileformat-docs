---
title: Find and Replace text in Hyperlinks | Syncfusion
description: This page shows how to find and replace text in hyperlinks using the Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to find and replace text in hyperlinks?

The following code illustrates how to find and replace text in hyperlinks.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Loads an existing file.
    FileStream inputstream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputstream);
    IWorksheet sheet = workbook.Worksheets[0];

    //Find and Replace text in hyperlinks
    for (int i = 0; i < sheet.HyperLinks.Count; i++)
    {
        IHyperLink hyperLink = sheet.HyperLinks[i];
        string address = hyperLink.Address;
        string displayText = hyperLink.TextToDisplay;
        hyperLink.Address = address.Replace("http://", "https://");
        if (!string.IsNullOrEmpty(displayText))
            hyperLink.TextToDisplay = displayText.Replace("http://", "https://");
    }
    
    // Saving the workbook
    FileStream outputstream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(outputstream);
    outputstream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Loads an existing file.
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx");
    IWorksheet sheet = workbook.Worksheets[0];

    //Find and Replace text in hyperlinks
    for (int i = 0; i < sheet.HyperLinks.Count; i++)
    {
        IHyperLink hyperLink = sheet.HyperLinks[i];
        string address = hyperLink.Address;
        string displayText = hyperLink.TextToDisplay;
        hyperLink.Address = address.Replace("http://", "https://");
        if (!string.IsNullOrEmpty(displayText))
            hyperLink.TextToDisplay = displayText.Replace("http://", "https://");
    }

    // Saving the workbook
    workbook.SaveAs("Output1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx

    'Loads an existing file.
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx")
    Dim sheet As IWorksheet = workbook.Worksheets(0)

    'Find and Replace text in hyperlinks
    For i As Integer = 0 To sheet.HyperLinks.Count - 1
        Dim hyperLink As IHyperLink = sheet.HyperLinks(i)
        Dim address As String = hyperLink.Address
        Dim displayText As String = hyperLink.TextToDisplay
        hyperLink.Address = address.Replace("http://", "https://")
        If Not String.IsNullOrEmpty(displayText) Then
            hyperLink.TextToDisplay = displayText.Replace("http://", "https://")
        End If
    Next

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}