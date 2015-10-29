---
title: XAMARIN
description: Briefs about loading and saving an Excel document in Xamarin platform.
platform: Xamarin
control: XlsIO
documentation: UG
---
# Xamarin

## Loading in Xamarin

The below code snippet illustrates how to load an Excel file using stream in Xamarin.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

string resourcePath = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx";

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Opens the workbook

IWorkbook workbook = application.Workbooks.Open(fileStream);

MemoryStream stream = new MemoryStream();

workbook.SaveAs(stream);

workbook.Close();

excelEngine.Dispose();

//Save the stream into xlsx file

Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.xlsx","application/msexcel", stream);

public interface ISave

{

void Save(string filename, string contentType, MemoryStream stream);

}

public interface ISaveWindowsPhone

{

Task Save(string filename, string contentType, MemoryStream stream);

}

class SaveWindowsPhone: ISave

{

public async Task Save(string filename, string contentType, MemoryStream stream)

{

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

StorageFile outFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);

using (Stream outStream = await outFile.OpenStreamForWriteAsync())

{

outStream.Write(stream.ToArray(), 0, (int)stream.Length);

}

await Windows.System.Launcher.LaunchFileAsync(outFile);

}

}



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim resourcePath As String = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx"

Dim assembly As Assembly = Type.GetType(App).GetTypeInfo().Assembly

Dim fileStream As Stream = assembly.GetManifestResourceStream(resourcePath)

'Opens the workbook 

Dim workbook As IWorkbook = application.Workbooks.Open(fileStream)

Dim stream As MemoryStream = New MemoryStream()

workbook.SaveAs(stream)

workbook.Close()

excelEngine.Dispose()

'Save the stream into xlsx file

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("sample.xlsx","application/ msexcel", stream)

Public Interface ISave

Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As Task

End Interface

Public Interface ISaveWindowsPhone

Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As void

End Interface

Friend Class SaveWindowsPhone

Implements ISave

Public async Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As Task

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

Dim outFile As StorageFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting)

Using outStream As Stream = await outFile.OpenStreamForWriteAsync()

outStream.Write(stream.ToArray(), 0, CInt(stream.Length))

End Using

await Windows.System.Launcher.LaunchFileAsync(outFile)

End Function

End Class



{% endhighlight %}

  {% endtabs %}  

## Saving in Xamarin

The below code snippet illustrates how to load an Excel file using stream in Xamarin Windows Phone platform.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

string resourcePath = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx";

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Opens the workbook 

IWorkbook workbook = application.Workbooks.Open(fileStream);

MemoryStream stream = new MemoryStream();

workbook.SaveAs(stream);

workbook.Close();

excelEngine.Dispose();

//Save the stream into xlsx file

Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.xlsx","application/msexcel", stream);

public interface ISave

{

void Save(string filename, string contentType, MemoryStream stream);

}

public interface ISaveWindowsPhone

{

Task Save(string filename, string contentType, MemoryStream stream);

}

class SaveWindowsPhone: ISave

{

public async Task Save(string filename, string contentType, MemoryStream stream)

{

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

StorageFile outFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);

using (Stream outStream = await outFile.OpenStreamForWriteAsync())

{

outStream.Write(stream.ToArray(), 0, (int)stream.Length);

}

await Windows.System.Launcher.LaunchFileAsync(outFile);

}

}



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim resourcePath As String = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx"

Dim assembly As Assembly = Type.GetType(App).GetTypeInfo().Assembly

Dim fileStream As Stream = assembly.GetManifestResourceStream(resourcePath)

'Opens the workbook

Dim workbook As IWorkbook = application.Workbooks.Open(fileStream)

Dim stream As MemoryStream = New MemoryStream()

workbook.SaveAs(stream)

workbook.Close()

excelEngine.Dispose()

'Save the stream into xlsx file

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("sample.xlsx","application/ msexcel", stream)

Public Interface ISave

Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As Task

End Interface

Public Interface ISaveWindowsPhone

Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As void

End Interface

Friend Class SaveWindowsPhone

Implements ISave

Public async Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As Task

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

Dim outFile As StorageFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting)

Using outStream As Stream = await outFile.OpenStreamForWriteAsync()

outStream.Write(stream.ToArray(), 0, CInt(stream.Length))

End Using

await Windows.System.Launcher.LaunchFileAsync(outFile)

End Function

End Class



{% endhighlight %}

  {% endtabs %}  

The below code snippet illustrates how to load an Excel file using stream in Xamarin Android platform.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

string resourcePath = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx";

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Opens the workbook. 

IWorkbook workbook = application.Workbooks.Open(fileStream);

MemoryStream stream = new MemoryStream();

workbook.SaveAs(stream);

workbook.Close();

excelEngine.Dispose();

public interface ISave

{

Task Save(string filename, string contentType, MemoryStream stream);

}

class SaveAndroid: ISave

{

public async Task Save(string fileName, String contentType, MemoryStream stream)

{

string root = null;

if (Android.OS.Environment.IsExternalStorageEmulated)

{

root = Android.OS.Environment.ExternalStorageDirectory.ToString();

}

else

root = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

Java.IO.File myDir = new Java.IO.File(root + "/Syncfusion");

myDir.Mkdir();

Java.IO.File file = new Java.IO.File(myDir, fileName);

if (file.Exists()) file.Delete();

try

{

FileOutputStream outs = new FileOutputStream(file);

outs.Write(stream.ToArray());

outs.Flush();

outs.Close();

}

catch (Exception e)

{

}

if (file.Exists())

{

Android.Net.Uri path = Android.Net.Uri.FromFile(file);

string extension = Android.Webkit.MimeTypeMap.GetFileExtensionFromUrl(Android.Net.Uri.FromFile(file).ToString());

string mimeType = Android.Webkit.MimeTypeMap.Singleton.GetMimeTypeFromExtension(extension);

Intent intent = new Intent(Intent.ActionView);

intent.SetDataAndType(path, mimeType);

Forms.Context.StartActivity(Intent.CreateChooser(intent, "Choose App"));

}

}

}



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim resourcePath As String = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx"

