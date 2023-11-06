---
title: Convert an Excel document to PDF in WinUI | Syncfusion
description: Convert an Excel document to PDF in WinUI using Sycfusion .NET Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert an Excel document to PDF in WinUI

Syncfusion XlsIO is a [WinUI Excel library](https://www.syncfusion.com/document-processing/excel-framework/winui/excel-library) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in WinUI**.

## Prerequisites
To use the WinUI 3 project templates, install the Windows App SDK extension for Visual Studio. For more details, refer [here](https://learn.microsoft.com/en-us/windows/apps/windows-app-sdk/set-up-your-development-environment?tabs=cs-vs-community%2Ccpp-vs-community%2Cvs-2022-17-1-a%2Cvs-2022-17-1-b).

## WinUI Desktop app

Step 1: Create a new C# WinUI Desktop app. Select Blank App, Packaged (WinUI 3 in Desktop) project.
<img src="WinUI_images\WinUI_images_img6.png" alt="Create a WinUI Desktop application project" width="100%" Height="Auto"/>

Step 2: Name the project and click **Create** button.
<img src="WinUI_images\WinUI_images_img7.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Install the [Syncfusion.XlsIORenderer.Net](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.NET) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
<img src="WinUI_images\WinUI_images_img8.png" alt="Install Syncfusion.XlsIORenderer.Net NuGet Package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components.

Step 4: Add a new button in **MainWindow.xaml** as shown below.
{% tabs %}
{% highlight c# tabtitle="C#" %}
<Window
    x:Class="Convert_Excel_to_PDF.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Convert_Excel_to_PDF"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Orientation="Horizontal" HorizontalAlignment="Center" VerticalAlignment="Center">
        <Button x:Name="myButton" Click="ConvertExceltoPDF">Convert Excel to PDF</Button>
    </StackPanel>
</Window>
{% endhighlight %}
{% endtabs %}

Step 5: Include the following namespaces in the **MainWindow.xaml.cs**.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.Pdf;
using Syncfusion.XlsIORenderer;
{% endhighlight %}
{% endtabs %}

Step 6: Include the below code snippet in the new action method of **ConvertExceltoPDF** in **MainWindow.xaml.cs**  to **convert an Excel document to PDF**.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Load an existing file
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    using (Stream inputStream = assembly.GetManifestResourceStream("Convert_Excel_to_PDF.InputTemplate.xlsx"))
    {
        IWorkbook workbook = application.Workbooks.Open(inputStream);

        //Initialize XlsIO renderer.
        XlsIORenderer renderer = new XlsIORenderer();

        //Convert Excel document into PDF document 
        PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

        //Create the MemoryStream to save the converted PDF.      
        MemoryStream pdfStream = new MemoryStream();

        //Save the converted PDF document to MemoryStream.
        pdfDocument.Save(pdfStream);
        pdfStream.Position = 0;

        // Save the PDF file or perform any other action with the PDF
        SaveHelper.SaveAndLaunch("Sample.pdf", pdfStream); 
    }
}
{% endhighlight %}
{% endtabs %}

## Save PDF document in WinUI
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
        
        if (extension == ".pdf")
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

A complete working example of how to convert an Excel document to PDF in WinUI is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/WinUI/Convert%20Excel%20to%20PDF).

By executing the program, you will get the **PDF document** as follows.

<img src="WinUI_images\WinUI_images_img9.png" alt="Excel to PDF in WinUI" width="100%" Height="Auto"/>

Click [here](https://www.syncfusion.com/document-processing/excel-framework/winui) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://ej2.syncfusion.com/aspnetcore/Excel/ExcelToPDF#/material3) in ASP.NET Core.
