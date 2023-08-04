---
title: Convert an Excel document to PDF in UWP | Syncfusion
description: Convert an Excel document to PDF in UWP using Sycfusion .NET Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert an Excel document to PDF in UWP

Syncfusion XlsIO is a [.NET Core Excel library](https://www.syncfusion.com/document-processing/excel-framework/net-core/excel-library) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in UWP**.

## Steps to convert an Excel document to PDF in UWP

Step 1: Create a new C# Blank App (Universal Windows) project.
<img src="UWP_images\UWP_images_img4.png" alt="Create a UWP application project" width="100%" Height="Auto"/>

Step 2: Name the project.
<img src="UWP_images\UWP_images_img5.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Install the [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
<img src="UWP_images\UWP_images_img6.png" alt="Install Syncfusion.XlsIORenderer.Net.Core NuGet Package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components.

Step 4: Add a new button in **MainPage.xaml** as shown below.
{% tabs %}
{% highlight c# tabtitle="C#" %}
<Page
    x:Class="Convert_Excel_to_PDF.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Convert_Excel_to_PDF"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <Button x:Name="button" Content="Convert Excel to PDF" Click="OnButtonClicked" HorizontalAlignment="Center" VerticalAlignment="Center"/>
    </Grid>
</Page>
{% endhighlight %}
{% endtabs %}

Step 5: Include the following namespaces in the **MainPage.xaml.cs**.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.Pdf;
using Syncfusion.XlsIORenderer;
{% endhighlight %}
{% endtabs %}

Step 6: Include the below code snippet in the click event of the button in **MainPage.xaml.cs**, to **convert the Excel document to PDF** and save the **PDF** document as a physical file and open the file for viewing.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Load an existing file
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    using (Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx"))
    {
        IWorkbook workbook =application.Workbooks.Open(inputStream);

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
        SavePDF(pdfStream);
    }
}
{% endhighlight %}
{% endtabs %}

## Save PDF document in UWP
{% tabs %}
{% highlight c# tabtitle="C#" %}
//Saves the PDF document
private async void SavePDF(Stream outputStream)
{
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = "Sample";
        savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync("Sample.pdf", CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
        Stream st = fileStream.AsStreamForWrite();
        st.SetLength(0);
        st.Write((outputStream as MemoryStream).ToArray(), 0, (int)outputStream.Length);
        st.Flush();
        st.Dispose();
        fileStream.Dispose();
        MessageDialog msgDialog = new MessageDialog("Do you want to view the Document?", "File created.");
        UICommand yesCmd = new UICommand("Yes");
        msgDialog.Commands.Add(yesCmd);
        UICommand noCmd = new UICommand("No");
        msgDialog.Commands.Add(noCmd);
        IUICommand cmd = await msgDialog.ShowAsync();
        if (cmd == yesCmd)
        {
            // Launch the retrieved file
            bool success = await Windows.System.Launcher.LaunchFileAsync(stFile);
        }
    }
}
{% endhighlight %}
{% endtabs %}

By executing the program, you will get the **PDF document** as follows.

<img src="UWP_images\UWP_images_img7.png" alt="Install Syncfusion.ExcelToPdfConverter.WinForms NuGet Package" width="100%" Height="Auto"/>

Click [here](https://www.syncfusion.com/document-processing/excel-framework/uwp) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://ej2.syncfusion.com/aspnetcore/Excel/ExcelToPDF#/material3) in ASP.NET Core.