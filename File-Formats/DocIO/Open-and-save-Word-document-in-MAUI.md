---
title: Open and save Word document in .NET MAUI | Syncfusion
description: Open and save Word document in .NET MAUI application using Syncfusion .NET MAUI Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Open and Save Word document in .NET MAUI

Syncfusion DocIO is a [.NET MAUI Word library](https://www.syncfusion.com/document-processing/word-framework/maui/word-library) used to **create, read, and edit Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **open and save a Word document in .NET MAUI**.

**Prerequisites:**
To create .NET Multi-platform App UI (.NET MAUI) apps, you need the latest versions of Visual Studio 2022 and .NET 6. For more details, refer [here](https://learn.microsoft.com/en-us/dotnet/maui/get-started/installation?view=net-maui-7.0&tabs=vswin).

## Steps to open and save Word document programmatically in .NET MAUI

Step 1: Create a new C# .NET MAUI app. Select **.NET MAUI App (Preview)** from the template and click the **Next** button.

Step 2: Enter the project name and click **Create**.

Step 3: Install the [Syncfusion.DocIO.NET](https://www.nuget.org/packages/Syncfusion.DocIO.Net) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering a Syncfusion license key in your application to use our components.

Step 4: Add a new button to the **MainPage.xaml** as shown below.

{% tabs %}

{% highlight XML %}
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
            xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
            x:Class="CreateWordSample.MainPage"
            BackgroundColor="{DynamicResource SecondaryColor}">
    <ScrollView>
        <Grid RowSpacing="25" RowDefinitions="Auto,Auto,Auto,Auto,*"
            Padding="{OnPlatform iOS='30,60,30,30', Default='30'}">
            <Button 
                Text="Create Document"
                FontAttributes="Bold"
                Grid.Row="0"
                SemanticProperties.Hint="Creates Word document you click"
                Clicked="CreateDocument"
                HorizontalOptions="Center" />
        </Grid>
    </ScrollView>
</ContentPage>
{% endhighlight %}

{% endtabs %}

Step 5: Include the following namespaces in the **MainPage.xaml.cs** file.

{% tabs %}

{% highlight c# tabtitle="C#" %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% endtabs %}

Step 6: Add a new action method **OpenAndSaveDocument** in MainPage.xaml.cs and include the below code snippet to **open an existing Word document in .NET MAUI**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//"App" is the class of Portable project
Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Input.docx")))
{

}
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

Step 8: Add below code example to **save the Word document in .NET MAUI**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Saves the Word document to the memory stream.
using MemoryStream ms = new();
document.Save(ms, FormatType.Docx);
ms.Position = 0;
//Save the memory stream as a file.
SaveService saveService = new();
saveService.SaveAndView("Sample.docx", "application/msword", ms);
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Read-and-Save-document/Open-and-save-Word-document/.NET-MAUI).

By executing the program, you will get the **Word document** as follows.

![MAUI open and save output Word document](MAUI_Images/OpenAndSaveOutput.png)

## Helper files for .NET MAUI

Download the helper files from this [link](https://www.syncfusion.com/downloads/support/directtrac/general/ze/HelperFiles_DocIO-2028573617.zip) and add them into the mentioned project. These helper files allow you to save the stream as a physical file and open the file for viewing.

<table>
  <tr>
  <td>
    <b>Folder Name</b>
  </td>
  <td>
    <b>File Name</b>
  </td>
  <td>
    <b>Summary</b>
  </td>
  </tr>
  <tr>
  <td>
    .NET MAUI Project
  </td>
  <td>
    SaveService.cs
  </td>
  <td>Represent the base class for save operation.
  </td>
  </tr>
  <tr>
  <td>
    Windows
  </td>
  <td>
    SaveWindows.cs
  </td>
  <td>Save implementation for Windows.
  </td>
  </tr>
  <tr>
  <td>
    Android
  </td>
  <td>
    SaveAndroid.cs
  </td>
  <td>Save implementation for Android device.
  </td>
  </tr>
  <tr>
  <td>
    Mac Catalyst
  </td>
  <td>
    SaveMac.cs
  </td>
  <td>Save implementation for Mac Catalyst device.
  </td>
  </tr>
  <tr>
  <td rowspan="2">
    iOS
  </td>
  <td>
    SaveIOS.cs
  </td>
  <td>
    Save implementation for iOS device
  </td>
  </tr>
  <tr>
  <td>
    PreviewControllerDS.cs<br/>QLPreviewItemFileSystem.cs
  </td>
  <td>
    Helper classes for viewing the <b>Word document</b> in iOS device
  </td>
  </tr>
</table>


