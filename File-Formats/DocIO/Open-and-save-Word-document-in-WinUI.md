---
title: Open and save Word document in WinUI | Syncfusion
description: Open and save Word document in WinUI application using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Open and Save Word document in WinUI

Syncfusion DocIO is a [WinUI Word library](https://www.syncfusion.com/document-processing/word-framework/winui/word-library) used to **create, read, and edit Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **open and save a Word document in WinUI**.

**Prerequisites:**
To use the WinUI 3 project templates, install the Windows App SDK extension for Visual Studio. For more details, refer [here](https://learn.microsoft.com/en-us/windows/apps/windows-app-sdk/set-up-your-development-environment?tabs=cs-vs-community%2Ccpp-vs-community%2Cvs-2022-17-1-a%2Cvs-2022-17-1-b).


## WinUI Desktop app

Step 1: Create a new C# WinUI Desktop app. Select Blank App, Packaged with WAP (WinUI 3 in Desktop) from the template and click the **Next** button.

Step 2: Enter the project name and click **Create**.

Step 3: Set the Target version to Windows 10, version 2004 (build 19041) and the Minimum version to Windows 10, version 1809 (build 17763) and then click **OK**.

Step 4: Install the [Syncfusion.DocIO.NET](https://www.nuget.org/packages/Syncfusion.DocIO.Net) NuGet package as a reference to your project from the [NuGet.org](https://www.nuget.org/).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering a Syncfusion license key in your application to use our components.

Step 5: Add a new button to the **MainWindow.xaml** as shown below.

{% tabs %}

{% highlight XML %}
<Window
    x:Class="CreateWordSample.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:CreateWordSample"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Orientation="Horizontal" HorizontalAlignment="Center" VerticalAlignment="Center">
        <Button x:Name="button" Click="OpenAndSaveDocument">Open and save Word document</Button>
    </StackPanel>
</Window>
{% endhighlight %}

{% endtabs %}

Step 6: Include the following namespaces in the **MainWindow.xaml.cs** file.

{% tabs %}

{% highlight c# tabtitle="C#" %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% endtabs %}

Step 7: Add a new action method **OpenAndSaveDocument** in MainWindow.xaml.cs and include the below code snippet to **open an existing Word document in WinUI Desktop app**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
    //"App" is the class of Portable project.
    Assembly assembly = typeof(Open_and_save_Word_document).GetTypeInfo().Assembly;
    using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Open_and_save_Word_document.Assets.Input.docx"), FormatType.Docx))
    {
    
    }
}
{% endhighlight %}

{% endtabs %}

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

Step 9: Add below code example to **save the Word document in WinUI Desktop app**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Save a Word document to the stream.
using MemoryStream outputStream = new();
document.Save(outputStream, FormatType.Docx);
//Save the stream as a Word document file in the local machine.
Save(outputStream, "Sample.docx");
{% endhighlight %}

{% endtabs %}

By executing the program, you will get the **Word document** as follows.

![WinUI Desktop open and save output Word document](WinUI_Images/OpenAndSaveOutput.png)

## WinUI UWP app

Step 1: Create a new C# WinUI UWP app. Select Blank App (WinUI 3 in UWP)from the template and **click** the Next button.

N> To get the UWP Experimental project templates and build UWP apps with WinUI 3, you should download the [Windows App SDK Experimental Extension](https://marketplace.visualstudio.com/items?itemName=ProjectReunion.MicrosoftProjectReunionPreview) for Visual Studio.

Step 2: Enter the project name and click **Create**.

Step 3: Set the Target version to Windows 10, version 2004 (build 19041) and the Minimum version to Windows 10, version 1809 (build 17763) and then click **OK**.

Step 4: Install the [Syncfusion.DocIO.NET](https://www.nuget.org/packages/Syncfusion.DocIO.Net) NuGet package as a reference to your project from the [NuGet.org](https://www.nuget.org/).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering a Syncfusion license key in your application to use our components.

Step 5: Add a new button in the **MainPage.xaml** as shown below.

{% tabs %}

{% highlight XML %}

<Page
    x:Class="CreateWordSample.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:CreateWordSample1"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <StackPanel Orientation="Horizontal" HorizontalAlignment="Center" VerticalAlignment="Center">
        <Button x:Name="button" Click="OpenAndSaveDocument">Open and save Word document</Button>
    </StackPanel>
</Page>

{% endhighlight %}

{% endtabs %}

Step 6: Include the following namespaces in the **MainPage.xaml.cs** file.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO.DLS;
using Syncfusion.DocIO;

{% endhighlight %}

{% endtabs %}

Step 7: Add a new action method **OpenAndSaveDocument** in MainPage.xaml.cs and include the below code snippet to **open an existing Word document in WinUI UWP app**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
    //"App" is the class of Portable project.
    Assembly assembly = typeof(Open_and_save_Word_document).GetTypeInfo().Assembly;
    using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Open_and_save_Word_document.Assets.Input.docx"), FormatType.Docx))
    {
    
    }
}
{% endhighlight %}

{% endtabs %}

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

Step 9: Add below code example to **save the Word document in WinUI UWP app**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Save the Word document to the MemoryStream.
using (MemoryStream stream = new MemoryStream())
{
    document.Save(stream, FormatType.Docx);
    //Save the stream as a Word document file in the local machine.
    Save(stream, "Sample.docx");
}
{% endhighlight %}

{% endtabs %}

Step 10: Add below code example to save the Word document as a physical file and open the file for viewing.

{% tabs %}

{% highlight c# tabtitle="C#" %}
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".docx";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file.
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file.
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% endtabs %}

By executing the program, you will get the **Word document** as follows.

![WinUI UWP open and save output Word document](WinUI_Images/OpenAndSaveOutput.png)
