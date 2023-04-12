---
title: Open and save Word document in UWP | Syncfusion
description: Open and save Word document in UWP application using Syncfusion UWP Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Open and Save Word document in UWP

Syncfusion DocIO is a [UWP Word library](https://www.syncfusion.com/document-processing/word-framework/uwp/word-library) used to **create, read, and edit Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **open and save a Word document in UWP**.

## Steps to open and save Word document programmatically in UWP:

Step 1: Create a new C# Blank App (Universal Windows) project.

Step 2: Install the [Syncfusion.DocIO.UWP](https://www.nuget.org/packages/Syncfusion.DocIO.UWP/) NuGet package as a reference to your UWP application from [NuGet.org](https://www.nuget.org/).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in the MainPage.xaml.cs file.

{% tabs %}

{% highlight c# tabtitle="C#" %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% endtabs %}

Step 4: Add a new button in the MainPage.xaml as shown below.

{% tabs %}

{% highlight XML %}

<Page
    x:Class="OpenAndSaveWordSample.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:OpenAndSaveWordSample"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <Button x:Name="button" Content="Open and Save Word document" Click="OnButtonClicked" HorizontalAlignment="Center" VerticalAlignment="Center"/>
    </Grid>
</Page>

{% endhighlight %}

{% endtabs %}

Step 5: Include the below code snippet in the click event of the button in MainPage.xaml.cs, to **Open an existing Word document in UWP**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
    //Load an existing Word document.
    Assembly assembly = typeof(Open_and_save_Word_document).GetTypeInfo().Assembly;
    using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Open_and_save_Word_document.Assets.Input.docx"), FormatType.Docx))
    {
    
    }
}
{% endhighlight %}

{% endtabs %}

Step 6: Add below code example to add a paragraph in the Word document.

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

Step 7: Add below code example to **save the Word document in UWP**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Save a Word document to the MemoryStream.
MemoryStream stream = new MemoryStream();
//Save the Word document to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
//Save the stream as Word document file in local machine
Save(stream, "Sample.docx");
{% endhighlight %}

{% endtabs %}

Step 8: Add below code example to save the Word document as a physical file and open the file for viewing.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Save the Word document.
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

![UWP open and save output Word document](UWP_images/OpenAndSaveOutput.png)