---
title: Open and save Word document in Blazor | DocIO | Syncfusion 
description: Open and save Word document in Blazor application using Syncfusion .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Open and save Word document in Blazor

Syncfusion DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) used to create, read, and edit **Word** documents programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **open and save a Word document in Blazor**.

**Prerequisites:**

* Visual Studio 2019 Preview
* Install the [.NET Core SDK 3.1 Preview](https://dotnet.microsoft.com/en-us/download/dotnet/3.1)

**Creating a Blazor project**

* Enable Visual Studio to use preview SDKs
* Open Tools > Options in the menu bar.
* Open the Projects and Solutions node. Open the .NET Core tab.
* Check the box for Use previews of the .NET Core SDK and click OK.
* Restart the Visual Studio 2019.

## Server-side application

Step 1: Create a new C# Blazor Server-Side application project. Select Blazor App from the template and click the Next button.

Step 2: Now, the project configuration window will popup. Click Create button to create a new project with the required project name.

Step 3: Choose **Blazor Server App** and click Create button to create a new Blazor Server-Side application for .NET Core 3.0.0-preview9.

Step 4: To **open and save a Word document in server-side application**, install [Syncfusion.DocIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) to the Blazor project.

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Create a razor file with name as **DocIO** under **Pages** folder and include the following namespaces in the file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
@page "/DocIO"
@using System.IO;
@using Open_and_save_Word_document;
@inject Open_and_save_Word_document.Data.WordService service
@inject Microsoft.JSInterop.IJSRuntime JS
{% endhighlight %}
{% endtabs %}

Step 6: Add the following code in **DocIO.razor** file to create a new button.

{% tabs %}
{% highlight CSHTML %}
<h2>Syncfusion DocIO library (DocIO)</h2>
<p>Syncfusion DocIO library (DocIO) is a Blazor DocIO library used to create, read, edit, and convert Word files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@OpenAndSaveDocument">Open and save Document</button>
{% endhighlight %}
{% endtabs %}

Step 7: Add the following code snippet in **DocIO.razor** file to **open and save Word document** and download it.

{% tabs %}
{% highlight c# tabtitle="C#" %}
@code {
    MemoryStream documentStream;
    /// <summary>
    /// Open and save the Word document and download it
    /// </summary>
    protected async void OpenAndSaveDocument()
    {
        documentStream = service.OpenAndSaveDocument();
        await JS.SaveAs("Sample.docx", documentStream.ToArray());
    }
}
{% endhighlight %}
{% endtabs %}

Step 8: Create a new cs file with name as **WordService** under Data folder and include the following namespaces in the file.

{% tabs %}

{% highlight c# tabtitle="C#" %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% endtabs %}

Step 9: Create a new MemoryStream method with name as **OpenAndSaveDocument** in **WordService** class and include the following code snippet to **open an existing Word document in Blazor** Server-Side application.

{% tabs %}

{% highlight c# tabtitle="C#" %}

public MemoryStream OpenAndSaveDocument()
{
    using (FileStream sourceStreamPath = new FileStream("Input.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite))
    {
        //Open an existing Word document.
        using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Docx))
    }
}
{% endhighlight %}

Step 10: Add below code example to add a paragraph in the Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Access the section in a Word document.
IWSection section = document.Sections[0];
//Add a new paragraph to the section.
IWParagraph paragraph = section.AddParagraph();
paragraph.ParagraphFormat.FirstLineIndent = 36;
paragraph.BreakCharacterFormat.FontSize = 12f;
IWTextRange text = paragraph.AppendText("In 2000, Adventure Works Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the Adventure Works Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.");
text.CharacterFormat.FontSize = 12f;
{% endhighlight %}

{% endtabs %}

Step 11: Add below code example to **save the Word document in Blazor**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Save the Word document to MemoryStream.
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
return stream;
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

Step 14: Add the following code snippet in the razor file of Navigation menu in the Shared folder.

{% tabs %}

{% highlight HTML %}

<li class="nav-item px-3">
    <NavLink class="nav-link" href="docio">
        <span class="oi oi-list-rich" aria-hidden="true"></span> Create Word
    </NavLink>
</li>

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Read-and-Save-document/Open-and-save-Word-document/Blazor/Server-side-application).

By executing the program, you will get the **Word document** as follows.

![Blazor Server-side output Word document](Blazor_Images/Blazor_Output.png)

## Client-side application

Step 1: Create a new C# Blazor Client-Side application project. Select Blazor App from the template and click the Next button.

Step 2: Now, the project configuration window will popup. Click Create button to create a new project with the required project name.

Step 3: Choose Blazor WebAssembly App and click Create button to create a new Blazor Client-Side application for .NET Core 3.0.0-preview9.

Step 4: To **open and save a Word document in client-side application**, install [Syncfusion.DocIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) to the Blazor project.

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Create a razor file with name as ``DocIO`` under ``Pages`` folder and add the following namespaces in the file.

{% tabs %}

{% highlight c# tabtitle="C#" %}
@page "/DocIO"
@using Syncfusion.DocIO
@using Syncfusion.DocIO.DLS
{% endhighlight %}

{% endtabs %}

Step 6: Add the following code to create a new button.

{% tabs %}

{% highlight CSHTML %}

<h2>Syncfusion DocIO library (DocIO)</h2>
<p>Syncfusion Blazor DocIO library (DocIO) used to create, read, edit, and convert DocIO files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@OpenAndSaveWordDocument">Open and save Document</button>

{% endhighlight %}

{% endtabs %}

Step 7: Create a new async method with name as ``OpenAndSaveDocument`` and include the following code snippet to **open an existing Word document in Blazor** Client-Side application.

{% tabs %}

{% highlight c# tabtitle="C#" %}

@functions {
    async void OpenAndSaveDocument()
    {
        using (Stream inputStream = await client.GetStreamAsync("Input.docx"))
        {
            //Open an existing Word document.
            using (WordDocument document = new WordDocument(inputStream, FormatType.Docx))
        }
    }
Step 8: Add below code example to add a paragraph in the Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Access the section in a Word document.
IWSection section = document.Sections[0];
//Add a new paragraph to the section.
IWParagraph paragraph = section.AddParagraph();
paragraph.ParagraphFormat.FirstLineIndent = 36;
paragraph.BreakCharacterFormat.FontSize = 12f;
IWTextRange text = paragraph.AppendText("In 2000, Adventure Works Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the Adventure Works Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.");
text.CharacterFormat.FontSize = 12f;
{% endhighlight %}

{% endtabs %}

Step 9: Add below code example to **save the Word document in Blazor**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Save the Word document to MemoryStream.
using (MemoryStream stream = new MemoryStream())
{
    document.Save(stream, FormatType.Docx);
    stream.Position = 0;
    //Download the Word document in the browser.
    await JS.SaveAs("Sample.docx", stream.ToArray());
}
{% endhighlight %}

{% endtabs %}

Step 10: Create a class file with FileUtils name and add the following code to invoke the JavaScript action to download the file in the browser.

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

Step 12: Add the following code snippet in the razor file of Navigation menu in the Shared folder.

{% tabs %}

{% highlight HTML %}

<li class="nav-item px-3">
    <NavLink class="nav-link" href="docio">
        <span class="oi oi-list-rich" aria-hidden="true"></span> Create Word
    </NavLink>
</li>

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Read-and-Save-document/Open-and-save-Word-document/Blazor/Client-side-application).

By executing the program, you will get the **Word document** as follows.

![Blazor Client-side output Word document](Blazor_Images/Blazor_Output.png)

N> Even though Word library works in client-side, it is recommended to use server-side deployment. Since the client-side deployment increases the application payload size.

Kindly explore the [supported and unsupported features of Word library in Blazor](https://help.syncfusion.com/file-formats/docio/supported-and-unsupported-features#blazor-supported-features)