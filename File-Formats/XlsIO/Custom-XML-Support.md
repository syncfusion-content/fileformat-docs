---
title: Custom XML Support in Syncfusion .NET Excel Library
description: In this section, you can learn how to create or edit Custom XML in Excel document using Syncfusion .NET Excel library
platform: file-formats
control: XlsIO
documentation: UG
---
# Custom XML Support in Syncfusion Excel Library

When you embed XML data in a document, the data is named as custom XML part, which is used to store arbitrary XML data in the workbook. 

Essential XlsIO supports the following functionalities with Custom XML:

* Adding CustomXmlPart to workbook
* Reading CustomXmlPart from workbook 

**Add** **Custom** **XML** 

Adding Custom XML part to workbook is achieved by using the **Add** method of **ICustomXmlPart** interface. 

The following code snippet illustrates on how to add a Custom XML part.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding CustomXmlData to Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.Add("SD10003");

  //Add XmlData to CustomXmlPart
  byte[] xmlData = File.ReadAllBytes("Test.xml");
  customXmlPart.Data = xmlData;

  workbook.SaveAs("CustomXml.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Adding CustomXmlData to Workbook
  Dim customXmlPart As ICustomXmlPart = workbook.CustomXmlparts.Add("SD10003")

  'Add XmlData to CustomXmlPart
  Dim xmlData() As Byte = File.ReadAllBytes("Test.xml")
  customXmlPart.Data = xmlData

  workbook.SaveAs("CustomXml.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("CustomXml.Test.xml");
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding CustomXmlData to Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.Add("SD10003");

  //Add XmlData to CustomXmlPart
  customXmlPart.Data = new byte[inputStream.Length];
  inputStream.Read(customXmlPart.Data, 0, customXmlPart.Data.Length);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "CustomXml";
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

  //Adding CustomXmlData to Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.Add("SD10003");

  //Add XmlData to CustomXmlPart
  byte[] xmlData = File.ReadAllBytes("Test.xml");
  customXmlPart.Data = xmlData;

  //Saving the workbook as stream
  FileStream stream = new FileStream("CustomXml.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("CustomXml.Test.xml");
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding CustomXmlData to Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.Add("SD10003");

  //Add XmlData to CustomXmlPart
  customXmlPart.Data = new byte[inputStream.Length];
  inputStream.Read(customXmlPart.Data, 0, customXmlPart.Data.Length);

  //Saving the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);

  string fileName = "CustomXml.xlsx";
  outputStream.Position = 0;

  //Save the document as file and view the saved document
  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add custom XML in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Custom%20XML%20Support/Add%20Custom%20XML). 

**Read** **Custom** **XML** 

Reading Custom XML part from workbook is achieved by using the **GetById** method of **ICustomXmlPart** interface. The following code snippet illustrates on how to read Custom XML parts from workbook.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("CustomXml.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Access CustomXmlPart from Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.GetById("SD10003");

  //Access XmlData from CustomXmlPart
  byte[] xmlData = customXmlPart.Data;
  System.Text.Encoding.Default.GetString(xmlData);

  workbook.SaveAs("CustomXml.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("CustomXml.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Access CustomXmlPart from Workbook
  Dim customXmlPart As ICustomXmlPart = workbook.CustomXmlparts.GetById("SD10003")

  'Access XmlData from CustomXmlPart
  Dim xmlData As Byte() = customXmlPart.Data
  System.Text.Encoding.Default.GetString(xmlData)

  workbook.SaveAs("CustomXml.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("CustomXml.CustomXml.xlsx");
  IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Access CustomXmlPart from Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.GetById("SD10003");

  //Access XmlData from CustomXmlPart
  byte[] xmlData = customXmlPart.Data;
  System.Text.Encoding.UTF8.GetString(xmlData);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "CustomXml";
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
  FileStream fileStream = new FileStream("CustomXml.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Access CustomXmlPart from Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.GetById("SD10003");

  //Access XmlData from CustomXmlPart
  byte[] xmlData = customXmlPart.Data;
  System.Text.Encoding.Default.GetString(xmlData);

  //Saving the workbook as stream
  FileStream stream = new FileStream("CustomXml1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}
{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("CustomXml.CustomXml.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Access CustomXmlPart from Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.GetById("SD10003");

  //Access XmlData from CustomXmlPart
  byte[] xmlData = customXmlPart.Data;
  System.Text.Encoding.UTF8.GetString(xmlData, 0, xmlData.Length);

  //Saving the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);

  string fileName = "CustomXml.xlsx";
  outputStream.Position = 0;

  //Save the document as file and view the saved document
  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
}
{% endhighlight %}
{% endtabs %}  

A complete working example to read custom XML in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Custom%20XML%20Support/Read%20Custom%20XML). 

N> Custom XML cannot be modified when the file is saved in Excel 97-2003 (\*.xls) format.
N> Custom XML can be created and modified when the file is saved in Excel 2007 and later versions (\*.xlsx).

