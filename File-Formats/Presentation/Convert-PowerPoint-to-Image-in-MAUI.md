---
title: Convert PowerPoint to Image in .NET MAUI | Syncfusion
description: Convert PowerPoint to image in .NET MAUI using .NET MAUI PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to Image in .NET MAUI

Syncfusion PowerPoint is a [.NET MAUI PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/maui/powerpoint-library) used to create, read, edit and convert PowerPoint presentation programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to image in .NET MAUI**.

## Prerequisites
To create .NET Multi-platform App UI (.NET MAUI) apps, you need the latest versions of Visual Studio 2022 and .NET 6. For more details, refer [here](https://learn.microsoft.com/en-us/dotnet/maui/get-started/installation?view=net-maui-8.0&tabs=vswin).

## Steps to convert PowerPoint to Image programmatically

Step 1: Create a new C# .NET MAUI app. Select **.NET MAUI App (Preview)** from the template and click the **Next** button.

![Create the MAUI app in Visual Studio](Workingwith_MAUI/Create_Project.png)

Step 2: Enter the project name and click **Create**.

![Create a project name for your new project](Workingwith_MAUI/Configuration_PPTXtoPDF.png)

Step 3: Install the [Syncfusion.PresentationRenderer.NET](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.NET) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.PresentationRenderer.NET NuGet package](Workingwith_MAUI/Nuget_Package_PPTXtoPDF.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Add a new button to the **MainPage.xaml** as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Convert_PowerPoint_Presentation_to_Image.MainPage">

    <ScrollView>
        <Grid RowSpacing="25" RowDefinitions="Auto,Auto,Auto,Auto,*"
            Padding="{OnPlatform iOS='30,60,30,30', Default='30'}">
            <Button 
                Text="Convert PPTX to Image"
                FontAttributes="Bold"
                Grid.Row="0"
                SemanticProperties.Hint="Convert PPTX to Image"
                Clicked="ConvertPPTXtoImage"
                HorizontalOptions="Center" />
        </Grid>
    </ScrollView>
</ContentPage>

{% endhighlight %}
{% endtabs %}

Step 5: Include the following namespaces in the **MainPage.xaml.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;

{% endhighlight %}
{% endtabs %}

Step 6: Add a new action method **ConvertPPTXtoImage** in MainPage.xaml.cs and include the below code snippet to **convert a PowerPoint to Image in .NET MAUI**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Loading an existing PowerPoint presentation.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Open the existing PowerPoint presentation with loaded stream.
using (IPresentation pptxDoc = Presentation.Open(assembly.GetManifestResourceStream("Convert_PowerPoint_Presentation_to_Image.Assets.Input.pptx")))
{
    //Initialize the PresentationRenderer.
    pptxDoc.PresentationRenderer = new PresentationRenderer();
    //Converts the first slide into image.
    Stream stream= pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg);
    //Reset the stream position.
    stream.Position = 0;
    //save and Launch the image file.
    SaveService saveService = new();
    saveService.SaveAndView("PPTXtoImage.Jpeg", "application/jpeg", stream as MemoryStream);
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI).

By executing the program, you will get the **image** as follows.

![PowerPoint to Image on macOS](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-Image.png)

## Helper files for .NET MAUI

Refer the below helper files and add them into the mentioned project. These helper files allow you to save the stream as a physical file and open the file for viewing.

<table>
  <tr>
  <td>
    <b>Folder Name</b>
  </td>
  <td>
    <b>File Name</b>
  </td>
  <td>
    <b>Summary</b>
  </td>
  </tr>
  <tr>
  <td>
    {{'[.NET MAUI Project](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image)'| markdownify }}
  </td>
  <td>
    {{'[SaveService.cs](https://github.com/SyncfusionExamples/PowerPoint-Examples/blob/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/SaveServices/SaveService.cs)'| markdownify }}
  </td>
  <td>Represent the base class for save operation.
  </td>
  </tr>
  <tr>
  <td>
    {{'[Windows](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/Windows)'| markdownify }}
  </td>
  <td>
    {{'[SaveWindows.cs](https://github.com/SyncfusionExamples/PowerPoint-Examples/blob/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/Windows/SaveWindows.cs)'| markdownify }}
  </td>
  <td>Save implementation for Windows.
  </td>
  </tr>
  <tr>
  <td>
    {{'[Android](https://github.com/SyncfusionExamples/PowerPoint-Examples/blob/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/Windows/SaveWindows.cs)'| markdownify }}
  </td>
  <td>
    {{'[SaveAndroid.cs](https://github.com/SyncfusionExamples/PowerPoint-Examples/blob/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/Android/SaveAndroid.cs)'| markdownify }}
  </td>
  <td>Save implementation for Android device.
  </td>
  </tr>
  <tr>
  <td>
    {{'[Mac Catalyst](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/MacCatalyst)'| markdownify }}
  </td>
  <td>
    {{'[SaveMac.cs](https://github.com/SyncfusionExamples/PowerPoint-Examples/blob/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/MacCatalyst/SaveMac.cs)'| markdownify }}
  </td>
  <td>Save implementation for Mac Catalyst device.
  </td>
  </tr>
  <tr>
  <td rowspan="2">
    {{'[iOS](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/iOS)'| markdownify }}
  </td>
  <td>
    {{'[SaveIOS.cs](https://github.com/SyncfusionExamples/PowerPoint-Examples/blob/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/iOS/SaveIOS.cs)'| markdownify }}
  </td>
  <td>
    Save implementation for iOS device
  </td>
  </tr>
  <tr>
  <td>
    {{'[PreviewControllerDS.cs](https://github.com/SyncfusionExamples/PowerPoint-Examples/blob/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/iOS/PreviewControllerDS.cs)'| markdownify }}<br/>{{'[QLPreviewItemFileSystem.cs](https://github.com/SyncfusionExamples/PowerPoint-Examples/blob/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/.NET-MAUI/Convert-PowerPoint-Presentation-to-Image/Platforms/iOS/QLPreviewItemFileSystem.cs)'| markdownify }}
  </td>
  <td>
    Helper classes for viewing the <b>PowerPoint Presenatation</b> in iOS device
  </td>
  </tr>
</table>

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/maui/powerpoint-library) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features. 

An online sample link to [convert PowerPoint Presentation to image](https://ej2.syncfusion.com/aspnetcore/PowerPoint/PPTXToImage#/material3) in ASP.NET Core. 