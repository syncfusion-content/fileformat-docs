---
title: Create Word document in Blazor | DocIO | Syncfusion 
description: Create Word document without Microsoft Word or interop dependencies in Blazor application using Syncfusion .NET Core Word (Essential DocIO) library
platform: file-formats
control: DocIO
documentation: UG
---

# Create Word document in Blazor

Syncfusion Essential DocIO is a [.NET Core Word library](https://www.syncfusion.com/word-framework/net-core/word-library) used to create, read, and edit **Word** documents programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **create a Word document in Blazor**.

**Prerequisites:**

* Visual Studio 2019 Preview
* Install the [.NET Core SDK 3.0 Preview](https://dotnet.microsoft.com/download/dotnet-core/3.0)

**Creating a Blazor project**

* Enable Visual Studio to use preview SDKs
* Open Tools > Options in the menu bar.
* Open the Projects and Solutions node. Open the .NET Core tab.
* Check the box for Use previews of the .NET Core SDK and click OK.
* Restart the Visual Studio 2019.

## Server-side application

1.Create a new C# Blazor Server-Side application project. Select Blazor App from the template and click the Next button.

![Create ASP.NET Core Web application in Visual Studio](Blazor_Images/Blazor_Create.png)

2.Now, the project configuration window will popup. Click Create button to create a new project with the required project name.

![Create a project name for your new project](Blazor_Images/Blazor_images_Server_ProjectName.png)

3.Choose **Blazor Server App** and click Create button to create a new Blazor Server-Side application for .NET Core 3.0.0-preview9.

![Select .NET Core, ASP.NET Core 3.0 and Blazor Server side.](Blazor_Images/Select_Server.png)

4.To **create a Word document in server-side application**, install [Syncfusion.DocIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) to the Blazor project.

![Install DocIO.NET Core NuGet Package](Blazor_Images/Install_Nuget.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.

5. Create a razor file with name as **DocIO** under **Pages** folder and include the following namespaces in the file.

{% capture codesnippet1 %}
{% tabs %}
{% highlight c# tabtitle="C#" %}
@page "/DocIO"
@using System.IO;
@using ServerSideApplication;
@inject ServerSideApplication.Data.WordService service
@inject Microsoft.JSInterop.IJSRuntime JS
{% endhighlight %}
{% endtabs %}
{% endcapture %}
{{ codesnippet1 | OrderList_Indent_Level_1 }}

6. Add the following code in **DocIO.razor** file to create a new button.

{% capture codesnippet2 %}

{% tabs %}
{% highlight CSHTML %}
<h2>Syncfusion DocIO library (Essential DocIO)</h2>
<p>Syncfusion DocIO library (Essential DocIO) is a Blazor DocIO library used to create, read, edit, and convert Word files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@CreateWord">Create Word</button>
{% endhighlight %}
{% endtabs %}
{% endcapture %}
{{ codesnippet2 | OrderList_Indent_Level_1 }}

7. Add the following code in **DocIO.razor** file to create and download the **Word document**.

{% capture codesnippet3 %}

{% tabs %}
{% highlight c# tabtitle="C#" %}
@code {
    MemoryStream documentStream;

    /// <summary>
    /// Create and download the Word document
    /// </summary>
    protected async void CreateWord()
    {
        documentStream = service.CreateWord();
        await JS.SaveAs("Sample.docx", documentStream.ToArray());
    }
}
{% endhighlight %}
{% endtabs %}
{% endcapture %}
{{ codesnippet3 | OrderList_Indent_Level_1 }}

8. Create a new cs file with name as **WordService** under Data folder and include the following namespaces in the file.

{% capture codesnippet4 %}

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using System.IO;

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet4 | OrderList_Indent_Level_1 }}

9. Create a new MemoryStream method with name as **CreateWord** in **WordService** class and include the following code snippet to **create a simple Word document in Blazor** Server-Side application.

{% capture codesnippet5 %}

{% tabs %}

{% highlight c# tabtitle="C#" %}

public MemoryStream CreateWord()
{
    //Creating a new document
    WordDocument document = new WordDocument();
    //Adding a new section to the document
    WSection section = document.AddSection() as WSection;
    //Set Margin of the section
    section.PageSetup.Margins.All = 72;
    //Set page size of the section
    section.PageSetup.PageSize = new Syncfusion.Drawing.SizeF(612, 792);

    //Create Paragraph styles
    WParagraphStyle style = document.AddParagraphStyle("Normal") as WParagraphStyle;
    style.CharacterFormat.FontName = "Calibri";
    style.CharacterFormat.FontSize = 11f;
    style.ParagraphFormat.BeforeSpacing = 0;
    style.ParagraphFormat.AfterSpacing = 8;
    style.ParagraphFormat.LineSpacing = 13.8f;

    style = document.AddParagraphStyle("Heading 1") as WParagraphStyle;
    style.ApplyBaseStyle("Normal");
    style.CharacterFormat.FontName = "Calibri Light";
    style.CharacterFormat.FontSize = 16f;
    style.CharacterFormat.TextColor = Syncfusion.Drawing.Color.FromArgb(46, 116, 181);
    style.ParagraphFormat.BeforeSpacing = 12;
    style.ParagraphFormat.AfterSpacing = 0;
    style.ParagraphFormat.Keep = true;
    style.ParagraphFormat.KeepFollow = true;
    style.ParagraphFormat.OutlineLevel = OutlineLevel.Level1;
    IWParagraph paragraph = section.HeadersFooters.Header.AddParagraph();

    paragraph.ApplyStyle("Normal");
    paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Left;
    WTextRange textRange = paragraph.AppendText("Adventure Works Cycles") as WTextRange;
    textRange.CharacterFormat.FontSize = 12f;
    textRange.CharacterFormat.FontName = "Calibri";
    textRange.CharacterFormat.TextColor = Syncfusion.Drawing.Color.Red;

    //Appends paragraph
    paragraph = section.AddParagraph();
    paragraph.ApplyStyle("Heading 1");
    paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
    textRange = paragraph.AppendText("Adventure Works Cycles") as WTextRange;
    textRange.CharacterFormat.FontSize = 18f;
    textRange.CharacterFormat.FontName = "Calibri";

    //Appends paragraph
    paragraph = section.AddParagraph();
    paragraph.ParagraphFormat.FirstLineIndent = 36;
    paragraph.BreakCharacterFormat.FontSize = 12f;
    textRange = paragraph.AppendText("Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base.") as WTextRange;
    textRange.CharacterFormat.FontSize = 12f;

    //Appends paragraph
    paragraph = section.AddParagraph();
    paragraph.ParagraphFormat.FirstLineIndent = 36;
    paragraph.BreakCharacterFormat.FontSize = 12f;
    textRange = paragraph.AppendText("In 2000, AdventureWorks Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.") as WTextRange;
    textRange.CharacterFormat.FontSize = 12f;

    //Saves the Word document to MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Closes the Word document
    document.Close();
    stream.Position = 0;

    return stream;
}
{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet5 | OrderList_Indent_Level_1 }}

10. Create a new class file in the project, with name as FileUtils and add the following code to invoke the JavaScript action to download the file in the browser.

{% capture codesnippet6 %}

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

11. Add the following JavaScript function in the _Host.cshtml in the Pages folder.

{% capture codesnippet7 %}

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

12. Add the following code snippet in the razor file of Navigation menu in the Shared folder.

{% capture codesnippet8 %}

{% tabs %}

{% highlight HTML %}

<li class="nav-item px-3">
     <NavLink class="nav-link" href="docio">
         <span class="oi oi-list-rich" aria-hidden="true"></span> Create Word
     </NavLink>
</li>

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet8 | OrderList_Indent_Level_1 }}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Getting-Started/Blazor/Server-side-application).

