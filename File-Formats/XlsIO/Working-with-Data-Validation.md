---
title: Working with Data Validation | Syncfusion
description: This section explains about how to create data validation rules. Data Validation is a list of rules to the data that can be entered in a cell.
platform: file-formats
control: XlsIO
documentation: UG
---
# Working with Data Validation 

Data Validation is a list of rules to the data that can be entered in a cell. This can be applied by using **IDataValidation** interface. XlsIO supports following validation types.

* **Text** **Length** **Validation**
* **Time** **Validation**
* **List** **Validation**
* **Number** **Validation**
* **Date** **Validation**
* **Custom** **Validation**

## Text Length Validation

The following code snippet illustrates how to set text length validation.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//Data validation for text length
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.TextLength;

//Text length should be lesser than 5 characters
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "0";
validation.SecondFormula = "5";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Data validation for text length
Dim validation As IDataValidation = sheet.Range("A3").DataValidation
validation.AllowType = ExcelDataType.TextLength

'Text length should be lesser than 5 characters
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between
validation.FirstFormula = "0"
validation.SecondFormula = "5"
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Data validation for text length
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.TextLength;

//Text length should be lesser than 5 characters
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "0";
validation.SecondFormula = "5";
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Data validation for text length
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.TextLength;

//Text length should be lesser than 5 characters
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "0";
validation.SecondFormula = "5";
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Data validation for text length
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.TextLength;

//Text length should be lesser than 5 characters
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "0";
validation.SecondFormula = "5";
{% endhighlight %}
{% endtabs %}  

A complete working example for text length data validation in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Data%20Validation/Text%20Length%20Validation).

## Time Validation

The following code snippet illustrates how to set time validation.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//Data validation for time
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Time;

//Time between 10:00 and 12:00 'o Clock
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "10.00";
validation.SecondFormula = "12.00";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Data validation for time
Dim validation As IDataValidation = sheet.Range("A3").DataValidation
validation.AllowType = ExcelDataType.Time

'Time between 10:00 and 12:00 'o Clock
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between
validation.FirstFormula = "10.00"
validation.SecondFormula = "12.00"
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Data validation for time
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Time;

//Time between 10:00 and 12:00 'o Clock
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "10.00";
validation.SecondFormula = "12.00";
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Data validation for time
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Time;

//Time between 10:00 and 12:00 'o Clock
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "10.00";
validation.SecondFormula = "12.00";
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Data validation for time
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Time;

//Time between 10:00 and 12:00 'o Clock
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "10.00";
validation.SecondFormula = "12.00";
{% endhighlight %}
{% endtabs %} 

A complete working example for time data validation in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Data%20Validation/Time%20Validation).  

## List Validation

The following code snippet illustrates how to set list validation.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//Data validation for list
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.ListOfValues = new string[] { "ListItem1", "ListItem2", "ListItem3" };
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Data validation for list
Dim validation As IDataValidation = sheet.Range("A3").DataValidation
validation.ListOfValues = New String() {"ListItem1", "ListItem2", "ListItem3"}
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Data validation for list
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.ListOfValues = new string[] { "ListItem1", "ListItem2", "ListItem3" };
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Data validation for list
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.ListOfValues = new string[] { "ListItem1", "ListItem2", "ListItem3" };
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Data validation for list
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.ListOfValues = new string[] { "ListItem1", "ListItem2", "ListItem3" };
{% endhighlight %}
{% endtabs %}   

A complete working example for list data validation in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Data%20Validation/List%20Validation). 

N> The ListOfValues property should be used when the values in the Data Validation list are entered manually whose limit is only 255 characters including separators.

## Number Validation

The following code snippet illustrates  how to set number validation.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//Data validation for number
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Integer;

//Value between 0 to 10
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "0";
validation.SecondFormula = "10";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Data validation for number
Dim validation As IDataValidation = sheet.Range("A3").DataValidation
validation.AllowType = ExcelDataType.Integer

