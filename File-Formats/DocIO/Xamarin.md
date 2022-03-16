---
title: Working with Xamarin
description: Create a Xamarin application and load the document
platform: file-formats
control: DocIO
documentation: UG
---

# Working with Xamarin

In your Xamarin application, please add the required assemblies in order to use DocIO. [Refer here for assemblies required](/File-Formats/DocIO/Assemblies-Required).

## Loading the document

The following code example illustrates how to load the Word document by using stream in Xamarin.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the Word document as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.docx");

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Loads or opens an existing word document through Open method of WordDocument class

await document.Open(docStream, FormatType.Docx);

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

await document.Save(stream, FormatType.Docx);

//Close the documents

document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the Word document as stream

Dim docStream As Stream = GetType(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.docx")

'Creates an empty Word document instance

Dim document As New WordDocument()

'Loads or opens an existing word document through Open method of WordDocument class

Await document.Open(docStream, FormatType.Docx)

Dim stream As New MemoryStream()

'Save the document into memory stream

await document.Save(stream, FormatType.Docx)

'Close the documents

document.Close()

{% endhighlight %}

{% endtabs %}

## Save the document 

The following code example illustrates how to save the Word document in Xamarin Windows Phone platform.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

MemoryStream memoryStream = new MemoryStream();

//Save the document into memory stream

await document.Save(stream, FormatType.Docx);

//Close the documents

document.Close();

Xamarin.Forms.DependencyService.Get<ISave>().Save("Result.docx", "application/msword", memoryStream);

public interface ISave

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

{% highlight vb.net tabtitle="VB.NET" %}

'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

Dim memoryStream As New MemoryStream()

'Save the document into memory stream

Await document.Save(stream, FormatType.Docx)

'Close the documents

document.Close()

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("Result.docx", "application/msword", memoryStream)

Public Interface ISave

Function Save(ByVal filename As String, ByVal contentType As String, ByVal stream As MemoryStream) As Task

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

The following code example illustrates how to save the Word document by using stream in Xamarin.Android platform.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

MemoryStream memoryStream = new MemoryStream();

//Save the document into memory stream

await document.Save(stream, FormatType.Docx);

//Close the documents

document.Close();

Xamarin.Forms.DependencyService.Get<ISave>().Save("Result.docx", "application/msword", memoryStream);

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

{% highlight vb.net tabtitle="VB.NET" %}

'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

Dim memoryStream As New MemoryStream()

'Save the document into memory stream

Await document.Save(stream, FormatType.Docx)

'Close the documents

document.Close()

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("Result.docx", "application/msword", memoryStream)

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

The following code example illustrates how to save the Word document by using stream in Xamarin.iOS platform.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

MemoryStream memoryStream = new MemoryStream();

//Save the document into memory stream

await document.Save(stream, FormatType.Docx);

//Close the documents

document.Close();

Xamarin.Forms.DependencyService.Get<ISave>().Save("Result.docx", "application/msword", memoryStream);

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

QLPreviewController preview = new QLPreviewController();

QLPreviewItem item = new QLPreviewItemBundle(filename, filePath);

preview.DataSource = new PreviewControllerDS(item);

//UIViewController uiView = currentView as UIViewController;

currentController.PresentViewController(preview, true, null);

}

}

}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}


'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

Dim memoryStream As New MemoryStream()

'Save the document into memory stream

Await document.Save(stream, FormatType.Docx)

'Close the documents

document.Close()

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("Result.docx", "application/msword", memoryStream)

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

Dim preview As New QLPreviewController()

Dim item As QLPreviewItem = New QLPreviewItemBundle(filename, filePath)

preview.DataSource = New PreviewControllerDS(item)

'UIViewController uiView = currentView as UIViewController;

currentController.PresentViewController(preview, True, Nothing)

End Function

End Class

{% endhighlight %}

{% endtabs %}

N> The Image and PDF conversions are not supported in Xamarin Platform.