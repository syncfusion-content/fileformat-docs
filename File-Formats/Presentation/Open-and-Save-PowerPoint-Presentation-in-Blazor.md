---
title: Open and save Presentation in Blazor | Syncfusion
description: Open and save Presentation in Blazor using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Open and save Presentation in Blazor

Syncfusion PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **open and save a Presentation in Blazor**.

## Server app

Step 1: Create a new C# Blazor Server app project. Select Blazor App from the template and click the Next button.

![Create ASP.NET Core Web application in Visual Studio for Blazor PowerPoint document ](Workingwith_Blazor/Create_project.png)

Step 2: Now, the project configuration window will popup. Click Create button to create a new project with the required project name.

![Create a project name for your new project](Workingwith_Blazor/Configure_project.png)

Step 3: Choose **Blazor Server App** and click Create button to create a new Blazor Server app for .NET Core 3.0.0-preview9.

![Select .NET Core, ASP.NET Core 3.0 and Blazor server_side.](Workingwith_Blazor/Core_application_Server.png)

Step 4: Install the [Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core/) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.Presentation.Net.Core Nuget Package](Workingwith_Core/install_nuget.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Create a razor file with name as **Presentation** under **Pages** folder and include the following namespaces in the file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@page "/presentation"
@using System.IO;
@using Open_and_save_PowerPoint;
@inject Open_and_save_PowerPoint.Data.PowerPointService service
@inject Microsoft.JSInterop.IJSRuntime JS

{% endhighlight %}
{% endtabs %}

Step 6: Add the following code to create a new button.

{% tabs %}
{% highlight CSHTML %}

<h2>Syncfusion PowerPoint library (Essential Presentation)</h2>
<p>Syncfusion Blazor PowerPoint library (Essential Presentation) used to create, read, edit, and convert PowerPoint files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@OpenAndSavePresentation">Open and Save Presentation</button>

{% endhighlight %}
{% endtabs %}

Step 7: Add the following code in **Presentation.razor** file to create and download the **Presentation document**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@code {
    MemoryStream documentStream;
    /// <summary>
    /// Generate and download the PowerPoint Presentaion
    /// </summary>
    protected async void OpenAndSavePresentation()
    {
        documentStream = service.OpenAndSavePresentation();
        await JS.SaveAs("Result.pptx", documentStream.ToArray());
    }
}

{% endhighlight %}
{% endtabs %}

Step 8: Create a new cs file with name as **PowerPointService** under Data folder and include the following namespaces in the file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 9: Create a new MemoryStream method with name as **OpenAndSavePresentation** in **PowerPointService** class and include the following code snippet to **open an existing PowerPoint Presentation in Blazor Server app**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using (FileStream sourceStreamPath = new FileStream(@"wwwroot/Template.pptx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite));
//Open an existing PowerPoint Presentation.
using (IPresentation pptxDoc = Presentation.Open(sourceStreamPath));

{% endhighlight %}
{% endtabs %}

Step 10: Add below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Get the first slide from the PowerPoint Presentation.
ISlide slide = pptxDoc.Slides[0];
//Get the first shape of the slide.
IShape shape = slide.Shapes[0] as IShape;
//Change the text of the shape.
if (shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 11: Add below code example to **save the PowerPoint Presentation in Blazor Server app**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the PowerPoint Presentation as stream.
MemoryStream pptxStream = new();
pptxDoc.Save(pptxStream);
pptxStream.Position = 0;
//Download Powerpoint document in the browser.
return pptxStream;

{% endhighlight %}
{% endtabs %}
            
Step 12: Create a new class file in the project, with name as FileUtils and add the following code to invoke the JavaScript action to download the file in the browser.

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

Step 13: Add the following JavaScript function in the _Host.cshtml in the Pages folder.

{% tabs %}
{% highlight HTML %}

<script type="text/javascript">
    function saveAsFile(filename, bytesBase64) 
    {
        if (navigator.msSaveBlob) 
        {
            //Download document in Edge browser
            var data = window.atob(bytesBase64);
            var bytes = new Uint8Array(data.length);
            for (var i = 0; i < data.length; i++) {
                bytes[i] = data.charCodeAt(i);
            }
            var blob = new Blob([bytes.buffer], { type: "application/octet-stream" });
            navigator.msSaveBlob(blob, filename);
        }
        else 
        {
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Read-and-save-PowerPoint-presentation/Open-and-save-PowerPoint/Blazor/Server-side-application).

By executing the program, you will get the **PowerPoint document** as follows.

![Blazor Server output PowerPoint document](Workingwith_Core/Open-and-Save-output-image.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/blazor) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features.

## WASM app

Step 1: Create a new C# Blazor WASM app project. Select Blazor App from the template and click the Next button.

![Create ASP.NET Core Web application in Visual Studio for Blazor PowerPoint document](Workingwith_Blazor/Create_project.png)

Step 2: Now, the project configuration window will popup. Click Create button to create a new project with the required project name.

![Create a project name for your new project](Workingwith_Blazor/Configure_project.png)

Step 3: Choose Blazor WebAssembly App and click Create button to create a new Blazor WASM app for .NET Core 3.0.0-preview9.

![Select .NET Core, ASP.NET Core 3.0 and Blazor server_side.](Workingwith_Blazor/Core_application_Client.png)

Step 4: To **create a PowerPoint document in WASM app**, install [Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core) to the Blazor project.

![Install Syncfusion.Presentation.Net.Core Nuget Package](Workingwith_Blazor/NuGet.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Create a razor file with name as ``Presentation`` under ``Pages`` folder and add the following namespaces in the file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@page "/presentation"
@inject Microsoft.JSInterop.IJSRuntime JS
@inject HttpClient client
@using Syncfusion.Presentation
@using System.IO

{% endhighlight %}
{% endtabs %}

Step 6: Add the following code to create a new button.

{% tabs %}
{% highlight CSHTML %}

<h2>Syncfusion PowerPoint library (Essential Presentation)</h2>
<p>Syncfusion Blazor PowerPoint library (Essential Presentation) used to create, read, edit, and convert PowerPoint files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@OpenAndSavePresentation">Open and Save Presentation</button>

{% endhighlight %}
{% endtabs %}

Step 7: Create a new async method with name as ``OpenAndSavePresentation`` and include the following code snippet to **open an existing PowerPoint Presentation in Blazor WASM app**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using (Stream inputStream = await client.GetStreamAsync("Data/Template.pptx"));
//Open an existing PowerPoint Presentation.
using (IPresentation pptxDoc = Syncfusion.Presentation.Presentation.Open(inputStream));

{% endhighlight %}
{% endtabs %}
      
Step 8: Add below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Get the first slide from the PowerPoint Presentation.
ISlide slide = pptxDoc.Slides[0];
//Get the first shape of the slide.
IShape shape = slide.Shapes[0] as IShape;
//Change the text of the shape.
if (shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 9: Add below code example to **save the PowerPoint Presentation in Blazor WASM app**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the PowerPoint Presentation as stream.
MemoryStream pptxStream = new();
pptxDoc.Save(pptxStream);
pptxStream.Position = 0;
//Download Powerpoint document in the browser.
await JS.SaveAs("Sample.pptx", pptxStream.ToArray());

{% endhighlight %}
{% endtabs %}

Step 10: To download the PowerPoint document in browser, create a class file with FileUtils name and add the following code to invoke the JavaScript action to download the file in the browser.

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

Step 11: Add the following JavaScript function in the Index.html file present under ``wwwroot``.

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Read-and-save-PowerPoint-presentation/Open-and-save-PowerPoint/Blazor/Client-side-application).

By executing the program, you will get the **PowerPoint document** as follows.

![Blazor WASM output PowerPoint document](Workingwith_Core/Open-and-Save-output-image.png)

N> Even though PowerPoint library works in WASM app, it is recommended to use server deployment. Since the WASM app deployment increases the application payload size. You can also explore our [Blazor PowerPoint library demo](https://blazor.syncfusion.com/demos/powerpoint/getting-started) that shows how to create and modify PowerPoint files from C# with just five lines of code.

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/blazor) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features.