By executing the program, you will get the **Word document** as follows.

![Blazor Server-side output Word document](Blazor_Images/Blazor_Output.png)

## Client-side application

1.Create a new C# Blazor Client-Side application project. Select Blazor App from the template and click the Next button.

![Create ASP.NET Core Web application in Visual Studio](Blazor_Images/Blazor_Create.png)

2.Now, the project configuration window will popup. Click Create button to create a new project with the required project name.

![Create a project name for your new project](Blazor_Images/Blazor_image_Client_ProjectName.png)

3.Choose Blazor WebAssembly App and click Create button to create a new Blazor Client-Side application for .NET Core 3.0.0-preview9.

![Select .NET Core, ASP.NET Core 3.0 and Blazor Client side.](Blazor_Images/Select_Client.png)

4.To **create a Word document in client-side application**, install [Syncfusion.DocIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) to the Blazor project.

![Install DocIO.NET Core NuGet Package](Blazor_Images/Install_Nuget.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.

5. Create a razor file with name as ``DocIO`` under ``Pages`` folder and add the following namespaces in the file.

{% capture codesnippet9 %}

{% tabs %}

{% highlight c# tabtitle="C#" %}
@page "/DocIO"
@inject Microsoft.JSInterop.IJSRuntime JS
@using Syncfusion.DocIO
@using Syncfusion.DocIO.DLS
@using System.IO
{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet9 | OrderList_Indent_Level_1 }}

6. Add the following code to create a new button.

{% capture codesnippet10 %}

{% tabs %}

{% highlight CSHTML %}

<h2>Syncfusion DocIO library (Essential DocIO)</h2>
<p>Syncfusion Blazor DocIO library (Essential DocIO) used to create, read, edit, and convert DocIO files in your applications without Microsoft Office dependencies.</p>
<button class="btn btn-primary" @onclick="@CreateWord">Create Word</button>

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet10 | OrderList_Indent_Level_1 }}