Dim assembly As Assembly = Type.GetType(App).GetTypeInfo().Assembly

Dim fileStream As Stream = assembly.GetManifestResourceStream(resourcePath)

'Opens the workbook. 

Dim workbook As IWorkbook = application.Workbooks.Open(fileStream)

Dim stream As MemoryStream = New MemoryStream()

workbook.SaveAs(stream)

workbook.Close()

excelEngine.Dispose()

'Save the stream into xlsx file

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("sample.xlsx","application/ msexcel", stream)

Public Interface ISave

Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As Task

End Interface

Friend Class SaveAndroid

Implements ISave

Public Async Function Save(ByVal fileName As String, ByVal contentType As String, ByVal stream As MemoryStream) As Task

Dim root As String = Nothing

If Android.OS.Environment.IsExternalStorageEmulated Then

root = Android.OS.Environment.ExternalStorageDirectory.ToString()

Else

root = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments)

End If

Dim myDir As New Java.IO.File(root & "/Syncfusion")

myDir.Mkdir()

Dim file As New Java.IO.File(myDir, fileName)

If file.Exists() Then

file.Delete()

End If

Try

Dim outs As New FileOutputStream(file)

outs.Write(stream.ToArray())

outs.Flush()

outs.Close()

Catch e As Exception

End Try

If file.Exists() Then

Dim path As Android.Net.Uri = Android.Net.Uri.FromFile(file)

Dim extension As String = Android.Webkit.MimeTypeMap.GetFileExtensionFromUrl(Android.Net.Uri.FromFile(file).ToString())

Dim mimeType As String = Android.Webkit.MimeTypeMap.Singleton.GetMimeTypeFromExtension(extension)

Dim intent As New Intent(Intent.ActionView)

intent.SetDataAndType(path, mimeType)

Forms.Context.StartActivity(Intent.CreateChooser(intent, "Choose App"))

End If

End Function

End Class



{% endhighlight %}

  {% endtabs %}  

The below code snippet illustrates how to load an Excel file using stream in Xamarin iOS platform.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

string resourcePath = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx";

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Opens the workbook. 

IWorkbook workbook = application.Workbooks.Open(fileStream);

MemoryStream stream = new MemoryStream();

workbook.SaveAs(stream);

workbook.Close();

excelEngine.Dispose();

public interface ISave

{

Task Save(string filename, string contentType, MemoryStream stream);

}

class SaveIOS: ISave

{

public async Task Save(string filename, string contentType, MemoryStream stream)

{

string path = Environment.GetFolderPath(Environment.SpecialFolder.Personal);

string filePath = Path.Combine(path, filename);

try

{

FileStream fileStream = File.Open(filePath, FileMode.Create);

stream.Position = 0;

stream.CopyTo(fileStream);

fileStream.Flush();

fileStream.Close();

}

catch (Exception e)

{

}

UIViewController currentController = UIApplication.SharedApplication.KeyWindow.RootViewController;

while (currentController.PresentedViewController != null)

currentController = currentController.PresentedViewController;

UIView currentView = currentController.View;

QLPreviewController qlPreview = new QLPreviewController();

QLPreviewItem item = new QLPreviewItemBundle(filename, filePath);

qlPreview.DataSource = new PreviewControllerDS(item);

currentController.PresentViewController(qlPreview, true, null);

}

}

}



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim resourcePath As String = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx"

Dim assembly As Assembly = Type.GetType(App).GetTypeInfo().Assembly

Dim fileStream As Stream = assembly.GetManifestResourceStream(resourcePath)

'Opens the workbook. 

Dim workbook As IWorkbook = application.Workbooks.Open(fileStream)

Dim stream As MemoryStream = New MemoryStream()

workbook.SaveAs(stream)

workbook.Close()

excelEngine.Dispose()

'Save the stream into xlsx file

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("sample.xlsx","application/ msexcel", stream)

Public Interface ISave

Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As Task

End Interface

Friend Class SaveIOS

Implements ISave

Public async Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As Task

Dim path As String = Environment.GetFolderPath(Environment.SpecialFolder.Personal)

Dim filePath As String = Path.Combine(path, filename)

Try

Dim fileStream As FileStream = File.Open(filePath, FileMode.Create)

stream.Position = 0

stream.CopyTo(fileStream)

fileStream.Flush()

fileStream.Close()

Catch e As Exception

End Try

Dim currentController As UIViewController = UIApplication.SharedApplication.KeyWindow.RootViewController

Do While currentController.PresentedViewController IsNot Nothing

currentController = currentController.PresentedViewController

Loop

Dim currentView As UIView = currentController.View

Dim qlPreview As New QLPreviewController()

Dim item As QLPreviewItem = New QLPreviewItemBundle(filename, filePath)

qlPreview.DataSource = New PreviewControllerDS(item)

currentController.PresentViewController(qlPreview, True, Nothing)

End Function

End Class



{% endhighlight %}

  {% endtabs %}  

