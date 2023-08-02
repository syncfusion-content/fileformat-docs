---
title: Convert an Excel document to PDF in WPF | Syncfusion
description: Convert an Excel document to PDF in WPF using Sycfusion .NET Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert an Excel document to PDF in WPF

Syncfusion XlsIO is a [.NET Excel library](https://www.syncfusion.com/document-processing/excel-framework/net/excel-library) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in WPF**.

## Steps to convert an Excel document to PDF in WPF

Step 1: Create a new WPF application project.
<img src="WPF_images\WPF_images_img4.png" alt="Create a WPF application project" width="100%" Height="Auto"/>

Step 2: Name the project, choose the framework and click **Create** button.
<img src="WPF_images\WPF_images_img5.png" alt="Name the project and choose the framework version" width="100%" Height="Auto"/>

Step 3: Install the [Syncfusion.ExcelToPdfConverter.Wpf](https://www.nuget.org/packages/Syncfusion.ExcelToPDFConverter.Wpf) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
<img src="WPF_images\WPF_images_img6.png" alt="Install Syncfusion.ExcelToPdfConverter.Wpf NuGet Package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components. 

Step 4: Add a new button in **MainWindow.xaml** as shown below.
{% tabs %}
{% highlight c# tabtitle="C#" %}
<Button Click="btnConvert_Click" Margin="0,0,10,12" VerticalAlignment="Bottom" Height="30" BorderBrush="LightBlue" HorizontalAlignment="Right" Width="180">
    <Button.Background>
        <LinearGradientBrush EndPoint="0.5,-0.04" StartPoint="0.5,1.04">
            <GradientStop Color="#FFD9E9F7" Offset="0"/>
            <GradientStop Color="#FFEFF8FF" Offset="1"/>
        </LinearGradientBrush>
    </Button.Background>
    <StackPanel Orientation="Horizontal" Height="23" Margin="0,0,0,-2.52" VerticalAlignment="Bottom" HorizontalAlignment="Right" Width="100">
        <Image Name="image2" Margin="2" HorizontalAlignment="Center" VerticalAlignment="Center" />
        <TextBlock Text="Convert Excel to PDF" Height="15.96" Width="126" Margin="0,4,0,3"/>
    </StackPanel>
</Button>
{% endhighlight %}
{% endtabs %}

Step 5: Include the following namespaces in the **MainWindow.xaml.cs**.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.Pdf;
using Syncfusion.ExcelToPdfConverter;
{% endhighlight %}
{% endtabs %}

Step 6: Include the below code snippet in **btnConvert_Click** to **convert an Excel document to PDF**.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize PDF document
  PdfDocument pdfDocument = new PdfDocument();

  //Convert Excel document into PDF document
  pdfDocument = converter.Convert();

  //Save the converted PDF document
  pdfDocument.Save("Sample.pdf");
}
{% endhighlight %}
{% endtabs %}

A complete working example of how to convert an Excel document to PDF in WPF is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/WPF/Convert%20Excel%20to%20PDF).

By executing the program, you will get the **PDF document** as follows.

<img src="WPF_images\WPF_images_img7.png" alt="Excel to PDF in WPF" width="100%" Height="Auto"/>

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://ej2.syncfusion.com/aspnetcore/Excel/ExcelToPDF#/material3) in ASP.NET Core.