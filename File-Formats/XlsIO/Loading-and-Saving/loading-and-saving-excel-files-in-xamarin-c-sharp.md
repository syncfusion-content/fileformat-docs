---
title: Loading and saving workbook in Xamarin | Syncfusion
description: Explains how to load and save Excel files in Xamarin applications using Syncfusion XlsIO
platform: file-formats
control: XlsIO
documentation: UG
---
# Loading and saving workbook in Xamarin

## Opening an existing workbook from stream

You can open an existing workbook from stream by using the overloads of [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_IO_Stream_) methods of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) interface.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Load the file into stream
Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = executingAssembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);
{% endhighlight %}
{% endtabs %}  

## Saving an Excel workbook to stream

You can also save the created or manipulated workbook to stream using overloads of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_IO_Stream_) methods.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Load the file into stream
Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = executingAssembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Xlsx;

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);
outputStream.Position = 0;

//Saves the memory stream as a file.
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", outputStream);
{% endhighlight %}
{% endtabs %} 

## Helper Files

Download the helper files from this [link](https://www.syncfusion.com/downloads/support/directtrac/general/ze/HELPER~1-1423062113.zip) and add them into the mentioned project. These helper files allow you to save the stream as a physical file and open the file for viewing. 

<table>
<tr>
<thead><th>
Project</th>
<th>
File Name
</th>
<th>
Summary
</th>
</thead>
</tr>
<tbody>
<tr>
<td>
Portable project
</td>
<td>
ISave.cs
</td>
<td>
Represent the base interface for save operation
</td>
</tr>
<tr>
<td>
iOS Project
</td>
<td>
<ul>
<li>SaveIOS.cs</li>
<li>PreviewControllerDS.cs</li>
</ul>
</td>
<td>
<ul>
<li>Save implementation for iOS device</li>
<li>Helper class for viewing the Excel file in iOS device</li>
</ul>
</td>
</tr>
<tr>
<td>
Android project
</td>
<td>
SaveAndroid.cs
</td>
<td>
Save implementation for Android device
</td>
</tr>
<tr>
<td>
WinPhone project
</td>
<td>
SaveWinPhone.cs
</td>
<td>
Save implementation for Windows Phone device
</td>
</tr>
<tr>
<td>
UWP project
</td>
<td>
SaveWindows.cs
</td>
<td>
Save implementation for UWP device.
</td>
</tr>
<tr>
<td>
Windows(8.1) project 
</td>
<td>
SaveWindows81.cs
</td>
<td>
Save implementation for WinRT device.
</td>
</tr>
</tbody>
</table>

The respective code snippets are given below also, for reference.

### Helper class for Portable project

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using System.IO;
using System.Threading.Tasks;

public interface ISave
{
  //Method to save document as a file and view the saved document
  Task SaveAndView(string filename, string contentType, MemoryStream stream);
}
{% endhighlight %}
{% endtabs %} 

### Helper class for Windows project

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Xamarin.Forms;
using Windows.Storage;
using Windows.Storage.Pickers;
using Xamarin.Forms.Platform.UWP;

[assembly: Dependency(typeof(SaveWindows))]

class SaveWindows: ISave
{
  public async Task SaveAndView(string filename, string contentType, MemoryStream stream)
  {
    //save the stream into the file. 
    if (Device.Idiom != TargetIdiom.Desktop)
    {
      StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
      StorageFile outFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
      using (Stream outStream = await outFile.OpenStreamForWriteAsync())
      {
        outStream.Write(stream.ToArray(), 0, (int)stream.Length);
      }
      if (contentType != "application/html")
        await Windows.System.Launcher.LaunchFileAsync(outFile);
    }
    else
    {
      StorageFile storageFile = null;
      FileSavePicker savePicker = new FileSavePicker();
      savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
      savePicker.SuggestedFileName = filename;
      switch (contentType)
      {
        case "application/vnd.openxmlformats-officedocument.presentationml.presentation":
          savePicker.FileTypeChoices.Add("PowerPoint Presentation", new List<string>() { ".pptx", });
          break;

        case "application/msexcel":
          savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx", });
          break;

        case "application/msword":
          savePicker.FileTypeChoices.Add("Word Document", new List<string>() { ".docx" });
          break;

        case "application/pdf":
          savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
          break;

        case "application/html":
          savePicker.FileTypeChoices.Add("HTML Files", new List<string>() { ".html" });
          break;
      }
      storageFile = await savePicker.PickSaveFileAsync();

      using (Stream outStream = await storageFile.OpenStreamForWriteAsync())
      {
        outStream.Write(stream.ToArray(), 0, (int)stream.Length);
      }

      //Invoke the saved file for Viewing.
      await Windows.System.Launcher.LaunchFileAsync(storageFile);
    }
  }
}
{% endhighlight %}
{% endtabs %} 

### Helper class for Android project

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using System;
using System.IO;
using GettingStarted.Droid;
using Android.Content;
using Java.IO;
using Xamarin.Forms;
using System.Threading.Tasks;

[assembly: Dependency(typeof(SaveAndroid))]

class SaveAndroid: ISave
{
  //Method to save document as a file in Android and view the saved document
  public async Task SaveAndView(string fileName, String contentType, MemoryStream stream)
  {
    string root = null;
    //Get the root path in android device.
    if (Android.OS.Environment.IsExternalStorageEmulated)
    {
      root = Android.OS.Environment.ExternalStorageDirectory.ToString();
    }
    else
      root = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

    //Create directory and file 
    Java.IO.File myDir = new Java.IO.File(root + "/Syncfusion");
    myDir.Mkdir();

    Java.IO.File file = new Java.IO.File(myDir, fileName);

    //Remove if the file exists
    if (file.Exists()) file.Delete();

    //Write the stream into the file
    FileOutputStream outs = new FileOutputStream(file);
    outs.Write(stream.ToArray());

    outs.Flush();
    outs.Close();

    //Invoke the created file for viewing
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
{% endtabs %} 

N> Introduced a new runtime permission model for the Android SDK version 23 and above. So, include the following code for enabling the Android file provider to save and view the generated PDF document.

Create a new XML file with the name of **provider_path.xml** under the **Resources** folder of **Android project** and add the following code in it. Eg: Resources/xml/provider_path.xml

{% tabs %}
{% highlight XAML %}
<?xml version="1.0" encoding="UTF-8" ?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
   <external-path name="external_files" path="."/>
</paths>
{% endhighlight %}
{% endtabs %}

Add the following code to the **AndroidManifest.xml** file located under Properties/AndroidManifest.xml.

{% tabs %}
{% highlight XAML %}
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android" android:versionCode="1" android:versionName="1.0" package="com.companyname.CreateXlsIOSample">
   <uses-sdk android:minSdkVersion="19" android:targetSdkVersion="27" />
   <application android:label="CreateXlsIOSample.Android">
      <provider android:name="androidx.core.content.FileProvider"
         android:authorities="${applicationId}.provider"
         android:exported="false"
         android:grantUriPermissions="true">
         <meta-data android:name="android.support.FILE_PROVIDER_PATHS"
            android:resource="@xml/provider_paths" />
      </provider>
   </application>
</manifest>
{% endhighlight %}
{% endtabs %}

### Helper class for iOS project

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using Xamarin.Forms;
using GettingStarted.iOS;
using UIKit;
using QuickLook;

[assembly: Dependency(typeof(SaveIOS))]

class SaveIOS: ISave
{
  //Method to save document as a file and view the saved document
  public async Task SaveAndView(string filename, string contentType, MemoryStream stream)
  {
    //Get the root path in iOS device.
    string path = Environment.GetFolderPath(Environment.SpecialFolder.Personal);
    string filePath = Path.Combine(path, filename);

    //Create a file and write the stream into it.
    FileStream fileStream = File.Open(filePath, FileMode.Create);
    stream.Position = 0;
    stream.CopyTo(fileStream);
    fileStream.Flush();
    fileStream.Close();

    //Invoke the saved document for viewing
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
{% endhighlight %}
{% endtabs %} 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using Foundation;
using QuickLook;
using System;
using System.IO;

public class PreviewControllerDS : QLPreviewControllerDataSource
{
  //Document cache
  private QLPreviewItem _item;

  //Setting the document
  public PreviewControllerDS(QLPreviewItem item)
  {
    _item = item;
  }

  //Setting document count to 1
  public override nint PreviewItemCount (QLPreviewController controller)
  {
    return 1;
  }

  //Return the document
  public override IQLPreviewItem GetPreviewItem (QLPreviewController controller, nint index)
  {
    return _item;
  }
}

public class QLPreviewItemFileSystem : QLPreviewItem
{
  string _fileName, _filePath;

  //Setting file name and path
  public QLPreviewItemFileSystem(string fileName, string filePath)
  {
    _fileName = fileName;
    _filePath = filePath;
  }

  //Return file name
  public override string ItemTitle
  {
    get
    {
      return _fileName;
    }
  }

  //Retun file path as NSUrl
  public override NSUrl ItemUrl
  {
    get
    {
      return NSUrl.FromFilename(_filePath);
    }
  }
}

public class QLPreviewItemBundle : QLPreviewItem
{
  string _fileName, _filePath;

  //Setting file name and path
  public QLPreviewItemBundle(string fileName, string filePath)
  {
    _fileName = fileName;
    _filePath = filePath;
  }

  //Return file name
  public override string ItemTitle
  {
    get
    {
      return _fileName;
    }
  }

  //Retun file path as NSUrl
  public override NSUrl ItemUrl
  {
    get
    {
      var documents = NSBundle.MainBundle.BundlePath;
      var lib = Path.Combine(documents, _filePath);
      var url = NSUrl.FromFilename(lib);
      return url;
    }
  }
}
{% endhighlight %}
{% endtabs %} 