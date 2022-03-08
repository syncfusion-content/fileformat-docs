---
title: Windows Phone
description: Briefs about loading and saving an Excel document in Windows Phone platform.
platform: file-formats
control: XlsIO
documentation: UG
---
# Windows Phone

In order to use XlsIO in your Windows Phone application, please add the required assemblies in your Windows Phone application. Refer [Assemblies Required](/File-Formats/XlsIO/Assemblies-Required).

## Loading the document

The below code snippet illustrates how to load an Excel file in Windows Phone.

{% tabs %}  

{% highlight C# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel; 

//Gets a local folder.

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

//Opens the workbook. 

StorageFile outFile = await local.GetFileAsync("Sample.xlsx"); 

IWorkbook workbook = await application.Workbooks.OpenAsync(outFile);

//Sets workbook version.

workbook.Version = ExcelVersion.Excel2013;

//Creates a storage file from FileSavePicker.

StorageFile storageFile = await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting);

//Saves changes to the specified storage file.

await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight VB.NET %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'Gets a local folder.

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder



'Opens the workbook.

Dim outFile As StorageFile = Await local.GetFileAsync("Sample.xlsx")

Dim workbook As IWorkbook = Await application.Workbooks.OpenAsync(outFile)



'Sets workbook version.

workbook.Version = ExcelVersion.Excel2013   

'Creates a storage file from FileSavePicker.

Dim storageFile As StorageFile = Await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting)



'Saves changes to the specified storage file.

Await workbook.SaveAsAsync(storageFile)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

The below code snippet illustrates how to load an Excel file using stream in Windows Phone.

{% tabs %}  

{% highlight C# %}
ExcelEngine excelEngine = new ExcelEngine(); 

IApplication application = excelEngine.Excel; 

//Gets a local folder.

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

//Opens the file as a stream. 

Stream outFile = await local.OpenStreamForReadAsync("sample.xlsx");



//Opens the workbook. 

IWorkbook workbook = await application.Workbooks.OpenAsync(outFile);

//Sets workbook version.

workbook.Version = ExcelVersion.Excel2013;

//Creates a storage file from FileSavePicker.

StorageFile storageFile = await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting);

//Saves changes to the specified storage file.

await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight VB.NET %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'Gets a local folder.

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder



'Opens the file as a stream.

Dim outFile As Stream = Await local.OpenStreamForReadAsync("Sample.xlsx")



'Opens the workbook. 

Dim workbook As IWorkbook = Await Application.Workbooks.OpenAsync(outFile)



'Sets workbook version.

workbook.Version = ExcelVersion.Excel2013



'Creates a storage file from FileSavePicker.

Dim storageFile As StorageFile = Await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting)

'Saves changes to the specified storage file.

Await workbook.SaveAsAsync(storageFile)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

The below code snippet illustrates how to load an encrypted Excel file in Windows Phone.

{% tabs %}  

{% highlight C# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Gets a local folder.

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder; 



//Opens the file. 

StorageFile openFile = await local.GetFileAsync("Sample.xlsx"); 

//Decryption: 

//Opens the encrypted workbook. 

IWorkbook workbook = await application.Workbooks.OpenAsync(openFile, ExcelParseOptions.Default, true, "password");

//Sets workbook version.

workbook.Version = ExcelVersion.Excel2013;

//Creates a storage file from FileSavePicker.

StorageFile storageFile = await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting);

//Saves changes to the specified storage file.

await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight VB.NET %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = ExcelEngine.Excel

'Gets a local folder.

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder



'Opens the file. 

Dim openFile As StorageFile = Await local.GetFileAsync("Sample.xlsx")



'Opens the Workbook. 

Dim workbook As IWorkbook = Await Application.Workbooks.OpenAsync(openFile, ExcelParseOptions.Default, True, "password")



'Sets workbook version.

workbook.Version = ExcelVersion.Excel2013

'Creates a storage file from FileSavePicker.

Dim storageFile As StorageFile = Await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting)



'Saves changes to the specified storage file.

Await workbook.SaveAsAsync(storageFile)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

The below code snippet illustrates how to load an XML file in Windows Phone.

{% tabs %}  

{% highlight C# %}
ExcelEngine excelEngine = new ExcelEngine(); 

IApplication application = excelEngine.Excel; 

//Gets a local folder.

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder; 



//Opens the XML file. 

StorageFile openFile = await local.GetFileAsync("Sample.xm1"); 

//Opens the workbook. 

IWorkbook workbook = await application.Workbooks.OpenAsync(openFile);



//Sets workbook version.

workbook.Version = ExcelVersion.Excel2013;

//Creates a storage file from FileSavePicker.

StorageFile storageFile = await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting);

//Saves changes to the specified storage file.

await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight VB.NET %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = ExcelEngine.Excel

'Gets a local folder.

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder



'Opens the XML file. 

Dim openFile As StorageFile = Await local.GetFileAsync("Sample.xml")



'Opens the Workbook. 

Dim workbook As IWorkbook = Await Application.Workbooks.OpenAsync(openFile)



'Sets workbook version.

workbook.Version = ExcelVersion.Excel2013

'Creates a storage file from FileSavePicker.

Dim storageFile As StorageFile = Await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting)



'Saves changes to the specified storage file.

Await workbook.SaveAsAsync(storageFile)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## Saving the document

The following code snippet illustrate how to save an Excel document in Windows Phone.

{% tabs %}  

{% highlight C# %}
ExcelEngine excelEngine = new ExcelEngine(); 

IApplication application = excelEngine.Excel; 



//Gets a local folder.

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder; 



//Opens the file as a stream. 

Stream outFile = await local.OpenStreamForReadAsync("sample.xlsx"); 

//Opens the workbook. 

IWorkbook workbook = await application.Workbooks.OpenAsync(outFile);

//Sets workbook version.

workbook.Version = ExcelVersion.Excel2013;

//Creates a storage file from FileSavePicker.

StorageFile storageFile = await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting);

//Saves changes to the specified storage file.

await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight VB.NET %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = ExcelEngine.Excel

'Gets a local folder.

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder



'Opens the file as a stream.

Dim outFile As Stream = Await local.OpenStreamForReadAsync("Sample.xlsx")



'Opens the workbook. 

Dim workbook As IWorkbook = Await Application.Workbooks.OpenAsync(outFile)

'Sets workbook version.

workbook.Version = ExcelVersion.Excel2013

'Creates a storage file from FileSavePicker.

Dim storageFile As StorageFile = Await local.CreateFileAsync("CreateSpreadsheet.xlsx", CreationCollisionOption.ReplaceExisting)



'Saves changes to the specified storage file.

Await workbook.SaveAsAsync(storageFile)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

