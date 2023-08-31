---
title: Convert PDF document to Image in WPF application | Syncfusion
description: Learn how to convert a PDF file to Image in WPF with easy steps using System Drawing library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert PDF file to Image in WPF

The Syncfusion PDF to Image converter is a .NET library used to convert PDF document to image in WPF application.

## Steps to convert PDF document to Image in WPF

Step 1: Create a new WPF application project.
![Create WPF sample](conversion_images/WPF_Step1.png)  

In project configuration window, name your project and select Create.
![WPF configuration window](conversion_images/WPF_Step2.png)

Step 2: Install the Syncfusion.PdfToImageConverter.Base NuGet package as a reference to your WPF application [NuGet.org](https://www.nuget.org/).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in the MainWindow.xaml.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.PdfToImageConverter;
using System.Drawing;
using System.IO;
using System.Windows;

{% endhighlight %}

Step 4: Add a new button in MainWindow.xaml to convert PDF document to Image file as follows.

{% highlight c# tabtitle="C#" %}

<Grid HorizontalAlignment="Left" Margin="0,0,0,-0.333" Width="793">
<Button Content="Convert PDF to Image" HorizontalAlignment="Left" Margin="318,210,0,0" VerticalAlignment="Top" Width="166" Click=" btnCreate_Click " Height="19"/>
<TextBlock HorizontalAlignment="Left" Margin="222,177,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Height="17"/>
<TextBlock HorizontalAlignment="Left" Margin="291,175,0,0" TextWrapping="Wrap" Text="Click the button to convert PDF to Image." VerticalAlignment="Top"/>
</Grid>

{% endhighlight %}

Step 5: Add the following code in btnCreate_Click to convert PDF document to Image using Convert method in PdfToImageConverter class. 

{% highlight c# tabtitle="C#" %}

//Initialize PDF to Image converter.
PdfToImageConverter imageConverter = new PdfToImageConverter();
//Load the PDF document as a stream
FileStream inputStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.ReadWrite);
imageConverter.Load(inputStream);
//Convert PDF to Image.
Stream outputStream = imageConvertor.Convert(0, false, false);
Bitmap image = new Bitmap(outputStream);
image.Save("sample.png");

{% endhighlight %}

By executing the program, you will get the image as follows.
![Convert PDFToImage WPF output](imageconversion_images/pdftoimageoutput.png)