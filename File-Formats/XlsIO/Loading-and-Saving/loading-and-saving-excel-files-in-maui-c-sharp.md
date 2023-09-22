---
title: Loading and saving workbook in .NET MAUI | Syncfusion
description: Explains how to load and save Excel files in .NET MAUI applications using Syncfusion Excel Library.
platform: file-formats
control: XlsIO
documentation: UG
---
# Loading and saving workbook in .NET MAUI

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
Stream inputStream = executingAssembly.GetManifestResourceStream("MAUISample.Sample.xlsx");

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
Stream inputStream = executingAssembly.GetManifestResourceStream("MAUISample.Sample.xlsx");

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
SaveService saveService = new SaveService();
saveService.SaveAndView("Output.xlsx", "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", ms);
{% endhighlight %}
{% endtabs %} 

## Helper Class

## Save Service class in portable project

Add the new class file with name as **SaveService** to the **Project** and add below code in it. This is the helper class used to save and view the Excel file in windows, android, iOS and MAC devices.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
namespace MAUISample.Services
{
  public partial class SaveService
  {
    //Method to save document as a file and view the saved document.
    public partial void SaveAndView(string filename, string contentType, MemoryStream stream);
  }
}
{% endhighlight %}
{% endtabs %}

## Save and View the Excel document in windows

Add the new class file with name **SaveWindows** file under **Project-> Platforms-> Windows** directory to save and view the Excel document in the windows machine and use the below code in it.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using Windows.Storage;
using Windows.Storage.Pickers;
using Windows.Storage.Streams;
using Windows.UI.Popups;

namespace MAUISample.Services
{
  public partial class SaveService
  {
    public async partial void SaveAndView(string filename, string contentType, MemoryStream stream)
    {
      StorageFile stFile;
      string extension = Path.GetExtension(filename);
      //Gets process windows handle to open the dialog in application process. 
      IntPtr windowHandle = System.Diagnostics.Process.GetCurrentProcess().MainWindowHandle;
      if (!Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons"))
      {
        //Creates file save picker to save a file. 
        FileSavePicker savePicker = new();
        savePicker.DefaultFileExtension = ".xlsx";
        savePicker.SuggestedFileName = filename;
        //Saves the file as xlsx file.
        savePicker.FileTypeChoices.Add("XLSX", new List<string>() { ".xlsx" });
        WinRT.Interop.InitializeWithWindow.Initialize(savePicker, windowHandle);
        stFile = await savePicker.PickSaveFileAsync();
      }
      else
      {
        StorageFolder local = ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
      }
      if (stFile != null)
      {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
          //Writes compressed data from memory to file.
          using Stream outstream = zipStream.AsStreamForWrite();
          outstream.SetLength(0);
          //Saves the stream as file.
          byte[] buffer = stream.ToArray();
          outstream.Write(buffer, 0, buffer.Length);
          outstream.Flush();
        }
        //Create message dialog box. 
        MessageDialog msgDialog = new("Do you want to view the document?", "File has been created successfully");
        UICommand yesCmd = new("Yes");
        msgDialog.Commands.Add(yesCmd);
        UICommand noCmd = new("No");
        msgDialog.Commands.Add(noCmd);

        WinRT.Interop.InitializeWithWindow.Initialize(msgDialog, windowHandle);

        //Showing a dialog box. 
        IUICommand cmd = await msgDialog.ShowAsync();
        if (cmd.Label == yesCmd.Label)
        {
          //Launch the saved file. 
          await Windows.System.Launcher.LaunchFileAsync(stFile);
        }
      }
    }
  }
}
{% endhighlight %}
{% endtabs %}

## Save and View the Excel document in Android

Add the new class file with name **SaveAndroid** file under **Project-> Platforms-> Android** directory to save and view the Excel document in the Android Device and use the below code in it.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using Android.Content;
using Android.OS;
using Java.IO;
using System;
using System.IO;
using System.Threading.Tasks;

namespace MAUISample.Services
{
  public partial class SaveService
  {
    public partial void SaveAndView(string filename, string contentType, MemoryStream stream)
    {
      string exception = string.Empty;
      string? root = null;

      if (Android.OS.Environment.IsExternalStorageEmulated)
      {
        root = Android.App.Application.Context!.GetExternalFilesDir(Android.OS.Environment.DirectoryDownloads)!.AbsolutePath;
      }
      else
        root = System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments);

      Java.IO.File myDir = new(root + "/Syncfusion");
      myDir.Mkdir();
      Java.IO.File file = new(myDir, filename);

      if (file.Exists())
      {
        file.Delete();
      }

      try
      {
        FileOutputStream outs = new(file);
        outs.Write(stream.ToArray());

        outs.Flush();
        outs.Close();
      }
      catch (Exception e)
      {
        exception = e.ToString();
      }
      if (file.Exists())
      {
        if (Build.VERSION.SdkInt >= Android.OS.BuildVersionCodes.N)
        {
          var fileUri = AndroidX.Core.Content.FileProvider.GetUriForFile(Android.App.Application.Context, Android.App.Application.Context.PackageName + ".provider", file);
          var intent = new Intent(Intent.ActionView);
          intent.SetData(fileUri);
          intent.AddFlags(ActivityFlags.NewTask);
          intent.AddFlags(ActivityFlags.GrantReadUriPermission);
          Android.App.Application.Context.StartActivity(intent);
        }
        else
        {
          var fileUri = Android.Net.Uri.Parse(file.AbsolutePath);
          var intent = new Intent(Intent.ActionView);
          intent.SetDataAndType(fileUri, contentType);
          intent = Intent.CreateChooser(intent, "Open File");
          intent!.AddFlags(ActivityFlags.NewTask);
          Android.App.Application.Context.StartActivity(intent);
        }
      }
    }
  }
}
{% endhighlight %}
{% endtabs %}

