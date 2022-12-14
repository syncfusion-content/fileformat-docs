---
title: Create PowerPoint document in Blazor | PowerPoint | Syncfusion 
description: A .NET Core PowerPoint library to create, read and edit PowerPoint files in Blazor applications. Supports text, shape, chart, table and combine PowerPoints.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Create PowerPoint document in Blazor

Syncfusion Essential PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/powerpoint-framework/net-core) used to create, read, and edit **PowerPoint** documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **create a PowerPoint document in Blazor**.

**Prerequisites**

* Visual Studio 2019 Preview
* Install [.NET Core SDK 3.1](https://dotnet.microsoft.com/en-us/download/dotnet/3.1)

**Creating a Blazor project**

* Enable Visual Studio to use preview SDKs
* Open Tools > Options in the menu bar.
* Open the Projects and Solutions node. Open the .NET Core tab.
* Check the box for Use previews of the .NET Core SDK and click OK.
* Restart the Visual Studio 2019.

## Server-side application

Step 1: Create a new C# Blazor Server-Side application project. Select Blazor App from the template and click the Next button.

![Create ASP.NET Core Web application in Visual Studio for Blazor PowerPoint document ](Workingwith_Blazor/Create_project.png)

Step 2: Now, the project configuration window will popup. Click Create button to create a new project with the required project name.

![Create a project name for your new project](Workingwith_Blazor/Configure_project.png)

Step 3: Choose **Blazor Server App** and click Create button to create a new Blazor Server-Side application for .NET Core 3.0.0-preview9.

![Select .NET Core, ASP.NET Core 3.0 and Blazor server_side.](Workingwith_Blazor/Core_application_Server.png)

Step 4: To **create a PowerPoint document in Server-side application**, install [Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core) to the Blazor project.

![Install .NET Core Nuget Package](Workingwith_Blazor/NuGet.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.

Step 5: Create a razor file with name as **Presentation** under **Pages** folder and include the following namespaces in the file.
{% capture codesnippet1 %}​
{% tabs %}
{% highlight c# tabtitle="C#" %}
@page "/Presentation"
@using System.IO;
@using ServerSideApplication;
@inject ServerSideApplication.Data.PresentationService service
@inject Microsoft.JSInterop.IJSRuntime JS
{% endhighlight %}
{% endtabs %}
{% endcapture %}
{{ codesnippet1 | OrderList_Indent_Level_1 }}

Step 6: Add the following code to create a new button.
{% capture codesnippet2 %}​
{% tabs %}

{% highlight CSHTML %}

<h2>Syncfusion Presentation library (Essential Presentation)</h2>
<p>Syncfusion Blazor Presentation library (Essential Presentation) used to create, read, edit, and convert Presentation files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@CreatePowerPoint">Create PowerPoint</button>

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet2 | OrderList_Indent_Level_1 }}

Step 7: Add the following code in **Presentation.razor** file to create and download the **Presentation document**.
{% capture codesnippet3 %}​
{% tabs %}

{% highlight c# tabtitle="C#" %}

@code {
    MemoryStream documentStream;

    /// <summary>
    /// Create and download the Presentation document
    /// </summary>
    protected async void CreatePowerPoint()
    {
        documentStream = service.CreatePowerPoint();
        await JS.SaveAs("Sample.pptx", documentStream.ToArray());
    }
}

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet3 | OrderList_Indent_Level_1 }}

Step 8: Create a new cs file with name as **PresentationService** under Data folder and include the following namespaces in the file.
{% capture codesnippet4 %}​
{% tabs %}

{% highlight c# tabtitle="C#" %}

@using Syncfusion.Presentation;
@using Syncfusion.OfficeChart;
@using System.IO;

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet4 | OrderList_Indent_Level_1 }}

Step 9: Create a new MemoryStream method with name as **CreatePowerPoint** and include the following code snippet to **create a PowerPoint document in Blazor** Server-Side application.
{% capture codesnippet5 %}​
{% tabs %}

