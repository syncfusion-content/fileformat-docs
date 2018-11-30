---
title: Working with Xamarin
description: Working with presentation library in Xamarin Platform
platform: file-formats
control: Presentation
documentation: UG
keywords: Working with presentation library in Xamarin Platform
---

# Working with Xamarin

In your Xamarin Application, please add the required assemblies in order to use Presentation. [Refer here for assemblies required](/File-Formats/Presentation/Assemblies-Required)

## Loading the Presentation

The following code example illustrates how to load the PowerPoint Presentation by using stream in Xamarin.
{% tabs %}
{% highlight c# %}
//Loads the PowerPoint Presentation as stream.

Assembly assembly = typeof(GettingStartedPresentation).GetTypeInfo().Assembly;

string resourcePath = "SampleBrowser.Presentation.Assets.HelloWorld.pptx";

Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Loads or opens existing Presentation using open method of Presentation class.

IPresentation presentation = await Presentation.OpenAsync(fileStream);

//Creates Memory stream to save Presentation.

MemoryStream stream = new MemoryStream();

//Saves Presentation in stream format.

presentation.Save(stream);

presentation.Close();
{% endhighlight %}
{% endtabs %}

## Saving the Presentation

The following code example illustrates how to save the PowerPoint Presentation in Xamarin Windows Phone platform.
{% tabs %}
{% highlight c# %}

//Creates new Presentation without slides.
IPresentation presentation = Presentation.Create();

//Adds new Blank type of slide.
ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds a shape with specified size and position.
IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 1.92 * 72, 1.51 * 72, 10.85 * 72, 4.12 * 72);

//Adds text into the shape.
shape.TextBody.AddParagraph("In 2000, AdventureWorks Cycles bought a small manufacturing plant, located in Mexico. It manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the another location for final product assembly. In 2001, the plant became the sole manufacturer and distributor of the touring bicycle product group.");

//Creates new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Saves Presentation in stream format.
presentation.Save(stream);

presentation.Close();

stream.Position = 0;

Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("GettingStartedSample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

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

The following code example illustrates how to save the PowerPoint Presentation in Xamarin.Android platform.
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

The following code example illustrates how to save the PowerPoint Presentation in Xamarin.iOS platform.

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

        QLPreviewController preview = new QLPreviewController();
        QLPreviewItem item = new QLPreviewItemBundle(filename, filePath);
        preview.DataSource = new PreviewControllerDS(item);

        currentController.PresentViewController(preview, true, null);
    }
}

{% endhighlight %}
{% endtabs %}

N> The image and PDF conversions are not supported in Xamarin platforms.
