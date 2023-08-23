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
    IWorksheet worksheet1 = workbook.Worksheets[0];

    IScenarios scenarios = worksheet1.Scenarios;

    //Add scenario with single range
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet1.Range["B3"], 3000);

    //Add scenario with multiple range
    List<object> values = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet1.Range["B3:B9"], values);

    //Save the workbook
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

    IScenarios scenarios = worksheet1.Scenarios;

    //Add scenario with single range
    IScenario scenario1 = scenarios.Add("Scenario1", worksheet1.Range["B3"], 3000);

    //Add scenario with multiple range
    List<object> values = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario2 = scenarios.Add("Scenario2", worksheet1.Range["B3:B9"], values);

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

    Dim scenarios As IScenarios = worksheet1.Scenarios

    'Add scenario with single range
    Dim scenario1 As IScenario = scenarios.Add("Scenario1", worksheet1.Range("B3"), 3000)

    'Add scenario with multiple range
    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario2 As IScenario = scenarios.Add("Scenario2", worksheet1.Range("B3:B9"), values1)

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

<img src="What_If_Analysis_images/Create_Scenario.png" alt="Create Scenario Manager" width="100%" Height="Auto"/>

### Edit Scenario

The **this[string name]** indexer enables you to retrieve a scenario from a collection of scenarios and make necessary edits to the scenario.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet worksheet1 = workbook.Worksheets[0];

    IScenarios scenarios = worksheet1.Scenarios;

    // Edit the scenario name
    scenarios["Scenario2"].Name = "Scenario1";

    //Save the workbook
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

    IScenarios scenarios = worksheet1.Scenarios;

    // Edit the scenario name
    scenarios["Scenario2"].Name = "Scenario1";

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

    Dim scenarios As IScenarios = worksheet1.Scenarios

    'Edit the scenario name
    scenarios("Scenario2").Name = "Scenario1"

    'Saving the workbook  
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

### Delete Scenario

Remove the existing scenario from the scenarios collection by using the **Delete** method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
IWorksheet worksheet1 = workbook.Worksheets[0];

IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario1 = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
IScenario scenario2 = scenarios.Add("Scenario2", worksheet1.Range["B3:B9"], values2);

//Delete the scenario 
scenario2.Delete();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IWorksheet worksheet1 = workbook.Worksheets[0];

IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario1 = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
IScenario scenario2 = scenarios.Add("Scenario2", worksheet1.Range["B3:B9"], values2);

//Delete the scenario 
scenario2.Delete();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim worksheet1 As IWorksheet = workbook.Worksheets(0)

Dim scenarios As IScenarios = worksheet1.Scenarios
'Add the scenarios in the worksheet
Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
Dim scenario1 As IScenario = scenarios.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
Dim scenario2 As IScenario = scenarios.Add("Scenario2", worksheet1.Range("B3:B9"), values2)

'Delete the scenario 
scenario2.Delete()
{% endhighlight %}
{% endtabs %}

### Merge Scenario

Merges the scenarios from another sheet into the current sheet's scenarios collection by using the **Merge** method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
IWorksheet worksheet1 = workbook.Worksheets[0];
IWorksheet worksheet2 = workbook.Worksheets[1];

IScenarios scenarios1 = worksheet1.Scenarios;
//Add the scenario in the first worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario1 = scenarios1.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

IScenarios scenarios2 = worksheet2.Scenarios;
//Add the scenario in the second worksheet
List<object> values2 = new List<object> { 500, 1000, 1500, 1200, 700, 500, 40000 };
IScenario scenario2 = scenarios2.Add("Scenario2", worksheet2.Range["B3:B9"], values2);

//Merge the second worksheet scenario into first worksheet.
worksheet1.Scenarios.Merge(worksheet2);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IWorksheet worksheet1 = workbook.Worksheets[0];
IWorksheet worksheet2 = workbook.Worksheets[1];

IScenarios scenarios1 = worksheet1.Scenarios;
//Add the scenario in the first worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario1 = scenarios1.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

