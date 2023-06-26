---
title: Open and save Presentation on macOS | Syncfusion
description: Open and save Presentation in .NET Core application on macOS using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Open and save Presentation on macOS

Syncfusion PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **open and save a Presentation in .NET Core application on macOS**.

## Steps to open and save PowerPoint Presentation programmatically

Step 1: Create a new C# .NET Core console application.

![Create .NET Core console project](Workingwith_Mac/CreateProject.png)

Step 2: Select the project version.

![Select project version](Workingwith_Mac/selectprojectverion.png)

Step 3: Install the [Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core/) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Presentation .Net Core Nuget](Workingwith_Mac/Install_Nuget1.png)
![Install Presentation .Net Core Nuget](Workingwith_Mac/Install_Nuget.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your applications to use our components.

Step 4: Include the following Namespaces in the **Program.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 5: Add the following code snippet in **Program.cs** file to **open an existing Presentation in .NET Core application on  macOS**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open(new FileStream("Sample.pptx",FileMode.Open));

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
if(shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 7: Add below code example to **save the PowerPoint Presentation in .NET Core application on  macOS**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the PowerPoint presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
outputStream.Position = 0;
outputStream.Flush();
outputStream.Dispose();
//Close the PowerPoint presentation
pptxDoc.Close();

{% endhighlight %}
{% endtabs %}

By executing the program, you will get the **PowerPoint document** as follows.

![.NET Core macOS output PowerPoint document](Workingwith_Core/Open-and-Save-output-image.png)