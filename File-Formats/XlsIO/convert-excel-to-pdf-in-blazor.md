---
title: Convert an Excel document to PDF in Blazor | Syncfusion
description: Convert an Excel document to PDF in blazor using Sycfusion Blazor Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert an Excel document to PDF in Blazor

Syncfusion XlsIO is a [Blazor Excel library](https://www.syncfusion.com/document-processing/excel-framework/blazor/excel-library) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in Blazor**.

## Excel to PDF in Blazor Server App

Step 1: Create a new C# Blazor Server app project.
<img src="Blazor_images\Blazor_images_Server_App.png" alt="Create a Blazor Server App project" width="100%" Height="Auto"/>

Step 2: Name the project.
<img src="Blazor_images\Blazor_images_Server_App_ProjectName.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Select the framework and click **Create** button.
<img src="Blazor_images\Blazor_images_Server_App_Framework.png" alt="Framework version" width="100%" Height="Auto"/>

Step 4: Install the [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
<img src="Blazor_images\Blazor_images_Server_App_Nuget.png" alt="Install Syncfusion.XlsIORenderer.Net.Core NuGet Package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components

Step 5: Create a razor file with name as **XlsIO** under **Pages** folder and include the following namespaces in the file.
{% tabs %}
{% highlight c# tabtitle="C#" %}
@page "/xlsio"
@using Convert_Excel_to_PDF;
@inject Convert_Excel_to_PDF.Data.ExcelService service
@inject Microsoft.JSInterop.IJSRuntime JS
{% endhighlight %}
{% endtabs %}

Step 6: Add the following code in **XlsIO.razor** file to create a new button.
{% tabs %}
{% highlight CSHTML %}
<h2>Syncfusion XlsIO library </h2>
<p>Syncfusion Blazor XlsIO library is used to create, read, edit, and convert Excel files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@ConvertExceltoPDF">Convert Excel to PDF</button>
{% endhighlight %}
{% endtabs %}

Step 7: Add the following code in **XlsIO.razor** file to create and download the **PDF document**.
{% tabs %}
{% highlight c# tabtitle="C#" %}
@code {
    MemoryStream documentStream;
    /// <summary>
    /// Convert Excel to PDF and download the PDF document
    /// </summary>
    protected async void ConvertExceltoPDF()
    {
        documentStream = service.ConvertExceltoPDF();
        await JS.SaveAs("Sample.pdf", documentStream.ToArray());
    }
}
{% endhighlight %}
{% endtabs %}

Step 8: Create a new cs file with name as **ExcelService** under Data folder and include the following namespaces in the file.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.Pdf;
using Syncfusion.XlsIORenderer;
{% endhighlight %}
{% endtabs %}

Step 9: Create a new MemoryStream method with name as **ConvertExceltoPDF** in **ExcelService** class and include the following code snippet to **convert an Excel document to Pdf** in Server app.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Load an existing file
    using (FileStream sourceStreamPath = new FileStream(@"wwwroot/InputTemplate.xlsx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite))
    {
        // Open the workbook.
        IWorkbook workbook = application.Workbooks.Open(sourceStreamPath);

        // Instantiate the Excel to PDF renderer.
        XlsIORenderer renderer = new XlsIORenderer();

        //Convert Excel document into PDF document 
        PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

        //Create the MemoryStream to save the converted PDF.      
        MemoryStream pdfStream = new MemoryStream();

        //Save the converted PDF document to MemoryStream.
        pdfDocument.Save(pdfStream);
        pdfStream.Position = 0;
        return pdfStream;
    }
}
{% endhighlight %}
{% endtabs %}

Step 10: Create a new class file in the project, with name as **FileUtils** and add the following code to invoke the JavaScript action to download the file in the browser.
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

Step 11: Add the following JavaScript function in the **_Host.cshtml** in the Pages folder.
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

Step 12: Add the following code snippet in the **NavMenu.razor** in the Shared folder.
{% tabs %}
{% highlight HTML %}
<li class="nav-item px-3">
    <NavLink class="nav-link" href="xlsio">
        <span class="oi oi-list-rich" aria-hidden="true"></span> Convert Excel to PDF
    </NavLink>
</li>
{% endhighlight %}
{% endtabs %}

A complete working example of how to convert an Excel document to PDF in Blazor Server App is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Blazor/Server%20Side/Convert%20Excel%20to%20PDF).

By executing the program, you will get the **PDF document** as follows.

<img src="Blazor_images\Blazor_images_Server_and_Client_App_Output.png" alt="Excel to PDF in Blazor Server App" width="100%" Height="Auto"/>

Click [here](https://www.syncfusion.com/document-processing/excel-framework/blazor) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://blazor.syncfusion.com/demos/excel/excel-to-pdf?theme=fluent) in Blazor.

## Excel to PDF in Blazor WASM app

Step 1: Create a new C# Blazor WASM app project.
<img src="Blazor_images\Blazor_images_Client_App.png" alt="Create a Blazor Wasm App project" width="100%" Height="Auto"/>

Step 2: Name the project.
<img src="Blazor_images\Blazor_images_Client_ProjectName.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Select the framework and click **Create** button.
<img src="Blazor_images\Blazor_images_Client_Framework.png" alt="Framework version" width="100%" Height="Auto"/> 

Step 4: Install the following **Nuget packages** in your application from [NuGet.org](https://www.nuget.org/).
* [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core)
* [SkiaSharp.NativeAssets.WebAssembly](https://www.nuget.org/packages/SkiaSharp.NativeAssets.WebAssembly)

<img src="Blazor_images\Blazor_images_Client_Nuget1.png" alt="Install Syncfusion.XlsIORenderer.Net.Core NuGet Package" width="100%" Height="Auto"/>

<img src="Blazor_images\Blazor_images_Client_Nuget2.png" alt="Install SkiaSharp.NativeAssets.WebAssembly NuGet Package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Add the following ItemGroup tag in the **Blazor WASM csproj** file.
{% tabs %}
{% highlight XAML  %}
<ItemGroup>
    <NativeFileReference Include="$(SkiaSharpStaticLibraryPath)\2.0.23\*.a" />
</ItemGroup>
{% endhighlight %}
{% endtabs %}

N> Install this wasm-tools and wasm-tools-net6 by using the "dotnet workload install wasm-tools" and "dotnet workload install wasm-tools-net6" commands in your command prompt respectively if you are facing issues related to Skiasharp during runtime.

Step 6: Enable the following property in the Blazor WASM csproj file.

{% tabs %}
{% highlight XAML %}
<PropertyGroup>
    <WasmNativeStrip>true</WasmNativeStrip>
</PropertyGroup>
{% endhighlight %}
{% endtabs %}

Step 7: Create a razor file with name as **XlsIO** under **Pages** folder and include the following namespaces in the file.
{% tabs %}
{% highlight c# tabtitle="C#" %}
@page "/xlsio"
@using Syncfusion.XlsIO
@using Syncfusion.Pdf
@using Syncfusion.XlsIORenderer
@inject Microsoft.JSInterop.IJSRuntime JS
@inject HttpClient client
{% endhighlight %}
{% endtabs %}

Step 8: Add the following code to create a new button.
{% tabs %}
{% highlight CSHTML %}
<h2>Syncfusion XlsIO library</h2>
<p>Syncfusion Blazor XlsIO library used to create, read, edit, and convert DocIO files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@ExcelToPDF">Convert Excel to PDF</button>
{% endhighlight %}
{% endtabs %}

Step 9: Create a new async method with name as **ExcelToPDF** and include the following code snippet to **create an Excel document in Blazor** WASM app.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Load an existing file
    using (Stream inputStream = await client.GetStreamAsync("Data/InputTemplate.xlsx"))
    {
        // Open the workbook.
        IWorkbook workbook = application.Workbooks.Open(inputStream);

        // Instantiate the Excel to PDF renderer.
        XlsIORenderer renderer = new XlsIORenderer();

        //Convert Excel document into PDF document
        PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

        //Create the MemoryStream to save the converted PDF.
        MemoryStream pdfStream = new MemoryStream();

        //Save the converted PDF document to MemoryStream.
        pdfDocument.Save(pdfStream);
        pdfStream.Position = 0;

        //Download PDF file in the browser.
        await JS.SaveAs("Output.pdf", pdfStream.ToArray());
    }
}
{% endhighlight %}
{% endtabs %}

Step 10: Create a class file with **FileUtils** name and add the following code to invoke the JavaScript action to download the file in the browser.
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

Step 11: Add the following JavaScript function in the **Index.html** file present under **wwwroot**.
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

Step 12: Add the following code snippet in the **NavMenu.razor** in the Shared folder
{% tabs %}
{% highlight CSHTML %}
<li class="nav-item px-3">
    <NavLink class="nav-link" href="xlsio">
        <span class="oi oi-list-rich" aria-hidden="true"></span> Convert Excel to PDF
    </NavLink>
</li>
{% endhighlight %}
{% endtabs %}

A complete working example of how to convert an Excel document to PDF in Blazor WASM App is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Blazor/Client%20Side/Convert%20Excel%20to%20PDF).

By executing the program, you will get the **PDF document** as follows.

<img src="Blazor_images\Blazor_images_Server_and_Client_App_Output.png" alt="Excel to PDF in Blazor WASM App" width="100%" Height="Auto"/>

N> To convert Excel to PDF, it is necessary to access the font stream internally. However, this cannot be done automatically in a Blazor WASM application. Therefore, we recommend using a Server app, even though Excel to PDF conversion works in a WASM app.

Click [here](https://www.syncfusion.com/document-processing/excel-framework/blazor) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://blazor.syncfusion.com/demos/excel/excel-to-pdf?theme=fluent) in Blazor.
