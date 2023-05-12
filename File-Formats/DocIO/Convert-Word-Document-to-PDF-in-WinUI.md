---
title: Convert Word document to PDF in WinUI | Syncfusion
description: Convert Word document to PDF without Microsoft Word or interop dependencies in WinUI application using WinUI Word (DocIO) library
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word document to PDF in WinUI

Syncfusion Essential DocIO is a [WinUI Word library](https://www.syncfusion.com/document-processing/word-framework/winui/word-library) used to create, read, edit, and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **create a Word document in WinUI**.

**Prerequisites:**
To use the WinUI 3 project templates, install the Windows App SDK extension for Visual Studio. For more details, refer [here](https://learn.microsoft.com/en-us/windows/apps/windows-app-sdk/set-up-your-development-environment?tabs=cs-vs-community%2Ccpp-vs-community%2Cvs-2022-17-1-a%2Cvs-2022-17-1-b).

## WinUI Desktop app

Step 1: Create a new C# WinUI Desktop app. Select Blank App, Packaged with WAP (WinUI 3 in Desktop) from the template and click the **Next** button.

![Create the WinUI Desktop app in Visual Studio](WinUI_Images/Create-Project-WinUI-WordtoPDF.png)

Step 2: Enter the project name and click **Create**.

![Create a project name for your new project](WinUI_Images/Project-Name-WinUI-WordtoPDF.png)

Step 4: Install [Syncfusion.DocIORenderer.NET](https://www.nuget.org/packages/Syncfusion.DocIORenderer.NET) NuGet package as a reference to your WinUI Desktop application from the [NuGet.org](https://www.nuget.org/).

![Install the DocIORenderer.NET NuGet package](WinUI_Images/Nuget-Package-WordtoPDF.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering a Syncfusion license key in your application to use our components.

Step 5: Add a new button to the **MainWindow.xaml** as shown below.

{% tabs %}

{% highlight c# tabtitle="C#" %}
<Window
    x:Class="Convert_Word_Document_to_PDF.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Convert_Word_Document_to_PDF"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Orientation="Horizontal" HorizontalAlignment="Center" VerticalAlignment="Center">
        <Button x:Name="button" Click="ConvertWordtoPDF">Convert Word to PDF</Button>
    </StackPanel>
</Window>

{% endhighlight %}

{% endtabs %}

Step 6: Include the following namespaces in the **MainWindow.xaml.cs** file.

{% tabs %}

{% highlight c# tabtitle="C#" %}
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIO;
using Syncfusion.DocIORenderer;
using Syncfusion.Pdf;
{% endhighlight %}

{% endtabs %}

Step 7: Add a new action method **ConvertWordtoPDF** in MainWindow.xaml.cs and include the below code snippet to **convert the Word document to PDF**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loading an existing Word document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Convert_Word_Document_to_PDF.Assets.Input.docx"), FormatType.Docx))
{
    //Instantiation of DocIORenderer for Word to PDF conversion
    using (DocIORenderer render = new DocIORenderer())
    {
        //Converts Word document into PDF document
        using (PdfDocument pdfDocument = render.ConvertToPDF(document))
        {
            //Save a PDF document to the stream.
            using MemoryStream outputStream = new();
            pdfDocument.Save(outputStream);

            //Save the stream as a Word document file in the local machine.
            SaveHelper.SaveAndLaunch("Sample.pdf", outputStream);
        }
    }                                              
}

{% endhighlight %}

{% endtabs %}

Step 8: Add a new SaveHelper.cs file. Create method in the name of SaveAndLaunch and Add below code example to save the PDF document as a physical file and open the file for viewing.

{% tabs %}

{% highlight c# tabtitle="C#" %}

public static async void SaveAndLaunch(string filename, MemoryStream stream)
{
    StorageFile storageFile;
    string extension = Path.GetExtension(filename);
    //Gets process windows handle to open the dialog in application process.
    IntPtr windowHandle = System.Diagnostics.Process.GetCurrentProcess().MainWindowHandle;
    if (!Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons"))
    {
        FileSavePicker savePicker = new();
        if (extension == ".docx")
        {
            savePicker.DefaultFileExtension = ".docx";
            savePicker.SuggestedFileName = filename;
            //Saves the file as Docx file.
            savePicker.FileTypeChoices.Add("DOCX", new List<string>() { ".docx" });
        }
        else if (extension == ".doc")
        {
            savePicker.DefaultFileExtension = ".doc";
            savePicker.SuggestedFileName = filename;
            //Saves the file as Doc file.
            savePicker.FileTypeChoices.Add("DOC", new List<string>() { ".doc" });
        }
        else if (extension == ".rtf")
        {
            savePicker.DefaultFileExtension = ".rtf";
            savePicker.SuggestedFileName = filename;
            //Saves the file as Xml file.
            savePicker.FileTypeChoices.Add("RTF", new List<string>() { ".rtf" });
        }
        else if (extension == ".pdf")
        {
            savePicker.DefaultFileExtension = ".pdf";
            savePicker.SuggestedFileName = filename;
            //Saves the file as Pdf file.
            savePicker.FileTypeChoices.Add("PDF", new List<string>() { ".pdf" });
        }

        WinRT.Interop.InitializeWithWindow.Initialize(savePicker, windowHandle);
        storageFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = ApplicationData.Current.LocalFolder;
        storageFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (storageFile != null)
    {
        using (IRandomAccessStream zipStream await storageFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Writes compressed data from memory to file.
            using Stream outstream = zipStream.AsStreamForWrite();
            outstream.SetLength(0);
            byte[] buffer = stream.ToArray();
            outstream.Write(buffer, 0, buffer.Length);
            outstream.Flush();
        }

        //Creates message dialog box. 
        MessageDialog msgDialog = new("Do you want to view the Document?", "File has been converted successfully");
        UICommand yesCmd = new("Yes");
        msgDialog.Commands.Add(yesCmd);
        UICommand noCmd = new("No");
        msgDialog.Commands.Add(noCmd);

        WinRT.Interop.InitializeWithWindow.Initialize(msgDialog, windowHandle);

        //Showing a dialog box. 
        IUICommand cmd = await msgDialog.ShowAsync();
        if (cmd.Label == yesCmd.Label)
        {
            //Launch the saved file. 
            await Windows.System.Launcher.LaunchFileAsync(storageFile);
        }
    }
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Getting-Started/WinUI/WinUI-Desktop-app).

By executing the program, you will get the **PDF document** as follows.

![WinUI Desktop output PDF document](WordToPDF_images/OutputImage.png)