N> Introduced a new runtime permission model for the Android SDK version 23 and above. So, include the following code for enabling the Android file provider to save and view the generated PDF document.

Create a new XML file with the name of **provider_path.xml** under the **Resources-> xml** folder of **Android project** and add the following code in it. Eg: Resources/xml/provider_path.xml

{% tabs %}
{% highlight XAML %}
<?xml version="1.0" encoding="UTF-8" ?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
   <external-path name="external_files" path="."/>
</paths>
{% endhighlight %}
{% endtabs %}

Add the following code to the **AndroidManifest.xml** file located under **Properties** folder.

{% tabs %}
{% highlight XAML %}
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android" android:versionCode="1" android:versionName="1.0" package="com.companyname.MAUISample">
   <uses-sdk android:minSdkVersion="19" android:targetSdkVersion="27" />
   <application android:label="MAUISample.Android">
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

## Save and View the Excel document in iOS

Add the new class file with name **SaveIOS** file under **Project-> Platforms-> iOS** directory to save and view the Excel document in the iOS Device and use the below code in it.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using QuickLook;
using UIKit;

namespace MAUISample.Services
{
  public partial class SaveService
  {
    public partial void SaveAndView(string filename, string contentType, MemoryStream stream)
    {
      string exception = string.Empty;
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
        exception = e.ToString();
      }
      if (contentType != "application/html" || exception == string.Empty)
      {
#pragma warning disable CA1416 
        UIViewController? currentController = UIApplication.SharedApplication!.KeyWindow!.RootViewController;
#pragma warning restore CA1416 
        while (currentController!.PresentedViewController != null)
          currentController = currentController.PresentedViewController;

        QLPreviewController qlPreview = new();
        QLPreviewItem item = new QLPreviewItemBundle(filename, filePath);
        qlPreview.DataSource = new PreviewControllerDS(item);
        currentController.PresentViewController((UIViewController)qlPreview, true, null);
      }
    }
  }
}
{% endhighlight %}
{% endtabs %}

## Save and View the Excel document in MacCatalyst

Add the new class file with name **SaveMAC** file under **Project-> Platforms-> MacCatalyst** directory to save and view the Excel document in the MAC Device and use the below code in it.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using Foundation;
using QuickLook;
using UIKit;

namespace MAUISample.Services
{
  public partial class SaveService
  {
    public partial void SaveAndView(string filename, string contentType, MemoryStream stream)
    {
      string path = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
      string filePath = Path.Combine(path, filename);
      stream.Position = 0;
      //Saves the document
      using FileStream fileStream = new(filePath, FileMode.Create, FileAccess.ReadWrite);
      stream.CopyTo(fileStream);
      fileStream.Flush();
      fileStream.Dispose();
#pragma warning disable CA1416 
      //Launch the file
      UIViewController? currentController = UIApplication.SharedApplication!.KeyWindow!.RootViewController;
#pragma warning restore CA1416 
      while (currentController!.PresentedViewController != null)
        currentController = currentController.PresentedViewController;
      UIView? currentView = currentController.View;

      QLPreviewController qlPreview = new();
      QLPreviewItem item = new QLPreviewItemBundle(filename, filePath);
      qlPreview.DataSource = new PreviewControllerDS(item);
      currentController.PresentViewController((UIViewController)qlPreview, true, null);
    }
  }
}

public class QLPreviewItemFileSystem : QLPreviewItem
{
  readonly string _fileName, _filePath;

  public QLPreviewItemFileSystem(string fileName, string filePath)
  {
    _fileName = fileName;
    _filePath = filePath;
  }

  public override string PreviewItemTitle
  {
    get
    {
      return _fileName;
    }
  }
  public override NSUrl PreviewItemUrl
  {
    get
    {
      return NSUrl.FromFilename(_filePath);
    }
  }
}

public class QLPreviewItemBundle : QLPreviewItem
{
  readonly string _fileName, _filePath;
  public QLPreviewItemBundle(string fileName, string filePath)
  {
    _fileName = fileName;
    _filePath = filePath;
  }

  public override string PreviewItemTitle
  {
    get
    {
      return _fileName;
    }
  }
  public override NSUrl PreviewItemUrl
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

public class PreviewControllerDS : QLPreviewControllerDataSource
{
  private readonly QLPreviewItem _item;

  public PreviewControllerDS(QLPreviewItem item)
  {
    _item = item;
  }

  public override nint PreviewItemCount(QLPreviewController controller)
  {
    return (nint)1;
  }

  public override IQLPreviewItem GetPreviewItem(QLPreviewController controller, nint index)
  {
    return _item;
  }
}
{% endhighlight %}
{% endtabs %}
