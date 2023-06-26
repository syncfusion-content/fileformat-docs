---
title: Open and save Presentation in WinUI | Syncfusion
description: Open and save Presentation in WinUI using WinUI PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Open and save Presentation in WinUI

Syncfusion PowerPoint is a [WinUI PowerPoint library](https://www.syncfusion.com/powerpoint-framework/winui/powerpoint-library) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **open and save a Presentation in WinUI**.

## Prerequisites
To use the WinUI 3 project templates, install the Windows App SDK extension for Visual Studio. For more details, refer [here](https://docs.microsoft.com/en-us/windows/apps/windows-app-sdk/set-up-your-development-environment).

## WinUI Desktop app

### Steps to open and save PowerPoint Presentation programmatically

Step 1: Create a new C# WinUI Desktop app. Select Blank App, Packaged with WAP (WinUI 3 in Desktop) from the template and click the **Next** button.

![Create the WinUI Desktop app in Visual Studio](Workingwith_WinUI/Create_Desktop_Project.png)

Step 2: Enter the project name and click **Create**.

![Create a project name for your new project](Workingwith_WinUI/Desktop_Configure.png)

Step 3: Set the Target version to Windows 10, version 2004 (build 19041) and the Minimum version to Windows 10, version 1809 (build 17763) and then click **OK**.

![Set the target version](Workingwith_WinUI/Target_Version.png)

Step 4: Install the [Syncfusion.Presentation.NET](https://www.nuget.org/packages/Syncfusion.Presentation.NET) NuGet package as a reference to your .NET Standard applications from the [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.Presentation.NET Nuget Package](Workingwith_WinUI/Install_Nuget.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering a Syncfusion license key in your application to use our components.

Step 5: Add a new button to the **MainWindow.xaml** as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

<Window
    x:Class="Read_and_edit_PowerPoint_presentation.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Read_and_edit_PowerPoint_presentation"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Orientation="Horizontal" HorizontalAlignment="Center" VerticalAlignment="Center">
        <Button x:Name="button" Click="CreateDocument">Create Document</Button>
    </StackPanel>
</Window>

{% endhighlight %}
{% endtabs %}

Step 6: Include the following namespaces in the **MainWindow.xaml.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 7: Add a new action method **CreateDocument** in MainWindow.xaml.cs and include the below code snippet to **open an existing PowerPoint Presentation in WinUI Desktop app**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Get a picture as stream.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream stream = assembly.GetManifestResourceStream("Read_and_edit_PowerPoint_presentation.Assets.Template.pptx");

{% endhighlight %}
{% endtabs %}

Step 8: Add below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Opens an existing PowerPoint presentation.
using IPresentation pptxDoc = Presentation.Open(stream);
//Get the first slide from the PowerPoint presentation.
ISlide slide = pptxDoc.Slides[0];
//Get the first shape of the slide.
IShape shape = slide.Shapes[0] as IShape;
//Modify the text of the shape.
if (shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 9: Add below code example to **save the PowerPoint Presentation in WinUI Desktop app**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the PowerPoint Presentation document to stream.
using MemoryStream pptx = new();
pptxDoc.Save(pptx);
//Saves and launch the file.
SaveHelper.SaveAndLaunch("Sample.pptx", pptx);

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Getting-started/WinUI/WinUI-Desktop-app/Read-and-edit-PowerPoint-presentation).

By executing the program, you will get the **PowerPoint document** as follows.

![WinUI Desktop app output PowerPoint document](Workingwith_Core/Open-and-Save-output-image.png)

### Save Presentation file in WinUI Desktop app

Step 1: Create a new class file in the name of **SaveHelper.cs** and add the below code snippet for save the **Presentation** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

/// <summary>
/// Saves and launch the file.
/// </summary>
/// <param name="filename">File name.</param>
/// <param name="stream">Stream to save.</param>
public static async void SaveAndLaunch(string filename, MemoryStream stream)
{
    StorageFile storageFile;
    string extension = Path.GetExtension(filename);
    //Gets process windows handle to open the dialog in application process.
    IntPtr windowHandle = System.Diagnostics.Process.GetCurrentProcess().MainWindowHandle;
    if (!Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons"))
    {
        FileSavePicker savePicker = new();
        if (extension == ".pptx")
        {
            savePicker.DefaultFileExtension = ".pptx";
            savePicker.SuggestedFileName = filename;
            //Saves the file as Docx file.
            savePicker.FileTypeChoices.Add("PPTX", new List<string>() { ".pptx" });
        }
        WinRT.Interop.InitializeWithWindow.Initialize(savePicker, windowHandle);
        storageFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = ApplicationData.Current.LocalFolder;
        storageFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (storageFile != null)
    {
        using (IRandomAccessStream zipStream = await storageFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Writes compressed data from memory to file.
            using Stream outstream = zipStream.AsStreamForWrite();
            outstream.SetLength(0);
            byte[] buffer = stream.ToArray();
            outstream.Write(buffer, 0, buffer.Length);
            outstream.Flush();
        }
        //Creates message dialog box. 
        MessageDialog msgDialog = new("Do you want to view the Document?", "File has been created successfully");
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
            await Windows.System.Launcher.LaunchFileAsync(storageFile);
        }
    }
}

{% endhighlight %}
{% endtabs %}

## WinUI UWP app

### Steps to open and save PowerPoint Presentation programmatically

Step 1: Create a new C# WinUI UWP app. Select Blank App (WinUI 3 in UWP)from the template and **click** the Next button.

![Create the WinUI UWP app in Visual Studio](Workingwith_WinUI/Create_UWP_Project.png)

N> To get the UWP Experimental project templates and build UWP apps with WinUI 3, you should download the [Windows App SDK Experimental Extension](https://aka.ms/projectreunion/previewdownload) for Visual Studio.

Step 2: Enter the project name and click **Create**.

![Create a project name for your new project](Workingwith_WinUI/UWP_Configure.png)

Step 3: Set the Target version to Windows 10, version 2004 (build 19041) and the Minimum version to Windows 10, version 1809 (build 17763) and then click **OK**.

![Set the target version](Workingwith_WinUI/Target_Version.png)

Step 4: Install the [Syncfusion.Presentation.NET](https://www.nuget.org/packages/Syncfusion.Presentation.NET) NuGet package as a reference to your .NET Standard applications from the [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.Presentation.NET Nuget Package](Workingwith_WinUI/Install_Nuget.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering a Syncfusion license key in your application to use our components.

Step 5: Add a new button to the **MainPage.xaml** as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

<Page
    x:Class="Read_and_edit_PowerPoint_presentation.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Read_and_edit_PowerPoint_presentation"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <StackPanel Orientation="Horizontal" HorizontalAlignment="Center" VerticalAlignment="Center">
        <Button x:Name="button" Click="CreatePresentation">Create Presentation</Button>
    </StackPanel>
</Page>

{% endhighlight %}
{% endtabs %}

Step 6: Include the following namespaces in the **MainPage.xaml.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 7: Add a new action method **CreatePresentation** in MainPage.xaml.cs and include the below code snippet to **open an existing PowerPoint Presentation in WinUI UWP app**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Open an existing PowerPoint presentation.
IPresentation pptxDoc = Presentation.Open(assembly.GetManifestResourceStream("Read_and_edit_PowerPoint_presentation.Assets.Template.pptx"));

{% endhighlight %}
{% endtabs %}

Step 8: Add below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Get the first slide from the PowerPoint presentation.
ISlide slide = pptxDoc.Slides[0];
//Gets the first shape of the slide.
IShape shape = slide.Shapes[0] as IShape;
//Modify the text of the shape.
if (shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 9: Add below code example to **save the PowerPoint Presentation in WinUI UWP app**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the Presentation files to MemoryStream.
MemoryStream stream = new MemoryStream();
pptxDoc.Save(stream);
//Save the stream as a Presentation file in the local machine.
Save(stream);

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Getting-started/WinUI/WinUI-UWP-app/Read-and-edit-PowerPoint-presentation).

By executing the program, you will get the **PowerPoint document** as follows.

![WinUI UWP app output PowerPoint document](Workingwith_Core/Open-and-Save-output-image.png)

### Save Presentation file in WinUI UWP app

{% tabs %}
{% highlight c# tabtitle="C#" %}

async void Save(MemoryStream stream)
{
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pptx";
        savePicker.SuggestedFileName = "Sample";
        savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync("Sample", CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file.
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = stream.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved PowerPoint file.
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}

{% endhighlight %}
{% endtabs %}
