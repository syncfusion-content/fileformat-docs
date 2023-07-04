---
title: Open and save Presentation in WPF | Syncfusion
description: Open and save Presentation in WPF using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Open and save Presentation in WPF

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **open and save a Presentation in WPF**.

## Steps to open and save PowerPoint Presentation programmatically

Step 1: Create a new C# WPF application project.

![Create WPF project](Workingwith_WPF/Project-Open-and-Save.png)

Step 2: Install the [Syncfusion.Presentation.Wpf](https://www.nuget.org/packages/Syncfusion.Presentation.Wpf/) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.Presentation.Wpf Nuget Package](Workingwith_WPF/Nuget-Package-Open-and-Save.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Add a new button in the **MainWindow.xaml** as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

<Window x:Class="Read_and_edit_PowerPoint_presentation.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:Read_and_edit_PowerPoint_presentation"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <Button x:Name="button" Content="Open and Save Presentation" Click="OpenAndSavePresentation" HorizontalAlignment="Center" VerticalAlignment="Center"/>
    </Grid>
</Window>

{% endhighlight %}
{% endtabs %}

Step 4: Include the following namespaces in the **MainWindow.xaml.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 5: Add the following code in **OpenAndSavePresentation** to **open an existing PowerPoint Presentation in WPF**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Opens an existing PowerPoint presentation.
IPresentation pptxDoc = Presentation.Open("Data/Template.pptx");

{% endhighlight %}
{% endtabs %}

Step 6: Add below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Gets the first slide from the PowerPoint presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the first shape of the slide
IShape shape = slide.Shapes[0] as IShape;
//Change the text of the shape
if (shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 7: Add below code example to **save the PowerPoint Presentation in WPF**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Saves the Presentation to the file system.
pptxDoc.Save("Result.pptx");
//Close the PowerPoint presentation
pptxDoc.Close();

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Read-and-save-PowerPoint-presentation/Open-and-save-PowerPoint/WPF).

By executing the program, you will get the **PowerPoint document** as follows.

![WPF output PowerPoint document](Workingwith_Core/Open-and-Save-output-image.png)