{% highlight c# tabtitle="C#" %}

public MemoryStream CreatePowerPoint()
{
    //Create a new instance of PowerPoint Presentation file           
    IPresentation pptxDoc = Presentation.Create();
		
    //Add a new slide to file and apply background color 
    ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.TitleOnly);
		
    //Specify the fill type and fill color for the slide background         
    slide.Background.Fill.FillType = FillType.Solid;    
    slide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(232, 241, 229);
		
    //Add title content to the slide by accessing the title placeholder of the  TitleOnly layout-slide 
    IShape titleShape = slide.Shapes[0] as IShape;     
    titleShape.TextBody.AddParagraph("Company History").HorizontalAlignment =  HorizontalAlignmentType.Center;
		
    //Add description content to the slide by adding a new TextBox IShape  
    IShape descriptionShape = slide.AddTextBox(53.22, 141.73, 874.19, 77.70);      
    descriptionShape.TextBody.Text = "IMN Solutions PVT LTD is the software company, established in 1987, by George Milton. The company has been listed as the trusted  partner for many high-profile organizations since 1988 and got awards for quality products from reputed organizations.";
								
    //Add bullet points to the slide 
    IShape bulletPointsShape = slide.AddTextBox(53.22, 270, 437.90, 116.32); 
		
    //Add a paragraph for a bullet point 
    IParagraph firstPara = bulletPointsShape.TextBody.AddParagraph("The company acquired the MCY corporation for 20 billion dollars and became the top revenue maker for the year 2015."); 
		
    //Format how the bullets should be displayed 
    firstPara.ListFormat.Type = ListType.Bulleted;
    firstPara.LeftIndent = 35;   
    firstPara.FirstLineIndent = -35; 
		
    //Add another paragraph for the next bullet point 
    IParagraph secondPara = bulletPointsShape.TextBody.AddParagraph("The company is participating in top open source projects in automation industry."); 
		
    //Format how the bullets should be displayed 
    secondPara.ListFormat.Type = ListType.Bulleted; 
    secondPara.LeftIndent = 35;  
    secondPara.FirstLineIndent = -35;
		
    //Add an auto-shape to the slide 
    IShape stampShape = slide.Shapes.AddShape(AutoShapeType.Explosion1, 48.93, 430.71, 104.13, 80.54); 
		
    //Format the auto-shape color by setting the fill type and text   
    stampShape.Fill.FillType = FillType.None;  
    stampShape.TextBody.AddParagraph("IMN").HorizontalAlignment =  HorizontalAlignmentType.Center;
		
    //Save the PowerPoint Presentation as stream
    MemoryStream stream = new MemoryStream();
    pptxDoc.Save(stream);
		
    //Close the PowerPoint Presentation as stream
    pptxDoc.Close();
    stream.Position = 0;
		
    //Download the PowerPoint document in the browser
    JS.SaveAs("Sample.pptx", stream.ToArray());
}
{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet5 | OrderList_Indent_Level_1 }}

Step 10: Create a new class file in the project, with name as FileUtils and add the following code to invoke the JavaScript action to download the file in the browser.
{% capture codesnippet6 %}​
{% tabs %}

{% highlight c# tabtitle="C#" %}

public static class FileUtils
{
    public static ValueTask<object> SaveAs(this IJSRuntime js, string filename, byte[] data)
       => js.InvokeAsync<object>(
           "saveAsFile",
           filename,
           Convert.ToBase64String(data));
}

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet6 | OrderList_Indent_Level_1 }}

Step 11: Add the following JavaScript function in the _Host.cshtml in the Pages folder.
{% capture codesnippet7 %}​
{% tabs %}

{% highlight HTML %}

