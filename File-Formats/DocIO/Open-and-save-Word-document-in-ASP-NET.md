---
title: Open and save Word document in ASP.NET | Syncfusion
description: Open and save Word document in ASP.NET application using Syncfusion .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Open and Save Word document in ASP.NET

Syncfusion DocIO is a [.NET Word library](https://www.syncfusion.com/document-processing/word-framework/net/word-library) used to **create, read, and edit Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **open and save a Word document in ASP.NET Web Forms**.

## Steps to open and save Word document programmatically:

Step 1: Create a new ASP.NET Web application project.

Step 2: Install the [Syncfusion.DocIO.AspNet](https://www.nuget.org/packages/Syncfusion.DocIO.AspNet) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Add a new Web Form in your project. Right click on the project and select **Add > New Item** and add a Web Form from the list. Name it as MainPage.

Step 4: Add a new button in the **MainPage.aspx** as shown below.

{% tabs %}

{% highlight HTML %}

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
    <asp:Button ID="Button1" runat="server" Text="Open and Save Document" OnClick="OnButtonClicked" />
    </div>
    </form>
</body>
</html>

{% endhighlight %}

{% endtabs %}

Step 5. Include the following namespace in your **MainPage.aspx.cs** file.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;

{% endhighlight %}

{% endtabs %}

Step 6: Include the below code snippets in the click event of the button in **MainPage.aspx.cs**, to **open an existing Word document in ASP.NET**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open an existing Word document.
WordDocument document = new WordDocument(Input.docx");
{% endhighlight %}

{% endtabs %}

Step 7: Add below code example to add a paragraph in the Word document.

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

Step 8: Add below code example to **save the Word document in ASP.NET**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Save the Word document and download as attachment.
document.Save("Sample.docx", FormatType.Docx, HttpContext.Current.Response, HttpContentDisposition.Attachment);
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Read-and-Save-document/Open-and-save-Word-document/ASP.NET).

By executing the program, you will get the **Word document** as follows.

![ASP.Net Web Open and save output Word document](ASP-NET_images/OpenAndSaveOutput.png)