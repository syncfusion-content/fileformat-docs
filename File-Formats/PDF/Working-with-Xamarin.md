---
title: Working with Xamarin
description: This section explains how to load and save PDF document in Xamarin
platform: file-formats
control: PDF
documentation: UG
---
# Working with Xamarin

In your Xamarin application, please add the required assemblies in order to use Essential PDF. [Refer here for assemblies required](/File-Formats/PDF/Assemblies-Required).

## Loading the document 

The following code example illustrates how to load the file by using stream in Xamarin.
{% tabs %}
{% highlight c# %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create booklet with two sides

PdfDocument document = PdfBookletCreator.CreateBooklet(loadedDocument, new SizeF(1000, 700), true);

MemoryStream memoryStream = new MemoryStream();

//Save the document into memory stream

document.Save(memoryStream);

//close the documents

document.Close(true);

loadedDocument.Close(true);

//Save the stream into pdf file

Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", memoryStream);

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

{% highlight vb.net %}

'Load the file as stream

Dim docStream As Stream = GetType(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf")

Dim loadedDocument As New PdfLoadedDocument(docStream)

'Create booklet with two sides

Dim document As PdfDocument = PdfBookletCreator.CreateBooklet(loadedDocument, New SizeF(1000, 700), True)

Dim memoryStream As New MemoryStream()

'Save the document into memory stream

document.Save(memoryStream)

'close the documents

document.Close(True)

loadedDocument.Close(True)

'Save the stream into pdf file

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("sample.pdf", "application/pdf", memoryStream)

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
## Saving the document 

The following code example illustrates how to save the PDF document in Xamarin windows phone platform.
{% tabs %}
{% highlight c# %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create Pdf graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a solid brush

PdfBrush brush = new PdfSolidBrush(Color.FromArgb(255, 0, 0, 0));

//Set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 36);

//Draw the text

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//create the stream

MemoryStream memoryStream = new MemoryStream();

//save the document into stream

document.Save(memoryStream);

//close the document

document.Close(true);

Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);

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

{% highlight vb.net %}

'Create a new document.

Dim document As New PdfDocument()

'Add a page

Dim page As PdfPage = document.Pages.Add()

'Create Pdf graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush

Dim brush As PdfBrush = New PdfSolidBrush(Color.FromArgb(255, 0, 0, 0))

'Set the font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 36)

'Draw the text

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'create the stream

Dim memoryStream As New MemoryStream()

'save the document into stream

document.Save(memoryStream)

'close the document

document.Close(True)

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("Output.pdf", "application/pdf", memoryStream)

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
The following code example illustrates how to save the file by using stream in xamarin android platform.
{% tabs %}
{% highlight c# %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create Pdf graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a solid brush

PdfBrush brush = new PdfSolidBrush(Color.FromArgb(255, 0, 0, 0));

//Set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 36);

//Draw the text

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//create the stream

MemoryStream memoryStream = new MemoryStream();

//save the document into stream

document.Save(memoryStream);

//close the document

document.Close(true);

Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);

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

{% highlight vb.net %}

'Create a new document

Dim document As New PdfDocument()

'Add a page

Dim page As PdfPage = document.Pages.Add()

'Create Pdf graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush

Dim brush As PdfBrush = New PdfSolidBrush(Color.FromArgb(255, 0, 0, 0))

'Set the font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 36)

'Draw the text

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'create the stream

Dim memoryStream As New MemoryStream()

'save the document into stream

document.Save(memoryStream)

'close the document

document.Close(True)

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("Output.pdf", "application/pdf", memoryStream)

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
The following code example illustrates how to save the file by using stream in xamarin iOS platform.
{% tabs %}
{% highlight c# %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create Pdf graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a solid brush

PdfBrush brush = new PdfSolidBrush(Color.FromArgb(255, 0, 0, 0));

//Set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 36);

//Draw the text

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//create the stream

MemoryStream memoryStream = new MemoryStream();

//save the document into stream

document.Save(memoryStream);

//close the document

document.Close(true);

Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);

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

//UIViewController uiView = currentView as UIViewController;

currentController.PresentViewController(qlPreview, true, null);

}

}

}





{% endhighlight %}

{% highlight vb.net %}

'Create a new document

Dim document As New PdfDocument()

'Add a page

Dim page As PdfPage = document.Pages.Add()

'Create Pdf graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush

Dim brush As PdfBrush = New PdfSolidBrush(Color.FromArgb(255, 0, 0, 0))

'Set the font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 36)

'Draw the text

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'create the stream

Dim memoryStream As New MemoryStream()

'save the document into stream

document.Save(memoryStream)

'close the document

document.Close(True)

Xamarin.Forms.DependencyService.Get(Of ISave)().Save("Output.pdf", "application/pdf", memoryStream)

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

'UIViewController uiView = currentView as UIViewController;

currentController.PresentViewController(qlPreview, True, Nothing)

End Function

End Class





{% endhighlight %}
{% endtabs %}