<script type="text/javascript">
    function saveAsFile(filename, bytesBase64) {
        if (navigator.msSaveBlob) {
            //Download document in Edge browser
            var data = window.atob(bytesBase64);
            var bytes = new Uint8Array(data.length);
            for (var i = 0; i < data.length; i++) {
                bytes[i] = data.charCodeAt(i);
            }
            var blob = new Blob([bytes.buffer], { type: "application/octet-stream" });
            navigator.msSaveBlob(blob, filename);
        }
        else {
            var link = document.createElement('a');
            link.download = filename;
            link.href = "data:application/octet-stream;base64," + bytesBase64;
            document.body.appendChild(link); // Needed for Firefox
            link.click();
            document.body.removeChild(link);
        }
    }
</script>

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet7 | OrderList_Indent_Level_1 }}

By executing the program, you will get the **PowerPoint document** as follows.

![Blazor Server-side output PowerPoint document](Workingwith_Blazor/Output.png)

## Client-side application

Step 1: Create a new C# Blazor Client-Side application project. Select Blazor App from the template and click the Next button.

![Create ASP.NET Core Web application in Visual Studio for Blazor PowerPoint document](Workingwith_Blazor/Create_project.png)

Step 2: Now, the project configuration window will popup. Click Create button to create a new project with the required project name.

![Create a project name for your new project](Workingwith_Blazor/Configure_project.png)

Step 3: Choose Blazor WebAssembly App and click Create button to create a new Blazor Client-Side application for .NET Core 3.0.0-preview9.

![Select .NET Core, ASP.NET Core 3.0 and Blazor server_side.](Workingwith_Blazor/Core_application_Client.png)

Step 4: To **create a PowerPoint document in Server-side application**, install [Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core) to the Blazor project.

![Install .NET Core Nuget Package](Workingwith_Blazor/NuGet.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.

Step 5: Create a razor file with name as ``Presentation`` under ``Pages`` folder and add the following namespaces in the file.
{% capture codesnippet8 %}​
{% tabs %}
{% highlight c# tabtitle="C#" %}
@page "/Presentation"
@using Syncfusion.Presentation
@using Syncfusion.OfficeChart
@using System.IO
@inject Microsoft.JSInterop.IJSRuntime JS
{% endhighlight %}
{% endtabs %}
{% endcapture %}
{{ codesnippet8 | OrderList_Indent_Level_1 }}

Step 6: Add the following code to create a new button.
{% capture codesnippet9 %}​
{% tabs %}

{% highlight CSHTML %}

<h2>Syncfusion Presentation library (Essential Presentation)</h2>
<p>Syncfusion Blazor Presentation library (Essential Presentation) used to create, read, edit, and convert Presentation files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@CreatePowerPoint">Create PowerPoint</button>

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet9 | OrderList_Indent_Level_1 }}

Step 7: Create a new async method with name as ``CreatePowerPoint`` and include the following code snippet to **create a PowerPoint document in Blazor** Client-Side application.
{% capture codesnippet10 %}​
{% tabs %}

