---
title: Security in Excel (XlsIO) Library | Syncfusion
description: This section explains all about the security feature of the Syncfusion Excel (XlsIO) Library and more.
platform: File-formats
control: XlsIO
documentation: UG
---

# Security in Excel (XlsIO) Library

You can protect an anonymous user from viewing, moving, editing or deleting important data from a worksheet or workbook by [protecting a worksheet or workbook](https://support.office.com/en-ca/article/Password-protect-worksheet-or-workbook-elements-dbf706e0-ba22-4a08-84d8-552db16eef11#bmprotectelements), with or without a password.

## Protect Workbook

To keep others from making structural changes to your documents such as moving, deleting and adding sheets, you can protect the workbook in the following ways. 

**Encryption** **with** **password**

There are two different passwords to encrypt a document.

1. **Password** **To** **Open** **-** This password helps to protect your workbook from unauthorized viewing or accessing.
2. **Password** **to** **Modify** **-** This password helps to allow give specific users permission to modify the workbook data and save changes to the file.

**Read****-****Only** **Recommended** **–** If the excel file is set as Read-only recommended, then Microsoft Excel displays a message recommending that you open the workbook as read-only when users open the excel file. This can be set with or without requiring a password to open the file.

The Following code snippets illustrate how to achieve the above options.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Encrypt the workbook with password
  workbook.PasswordToOpen = "password";

  //Set the password to modify the workbook
  workbook.SetWriteProtectionPassword("modify_password");

  //Set the workbook as read-only
  workbook.ReadOnlyRecommended = true;

  workbook.SaveAs("Encrypt.xlsx");
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)

  'Encrypt the workbook with password
  workbook.PasswordToOpen = "password"

  'Set the password to modify the workbook
  workbook.SetWriteProtectionPassword("modify_password")

  'Set the workbook as read-only
  workbook.ReadOnlyRecommended = True

  workbook.SaveAs("Encrypt.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Encrypt the workbook with password
  workbook.PasswordToOpen = "password";

  //Set the password to modify the workbook
  workbook.SetWriteProtectionPassword("modify_password");

  //Set the workbook as read-only
  workbook.ReadOnlyRecommended = true;               

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  workbook.SaveAs(stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Encrypt the workbook with password
  workbook.PasswordToOpen = "password";

  //Set the password to modify the workbook
  workbook.SetWriteProtectionPassword("modify_password");

  //Set the workbook as read-only
  workbook.ReadOnlyRecommended = true;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Encrypt.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Encrypt the workbook with password
  workbook.PasswordToOpen = "password";

  //Set the password to modify the workbook
  workbook.SetWriteProtectionPassword("modify_password");

  //Set the workbook as read-only
  workbook.ReadOnlyRecommended = true;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

Now, the encrypted workbook can be saved. Refer [Save Excel file](/file-formats/xlsio/loading-and-saving-workbook#saving-a-excel-workbook-to-file-system). 

**Opening** **an** **encrypted** **workbook**

You can open an existing encrypted workbook (decrypting) from either the file system or the stream using the following overloads.

{% tabs %}
{% highlight C# %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileName, ExcelParseOptions.Default, false, "password");
{% endhighlight %}

{% highlight VB.NET %}
'Creates a new instance for ExcelEngine
Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(fileName, ExcelParseOptions.Default, False, "password")
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.

//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileName, ExcelParseOptions.Default, false, "password");
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(workbookStream, ExcelParseOptions.Default, false, "password");
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileName, ExcelParseOptions.Default, false, "password");
{% endhighlight %}
{% endtabs %}

**Removing** **encryption**

The following code illustrates how to remove a protection for an encrypted document.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx", ExcelParseOptions.Default, true, "password");

  //Removing a protection
  workbook.PasswordToOpen = string.Empty;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx", ExcelParseOptions.Default, True, "password")

  'Removing a protection
  workbook.PasswordToOpen = String.Empty

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet sheet = workbook.Worksheets[0];

  //Removing a protection
  workbook.PasswordToOpen = string.Empty;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
                
  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  workbook.SaveAs(stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");

  //Removing a protection
  workbook.PasswordToOpen = string.Empty;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet sheet = workbook.Worksheets[0];

  //Removing a protection
  workbook.PasswordToOpen = string.Empty;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

### Protect workbook elements

XlsIO provides options to protect and unprotect workbook elements with password. The following code example illustrates how to protect a workbook with a password.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  bool isProtectWindow = true;
  bool isProtectContent = true;

  //Protect Workbook
  workbook.Protect(isProtectWindow, isProtectContent, "password");

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("ProtectWorkbook.xlsx")

  Dim isProtectWindow As Boolean = True
  Dim isProtectContent As Boolean = True

  'protect workbook
  workbook.Protect(isProtectWindow, isProtectContent, "password")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet sheet = workbook.Worksheets[0];

  bool isProtectWindow = true;
  bool isProtectContent = true;

  //Protect Workbook
  workbook.Protect(isProtectWindow, isProtectContent, "password");

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
                
  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  workbook.SaveAs(stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream = new FileStream("ProtectWorkbook.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);

  bool isProtectWindow = true;
  bool isProtectContent = true;

  //Protect Workbook
  workbook.Protect(isProtectWindow, isProtectContent, "password");

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet sheet = workbook.Worksheets[0];

  bool isProtectWindow = true;
  bool isProtectContent = true;

  //Protect Workbook
  workbook.Protect(isProtectWindow, isProtectContent, "password");

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

### Unprotect Workbook elements

You can unprotect or remove protection for a workbook as shown below.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("ProtectedWorkbook.xlsx");

  //Unprotect (unlock) Workbook using Password
  workbook.Unprotect("password");

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("ProtectedWorkbook.xlsx")

  'Unprotect (unlock) Workbook using Password
  workbook.Unprotect("password")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet sheet = workbook.Worksheets[0];

  //Unprotect (unlock) Workbook using Password
  workbook.Unprotect("password");

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
                
  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  workbook.SaveAs(stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream = new FileStream("ProtectedWorkbook.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);

  //Unprotect (unlock) Workbook using Password
  workbook.Unprotect("password");

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet sheet = workbook.Worksheets[0];

  //Unprotect (unlock) Workbook using Password
  workbook.Unprotect("password");

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

## Protect Worksheet 

XlsIO provides support for protecting and unprotecting elements in worksheets by using the **Protect** method of **IWorksheet****.** The following code example illustrates how to protect a worksheet with a password. 

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Protecting the Worksheet by using a Password
  sheet.Protect("syncfusion", ExcelSheetProtection.All);

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Protecting the Worksheet by using a Password
  sheet.Protect("syncfusion", ExcelSheetProtection.All)

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Protecting the Worksheet by using a Password
  sheet.Protect("syncfusion", ExcelSheetProtection.All);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
                
  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  workbook.SaveAs(stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Protecting the Worksheet by using a Password
  sheet.Protect("syncfusion", ExcelSheetProtection.All);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Protecting the Worksheet by using a Password
  sheet.Protect("syncfusion", ExcelSheetProtection.All);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

N> By using the ExcelSheetProtection enumerator, you can set protection to the workbook elements/operations.

**Chart** **Sheet** **Protection**

Essential XlsIO can also provide support to protect or unprotect a chart sheet.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("sample.xlsx");
  IChart chart = workbook.Charts[0];

  //Protect chart sheet
  chart.Protect("syncfusion", ExcelSheetProtection.All);

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim chart As IChart = workbook.Charts(0)

  'Protect chart sheet
  chart.Protect("syncfusion", ExcelSheetProtection.All)

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IChart chart = workbook.Charts[0];

  //Protect chart sheet
  chart.Protect("syncfusion", ExcelSheetProtection.All);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
                
  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  workbook.SaveAs(stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream = new FileStream("ChartSheet.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IChart chart = workbook.Charts[0];

  //Protect chart sheet
  chart.Protect("syncfusion", ExcelSheetProtection.All);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IChart chart = workbook.Charts[0];

  //Protect chart sheet
  chart.Protect("syncfusion", ExcelSheetProtection.All);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

**Un****-****Protect** **Worksheet** 

You can also unprotect the worksheet by using the **Unprotect** method of XlsIO. The following code example illustrates how to remove worksheet protection.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Unprotecting (unlocking) the Worksheet using the Password
  sheet.Unprotect("syncfusion");

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("sample.xlsx")
  Dim sheet As IWorkbook = workbook.Worksheets(0)

  'Unprotecting (unlocking) the Worksheet using the Password
  sheet.Unprotect("syncfusion")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet sheet = workbook.Worksheets[0];

  //Unprotecting (unlocking) the Worksheet using the Password
  sheet.Unprotect("syncfusion");

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
                
  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  workbook.SaveAs(stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Unprotecting (unlocking) the Worksheet using the Password
  worksheet.Unprotect("syncfusion");

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet sheet = workbook.Worksheets[0];

  //Unprotecting (unlocking) the Worksheet using the Password
  sheet.Unprotect("syncfusion");

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

**Removing** **protection** **of** **a** **Chart** **Sheet**

You can remove the protection of a chart sheet as shown below.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IChart chart = workbook.Charts[0];

  //Unprotect chart sheet
  chart.Unprotect("syncfusion");

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim chart As IChart = workbook.Charts(0)

  'Unprotect chart sheet
  chart.Unprotect("syncfusion")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IChart chart = workbook.Charts[0];

  //Unprotect chart sheet
  chart.Unprotect("syncfusion");

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
                
  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  workbook.SaveAs(stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IChart chart = workbook.Charts[0];

  //Unprotect chart sheet
  chart.Unprotect("syncfusion");

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IChart chart = workbook.Charts[0];

  //Unprotect chart sheet
  chart.Unprotect("syncfusion");

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

## Protect Cell

XlsIO supports locking and unlocking cells by using the cell's **Locked** property of __CellStyle__. This can be manipulated to make certain cells editable in a protected worksheet. 

N> By default, cells are locked. Lock or Unlock cell in an unprotected worksheet has no effect. 

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Unlocking a cell to edit in worksheet protection mode
  worksheet.Range["A1"].CellStyle.Locked = false;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)
  
  'Unlocking a cell to edit in worksheet protection mode
  worksheet.Range("A1").CellStyle.Locked = False

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//Encrypt and Decrypt can be performed by referring .NET Standard assemblies in UWP platform.

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Unlocking a cell to edit in worksheet protection mode
  worksheet.Range["A1"].CellStyle.Locked = false;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
                
  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  workbook.SaveAs(stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Unlocking a cell to edit in worksheet protection mode
  worksheet.Range["A1"].CellStyle.Locked = false;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Security.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelParseOptions.Default, true, "password");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Unlocking a cell to edit in worksheet protection mode
  worksheet.Range["A1"].CellStyle.Locked = false;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  


N> Security features are now supported in .NET Standard 1.4 onwards.

All complete working examples for above topics are present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/XlsIO-Excel-Protect-UnProtect). 
