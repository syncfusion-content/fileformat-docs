---
title: Open and save Presentation in ASP.NET Core | Syncfusion
description: Open and save Presentation in ASP.NET Core using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Open and save PowerPoint Presentation in ASP.NET Core

Syncfusion PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **open and save a Presentation in ASP.NET Core**.

## Steps to open and save PowerPoint Presentation programmatically

Step 1: Create a new C# ASP.NET Core web application project.

![Create ASP.NET Core Web project for PowerPoint file](Workingwith_Core/Create-Project-Open-and-Save.png)

Step 2: Install the [Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core/) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.Presentation.Net.Core Nuget Package](Workingwith_Core/Nuget-Package_Open_and_Save.png)

Step 3: Include the following namespaces in **HomeController.cs**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 4: A default action method named Index will be present in **HomeController.cs**. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 5: Add a new button in the **Index.cshtml** as shown below.

{% tabs %}
{% highlight HTML %}

@{
    Html.BeginForm("CreatePowerPoint", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Create PowerPoint" style="width:150px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}
{% endtabs %}

Step 6: Add a new action method **CreatePowerPoint** in HomeController.cs and include the below code snippet to **open an existing Presentation in ASP.NET Core**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

FileStream fileStreamPath = new(Path.GetFullPath(@"Data/Template.pptx"), FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Open an existing PowerPoint presentation.
IPresentation pptxDoc = Presentation.Open(fileStreamPath);

{% endhighlight %}
{% endtabs %}

Step 7: Add below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Get the first slide from the PowerPoint presentation.
ISlide slide = pptxDoc.Slides[0];
//Get the first shape of the slide.
IShape shape = slide.Shapes[0] as IShape;
//Change the text of the shape.
if (shape.TextBody.Text == "Company History")
shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 8: Add below code example to **save the PowerPoint Presentation in ASP.NET Core**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the PowerPoint Presentation as stream.
MemoryStream pptxStream = new();
pptxDoc.Save(pptxStream);
pptxStream.Position = 0;
//Download Powerpoint document in the browser.
return File(pptxStream, "application/powerpoint", "Result.pptx");

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Getting-started/ASP.NET-Core/Read-and-edit-PowerPoint-presentation)

By executing the program, you will get the **PowerPoint document** as follows.

![ASP.Net Core output PowerPoint document](Workingwith_Core/Open-and-Save-output-image.png)