---
title: Create Word document in Blazor | DocIO | Syncfusion 
description: Create Word document without Microsoft Word or interop dependencies in Blazor application using Syncfusion .NET Core (Essential DocIO) library
platform: file-formats
control: DocIO
documentation: UG
---

# Create Word document in Blazor

Syncfusion Essential DocIO is a [.NET Core Word library](https://www.syncfusion.com/word-framework/net-core/word-library) used to create, read, and edit Word documents programmatically without Microsoft Word or interop dependencies. Using this library, you can create a Word document in Blazor.

**Prerequisites:**

* Visual Studio 2019 Preview
* Install [.NET Core SDK 3.0 Preview](https://dotnet.microsoft.com/download/dotnet-core/3.0)

**Creating a Blazor project**
<ol><li>Enable Visual Studio to use preview SDKs:</li>
<ul>
<li>Open Tools > Options in the menu bar.</li>
<li>Open the Projects and Solutions node. Open the .NET Core tab.</li>
<li>Check the box for Use previews of the .NET Core SDK and click OK.</li>
</ul>
<li>Restart the Visual Studio 2019.</li>
</ol>

## Client-side application

* Create a new project.

![Create ASP.NET Core Web application in Visual Studio](Blazor_Images/Blazor_Create.png)

* Select ASP.NET Core Web Application and click Next.

![Create a project name for your new project](Blazor_Images/Blazor_Configure.png)

* Select **.NET Core**, **ASP.NET Core 3.0** and **Blazor (client-side)**.

![Select .NET Core, ASP.NET Core 3.0 and Blazor Client side.](Blazor_Images/Select_Client.png)

**Creating a Word document in client-side application**

* To create a Word document, install [Syncfusion.DocIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) to the Blazor project.

![Install DocIO.NET Core NuGet Package](Blazor_Images/Install_Nuget.png)

* Add the following namespace in the Index.razor to create a Word document from the scratch.

{% tabs %}

{% highlight c# %}

@using Syncfusion.DocIO;
@using Syncfusion.DocIO.DLS;
@using System.IO;

{% endhighlight %}

{% endtabs %}

* Add a button and hook the click event function.

{% tabs %}

{% highlight HTML %}

<button class="btn btn-primary" onclick="@CreateWord">Create Word</button>

{% endhighlight %}

{% endtabs %}

* Add the following code to create a Word document in Blazor.

{% tabs %}

{% highlight c# %}

@functions {

    void CreateWord()
    {
        // Creating a new document.
        WordDocument document = new WordDocument();
        //Adding a new section to the document.
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

        //Appends paragraph.
        paragraph = section.AddParagraph();
        paragraph.ApplyStyle("Heading 1");
        paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
        textRange = paragraph.AppendText("Adventure Works Cycles") as WTextRange;
        textRange.CharacterFormat.FontSize = 18f;
        textRange.CharacterFormat.FontName = "Calibri";
	
        //Appends paragraph.
        paragraph = section.AddParagraph();
        paragraph.ParagraphFormat.FirstLineIndent = 36;
        paragraph.BreakCharacterFormat.FontSize = 12f;
        textRange = paragraph.AppendText("Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base.") as WTextRange;
        textRange.CharacterFormat.FontSize = 12f;

        //Appends paragraph.
        paragraph = section.AddParagraph();
        paragraph.ParagraphFormat.FirstLineIndent = 36;
        paragraph.BreakCharacterFormat.FontSize = 12f;
        textRange = paragraph.AppendText("In 2000, AdventureWorks Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.") as WTextRange;
        textRange.CharacterFormat.FontSize = 12f;

        //Saves the Word document to  MemoryStream
        MemoryStream stream = new MemoryStream();
        document.Save(stream, FormatType.Docx);
        //Closes the Word document
        document.Close();
        stream.Position = 0;

        //Download the Word document in the browser.
		JS.SaveAs("Sample.docx", stream.ToArray());
    }
}

{% endhighlight %}

{% endtabs %}

**To download the Word document in browser**

Create a class file with FileUtil name and add the following code to invoke the JavaScript action to download the file in the browser.

* Add the following code in the created class file.

{% tabs %}

{% highlight c# %}

public static class FileUtil
{
    public static Task SaveAs(this IJSRuntime js, string filename, byte[] data)
       => js.InvokeAsync<object>(
           "saveAsFile",
           filename,
           Convert.ToBase64String(data));
}

{% endhighlight %}

{% endtabs %}

* Add the following JavaScript function in the Index.html.

{% tabs %}

{% highlight HTML %}

<script type="text/javascript">
    function saveAsFile(filename, bytesBase64) {
        var link = document.createElement('a');
        link.download = filename;
        link.href = "data:application/octet-stream;base64," + bytesBase64;
        document.body.appendChild(link); // Needed for Firefox
        link.click();
        document.body.removeChild(link);
    }
</script>

{% endhighlight %}

{% endtabs %}

By executing the program, you will get the Word document as follows.

![Blazor Client-side output Word document](Blazor_Images/Blazor_Output.png)

N> Even though Word library works in client-side, it is recommended to use server-side deployment. Since the client-side deployment increases the application payload size.

## Server-side application

* Create a new project.

![Create ASP.NET Core Web application in Visual Studio](Blazor_Images/Blazor_Create.png)

* Select ASP.NET Core Web Application and click Next.

![Create a project name for your new project](Blazor_Images/Blazor_Configure.png)

* Select **.NET Core, ASP.NET Core 3.0** and **Blazor (server-side)**.

![Select .NET Core, ASP.NET Core 3.0 and Blazor Server side.](Blazor_Images/Select_Server.png)

**Creating a Word document in server-side application**

* To create a Word document, install [Syncfusion.DocIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) to the Blazor project.

![Install DocIO.NET Core NuGet Package](Blazor_Images/Install_Nuget.png)

* Add the following namespace in the Index.razor to create a Word document from the scratch.

{% tabs %}

{% highlight c# %}

@using Syncfusion.DocIO;
@using Syncfusion.DocIO.DLS;
@using System.IO;

{% endhighlight %}

{% endtabs %}

* Add a button and hook the click event function.

{% tabs %}

{% highlight HTML %}

<button class="btn btn-primary" onclick="@CreateWord">Create Word</button>

{% endhighlight %}

{% endtabs %}

* Add the following code to create a Word document in Blazor.

{% tabs %}

{% highlight C# %}

@functions {

    void CreateWord()
    {
        // Creating a new document.
        WordDocument document = new WordDocument();
        //Adding a new section to the document.
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

        //Appends paragraph.
        paragraph = section.AddParagraph();
        paragraph.ApplyStyle("Heading 1");
        paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
        textRange = paragraph.AppendText("Adventure Works Cycles") as WTextRange;
        textRange.CharacterFormat.FontSize = 18f;
        textRange.CharacterFormat.FontName = "Calibri";

        //Appends paragraph.
        paragraph = section.AddParagraph();
        paragraph.ParagraphFormat.FirstLineIndent = 36;
        paragraph.BreakCharacterFormat.FontSize = 12f;
        textRange = paragraph.AppendText("Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base.") as WTextRange;
        textRange.CharacterFormat.FontSize = 12f;

        //Appends paragraph.
        paragraph = section.AddParagraph();
        paragraph.ParagraphFormat.FirstLineIndent = 36;
        paragraph.BreakCharacterFormat.FontSize = 12f;
        textRange = paragraph.AppendText("In 2000, AdventureWorks Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.") as WTextRange;
        textRange.CharacterFormat.FontSize = 12f;

        //Saves the Word document to  MemoryStream
        MemoryStream stream = new MemoryStream();
        document.Save(stream, FormatType.Docx);
        //Closes the Word document
        document.Close();
        stream.Position = 0;

        //Download the Word document in the browser.
		JS.SaveAs("Sample.docx", stream.ToArray());
    }
}

{% endhighlight %}

{% endtabs %}

**To download the Word document in browser**

Create a class file with FileUtil name and add the following code to invoke the JavaScript action to download the file in the browser.

* Add the following code in the created class file.

{% tabs %}

{% highlight c# %}

public static class FileUtil
{
    public static Task SaveAs(this IJSRuntime js, string filename, byte[] data)
       => js.InvokeAsync<object>(
           "saveAsFile",
           filename,
           Convert.ToBase64String(data));
}

{% endhighlight %}

{% endtabs %}

* Add the following JavaScript function in the _Host.cshtml in the pages folder.

{% tabs %}

{% highlight HTML %}

<script type="text/javascript">
    function saveAsFile(filename, bytesBase64) {
        var link = document.createElement('a');
        link.download = filename;
        link.href = "data:application/octet-stream;base64," + bytesBase64;
        document.body.appendChild(link); // Needed for Firefox
        link.click();
        document.body.removeChild(link);
    }
</script>

{% endhighlight %}

{% endtabs %}

By executing the program, you will get the Word document as follows.

![Blazor Server-side output Word document](Blazor_Images/Blazor_Output.png)