IScenarios scenarios2 = worksheet2.Scenarios;
//Add the scenario in the second worksheet
List<object> values2 = new List<object> { 500, 1000, 1500, 1200, 700, 500, 40000 };
IScenario scenario2 = scenarios2.Add("Scenario2", worksheet2.Range["B3:B9"], values2);

//Merge the second worksheet scenario into first worksheet.
worksheet1.Scenarios.Merge(worksheet2);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim worksheet1 As IWorksheet = workbook.Worksheets(0)
Dim worksheet2 As IWorksheet = workbook.Worksheets(1)

Dim scenarios1 as IScenarios = worksheet1.Scenarios
'Add the scenario in the first worksheet
Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
Dim scenario1 As IScenario = scenarios1.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

Dim scenarios2 as IScenarios  = worksheet2.Scenarios
'Add the scenario in the second worksheet
Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
Dim scenario2 As IScenario = scenarios2.Add("Scenario2", worksheet2.Range("B3:B9"), values2)

'Merge the second worksheet scenario into first worksheet.
worksheet1.Scenarios.Merge(worksheet2)
{% endhighlight %}
{% endtabs %}

### Create Summary

Creates a new worksheet that contains a summary report for the scenarios on the specified worksheet by using **CreateSummary** method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
IWorksheet worksheet1 = workbook.Worksheets[0];

IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario1 = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
IScenario scenario2 = scenarios.Add("Scenario2", worksheet1.Range["B3:B9"], values2);

List<object> values3 = new List<object> { 1000, 500, 2000, 800, 1300, 1500, 35000 };
IScenario scenario3 = scenarios.Add("Scenario3", worksheet1.Range["B3:B9"], values3);

//Create Summary for the sheet1
scenarios.CreateSummary(ExcelSummaryReportType.ScenarioSummary, worksheet1.Range["B10:B11"]);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IWorksheet worksheet1 = workbook.Worksheets[0];

IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario1 = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
IScenario scenario2 = scenarios.Add("Scenario2", worksheet1.Range["B3:B9"], values2);

List<object> values3 = new List<object> { 1000, 500, 2000, 800, 1300, 1500, 35000 };
IScenario scenario3 = scenarios.Add("Scenario3", worksheet1.Range["B3:B9"], values3);

//Create Summary for the sheet1
scenarios.CreateSummary(ExcelSummaryReportType.ScenarioSummary, worksheet1.Range["B10:B11"]);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim worksheet1 As IWorksheet = workbook.Worksheets(0)

Dim scenarios As IScenarios = worksheet1.Scenarios
'Add the scenarios in the worksheet
Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
Dim scenario1 As IScenario = scenarios.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
Dim scenario2 As IScenario = scenarios.Add("Scenario2", worksheet1.Range("B3:B9"), values2)

Dim values3 As New List(Of Object) From {1000, 500, 2000, 800, 1300, 1500, 35000}
Dim scenario3 As IScenario = scenarios.Add("Scenario3", worksheet1.Range("B3:B9"), values3)

'Create Summary for the sheet1
scenarios.CreateSummary(ExcelSummaryReportType.ScenarioSummary, worksheet1.Range("B10:B11"))
{% endhighlight %}
{% endtabs %}

### Apply Scenario

Update the scenario values in the worksheet and display it using the **Show** method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
IWorksheet worksheet1 = workbook.Worksheets[0];

IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario1 = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
IScenario scenario2 = scenarios.Add("Scenario2", worksheet1.Range["B3:B9"], values2);

//Show the scenario 
scenario2.Show();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IWorksheet worksheet1 = workbook.Worksheets[0];

IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario1 = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
IScenario scenario2 = scenarios.Add("Scenario2", worksheet1.Range["B3:B9"], values2);

//Show the scenario 
scenario2.Show()
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim worksheet1 As IWorksheet = workbook.Worksheets(0)

Dim scenarios As IScenarios = worksheet1.Scenarios
'Add the scenarios in the worksheet
Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
Dim scenario1 As IScenario = scenarios.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
Dim scenario2 As IScenario = scenarios.Add("Scenario2", worksheet1.Range("B3:B9"), values2)

'Show the scenario 
scenario2.Show()
{% endhighlight %}
{% endtabs %}

