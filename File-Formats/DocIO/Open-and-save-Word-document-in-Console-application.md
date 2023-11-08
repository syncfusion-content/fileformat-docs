---
title: Open and save Word document in Console Application | Syncfusion 
description: Open and save Word document in Console Application using .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Open and save Word document in Console Application

Syncfusion DocIO is a [.NET Word library](https://www.syncfusion.com/document-processing/word-framework/net/word-library) used to create, read, edit, and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **open and save Word document in Console Application**.

## Open and save Word document using .NET Core and Latest

The below steps illustrates open and save **Word document** in console application using **.NET Core**.

Step 1: Create a new **.NET Core console application** project.
![Create a C# Console application in Visual Studio](Console-Images/.NET/Console-Template-Net-Core.png)

Step 2: Install the [Syncfusion.DocIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.DocIO.Net.Core NuGet Package](Console-Images/.NET/Nuget-Package-NET-Core.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in **Program.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO; 
using Syncfusion.DocIO.DLS; 

{% endhighlight %}
{% endtabs %}

Step 4: Add the following code snippet in Program.cs file to **open an existing Word document in console application**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Open an existing Word document.
using (WordDocument document = new WordDocument(new FileStream("Input.docx", FileMode.Open, FileAccess.Read)));

{% endhighlight %}
{% endtabs %}

Step 5: Add below code example to **add a paragraph** in the Word document.

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

Step 6: Add below code example to **save the Word document in .NET Core console application**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a FileStream to save the Word file.
using (FileStream outputStream = new FileStream("Result.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
{
    //Save the Word file.
    document.Save(outputStream, FormatType.Docx);
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Read-and-Save-document/Open-and-save-Word-document/.NET-Standard).

By executing the program, you will get the **Word document** as follows.

![Output Word document in .NET Core console application](Blazor_Images/Blazor_Output.png)

## Open and save Word document in .NET Framework

The below steps illustrates open and save **Word document** in console application using **.NET Framework**.

Step 1: Create a new **.NET FrameWork console application** project.
![Create a C# Console application in Visual Studio](Console-Images/.NET-FrameWork/Console-Template-Net-FrameWork.png)

Step 2: Install [Syncfusion.DocIO.WinForms](https://www.nuget.org/packages/Syncfusion.DocIO.WinForms/) NuGet package as a reference to your Windows Forms application from the [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.DocIO.WinForms NuGet package](Console-Images/.NET-FrameWork/Nuget-Package-NET-FrameWork.png)

N> 1. The [Syncfusion.DocIO.WinForms](https://www.nuget.org/packages/Syncfusion.DocIO.WinForms/) is a dependency for Syncfusion Windows Forms GUI controls and is named with the suffix "WinForms". It contains platform-independent .NET Framework assemblies (compatible with versions 4.0, 4.5, 4.5.1, and 4.6) for the Word library and does not include any Windows Forms-related references or code. Therefore, we recommend using this package for .NET Framework Console applications.
N> 2. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in **Program.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;

{% endhighlight %}
{% endtabs %}

Step 4: Add the following code snippet in **Program.cs** file to **open an existing Word document in .NET FrameWork console application**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Open an existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx));

{% endhighlight %}
{% endtabs %}

Step 5: Add below code example to **add a paragraph** in the Word document.

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

Step 6: Add below code example to **save the Word document in .NET FrameWork console application**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the Word file.
document.Save("Result.docx");

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Read-and-Save-document/Open-and-save-Word-document/.NET-Framework).

By executing the program, you will get the **Word document** as follows.

![Output Word document in .NET FrameWork console application](Blazor_Images/Blazor_Output.png)