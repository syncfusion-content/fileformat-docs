---
title: What If Analysis Scenario Manager in Excel | Excel library | Syncfusion
description: This section illustrates about Excel What If Analysis Scenario Manager and its various features in Syncfusion XlsIO (a .NET Excel library).
platform: file-formats
control: XlsIO
documentation: UG
---

# What-If Analysis

## Scenario Manager
Scenario Manager in Excel allows you to create and manage scenarios for different sets of input values to see how they impact the results of formulas in a worksheet.

### Create Scenario

The following code snippet explains how to create a scenario and add it to the worksheet.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;

    //Add scenario with single range
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3"], 3000);

    //Add scenario with multiple range
    List<object> values = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3:B9"], values);

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;

    //Add scenario with single range
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3"], 3000);

    //Add scenario with multiple range
    List<object> values = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3:B9"], values);

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim scenarios As IScenarios = worksheet.Scenarios

    'Add scenario with single range
    Dim scenario1 As IScenario = scenarios.Add("Scenario1", worksheet.Range("B3"), 3000)

    'Add scenario with multiple range
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario2 As IScenario = scenarios.Add("Scenario2", worksheet.Range("B3:B9"), values1)

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

<img src="What_If_Analysis_images/Create_Scenario.png" alt="Create Scenario Manager" width="100%" Height="Auto"/>

### Edit Scenario

The changing cells range and values of the scenario can be edited by using the **ModifyScenario** method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3: B8"], values2);

    //Modify the scenario 
    scenario1.ModifyScenario(scenario2.ChangingCells, scenario2.Values);

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3: B8"], values2);

    //Modify the scenario 
    scenario1.ModifyScenario(scenario2.ChangingCells, scenario2.Values);

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim scenarios As IScenarios = worksheet.Scenarios
    'Add scenarios in the worksheet
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario1 As IScenario = scenarios.Add("Scenario1", worksheet.Range("B3:B9"), values1)

    Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500}
    Dim scenario2 As IScenario = scenarios.Add("Scenario2", worksheet.Range("B3:B8"), values2)

    'Modify the scenario 
    scenario1.ModifyScenario(scenario2.ChangingCells, scenario2.Values)

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

### Delete Scenario

Remove the existing scenario from the scenarios collection by using the **Delete** method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;

    //Add scenario in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3:B9"], values2);

    //Delete the scenario 
    scenario2.Delete();

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;

    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3:B9"], values2);

    //Delete the scenario 
    scenario2.Delete();

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim scenarios As IScenarios = worksheet.Scenarios

    'Add scenario in the worksheet
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario1 As IScenario = scenarios.Add("Scenario1", worksheet.Range("B3:B9"), values1)

    Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
    Dim scenario2 As IScenario = scenarios.Add("Scenario2", worksheet.Range("B3:B9"), values2)

    'Delete the scenario
    scenario2.Delete()

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

### Merge Scenario

