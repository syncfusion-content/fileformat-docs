---
title: Convert an Excel document to PDF in Xamarin | Syncfusion
description: Convert an Excel document to PDF in Xamarin using Xamarin Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel Document to PDF in Xamarin

Syncfusion XlsIO is a [Xamarin Excel library](https://www.syncfusion.com/document-processing/excel-framework/xamarin/excel-library) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in Xamarin**.

## Steps to convert Excel document to PDF in Xamarin

Step 1: Create a new Xamarin.Forms application project.
<img src="XAMARIN_images\XAMARIN_images_img5.png" alt="Create a Xamarin application project" width="100%" Height="Auto"/>

Step 2: Name the project and click **Create** button.
<img src="XAMARIN_images\XAMARIN_images_img6.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Select a project template and required platforms to deploy the application. In this application the portable assemblies to be shared across multiple platforms, the .NET Standard code sharing strategy has been selected. For more details about code sharing refer [here](https://learn.microsoft.com/en-us/xamarin/cross-platform/app-fundamentals/code-sharing).

N> If .NET Standard is not available in the code sharing strategy, the Portable Class Library (PCL) can be selected.

<img src="XAMARIN_images\XAMARIN_images_img7.png" alt="Select the Template" width="100%" Height="Auto"/>

Step 4: Install the [Syncfusion.Xamarin.XlsIORenderer](https://www.nuget.org/packages/Syncfusion.Xamarin.XlsIORenderer) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
<img src="XAMARIN_images\XAMARIN_images_img8.png" alt="Install Syncfusion.Xamarin.XlsIORenderer NuGet Package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Add new Forms XAML page in **portable project**. If there is no XAML page is defined in the App class. Otherwise proceed to the next step.
<ul>
<li>
To add the new XAML page, right click on the project and select <b>Add > New Item</b> and add a Forms XAML Page from the list. Name it as MainXamlPage.
</li>
<li>
In App class of <b>portable project</b> (App.cs), replace the existing constructor of App class with the code snippet given below which invokes the <b>MainXamlPage</b>.
</li>
</ul>

{% tabs %}
{% highlight c# tabtitle="C#" %}
public App()
{
    // The root page of your application
    MainPage = new MainXamlPage();
}
{% endhighlight %}
{% endtabs %}

Step 6: In the **MainXamlPage.xaml** add new button as shown below.
{% tabs %}
{% highlight c# tabtitle="C#" %}
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Convert_Excel_to_PDF.MainPage">

    <StackLayout VerticalOptions="Center">
       <Button Text="Convert Excel to PDF" Clicked="OnButtonClicked" HorizontalOptions="Center"/>
    </StackLayout>
</ContentPage>
{% endhighlight %}
{% endtabs %}

Step 7: Include the following namespace in the **MainXamlPage.xaml.cs** file.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.Pdf;
using Syncfusion.XlsIORenderer;
{% endhighlight %}
{% endtabs %}

Step 8: Include the below code snippet in the click event of the button in **MainXamlPage.xaml.cs** to **convert an Excel document to PDF** and save it in a stream.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
    using(Stream inputStream = executingAssembly.GetManifestResourceStream("Convert-Excel-to-PDF.InputTemplate.xlsx"))
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

        //Save the stream as a file in the device and invoke it for viewing.
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.pdf", "application/pdf", pdfStream);
    }
}  
{% endhighlight %}
{% endtabs %}

## Helper files for Xamarin

Refer the below helper files and add them into the mentioned project. These helper files allow you to save the stream as a physical file and open the file for viewing.

<table>
  <tr>
  <td>
    <b>Project</b>
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
    Portable project
  </td>
  <td>
    ISave.cs
  </td>
  <td>Represent the base interface for save operation
  </td>
  </tr>
  <tr>
  <td rowspan="2">
    iOS project
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
    PreviewControllerDS.cs
  </td>
  <td>
    Helper class for viewing the <b>Excel document</b> in iOS device
  </td>
  </tr>
  <tr>
  <td>
    Android project
  </td>
  <td>
   SaveAndroid.cs
  </td>
  <td>Save implementation for Android device
  </td>
  </tr>
  <tr>
  <td>
    UWP project
  </td>
  <td>
    SaveWindows.cs
  </td>
  <td>Save implementation for UWP device.
  </td>
  </tr>
</table>

Compile and execute the application. Now this application **convert an Excel document to PDF**.

By executing the program, you will get the **PDF document** as follows.

<img src="XAMARIN_images\XAMARIN_images_img9.png" alt="Excel to PDF in Xamarin" width="100%" Height="Auto"/>

Click [here](https://www.syncfusion.com/document-processing/excel-framework/xamarin) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://ej2.syncfusion.com/aspnetcore/Excel/ExcelToPDF#/material3) in ASP.NET Core.