{% highlight c# tabtitle="C#" %}

@functions {

	async void CreatePowerPoint()
	{
		//Create a new instance of PowerPoint Presentation file           
		IPresentation pptxDoc = Presentation.Create();
		
		//Add a new slide to file and apply background color 
		ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.TitleOnly);
		
		//Specify the fill type and fill color for the slide background         
		slide.Background.Fill.FillType = FillType.Solid;    
		slide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(232, 241, 229);
		
		//Add title content to the slide by accessing the title placeholder of the  TitleOnly layout-slide 
		IShape titleShape = slide.Shapes[0] as IShape;     
		titleShape.TextBody.AddParagraph("Company History").HorizontalAlignment =  HorizontalAlignmentType.Center;
		
		//Add description content to the slide by adding a new TextBox IShape  
		IShape descriptionShape = slide.AddTextBox(53.22, 141.73, 874.19, 77.70);      
		descriptionShape.TextBody.Text = "IMN Solutions PVT LTD is the software company, established in 1987, by George Milton. The company has been listed as the trusted  partner for many high-profile organizations since 1988 and got awards for quality products from reputed organizations.";
								
		//Add bullet points to the slide 
		IShape bulletPointsShape = slide.AddTextBox(53.22, 270, 437.90, 116.32); 
		
		//Add a paragraph for a bullet point 
		IParagraph firstPara = bulletPointsShape.TextBody.AddParagraph("The company acquired the MCY corporation for 20 billion dollars and became the top revenue maker for the year 2015."); 
		
		//Format how the bullets should be displayed 
		firstPara.ListFormat.Type = ListType.Bulleted;
		firstPara.LeftIndent = 35;   
		firstPara.FirstLineIndent = -35; 
		
		//Add another paragraph for the next bullet point 
		IParagraph secondPara = bulletPointsShape.TextBody.AddParagraph("The company is participating in top open source projects in automation industry."); 
		
		//Format how the bullets should be displayed 
		secondPara.ListFormat.Type = ListType.Bulleted; 
		secondPara.LeftIndent = 35;  
		secondPara.FirstLineIndent = -35;
		
		//Add an auto-shape to the slide 
		IShape stampShape = slide.Shapes.AddShape(AutoShapeType.Explosion1, 48.93, 430.71, 104.13, 80.54); 
		
		//Format the auto-shape color by setting the fill type and text   
		stampShape.Fill.FillType = FillType.None;  
		stampShape.TextBody.AddParagraph("IMN").HorizontalAlignment =  HorizontalAlignmentType.Center;
		
		//Save the PowerPoint Presentation as stream
		MemoryStream stream = new MemoryStream();
		pptxDoc.Save(stream);
		
		//Close the PowerPoint Presentation as stream
		pptxDoc.Close();
		stream.Position = 0;
		
		//Download the PowerPoint document in the browser
		JS.SaveAs("Sample.pptx", stream.ToArray());
	}
}

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet10 | OrderList_Indent_Level_1 }}

Step 8: To download the PowerPoint document in browser, create a class file with FileUtils name and add the following code to invoke the JavaScript action to download the file in the browser.
{% capture codesnippet11 %}​
{% tabs %}

{% highlight c# tabtitle="C#" %}

public static class FileUtils
{
    public static ValueTask<object> SaveAs(this IJSRuntime js, string filename, byte[] data)
       => js.InvokeAsync<object>(
           "saveAsFile",
           filename,
           Convert.ToBase64String(data));
}

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet11 | OrderList_Indent_Level_1 }}

Step 9: Add the following JavaScript function in the _Host.cshtml in the Pages folder.
{% capture codesnippet12 %}​
{% tabs %}

{% highlight HTML %}

<script type="text/javascript">
    function saveAsFile(filename, bytesBase64) {
        if (navigator.msSaveBlob) {
            //Download document in Edge browser
            var data = window.atob(bytesBase64);
            var bytes = new Uint8Array(data.length);
            for (var i = 0; i < data.length; i++) {
                bytes[i] = data.charCodeAt(i);
            }
            var blob = new Blob([bytes.buffer], { type: "application/octet-stream" });
            navigator.msSaveBlob(blob, filename);
        }
        else {
            var link = document.createElement('a');
            link.download = filename;
            link.href = "data:application/octet-stream;base64," + bytesBase64;
            document.body.appendChild(link); // Needed for Firefox
            link.click();
            document.body.removeChild(link);
        }
    }
</script>

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet12 | OrderList_Indent_Level_1 }}

By executing the program, you will get the **PowerPoint document** as follows.

![Blazor Client-Side output PowerPoint document](Workingwith_Blazor/Output.png)

N> Even though PowerPoint library works in client-side, it is recommended to use server-side deployment. Since the client-side deployment increases the application payload size. You can also explore our [Blazor PowerPoint library demo](https://blazor.syncfusion.com/demos/presentation/getting-started) that shows how to create and modify PowerPoint files from C# with just five lines of code.

Kindly explore the [supported and unsupported features of PowerPoint library in Blazor](https://help.syncfusion.com/file-formats/presentation/supported-and-unsupported-features).