---
title: Convert PowerPoint to PDF in WPF | Syncfusion
description: Convert PowerPoint to PDF in WPF using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to PDF in WPF

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to PDF in WPF**.

## Steps to convert PowerPoint to PDF programmatically

Step 1: Create a new C# WPF application project.

![Create WPF project](Workingwith_WPF/Project-Open-and-Save.png)

Step 2: Install the [Syncfusion.PresentationToPdfConverter.Wpf](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.Wpf) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.PresentationToPdfConverter.Wpf Nuget Package](Workingwith_WPF/Nuget-Package-Open-and-Save.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Add a new button in the **MainWindow.xaml** as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

<Window x:Class="Create_PowerPoint_Presentation_to_PDF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:Create_PowerPoint_Presentation_to_PDF"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <Button Click="btnConvert_Click" VerticalAlignment="Center" Height="19" BorderBrush="LightBlue" HorizontalAlignment="Center" Width="120">
            <Button.Background>
                <LinearGradientBrush EndPoint="0.5,-0.04" StartPoint="0.5,1.04">
                    <GradientStop Color="#FFD9E9F7" Offset="0"/>
                    <GradientStop Color="#FFEFF8FF" Offset="1"/>
                </LinearGradientBrush>
            </Button.Background>
            <StackPanel Orientation="Horizontal" Height="20" VerticalAlignment="Center" HorizontalAlignment="Left" Width="140">
                <Image Name="image2" Margin="2" HorizontalAlignment="Center" VerticalAlignment="Center" />
                <TextBlock Text="Convert PPTX to PDF" Height="16" Width="126" />
            </StackPanel>
        </Button>
    </Grid>
</Window>


{% endhighlight %}
{% endtabs %}

Step 4: Include the following namespaces in the **MainWindow.xaml.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;
using Syncfusion.PresentationToPdfConverter;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}

Step 5: Add the following code in **btnConvert_Click** to **convert PowerPoint to PDF in WPF**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Opens a PowerPoint Presentation
using (IPresentation pptxDoc = Presentation.Open(Path.GetFullPath(@"../../Data/Input.pptx")))
{
    //Converts the PowerPoint Presentation into PDF document
    using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
    {
        //Saves the PDF document
        pdfDocument.Save(Path.GetFullPath(@"../../Sample.pdf"));
    }                   
} 

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from GitHub.

By executing the program, you will get the **PDF** as follows.

![Converted PDF from PowerPoint in WPF](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-PDF.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features.
