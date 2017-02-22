---
title: Xamarin
description: Briefs about loading and saving an Excel document in Xamarin platform.
platform: file-formats
control: XlsIO
documentation: UG
---
# Xamarin

In order to use XlsIO in your Xamarin application, please add the required assemblies. Refer [Assemblies Required](/File-Formats/XlsIO/Assemblies-Required).

## Loading a Document
The below code illustrates how to load an Excel document using stream in Xamarin.

{% tabs %}  
{% highlight c# %}
void btnCreate_Click(object sender, System.EventArgs e)
{
	ExcelEngine excelEngine = new ExcelEngine();
	IApplication application = excelEngine.Excel;
	application.DefaultVersion = ExcelVersion.Excel2013;

	string resourcePath = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx";
	//"App" is the class of Portable project.
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;

	Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

	//Opens the workbook
	IWorkbook workbook = application.Workbooks.Open(fileStream);
}
{% endhighlight %}
{% endtabs %}  

## Saving a Document

The below code illustrates how to save an Excel document using stream in Xamarin.

{% tabs %}  
{% highlight c# %}
void btnCreate_Click(object sender, System.EventArgs e)
{
	ExcelEngine excelEngine = new ExcelEngine();
	IApplication application = excelEngine.Excel;
	application.DefaultVersion = ExcelVersion.Excel2013;

	string resourcePath = "SampleBrowser.Samples.XlsIO.Template.Sample.xlsx";
	//"App" is the class of Portable project.
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

	//Opens the workbook 
	IWorkbook workbook = application.Workbooks.Open(fileStream);

	MemoryStream stream = new MemoryStream();
	workbook.SaveAs(stream);

	workbook.Close();
	excelEngine.Dispose();

	//Save the stream into xlsx file
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("sample.xlsx","application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

{% tabs %}  
{% highlight c# %}
using System.IO;
using System.Threading.Tasks;

private interface ISave
{
	//Method to save document as a file and view the saved document
	void SaveAndView(string filename, string contentType, MemoryStream stream);
}
{% endhighlight %}
{% endtabs %}

N> SaveAndView is helper method to save the stream as a physical file and open the file in default viewer. The operation varies between Windows Phone, Android and iOS platforms as described in the code samples below.

### Windows Phone

{% tabs %}  
{% highlight c# %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Windows.Storage;
using System.IO;
using Xamarin.Forms;

[assembly: Dependency(typeof(SaveWindowsPhone))]

class SaveWindowsPhone: ISave
{
	//Method to save document as a file in Windows Phone and view the saved document.
	public async Task SaveAndView(string filename, string contentType, MemoryStream stream)
    {
        //Save the stream to a file. 
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        StorageFile outFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
        using (Stream outStream = await outFile.OpenStreamForWriteAsync())
        {
            outStream.Write(stream.ToArray(), 0, (int)stream.Length);
        }

        //Launch the saved file for viewing in default viewer.
        await Windows.System.Launcher.LaunchFileAsync(outFile);
    }
}
{% endhighlight %}
{% endtabs %}

### Android

{% tabs %}  
{% highlight c# %}
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
    //Method to save document as a file in Android and view the saved document.
    public async Task SaveAndView(string fileName, String contentType, MemoryStream stream)
    {
        string root = null;
		
        //Get the root path of android device.
        if (Android.OS.Environment.IsExternalStorageEmulated)
        {
            root = Android.OS.Environment.ExternalStorageDirectory.ToString();
        }
        else
            root = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

        //Create directory and file.
        Java.IO.File myDir = new Java.IO.File(root + "/Syncfusion");
        myDir.Mkdir();

        Java.IO.File file = new Java.IO.File(myDir, fileName);

        //Remove the file if exists.
        if (file.Exists()) file.Delete();

        //Write the stream into file.
        FileOutputStream outs = new FileOutputStream(file);
        outs.Write(stream.ToArray());

        outs.Flush();
        outs.Close();

        //Launch the saved file for viewing in default viewer.
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

### iOS

{% tabs %}  
{% highlight c# %}
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
    //Method to save document as a file in iOS and view the saved document.
    public async Task SaveAndView(string filename, string contentType, MemoryStream stream)
    {
        //Get the root path of iOS device.
        string path = Environment.GetFolderPath(Environment.SpecialFolder.Personal);
        string filePath = Path.Combine(path, filename);

        //Create a file and write the stream into it.
        FileStream fileStream = File.Open(filePath, FileMode.Create);
        stream.Position = 0;
        stream.CopyTo(fileStream);
        
		fileStream.Flush();
        fileStream.Close();

        //Launch the saved file for viewing in default viewer.
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

N> Launcing a file in default viewer is different in iOS when compared to Windows Phone and Android. This requires the helper class PreviewControllerDS, as described in the code samples below.

{% tabs %}  
{% highlight c# %}
using System;
using QuickLook;

public class PreviewControllerDS : QLPreviewControllerDataSource
{
	private QLPreviewItem _item;

	public PreviewControllerDS(QLPreviewItem item)
	{
		_item = item;
	}

	public override nint PreviewItemCount (QLPreviewController controller)
	{
		return (nint)1;
	}

	public override IQLPreviewItem GetPreviewItem (QLPreviewController controller, nint index)
	{
		return _item;
	}
}

using System;
using QuickLook;
using Foundation;
using System.IO;

public class QLPreviewItemFileSystem : QLPreviewItem
{
	string _fileName, _filePath;

	public QLPreviewItemFileSystem(string fileName, string filePath)
	{
		_fileName = fileName;
		_filePath = filePath;
	}

	public override string ItemTitle
	{
		get
		{
			return _fileName;
		}
	}
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
	public QLPreviewItemBundle(string fileName, string filePath)
	{
		_fileName = fileName;
		_filePath = filePath;
	}

	public override string ItemTitle
	{
		get
		{
			return _fileName;
		}
	}
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