'Value between 0 to 10
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between
validation.FirstFormula = "0"
validation.SecondFormula = "10"
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Data validation for number
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Integer;

//Value between 0 to 10
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "0";
validation.SecondFormula = "10";
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Data validation for number
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Integer;

//Value between 0 to 10
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "0";
validation.SecondFormula = "10";
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Data validation for number
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Integer;

//Value between 0 to 10
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstFormula = "0";
validation.SecondFormula = "10";
{% endhighlight %}
{% endtabs %}   

A complete working example for number data validation in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Data%20Validation/Number%20Validation). 

## Date Validation

The following code snippet illustrates how to set date validation.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//Data validation for date
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Date;

//Date between 10/5/2003 to 10/5/2004
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstDateTime = new DateTime(2003, 5, 10);
validation.SecondDateTime = new DateTime(2004, 5, 10);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Data validation for date
Dim validation As IDataValidation = sheet.Range("A3").DataValidation
validation.AllowType = ExcelDataType.Date

'Date between 10/5/2003 to 10/5/2004
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between
validation.FirstDateTime = New DateTime(2003, 5, 10)
validation.SecondDateTime = New DateTime(2004, 5, 10)
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Data validation for date
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Date;

//Date between 10/5/2003 to 10/5/2004
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstDateTime = new DateTime(2003, 5, 10);
validation.SecondDateTime = new DateTime(2004, 5, 10);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Data validation for date
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Date;

//Date between 10/5/2003 to 10/5/2004
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstDateTime = new DateTime(2003, 5, 10);
validation.SecondDateTime = new DateTime(2004, 5, 10);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Data validation for date
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.Date;

//Date between 10/5/2003 to 10/5/2004
validation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
validation.FirstDateTime = new DateTime(2003, 5, 10);
validation.SecondDateTime = new DateTime(2004, 5, 10);
{% endhighlight %}
{% endtabs %} 

A complete working example for number data validation in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Data%20Validation/Number%20Validation).   

## Custom Validation

Custom validation can be set to a cell with its __AllowType__ as __User__. The following code snippet illustrates how to set custom validation.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//Data validation for custom data
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.User;
validation.FirstFormula = "=A1>10";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Data validation for custom data
Dim validation As IDataValidation = sheet.Range("A3").DataValidation
validation.AllowType = ExcelDataType.User
validation.FirstFormula = "=A1>10"
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Data validation for custom data
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.User;
validation.FirstFormula = "=A1>10";
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Data validation for custom data
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.User;
validation.FirstFormula = "=A1>10";
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Data validation for custom data
IDataValidation validation = sheet.Range["A3"].DataValidation;
validation.AllowType = ExcelDataType.User;
validation.FirstFormula = "=A1>10";
{% endhighlight %}
{% endtabs %}   

