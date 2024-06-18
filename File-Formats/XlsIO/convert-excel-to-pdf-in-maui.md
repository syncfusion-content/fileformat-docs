---
title: Convert an Excel document to PDF in .NET MAUI | Syncfusion
description: Convert an Excel document to PDF in .NET MAUI using .NET MAUI Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel document to PDF in .NET MAUI

Syncfusion XlsIO is a [.NET MAUI Excel library](https://www.syncfusion.com/document-processing/excel-framework/maui/excel-library) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in .NET MAUI**.

## Prerequisites
To create .NET Multi-platform App UI (.NET MAUI) apps, you need the latest versions of Visual Studio 2022 and .NET 6. For more details, refer [here](https://learn.microsoft.com/en-us/dotnet/maui/get-started/installation?view=net-maui-7.0&tabs=vswin).

## Steps to convert Excel document to PDF in .NET MAUI

Step 1: Create a new C# .NET MAUI application project.

![Create a .NET MAUI application in visual studio](MAUI_images\MAUI_images_img5.png)

Step 2: Name the project and click **Create** button.

![Name the project](MAUI_images\MAUI_images_img6.png)

Step 3: Install the [Syncfusion.XlsIORenderer.Net](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.NET) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.XlsIORenderer.Net NuGet Package](MAUI_images\MAUI_images_img7.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering a Syncfusion license key in your application to use our components.

Step 4: Add a new button to the **MainPage.xaml** as shown below.
{% tabs %}
{% highlight c# tabtitle="C#" %}

<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Convert_Excel_to_PDF.MainPage">
    <ScrollView>
        <Grid RowSpacing="25" RowDefinitions="Auto,Auto,Auto,Auto,*"
            Padding="{OnPlatform iOS='30,60,30,30', Default='30'}">
            <Button 
                Text="Convert Excel to PDF"
                FontAttributes="Bold"
                Grid.Row="0"
                SemanticProperties.Hint="Convert Excel to PDF"
                Clicked="ConvertExceltoPDF"
                HorizontalOptions="Center" />
        </Grid>
    </ScrollView>
</ContentPage>
{% endhighlight %}
{% endtabs %}

Step 5: Include the following namespaces in the **MainPage.xaml.cs** file.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.Pdf;
using Syncfusion.XlsIORenderer;
{% endhighlight %}
{% endtabs %}

Step 6: Add a new action method **ConvertExceltoPDF** in MainPage.xaml.cs and include the below code snippet to **convert an Excel document to PDF**.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
    using (Stream inputStream = executingAssembly.GetManifestResourceStream("Convert_Excel_to_PDF.InputTemplate.xlsx"))
    {
        // Open the workbook.
        IWorkbook workbook = application.Workbooks.Open(inputStream);

        // Instantiate the Excel to PDF renderer.
        XlsIORenderer renderer = new XlsIORenderer();

        //Convert Excel document into PDF document 
        PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

        //Create the MemoryStream to save the converted PDF.      
        MemoryStream pdfStream = new MemoryStream();

        //Save the converted PDF document to MemoryStream.
        pdfDocument.Save(pdfStream);
        pdfStream.Position = 0;

        //save and Launch the PDF document
        SaveService saveService = new();
        saveService.SaveAndView("Sample.pdf", "application/pdf", pdfStream);
    }
}
{% endhighlight %}
{% endtabs %}

## Helper files for .NET MAUI

Refer the below helper files and add them into the mentioned project. These helper files allow you to save the stream as a physical file and open the file for viewing.

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
    {{'[.NET MAUI Project](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF)'| markdownify }}
  </td>
  <td>
    {{'[SaveService.cs](https://github.com/SyncfusionExamples/XlsIO-Examples/blob/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Services/SaveService.cs)'| markdownify }}
  </td>
  <td>Represent the base class for save operation.
  </td>
  </tr>
  <tr>
  <td>
    {{'[Windows](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/Windows)'| markdownify }}
  </td>
  <td>
    {{'[SaveWindows.cs](https://github.com/SyncfusionExamples/XlsIO-Examples/blob/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/Windows/SaveWindow.cs)'| markdownify }}
  </td>
  <td>Save implementation for Windows.
  </td>
  </tr>
  <tr>
  <td>
    {{'[Android](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/Android)'| markdownify }}
  </td>
  <td>
    {{'[SaveAndroid.cs](https://github.com/SyncfusionExamples/XlsIO-Examples/blob/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/Android/SaveAndroid.cs)'| markdownify }}
  </td>
  <td>Save implementation for Android device.
  </td>
  </tr>
  <tr>
  <td>
    {{'[Mac Catalyst](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/MacCatalyst)'| markdownify }}
  </td>
  <td>
    {{'[SaveMac.cs](https://github.com/SyncfusionExamples/XlsIO-Examples/blob/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/MacCatalyst/SaveMac.cs)'| markdownify }}
  </td>
  <td>Save implementation for Mac Catalyst device.
  </td>
  </tr>
  <tr>
  <td rowspan="2">
    {{'[iOS](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/iOS)'| markdownify }}
  </td>
  <td>
    {{'[SaveIOS.cs](https://github.com/SyncfusionExamples/XlsIO-Examples/blob/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/iOS/SaveIOS.cs)'| markdownify }}
  </td>
  <td>
    Save implementation for iOS device
  </td>
  </tr>
  <tr>
  <td>
     {{'[PreviewControllerDS.cs](https://github.com/SyncfusionExamples/XlsIO-Examples/blob/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/iOS/PreviewControllerDS.cs)'| markdownify }}<br/>{{'[QLPreviewItemFileSystem.cs](https://github.com/SyncfusionExamples/XlsIO-Examples/blob/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF/ConvertExceltoPDF/Platforms/iOS/QLPreviewItemFileSystem.cs)'| markdownify }}
  </td>
  <td>
    Helper classes for viewing the <b>Excel document</b> in iOS device
  </td>
  </tr>
</table>

A complete working example of how to convert an Excel document to PDF in .NET MAUI is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/.NET%20MAUI/ConvertExceltoPDF).

By executing the program, you will get the **PDF document** as follows.

![Output File](MAUI_images\MAUI_images_img8.png)

Click [here](https://www.syncfusion.com/document-processing/excel-framework/maui) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://ej2.syncfusion.com/aspnetcore/Excel/ExcelToPDF#/material3) in ASP.NET Core.