### Set Name

The name of the scenario can be defined using the **Name** property..

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

//Set the name of the scenario
scenario.Name = "ScenarioNameChanged";
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);;

//Set the name of the scenario
scenario.Name = "ScenarioNameChanged";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim scenarios As IScenarios = worksheet1.Scenarios
'Add the scenarios in the worksheet
Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
Dim scenario As IScenario = scenarios.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

'Set the name of the scenario
scenario.Name = "ScenarioNameChanged"
{% endhighlight %}
{% endtabs %}

### Hide Scenario

The scenario can be hidden using the **Hidden** property. It is a boolean property, with its default value set to false.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

//Hidden the scenario
scenario.Hidden = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

//Hidden the scenario
scenario.Hidden = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim scenarios As IScenarios = worksheet1.Scenarios
'Add the scenarios in the worksheet
Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
Dim scenario As IScenario = scenarios.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

'Hidden the scenario
scenario.Hidden = True
{% endhighlight %}
{% endtabs %}

### Protect Scenario

The scenario can be locked using the **Locked** property. It is a boolean property, with its default value set to true.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

//Set the scenario to be locked
scenario.Locked = false;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

//Set the scenario to be locked
scenario.Locked = false;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim scenarios As IScenarios = worksheet1.Scenarios
'Add the scenarios in the worksheet
Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
Dim scenario As IScenario = scenarios.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

'Set the scenario to be locked
scenario.Locked = False
{% endhighlight %}
{% endtabs %}

### Add Comment

The comment associated with that particular scenario can be generated using the **Comment** property.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

//Set the comment value 
scenario.Comment = "Scenario 1 can be created";
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IScenarios scenarios = worksheet1.Scenarios;
//Add the scenarios in the worksheet
List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
IScenario scenario = scenarios.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

//Set the comment value 
scenario.Comment = "Scenario 1 can be created";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim scenarios As IScenarios = worksheet1.Scenarios
'Add the scenarios in the worksheet
Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
Dim scenario As IScenario = scenarios.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

'Set the comment value 
scenario.Comment = "Scenario 1 can be created"
{% endhighlight %}
{% endtabs %}

The following code snippet illustrates how to create a scenario manager with all the above discussed properties and methods.

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

    //Adding the scenario in the first worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios1.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios1.Add("Scenario2", worksheet1.Range["B3:B9"], values2);

    List<object> values3 = new List<object> { 1000, 500, 2000, 800, 1300, 1500, 35000 };
    IScenario scenario3 = scenarios1.Add("Scenario3", worksheet1.Range["B3:B9"], values3);

    IScenarios scenarios2 = worksheet2.Scenarios;

    //Adding the scenario in the second worksheet
    List<object> values4 = new List<object> { 2000, 700, 1500, 900, 1000, 2000, 25000 };
    IScenario scenario4 = scenarios2.Add("Scenario4", worksheet2.Range["B3:B9"], values4);

    List<object> values5 = new List<object> { 3500, 3000, 1500, 2200, 700, 500, 20000 };
    IScenario scenario5 = scenarios2.Add("Scenario5", worksheet2.Range["B3:B9"], values5);

    //Show the scenario
    scenario3.Show();

    //Modify the  Scenario 
    List<object> values6 = new List<object> { 2000, 3000, 1500, 2200, 2000, 1500, 40000 };
    scenario2.ModifyScenario(worksheet1.Range["B3:B9"], values6);

    //Merge the Scenario
    scenarios1.Merge(worksheet2);

    //Delete the Scenario
    scenario5.Delete();

    //Create Summary
    scenarios1.CreateSummary(ExcelSummaryReportType.ScenarioSummary, worksheet1.Range["B10:B11"]);

    //Save the workbook
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

    //Adding the scenario in the first worksheet
    List<object> values1 = new List<object> { 3000, 2000, 1000, 1600, 500, 1000, 30000 };
    IScenario scenario1 = scenarios1.Add("Scenario1", worksheet1.Range["B3:B9"], values1);

    List<object> values2 = new List<object> { 2500, 1000, 1500, 1200, 700, 500, 40000 };
    IScenario scenario2 = scenarios1.Add("Scenario2", worksheet1.Range["B3:B9"], values2);

    List<object> values3 = new List<object> { 1000, 500, 2000, 800, 1300, 1500, 35000 };
    IScenario scenario3 = scenarios1.Add("Scenario3", worksheet1.Range["B3:B9"], values3);

    IScenarios scenarios2 = worksheet2.Scenarios;

    //Adding the scenario in the second worksheet
    List<object> values4 = new List<object> { 2000, 700, 1500, 900, 1000, 2000, 25000 };
    IScenario scenario4 = scenarios2.Add("Scenario4", worksheet2.Range["B3:B9"], values4);

    List<object> values5 = new List<object> { 3500, 3000, 1500, 2200, 700, 500, 20000 };
    IScenario scenario5 = scenarios2.Add("Scenario5", worksheet2.Range["B3:B9"], values5);

    //Show the scenario
    scenario3.Show();

    //Modify the  Scenario 
    List<object> values6 = new List<object> { 2000, 3000, 1500, 2200, 2000, 1500, 40000 };
    scenario2.ModifyScenario(worksheet1.Range["B3:B9"], values6);

    //Merge the Scenario
    scenarios1.Merge(worksheet2);

    //Delete the Scenario
    scenario5.Delete();

    //Create Summary
    scenarios1.CreateSummary(ExcelSummaryReportType.ScenarioSummary, worksheet1.Range["B10:B11"]);

    //Save the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create an instance of ExcelEngine
