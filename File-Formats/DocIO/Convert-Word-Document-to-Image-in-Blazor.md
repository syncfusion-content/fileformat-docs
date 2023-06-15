---
title: Convert Word to Image in Blazor | DocIO | Syncfusion 
description: Convert Word to image without Microsoft Word or interop dependencies in Blazor application using Blazor Word (DocIO) library.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word document to Image in Blazor

Syncfusion DocIO is a [Blazor Word library](https://www.syncfusion.com/document-processing/word-framework/blazor/word-library) used to create, read, edit, and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **convert a Word document to image in Blazor**.

## Word to Image in Blazor Server app

Step 1: Create a new C# Blazor Server app project. Select Blazor Server App from the template and click the Next button.

![Create Blazor Server app](Blazor_Images/Create-server-project-WordToPDF.png)

Step 2: Now, the project configuration window will popup. Click Create button to create a new project with the required project name.

![Create a project name for your new project](Blazor_Images/Configuration-WordtoImage.png)

Step 3: To **convert a Word document to image in server app**, install [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core) to the Blazor project.

![Install Syncfusion.DocIORenderer.Net.Core NuGet Package](Blazor_Images/Nuget-Package-WordtoImage.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Create a razor file with name as **DocIO** under **Pages** folder and include the following namespaces in the file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@page "/docio"
@using Convert_Word_Document_to_Image;
@inject Convert_Word_Document_to_Image.Data.WordService service;
@inject Microsoft.JSInterop.IJSRuntime JS;

{% endhighlight %}
{% endtabs %}

Step 5: Add the following code in **DocIO.razor** file to create a new button.

{% tabs %}
{% highlight CSHTML %}

<h2>Syncfusion DocIO library </h2>
<p>Syncfusion DocIO library is a Blazor DocIO library used to create, read, edit, and convert Word files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@ConvertWordtoImage">Convert Word to Image</button>

{% endhighlight %}
{% endtabs %}

Step 6: Add the following code in **DocIO.razor** file to create and download the **image**.

{% tabs %}
{% highlight c# tabtitle="C#" %}
@code {
    MemoryStream documentStream;
    /// <summary>
    /// Convert Word to image and download the image file
    /// </summary>
    protected async void ConvertWordtoImage()
    {
        documentStream = service.ConvertWordtoImage();
        await JS.SaveAs("WordToImage.Jpeg", documentStream.ToArray());
    }
}
{% endhighlight %}
{% endtabs %}

Step 7: Create a new cs file with name as **WordService** under Data folder and include the following namespaces in the file.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;

{% endhighlight %}

{% endtabs %}

Step 8: Create a new MemoryStream method with name as **ConvertWordtoImage** in **WordService** class and include the following code snippet to **convert the Word document to image** in Server app.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Open the file as Stream
using (FileStream sourceStreamPath = new FileStream(@"wwwroot/Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite))
{
    //Open an existing Word document.
    using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Docx))
    {
        //Instantiation of DocIORenderer for Word to image conversion
        using (DocIORenderer render = new DocIORenderer())
        {
            Stream imageStream = document.RenderAsImages(0, ExportImageFormat.Jpeg);
            //Reset the stream position.
            imageStream.Position = 0;
            return (MemoryStream)imageStream;
        }
    }
}

{% endhighlight %}

{% endtabs %}

Step 9: Create a new class file in the project, with name as FileUtils and add the following code to invoke the JavaScript action to download the file in the browser.

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

Step 10: Add the following JavaScript function in the _Host.cshtml in the Pages folder.

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

Step 11: Add the following code snippet in the razor file of Navigation menu in the Shared folder.

{% tabs %}

{% highlight HTML %}

<div class="nav-item px-3">
    <NavLink class="nav-link" href="docio">
        <span class="oi oi-list-rich" aria-hidden="true"></span> Convert Word to Image
    </NavLink>
</div>

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Convert-Word-to-image/Blazor/Server-app).

By executing the program, you will get the **image** as follows.

![Word to Image in Blazor Server app](WordToPDF_images/Output-WordtoImage.png)

## Word to Image in Blazor WASM app

Step 1: Create a new C# Blazor WASM app project. Select Blazor App from the template and click the **Next** button.

![Create Blazor WebAssembly app ](Blazor_Images/Blazor_WASM.png)

Step 2: Now, the project configuration window will popup. Click **Create** button to create a new project with the required project name.

![Create a project name for your new project](Blazor_Images/Web_Assembly_WordtoImage.png)

Step 3: Install the following **Nuget packages** in your application from [Nuget.org](https://www.nuget.org/).
* [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core)
* [SkiaSharp.NativeAssets.WebAssembly](https://www.nuget.org/packages/SkiaSharp.NativeAssets.WebAssembly)

![Install Syncfusion.DocIORenderer.Net.Core NuGet Package](Blazor_Images/Nuget-Package-WordtoImage.png)
![Install SkiaSharp.NativeAssets.WebAssembly NuGet Package](Blazor_Images/SkiaSharp-Nuget-WordtoPDF.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Add the following ItemGroup tag in the **Blazor WASM csproj** file.
{% tabs %}

{% highlight XAML  %}
<ItemGroup>
    <NativeFileReference Include="$(SkiaSharpStaticLibraryPath)\2.0.23\*.a" />
</ItemGroup>
{% endhighlight %}

{% endtabs %}

N> Install this wasm-tools and wasm-tools-net6 by using the "dotnet workload install wasm-tools" and "dotnet workload install wasm-tools-net6" commands in your command prompt respectively if you are facing issues related to Skiasharp during runtime.

Step 5: Enable the following property in the Blazor WASM csproj file.

{% tabs %}
{% highlight XAML %}
<PropertyGroup>
    <WasmNativeStrip>true</WasmNativeStrip>
</PropertyGroup>
{% endhighlight %}
{% endtabs %}

Step 6: Create a razor file with name as ``DocIO`` under ``Pages`` folder and add the following namespaces in the file.

{% tabs %}

{% highlight c# tabtitle="C#" %}
@page "/docio"
@using Syncfusion.DocIO
@using Syncfusion.DocIORenderer
@using Syncfusion.DocIO.DLS
@inject Microsoft.JSInterop.IJSRuntime JS
@inject HttpClient client
{% endhighlight %}

{% endtabs %}

Step 7: Add the following code to create a new button.

{% tabs %}

{% highlight CSHTML %}

<h2>Syncfusion DocIO library (Essential DocIO)</h2>
<p>Syncfusion Blazor DocIO library (Essential DocIO) used to create, read, edit, and convert DocIO files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@WordToImage">Convert Word to Image</button>

{% endhighlight %}

{% endtabs %}

Step 8: Create a new async method with name as ``WordToImage`` and include the following code snippet to **convert a Word document to image in Blazor** WASM app.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Open the file as Stream
using (FileStream sourceStreamPath = new FileStream(@"wwwroot/Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite))
{
    //Open an existing Word document.
    using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Docx))
    {
        //Instantiation of DocIORenderer for Word to image conversion
        using (DocIORenderer render = new DocIORenderer())
        {
            MemoryStream imageStream = (MemoryStream)document.RenderAsImages(0, ExportImageFormat.Jpeg);
            //Reset the stream position.
            imageStream.Position = 0;
            //Download PDF file in the browser.
            await JS.SaveAs("WordToImage.Jpeg", imageStream.ToArray());
        }
    }
}

{% endhighlight %}

{% endtabs %}

Step 9: Create a class file with FileUtils name and add the following code to invoke the JavaScript action to download the file in the browser.

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

Step 10: Add the following JavaScript function in the Index.html file present under ``wwwroot``.

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

Step 11: Add the following code snippet in the razor file of Navigation menu in the Shared folder.

{% tabs %}

{% highlight HTML %}

 <div class="nav-item px-3">
    <NavLink class="nav-link" href="docio">
        <span class="oi oi-list-rich" aria-hidden="true"></span> Word to Image
    </NavLink>
</div>

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Convert-Word-to-image/Blazor/Client-side-application).

By executing the program, you will get the **image** as follows.

![Blazor WASM app output](WordToPDF_images/Output-WordtoImage.png)

N> To convert Word to image, it is necessary to access the font stream internally. However, this cannot be done automatically in a Blazor WASM application. Therefore, we recommend using a Server app, even though Word to image conversion works in a WASM app.