Merges the scenarios from another sheet into the current sheet's scenarios collection by using the **Merge** method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet1 = workbook.Worksheets[0];
    IWorksheet worksheet2 = workbook.Worksheets[1];

    IScenarios scenarios1 = worksheet1.Scenarios;
    //Add scenario in the first worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios1.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

    IScenarios scenarios2 = worksheet2.Scenarios;
    //Add scenario in the second worksheet
    List<object> values2 = new List<object> { 500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios2.Add("Scenario2", worksheet2.Range["B3:B9"], values2);

    //Merge the second worksheet scenario into first worksheet.
    worksheet1.Scenarios.Merge(worksheet2);

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet1 = workbook.Worksheets[0];
    IWorksheet worksheet2 = workbook.Worksheets[1];

    IScenarios scenarios1 = worksheet1.Scenarios;
    //Add scenario in the first worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios1.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

    IScenarios scenarios2 = worksheet2.Scenarios;
    //Add scenario in the second worksheet
    List<object> values2 = new List<object> { 500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios2.Add("Scenario2", worksheet2.Range["B3:B9"], values2);

    //Merge the second worksheet scenario into first worksheet.
    worksheet1.Scenarios.Merge(worksheet2);

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet1 As IWorksheet = workbook.Worksheets(0)
    Dim worksheet2 As IWorksheet = workbook.Worksheets(1)

    Dim scenarios1 As IScenarios = worksheet1.Scenarios
    'Add scenario in the first worksheet
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario1 As IScenario = scenarios1.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

    Dim scenarios2 As IScenarios = worksheet2.Scenarios
    'Add scenario in the second worksheet
    Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
    Dim scenario2 As IScenario = scenarios2.Add("Scenario2", worksheet2.Range("B3:B9"), values2)

    'Merge the second worksheet scenario into first worksheet.
    worksheet1.Scenarios.Merge(worksheet2)

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

### Create Summary

Creates a new worksheet that contains a summary report for the scenarios on the specified worksheet by using **CreateSummary** method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3:B9"], values2);

    List<object> values3 = new List<object> { 1000, 500, 2000, 800, 1300, 1500, 35000 };
    IScenario scenario3 = scenarios.Add("Scenario3", worksheet.Range["B3:B9"], values3);

    //Create Summary for the sheet1
    scenarios.CreateSummary(ExcelSummaryReportType.ScenarioSummary, worksheet.Range["B10:B11"]);

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3:B9"], values2);

    List<object> values3 = new List<object> { 1000, 500, 2000, 800, 1300, 1500, 35000 };
    IScenario scenario3 = scenarios.Add("Scenario3", worksheet.Range["B3:B9"], values3);

    //Create Summary for the sheet1
    scenarios.CreateSummary(ExcelSummaryReportType.ScenarioSummary, worksheet.Range["B10:B11"]);

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim scenarios As IScenarios = worksheet.Scenarios
    'Add scenarios in the worksheet
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario1 As IScenario = scenarios.Add("Scenario1", worksheet.Range("B3:B9"), values1)

    Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
    Dim scenario2 As IScenario = scenarios.Add("Scenario2", worksheet.Range("B3:B9"), values2)

    Dim values3 As New List(Of Object) From {1000, 500, 2000, 800, 1300, 1500, 35000}
    Dim scenario3 As IScenario = scenarios.Add("Scenario3", worksheet.Range("B3:B9"), values3)

    'Create Summary for the sheet1
    scenarios.CreateSummary(ExcelSummaryReportType.ScenarioSummary, worksheet.Range("B10:B11"))

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

<img src="What_If_Analysis_images/Create_Summary.png" alt="Create Scenario Manager" width="100%" Height="Auto"/>

### Apply Scenario

Update the scenario values in the worksheet and display it using the **Show** method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];
              
    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3:B9"], values2);

    //Show the scenario 
    scenario2.Show();

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet.Range["B3:B9"], values2);

    //Show the scenario 
    scenario2.Show();

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim scenarios As IScenarios = worksheet.Scenarios
    'Add scenarios in the worksheet
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario1 As IScenario = scenarios.Add("Scenario1", worksheet.Range("B3:B9"), values1)

    Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
    Dim scenario2 As IScenario = scenarios.Add("Scenario2", worksheet.Range("B3:B9"), values2)

    'Show the scenario 
    scenario2.Show()

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

### Set Name

The name of the scenario can be defined using the **Name** property..

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    //Set the name of the scenario
    scenario.Name = "ScenarioNameChanged";

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    //Set the name of the scenario
    scenario.Name = "ScenarioNameChanged";

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim scenarios As IScenarios = worksheet.Scenarios
    'Add scenarios in the worksheet
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario As IScenario = scenarios.Add("Scenario1", worksheet.Range("B3:B9"), values1)

    'Set the name of the scenario
    scenario.Name = "ScenarioNameChanged"
    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

### Hide Scenario

The scenario can be hidden using the **Hidden** property. It is a boolean property, with its default value set to false.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    //Hidden the scenario
    scenario.Hidden = true;

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    //Hidden the scenario
    scenario.Hidden = true;

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim scenarios As IScenarios = worksheet.Scenarios
    'Add the scenarios in the worksheet
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario As IScenario = scenarios.Add("Scenario1", worksheet.Range("B3:B9"), values1)

    'Hidden the scenario
    scenario.Hidden = True

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

### Protect Scenario

The scenario can be locked using the **Locked** property. It is a boolean property, with its default value set to true.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add  scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    //Set the scenario to be locked
    scenario.Locked = false;

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    //Set the scenario to be locked
    scenario.Locked = false;

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim scenarios As IScenarios = worksheet.Scenarios
    'Add scenarios in the worksheet
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario As IScenario = scenarios.Add("Scenario1", worksheet.Range("B3:B9"), values1)

    'Set the scenario to be locked
    scenario.Locked = False

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using

{% endhighlight %}
{% endtabs %}

### Add Comment

The comment associated with that particular scenario can be generated using the **Comment** property.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    //Set the comment value 
    scenario.Comment = "Scenario 1 can be created";

    //Saving the workbook as stream
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];

    IScenarios scenarios = worksheet.Scenarios;
    //Add the scenarios in the worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario = scenarios.Add("Scenario1", worksheet.Range["B3:B9"], values1);

    //Set the comment value 
    scenario.Comment = "Scenario 1 can be created";

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    Dim scenarios As IScenarios = worksheet.Scenarios
    'Add the scenarios in the worksheet
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario As IScenario = scenarios.Add("Scenario1", worksheet.Range("B3:B9"), values1)

    'Set the comment value 
    scenario.Comment = "Scenario 1 can be created"

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}