Using excelEngine As ExcelEngine = New ExcelEngine

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim worksheet1 As IWorksheet = workbook.Worksheets(0)
    Dim worksheet2 As IWorksheet = workbook.Worksheets(1)

    Dim scenarios1 As IScenarios = worksheet1.Scenarios

    'Adding the scenario in the first worksheet

    Dim values1 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario1 As IScenario = scenarios1.Add("Scenario1", worksheet1.Range("B3:B9"), values1)

    Dim values2 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
    Dim scenario2 As IScenario = scenarios1.Add("Scenario2", worksheet1.Range("B3:B9"), values2)

    Dim values3 As New List(Of Object) From {1000, 500, 2000, 800, 1300, 1500, 35000}
    Dim scenario3 As IScenario = scenarios1.Add("Scenario3", worksheet1.Range("B3:B9"), values3)

    Dim scenarios2 As IScenarios = worksheet2.Scenarios

    'Adding the scenario in the second worksheet
    Dim values4 As New List(Of Object) From {3000, 2000, 1000, 1600, 500, 1000, 30000}
    Dim scenario4 As IScenario = scenarios2.Add("Scenario4", worksheet1.Range("B3:B9"), values4)

    Dim values5 As New List(Of Object) From {2500, 1000, 1500, 1200, 700, 500, 40000}
    Dim scenario5 As IScenario = scenarios2.Add("Scenario5", worksheet1.Range("B3:B9"), values5)

    'Show the scenario
    scenario3.Show()

    'Modify the  Scenario 
    Dim values6 As New List(Of Object) From {2000, 3000, 1500, 2200, 2000, 1500, 40000}
    scenario2.ModifyScenario(worksheet1.Range("B3:B9"), values6)

    'Merge the Scenario
    scenarios1.Merge(worksheet2)

    'Delete the Scenario
    scenario5.Delete()

    'Create Summary
    scenarios1.CreateSummary(ExcelSummaryReportType.ScenarioSummary, worksheet1.Range("B10:B11"))

    'Save the workbook
    workbook.SaveAs("Output.xlsx")

End Using
{% endhighlight %}
{% endtabs %}

By executing the program, you will get the Excel file as below.
<img src="What_If_Analysis_images/Sheet1_Scenarios.png" alt="Sheet1 Scenarios Collection" width="100%" Height="Auto"/>
<img src="What_If_Analysis_images/Sheet2_Scenarios.png" alt="Sheet2 Scenarios Collection" width="100%" Height="Auto"/>
<img src="What_If_Analysis_images/Create_Summary.png" alt="Create Summary for sheet1" width="100%" Height="Auto"/>