7. Create a new async method with name as ``CreateWord`` and include the following code snippet to **create a Word document in Blazor** Client-Side application.

{% capture codesnippet11 %}

{% tabs %}

{% highlight c# tabtitle="C#" %}

@functions {

    async void CreateWord()
    {
        //Creating a new document
        WordDocument document = new WordDocument();
        //Adding a new section to the document
        WSection section = document.AddSection() as WSection;
        //Set Margin of the section
        section.PageSetup.Margins.All = 72;
        //Set page size of the section
        section.PageSetup.PageSize = new Syncfusion.Drawing.SizeF(612, 792);

        //Create Paragraph styles
        WParagraphStyle style = document.AddParagraphStyle("Normal") as WParagraphStyle;
        style.CharacterFormat.FontName = "Calibri";
        style.CharacterFormat.FontSize = 11f;
        style.ParagraphFormat.BeforeSpacing = 0;
        style.ParagraphFormat.AfterSpacing = 8;
        style.ParagraphFormat.LineSpacing = 13.8f;

        style = document.AddParagraphStyle("Heading 1") as WParagraphStyle;
        style.ApplyBaseStyle("Normal");
        style.CharacterFormat.FontName = "Calibri Light";
        style.CharacterFormat.FontSize = 16f;
        style.CharacterFormat.TextColor = Syncfusion.Drawing.Color.FromArgb(46, 116, 181);
        style.ParagraphFormat.BeforeSpacing = 12;
        style.ParagraphFormat.AfterSpacing = 0;
        style.ParagraphFormat.Keep = true;
        style.ParagraphFormat.KeepFollow = true;
        style.ParagraphFormat.OutlineLevel = OutlineLevel.Level1;
        IWParagraph paragraph = section.HeadersFooters.Header.AddParagraph();

        paragraph.ApplyStyle("Normal");
        paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Left;
        WTextRange textRange = paragraph.AppendText("Adventure Works Cycles") as WTextRange;
        textRange.CharacterFormat.FontSize = 12f;
        textRange.CharacterFormat.FontName = "Calibri";
        textRange.CharacterFormat.TextColor = Syncfusion.Drawing.Color.Red;

        //Appends paragraph
        paragraph = section.AddParagraph();
        paragraph.ApplyStyle("Heading 1");
        paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
        textRange = paragraph.AppendText("Adventure Works Cycles") as WTextRange;
        textRange.CharacterFormat.FontSize = 18f;
        textRange.CharacterFormat.FontName = "Calibri";
	
        //Appends paragraph
        paragraph = section.AddParagraph();
        paragraph.ParagraphFormat.FirstLineIndent = 36;
        paragraph.BreakCharacterFormat.FontSize = 12f;
        textRange = paragraph.AppendText("Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base.") as WTextRange;
        textRange.CharacterFormat.FontSize = 12f;

        //Appends paragraph
        paragraph = section.AddParagraph();
        paragraph.ParagraphFormat.FirstLineIndent = 36;
        paragraph.BreakCharacterFormat.FontSize = 12f;
        textRange = paragraph.AppendText("In 2000, AdventureWorks Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.") as WTextRange;
        textRange.CharacterFormat.FontSize = 12f;

        //Saves the Word document to MemoryStream
        MemoryStream stream = new MemoryStream();
        document.Save(stream, FormatType.Docx);
        //Closes the Word document
        document.Close();
        stream.Position = 0;

        //Download the Word document in the browser
        JS.SaveAs("Sample.docx", stream.ToArray());
    }
}

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet11 | OrderList_Indent_Level_1 }}

8. Create a class file with FileUtils name and add the following code to invoke the JavaScript action to download the file in the browser.

{% capture codesnippet12 %}

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
{{ codesnippet12 | OrderList_Indent_Level_1 }}

9. Add the following JavaScript function in the Index.html file present under ``wwwroot``.

{% capture codesnippet13 %}

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
{{ codesnippet13 | OrderList_Indent_Level_1 }}

10. Add the following code snippet in the razor file of Navigation menu in the Shared folder.

{% capture codesnippet14 %}

{% tabs %}

{% highlight HTML %}

<li class="nav-item px-3">
     <NavLink class="nav-link" href="docio">
         <span class="oi oi-list-rich" aria-hidden="true"></span> Create Word
     </NavLink>
</li>

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet14 | OrderList_Indent_Level_1 }}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Getting-Started/Blazor/Client-side-application).

By executing the program, you will get the **Word document** as follows.

![Blazor Client-side output Word document](Blazor_Images/Blazor_Output.png)

N> Even though Word library works in client-side, it is recommended to use server-side deployment. Since the client-side deployment increases the application payload size.

Kindly explore the [supported and unsupported features of Word library in Blazor](https://help.syncfusion.com/file-formats/docio/supported-and-unsupported-features#blazor-supported-features)