---
title: Convert PowerPoint to PDF in UWP | Syncfusion
description: Convert PowerPoint to PDF in UWP using UWP PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to PDF in UWP

Syncfusion PowerPoint is a [UWP PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/uwp/powerpoint-library) used to create, read, edit and **convert PowerPoint documents** programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to PDF in UWP**.

## Steps to convert PowerPoint to PDF programmatically

Step 1: Create a new C# UWP application project.

![Create UWP project](Workingwith_UWP/Project-Open-and-Save.png)

Step 2: Install the [Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.PresentationRenderer.Net.Core Nuget Package](Azure_Images/App_Service_Linux/Nuget_Package_PowerPoint_Presentation_to_PDF.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Add a new button in the MainPage.xaml as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

<Page
    x:Class="Convert_PowerPoint_Presentation_to_PDF.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Convert_PowerPoint_Presentation_to_PDF"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <Button x:Name="button" Content="Convert PPTX to PDF" Click="OnButtonClicked" HorizontalAlignment="Center" VerticalAlignment="Center"/>
    </Grid>
</Page>

{% endhighlight %}
{% endtabs %}

Step 4: Include the following namespaces in the **MainPage.xaml.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;

{% endhighlight %}
{% endtabs %}

Step 5: Include the below code snippet in the click event of the button in **MainPage.xaml.cs**, to convert the PowerPoint to PDF and save the PDF document as a physical file and open the file for viewing.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Open an existing PowerPoint presentation
using (IPresentation pptxDoc = Presentation.Open(assembly.GetManifestResourceStream("Convert_PowerPoint_Presentation_to_PDF.Assets.Input.pptx")))
{
    //Convert the PowerPoint document to PDF document.
    using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
    {
        // Create a MemoryStream to hold the PDF data.
        MemoryStream pdfStream = new MemoryStream();
        pdfDocument.Save(pdfStream);

        //Save the PDF file
        SavePDF(pdfStream);
    }
} 

{% endhighlight %}
{% endtabs %}

## Save PDF document in UWP

{% tabs %}
{% highlight c# tabtitle="C#" %}

StorageFile stFile;
if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
{
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Sample";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
    stFile = await savePicker.PickSaveFileAsync();
}
else
{
    StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
    stFile = await local.CreateFileAsync("Sample.pdf", CreationCollisionOption.ReplaceExisting);
}
if (stFile != null)
{
    Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
    Stream st = fileStream.AsStreamForWrite();
    st.SetLength(0);
    st.Write((outputStream as MemoryStream).ToArray(), 0, (int)outputStream.Length);
    st.Flush();
    st.Dispose();
    fileStream.Dispose();
    MessageDialog msgDialog = new MessageDialog("Do you want to view the Document?", "File created.");
    UICommand yesCmd = new UICommand("Yes");
    msgDialog.Commands.Add(yesCmd);
    UICommand noCmd = new UICommand("No");
    msgDialog.Commands.Add(noCmd);
    IUICommand cmd = await msgDialog.ShowAsync();
    if (cmd == yesCmd)
    {
        // Launch the retrieved file
        bool success = await Windows.System.Launcher.LaunchFileAsync(stFile);
    }
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-presentation-to-PDF/UWP).

By executing the program, you will get the **PDF** as follows.

![PowerPoint to PDF in UWP](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-PDF.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/uwp) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features.

An online sample link to [convert PowerPoint Presentation to PDF](https://ej2.syncfusion.com/aspnetcore/PowerPoint/PPTXToPDF#/material3) in ASP.NET Core.