The following code snippet shows all the data validation supports discussed previously.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Data Validation for Text Length
  IDataValidation txtLengthValidation = worksheet.Range["A3"].DataValidation;
  worksheet.Range["A1"].Text = "Enter the Text in A3";
  worksheet.Range["A1"].AutofitColumns();
  txtLengthValidation.AllowType = ExcelDataType.TextLength;
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  txtLengthValidation.FirstFormula = "0";
  txtLengthValidation.SecondFormula = "5";

  //Shows the error message
  txtLengthValidation.ShowErrorBox = true;
  txtLengthValidation.ErrorBoxText = "Text length should be lesser than 5 characters";
  txtLengthValidation.ErrorBoxTitle = "ERROR";
  txtLengthValidation.PromptBoxText = "Data validation for text length";
  txtLengthValidation.ShowPromptBox = true;

  //Data Validation for Time
  IDataValidation timeValidation = worksheet.Range["B3"].DataValidation;
  worksheet.Range["B1"].Text = "Enter the time between 10:00 and 12:00 'o Clock in B3";
  worksheet.Range["B1"].AutofitColumns();
  timeValidation.AllowType = ExcelDataType.Time;
  timeValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  timeValidation.FirstFormula = "10.00";
  timeValidation.SecondFormula = "12.00";

  //Shows the error message
  timeValidation.ShowErrorBox = true;
  timeValidation.ErrorBoxText = "Enter a correct time";
  timeValidation.ErrorBoxTitle = "ERROR";
  timeValidation.PromptBoxText = "Data validation for time";
  timeValidation.ShowPromptBox = true;

  //Data Validation for List
  IDataValidation listValidation = worksheet.Range["C3"].DataValidation;
  worksheet.Range["C1"].Text = "Data Validation List in C3";
  worksheet.Range["C1"].AutofitColumns();
  listValidation.ListOfValues = new string[] { "ListItem1", "ListItem2", "ListItem3" };

  //Shows the error message
  listValidation.ErrorBoxText = "Choose the value from the list";
  listValidation.ErrorBoxTitle = "ERROR";
  listValidation.PromptBoxText = "Data validation for list";
  listValidation.IsPromptBoxVisible = true;
  listValidation.ShowPromptBox = true;

  //Data Validation for Numbers
  IDataValidation numberValidation = worksheet.Range["D3"].DataValidation;
  worksheet.Range["D1"].Text = "Enter the Number in D3";
  worksheet.Range["D1"].AutofitColumns();
  numberValidation.AllowType = ExcelDataType.Integer;
  numberValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  numberValidation.FirstFormula = "0";
  numberValidation.SecondFormula = "10";

  //Shows the error message
  numberValidation.ShowErrorBox = true;
  numberValidation.ErrorBoxText = "Enter Value between 0 to 10";
  numberValidation.ErrorBoxTitle = "ERROR";
  numberValidation.PromptBoxText = "Data validation for numbers";
  numberValidation.ShowPromptBox = true;

  //Data Validation for Date
  IDataValidation dateValidation = worksheet.Range["E3"].DataValidation;
  worksheet.Range["E1"].Text = "Enter the Date in E3";
  worksheet.Range["E1"].AutofitColumns();
  dateValidation.AllowType = ExcelDataType.Date;
  dateValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  dateValidation.FirstDateTime = new DateTime(2003, 5, 10);
  dateValidation.SecondDateTime = new DateTime(2004, 5, 10);

  //Shows the error message
  dateValidation.ShowErrorBox = true;
  dateValidation.ErrorBoxText = "Enter Value between 10/5/2003 to 10/5/2004";
  dateValidation.ErrorBoxTitle = "ERROR";
  dateValidation.PromptBoxText = "Data validation for date";
  dateValidation.ShowPromptBox = true;

  //Data validation for custom data
  IDataValidation validation = worksheet.Range["A3"].DataValidation;
  validation.AllowType = ExcelDataType.User;
  validation.FirstFormula = "=A1>10";

  //Shows the error message
  validation.ErrorBoxText = "Enter value in A1 greater than 10";
  validation.ErrorBoxTitle = "ERROR";
  validation.PromptBoxText = "Custom DataValidation";
  validation.ShowPromptBox = true;

  workbook.SaveAs("DataValidation.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Data Validation for Text Length
  Dim txtLengthValidation As IDataValidation = worksheet.Range("A3").DataValidation
  worksheet.Range("A1").Text = "Enter the Text in A3"
  worksheet.Range("A1").AutofitColumns()
  txtLengthValidation.AllowType = ExcelDataType.TextLength
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between
  txtLengthValidation.FirstFormula = "0"
  txtLengthValidation.SecondFormula = "5"

  'Shows the error message
  txtLengthValidation.ShowErrorBox = True
  txtLengthValidation.ErrorBoxText = "Text length should be lesser than 5 characters"
  txtLengthValidation.ErrorBoxTitle = "ERROR"
  txtLengthValidation.PromptBoxText = "Data validation for text length"
  txtLengthValidation.ShowPromptBox = True

  'Data Validation for Time
  Dim timeValidation As IDataValidation = worksheet.Range("B3").DataValidation
  worksheet.Range("B1").Text = "Enter the time between 10:00 and 12:00 'o Clock in B3"
  worksheet.Range("B1").AutofitColumns()
  timeValidation.AllowType = ExcelDataType.Time
  timeValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between
  timeValidation.FirstFormula = "10.00"
  timeValidation.SecondFormula = "12.00"

  'Shows the error message
  timeValidation.ShowErrorBox = True
  timeValidation.ErrorBoxText = "Enter a correct time"
  timeValidation.ErrorBoxTitle = "ERROR"
  timeValidation.PromptBoxText = "Data validation for time"
  timeValidation.ShowPromptBox = True

  'Data Validation for List
  Dim listValidation As IDataValidation = worksheet.Range("C3").DataValidation
  worksheet.Range("C1").Text = "Data Validation List in C3"
  worksheet.Range("C1").AutofitColumns()
  listValidation.ListOfValues = New String() {"ListItem1", "ListItem2", "ListItem3"}

  'Shows the error message
  listValidation.ErrorBoxText = "Choose the value from the list"
  listValidation.ErrorBoxTitle = "ERROR"
  listValidation.PromptBoxText = "Data validation for list"
  listValidation.IsPromptBoxVisible = True
  listValidation.ShowPromptBox = True

  'Data Validation for Numbers
  Dim numberValidation As IDataValidation = worksheet.Range("D3").DataValidation
  worksheet.Range("D1").Text = "Enter the Number in D3"
  worksheet.Range("D1").AutofitColumns()
  numberValidation.AllowType = ExcelDataType.Integer
  numberValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between
  numberValidation.FirstFormula = "0"
  numberValidation.SecondFormula = "10"

  'Shows the error message
  numberValidation.ShowErrorBox = True
  numberValidation.ErrorBoxText = "Enter Value between 0 to 10"
  numberValidation.ErrorBoxTitle = "ERROR"
  numberValidation.PromptBoxText = "Data validation for numbers"
  numberValidation.ShowPromptBox = True

  'Data Validation for Date
  Dim dateValidation As IDataValidation = worksheet.Range("E3").DataValidation
  worksheet.Range("E1").Text = "Enter the Date in E3"
  worksheet.Range("E1").AutofitColumns()
  dateValidation.AllowType = ExcelDataType.Date
  dateValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between
  dateValidation.FirstDateTime = New DateTime(2003, 5, 10)
  dateValidation.SecondDateTime = New DateTime(2004, 5, 10)

  'Shows the error message
  dateValidation.ShowErrorBox = True
  dateValidation.ErrorBoxText = "Enter Value between 10/5/2003 to 10/5/2004"
  dateValidation.ErrorBoxTitle = "ERROR"
  dateValidation.PromptBoxText = "Data validation for date"
  dateValidation.ShowPromptBox = True

  'Data validation for custom data
  Dim validation As IDataValidation = worksheet.Range("A3").DataValidation
  validation.AllowType = ExcelDataType.User
  validation.FirstFormula = "=A1>10"

  'Shows the error message
  validation.ErrorBoxText = "Enter value in A1 greater than 10"
  validation.ErrorBoxTitle = "ERROR"
  validation.PromptBoxText = "Custom DataValidation"
  validation.ShowPromptBox = True

  workbook.SaveAs("DataValidation.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Data Validation for Text Length
  IDataValidation txtLengthValidation = worksheet.Range["A3"].DataValidation;
  worksheet.Range["A1"].Text = "Enter the Text in A3";
  worksheet.Range["A1"].AutofitColumns();
  txtLengthValidation.AllowType = ExcelDataType.TextLength;
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  txtLengthValidation.FirstFormula = "0";
  txtLengthValidation.SecondFormula = "5";

  //Shows the error message
  txtLengthValidation.ShowErrorBox = true;
  txtLengthValidation.ErrorBoxText = "Text length should be lesser than 5 characters";
  txtLengthValidation.ErrorBoxTitle = "ERROR";
  txtLengthValidation.PromptBoxText = "Data validation for text length";
  txtLengthValidation.ShowPromptBox = true;

  //Data Validation for Time
  IDataValidation timeValidation = worksheet.Range["B3"].DataValidation;
  worksheet.Range["B1"].Text = "Enter the time between 10:00 and 12:00 'o Clock in B3";
  worksheet.Range["B1"].AutofitColumns();
  timeValidation.AllowType = ExcelDataType.Time;
  timeValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  timeValidation.FirstFormula = "10.00";
  timeValidation.SecondFormula = "12.00";

  //Shows the error message
  timeValidation.ShowErrorBox = true;
  timeValidation.ErrorBoxText = "Enter a correct time";
  timeValidation.ErrorBoxTitle = "ERROR";
  timeValidation.PromptBoxText = "Data validation for time";
  timeValidation.ShowPromptBox = true;

  //Data Validation for List
  IDataValidation listValidation = worksheet.Range["C3"].DataValidation;
  worksheet.Range["C1"].Text = "Data Validation List in C3";
  worksheet.Range["C1"].AutofitColumns();
  listValidation.ListOfValues = new string[] { "ListItem1", "ListItem2", "ListItem3" };

  //Shows the error message
  listValidation.ErrorBoxText = "Choose the value from the list";
  listValidation.ErrorBoxTitle = "ERROR";
  listValidation.PromptBoxText = "Data validation for list";
  listValidation.IsPromptBoxVisible = true;
  listValidation.ShowPromptBox = true;

  //Data Validation for Numbers
  IDataValidation numberValidation = worksheet.Range["D3"].DataValidation;
  worksheet.Range["D1"].Text = "Enter the Number in D3";
  worksheet.Range["D1"].AutofitColumns();
  numberValidation.AllowType = ExcelDataType.Integer;
  numberValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  numberValidation.FirstFormula = "0";
  numberValidation.SecondFormula = "10";

  //Shows the error message
  numberValidation.ShowErrorBox = true;
  numberValidation.ErrorBoxText = "Enter Value between 0 to 10";
  numberValidation.ErrorBoxTitle = "ERROR";
  numberValidation.PromptBoxText = "Data validation for numbers";
  numberValidation.ShowPromptBox = true;

  //Data Validation for Date
  IDataValidation dateValidation = worksheet.Range["E3"].DataValidation;
  worksheet.Range["E1"].Text = "Enter the Date in E3";
  worksheet.Range["E1"].AutofitColumns();
  dateValidation.AllowType = ExcelDataType.Date;
  dateValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  dateValidation.FirstDateTime = new DateTime(2003, 5, 10);
  dateValidation.SecondDateTime = new DateTime(2004, 5, 10);

  //Shows the error message
  dateValidation.ShowErrorBox = true;
  dateValidation.ErrorBoxText = "Enter Value between 10/5/2003 to 10/5/2004";
  dateValidation.ErrorBoxTitle = "ERROR";
  dateValidation.PromptBoxText = "Data validation for date";
  dateValidation.ShowPromptBox = true;

  //Data validation for custom data
  IDataValidation validation = worksheet.Range["A3"].DataValidation;
  validation.AllowType = ExcelDataType.User;
  validation.FirstFormula = "=A1>10";

  //Shows the error message
  validation.ErrorBoxText = "Enter value in A1 greater than 10";
  validation.ErrorBoxTitle = "ERROR";
  validation.PromptBoxText = "Custom DataValidation";
  validation.ShowPromptBox = true;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "DataValidation";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Data Validation for Text Length
  IDataValidation txtLengthValidation = worksheet.Range["A3"].DataValidation;
  worksheet.Range["A1"].Text = "Enter the Text in A3";
  worksheet.Range["A1"].AutofitColumns();
  txtLengthValidation.AllowType = ExcelDataType.TextLength;
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  txtLengthValidation.FirstFormula = "0";
  txtLengthValidation.SecondFormula = "5";

  //Shows the error message
  txtLengthValidation.ShowErrorBox = true;
  txtLengthValidation.ErrorBoxText = "Text length should be lesser than 5 characters";
  txtLengthValidation.ErrorBoxTitle = "ERROR";
  txtLengthValidation.PromptBoxText = "Data validation for text length";
  txtLengthValidation.ShowPromptBox = true;

  //Data Validation for Time
  IDataValidation timeValidation = worksheet.Range["B3"].DataValidation;
  worksheet.Range["B1"].Text = "Enter the time between 10:00 and 12:00 'o Clock in B3";
  worksheet.Range["B1"].AutofitColumns();
  timeValidation.AllowType = ExcelDataType.Time;
  timeValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  timeValidation.FirstFormula = "10.00";
  timeValidation.SecondFormula = "12.00";

  //Shows the error message
  timeValidation.ShowErrorBox = true;
  timeValidation.ErrorBoxText = "Enter a correct time";
  timeValidation.ErrorBoxTitle = "ERROR";
  timeValidation.PromptBoxText = "Data validation for time";
  timeValidation.ShowPromptBox = true;

  //Data Validation for List
  IDataValidation listValidation = worksheet.Range["C3"].DataValidation;
  worksheet.Range["C1"].Text = "Data Validation List in C3";
  worksheet.Range["C1"].AutofitColumns();
  listValidation.ListOfValues = new string[] { "ListItem1", "ListItem2", "ListItem3" };

  //Shows the error message
  listValidation.ErrorBoxText = "Choose the value from the list";
  listValidation.ErrorBoxTitle = "ERROR";
  listValidation.PromptBoxText = "Data validation for list";
  listValidation.IsPromptBoxVisible = true;
  listValidation.ShowPromptBox = true;

  //Data Validation for Numbers
  IDataValidation numberValidation = worksheet.Range["D3"].DataValidation;
  worksheet.Range["D1"].Text = "Enter the Number in D3";
  worksheet.Range["D1"].AutofitColumns();
  numberValidation.AllowType = ExcelDataType.Integer;
  numberValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  numberValidation.FirstFormula = "0";
  numberValidation.SecondFormula = "10";

  //Shows the error message
  numberValidation.ShowErrorBox = true;
  numberValidation.ErrorBoxText = "Enter Value between 0 to 10";
  numberValidation.ErrorBoxTitle = "ERROR";
  numberValidation.PromptBoxText = "Data validation for numbers";
  numberValidation.ShowPromptBox = true;

  //Data Validation for Date
  IDataValidation dateValidation = worksheet.Range["E3"].DataValidation;
  worksheet.Range["E1"].Text = "Enter the Date in E3";
  worksheet.Range["E1"].AutofitColumns();
  dateValidation.AllowType = ExcelDataType.Date;
  dateValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  dateValidation.FirstDateTime = new DateTime(2003, 5, 10);
  dateValidation.SecondDateTime = new DateTime(2004, 5, 10);

  //Shows the error message
  dateValidation.ShowErrorBox = true;
  dateValidation.ErrorBoxText = "Enter Value between 10/5/2003 to 10/5/2004";
  dateValidation.ErrorBoxTitle = "ERROR";
  dateValidation.PromptBoxText = "Data validation for date";
  dateValidation.ShowPromptBox = true;

  //Data validation for custom data
  IDataValidation validation = worksheet.Range["A3"].DataValidation;
  validation.AllowType = ExcelDataType.User;
  validation.FirstFormula = "=A1>10";

  //Shows the error message
  validation.ErrorBoxText = "Enter value in A1 greater than 10";
  validation.ErrorBoxTitle = "ERROR";
  validation.PromptBoxText = "Custom DataValidation";
  validation.ShowPromptBox = true;

  FileStream file = new FileStream("DataValidation.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(file);
  file.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Data Validation for Text Length
  IDataValidation txtLengthValidation = worksheet.Range["A3"].DataValidation;
  worksheet.Range["A1"].Text = "Enter the Text in A3";
  worksheet.Range["A1"].AutofitColumns();
  txtLengthValidation.AllowType = ExcelDataType.TextLength;
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  txtLengthValidation.FirstFormula = "0";
  txtLengthValidation.SecondFormula = "5";

  //Shows the error message
  txtLengthValidation.ShowErrorBox = true;
  txtLengthValidation.ErrorBoxText = "Text length should be lesser than 5 characters";
  txtLengthValidation.ErrorBoxTitle = "ERROR";
  txtLengthValidation.PromptBoxText = "Data validation for text length";
  txtLengthValidation.ShowPromptBox = true;

  //Data Validation for Time
  IDataValidation timeValidation = worksheet.Range["B3"].DataValidation;
  worksheet.Range["B1"].Text = "Enter the time between 10:00 and 12:00 'o Clock in B3";
  worksheet.Range["B1"].AutofitColumns();
  timeValidation.AllowType = ExcelDataType.Time;
  timeValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  timeValidation.FirstFormula = "10.00";
  timeValidation.SecondFormula = "12.00";

  //Shows the error message
  timeValidation.ShowErrorBox = true;
  timeValidation.ErrorBoxText = "Enter a correct time";
  timeValidation.ErrorBoxTitle = "ERROR";
  timeValidation.PromptBoxText = "Data validation for time";
  timeValidation.ShowPromptBox = true;

  //Data Validation for List
  IDataValidation listValidation = worksheet.Range["C3"].DataValidation;
  worksheet.Range["C1"].Text = "Data Validation List in C3";
  worksheet.Range["C1"].AutofitColumns();
  listValidation.ListOfValues = new string[] { "ListItem1", "ListItem2", "ListItem3" };

  //Shows the error message
  listValidation.ErrorBoxText = "Choose the value from the list";
  listValidation.ErrorBoxTitle = "ERROR";
  listValidation.PromptBoxText = "Data validation for list";
  listValidation.IsPromptBoxVisible = true;
  listValidation.ShowPromptBox = true;

  //Data Validation for Numbers
  IDataValidation numberValidation = worksheet.Range["D3"].DataValidation;
  worksheet.Range["D1"].Text = "Enter the Number in D3";
  worksheet.Range["D1"].AutofitColumns();
  numberValidation.AllowType = ExcelDataType.Integer;
  numberValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  numberValidation.FirstFormula = "0";
  numberValidation.SecondFormula = "10";

  //Shows the error message
  numberValidation.ShowErrorBox = true;
  numberValidation.ErrorBoxText = "Enter Value between 0 to 10";
  numberValidation.ErrorBoxTitle = "ERROR";
  numberValidation.PromptBoxText = "Data validation for numbers";
  numberValidation.ShowPromptBox = true;

  //Data Validation for Date
  IDataValidation dateValidation = worksheet.Range["E3"].DataValidation;
  worksheet.Range["E1"].Text = "Enter the Date in E3";
  worksheet.Range["E1"].AutofitColumns();
  dateValidation.AllowType = ExcelDataType.Date;
  dateValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  dateValidation.FirstDateTime = new DateTime(2003, 5, 10);
  dateValidation.SecondDateTime = new DateTime(2004, 5, 10);

  //Shows the error message
  dateValidation.ShowErrorBox = true;
  dateValidation.ErrorBoxText = "Enter Value between 10/5/2003 to 10/5/2004";
  dateValidation.ErrorBoxTitle = "ERROR";
  dateValidation.PromptBoxText = "Data validation for date";
  dateValidation.ShowPromptBox = true;

  //Data validation for custom data
  IDataValidation validation = worksheet.Range["A3"].DataValidation;
  validation.AllowType = ExcelDataType.User;
  validation.FirstFormula = "=A1>10";

  //Shows the error message
  validation.ErrorBoxText = "Enter value in A1 greater than 10";
  validation.ErrorBoxTitle = "ERROR";
  validation.PromptBoxText = "Custom DataValidation";
  validation.ShowPromptBox = true;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("DataValidation.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("DataValidation.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}
