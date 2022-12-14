---
title: Create and edit PowerPoint files in ASP.NET Core |Syncfusion|
description: A .NET Core PowerPoint library to create, read and edit PowerPoint files in .NET Core applications. Supports text, shape, chart, table and combine PowerPoints.
platform: file-formats
control: PowerPoint
documentation: UG
---
# Create, read and edit a PowerPoint file in ASP.NET Core

You can create or edit a PowerPoint file with the Syncfusion [ASP.NET Core PowerPoint library](https://help.syncfusion.com/file-formats/presentation/create-read-edit-powerpoint-files-in-asp-net-core-c-sharp). The below are the steps.

## Create a PowerPoint file in ASP.NET Core

Step 1: Create a new C# ASP.NET Core web application project.

![Create ASP.NET Core Web project for PowerPoint file](Workingwith_Core/CreateCore.png)

Step 2: Select Web Application pattern (Model-View-Controller) for the project.

![Select Web Application pattern for PowerPoint file](Workingwith_Core/MVC.png)

Step 3: Install the [Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core/) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Presentation .Net Core Nuget](Workingwith_Core/install_nuget.png)

Step 4: After installing the **Syncfusion.Presentation.Net.Core** nuget package, the following assemblies were included in our project.
<ul>
<li>Syncfusion.Compression.Net.Core</li>
<li>Syncfusion.Licensing</li>
<li>Syncfusion.OfficeChart.Net.Core</li>
<li>Syncfusion.Presentation.Portable</li>
</ul>
		 
![Installed Assemblies in Presentation ASP.NET Core](Workingwith_Core/installed_assemblies.png)

Step 5: The below code snippets demonstrate how to create a PowerPoint Presentation in ASP.NET Core platform.

**Create Presentation instance:**

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new instance of PowerPoint Presentation file
IPresentation pptxDoc = Presentation.Create();

{% endhighlight %}

{% endtabs %}

**Add a new slide**

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Add a new slide to file and apply background color
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.TitleOnly);

{% endhighlight %}

{% endtabs %}

**Apply Background**

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Specify the fill type and fill color for the slide background 
slide.Background.Fill.FillType = FillType.Solid;
slide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(232, 241, 229);

{% endhighlight %}

{% endtabs %}

**Add title content:**

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Add title content to the slide by accessing the title placeholder of the TitleOnly layout-slide
IShape titleShape = slide.Shapes[0] as IShape;
titleShape.TextBody.AddParagraph("Company History").HorizontalAlignment = HorizontalAlignmentType.Center;

{% endhighlight %}

{% endtabs %}

**Add description content:**

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Add description content to the slide by adding a new TextBox
IShape descriptionShape = slide.AddTextBox(53.22, 141.73, 874.19, 77.70);
descriptionShape.TextBody.Text = "IMN Solutions PVT LTD is the software company, established in 1987, by George Milton. The company has been listed as the trusted partner for many high-profile organizations since 1988 and got awards for quality products from reputed organizations.";

{% endhighlight %}

{% endtabs %}

**Add bullet points:**

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Add bullet points to the slide
IShape bulletPointsShape = slide.AddTextBox(53.22, 270, 437.90, 116.32);

//Add a paragraph for a bullet point
IParagraph firstPara = bulletPointsShape.TextBody.AddParagraph("The company acquired the MCY corporation for 20 billion dollars and became the top revenue maker for the year 2015.");

//Format how the bullets should be displayed
firstPara.ListFormat.Type = ListType.Bulleted;
firstPara.LeftIndent = 35;
firstPara.FirstLineIndent = -35;

// Add another paragraph for the next bullet point
IParagraph secondPara = bulletPointsShape.TextBody.AddParagraph("The company is participating in top open source projects in automation industry.");

//Format how the bullets should be displayed
secondPara.ListFormat.Type = ListType.Bulleted;
secondPara.LeftIndent = 35;
secondPara.FirstLineIndent = -35;

{% endhighlight %}

{% endtabs %}

**Add an image:**

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Gets a picture as stream.
FileStream pictureStream = new FileStream("Image.jpg", FileMode.Open);

//Adds the picture to a slide by specifying its size and position.
slide.Shapes.AddPicture(pictureStream, 499.79, 238.59, 364.54, 192.16);

{% endhighlight %}

{% endtabs %}

You can download the image used in the sample from [here](http://www.syncfusion.com/downloads/support/directtrac/general/ze/Image-1995521764.zip).

**Add a shape:**

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Add an auto-shape to the slide
IShape stampShape = slide.Shapes.AddShape(AutoShapeType.Explosion1, 48.93, 430.71, 104.13, 80.54);

//Format the auto-shape color by setting the fill type and text
stampShape.Fill.FillType = FillType.None;
stampShape.TextBody.AddParagraph("IMN").HorizontalAlignment = HorizontalAlignmentType.Center;

{% endhighlight %}

{% endtabs %}

**Save and close the presentation:**

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Release all resources from stream
outputStream.Dispose();

//Close the PowerPoint presentation
pptxDoc.Close();

{% endhighlight %}

{% endtabs %}

The output of the above code example will generate the below PowerPoint slide.

![ASP.Net Core PowerPoint Library Output](Workingwith_Core/GettingStartedSample.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your applications to use our components.

## Read and edit a PowerPoint file in ASP.NET Core

You can edit an existing PowerPoint file using this library. The below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open(new FileStream("Sample.pptx",FileMode.Open));

//Gets the first slide from the PowerPoint presentation
ISlide slide = pptxDoc.Slides[0];

//Gets the first shape of the slide
IShape shape = slide.Shapes[0] as IShape;

//Change the text of the shape
if(shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

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

N> You can also explore our [.NET Core PowerPoint library demo](https://ej2.syncfusion.com/aspnetcore/Presentation/Default#/bootstrap5) that shows how to create and modify PowerPoint files from C# with just five lines of code.
