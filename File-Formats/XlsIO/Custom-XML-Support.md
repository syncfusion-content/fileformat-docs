---
title: Custom XML Support
description: Briefs about Custom XML Support in XlsIO
platform: File-Formats
control: XlsIO
documentation: UG
---
# Custom XML Support

When you embed XML data in a document, the data is named as custom XML part which is used to store arbitrary XML data in the workbook. 

Essential XlsIO supports the following functionalities with Custom XML such as,

* Adding CustomXmlPart to workbook
* Reading CustomXmlPart from workbook 

**Add** **Custom** **XML** 

Adding Custom XML part to workbook is achieved by using **Add** method of **ICustomXmlPart** interface. 

The following code snippet illustrates on how to add a Custom XML part.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
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

workbook.Close();
excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()
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

workbook.Close()
excelEngine.Dispose()



{% endhighlight %}
{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("CustomXml.Test.xml");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);
IWorksheet worksheet = workbook.Worksheets[0];

//Adding CustomXmlData to Workbook
ICustomXmlPart customXmlPart = workbook.CustomXmlparts.Add("SD10003");

//Add XmlData to CustomXmlPart
customXmlPart.Data = new byte[inputStream.Length];
inputStream.Read(customXmlPart.Data, 0,customXmlPart.Data.Length);
                        
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "CustomXml";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();

{% endhighlight %}
{% highlight asp.netcore %}
ExcelEngine excelEngine = new ExcelEngine();
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
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}
{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("CustomXml.Test.xml");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

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

workbook.Close();
excelEngine.Dispose();

string fileName = "CustomXml.xlsx";

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();
{% endhighlight %}

  {% endtabs %}  

**Read** **Custom** **XML** 

Reading Custom XML part from workbook is achieved by using **GetById** method of **ICustomXmlPart** interface. The following code snippet illustrates on how to read Custom XML parts from workbook.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
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

workbook.Close();
excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()
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

workbook.Close()
excelEngine.Dispose()



{% endhighlight %}
{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("CustomXml.CustomXml.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

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

workbook.Close();
excelEngine.Dispose();
{% endhighlight %}
{% highlight asp.netcore %}
ExcelEngine excelEngine = new ExcelEngine();
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
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}
{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("CustomXml.CustomXml.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream);
IWorksheet worksheet = workbook.Worksheets[0];

//Access CustomXmlPart from Workbook
ICustomXmlPart customXmlPart = workbook.CustomXmlparts.GetById("SD10003");

//Access XmlData from CustomXmlPart
byte[] xmlData = customXmlPart.Data;

System.Text.Encoding.UTF8.GetString(xmlData,0,xmlData.Length);

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

string fileName = "CustomXml.xlsx";

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();
{% endhighlight %}

  {% endtabs %}  

N> Custom XML cannot be modified when the file is saved in Excel 97-2003 (\*.xls) format.
N> Custom XML can be created and modified when the file is saved in Excel 2007 and later versions (\*.xlsx).

