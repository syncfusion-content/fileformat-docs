---
title: Convert Word to Image in C# | DocIO | Syncfusion
description: Learn how to convert a Word document to image using the .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Rendering / Converting Word document to Image in Word Library

The Essential DocIO converts the Word document to images using the [RenderAsImages](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_RenderAsImages_Syncfusion_DocIO_DLS_ImageType_) method.

To quickly start converting a Word document to an image, please check out this video:
{% youtube "https://www.youtube.com/watch?v=hoV3i7nl85I" %}

Refer to the following links for assemblies and NuGet packages required based on platforms to convert the Word document to image.

* [Word to image conversion assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-image) 
* [Word to image conversion NuGet packages](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-image)

The following namespaces are required to compile the code in this topic:

**For WPF, Windows Forms, ASP.NET and ASP.NET MVC applications**
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.OfficeChart
* using Syncfusion.OfficeChartToImageConverter

**For ASP.NET Core, Blazor, Xamarin, WinUI and .NET MAUI applications**
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocIORenderer

T> 1. You can get the good quality converted images by specifying the image type as Metafile in the platforms targeting .NET Framework.
T> 2. You can specify the quality of the converted charts by setting the scaling mode.

## Convert the entire Word to images

You can convert an entire Word document to images.

The following code example illustrates how to convert the entire Word document to images.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
    //Load file stream into Word document.
    using (WordDocument wordDocument = new WordDocument(docStream, FormatType.Docx))
    {
        //Create a new instance of DocIORenderer class.
        using (DocIORenderer render = new DocIORenderer())
        {
            //Convert the entire Word document to images.
            Stream[] imageStreams = wordDocument.RenderAsImages(); 
            int i = 0;
            foreach (Stream stream in imageStreams)
            {
                //Reset the stream position.
                stream.Position = 0;
                //Save the stream as file.
                using (FileStream fileStreamOutput = File.Create("WordToImage_" + i + ".jpeg"))
                {
                    stream.CopyTo(fileStreamOutput);
                }
                i++;
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load an existing Word document.
using(WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx))
{
    //Initialize the ChartToImageConverter for converting charts during Word to image conversion.
    wordDocument.ChartToImageConverter = new ChartToImageConverter();
    //Set the scaling mode for charts (Normal mode reduces the file size).
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
    //Convert the entire Word document to images.
    Image[] images = wordDocument.RenderAsImages(ImageType.Bitmap);
    int i = 0;
    foreach (Image image in images)
    {
        //Save the image as jpeg.
        image.Save("WordToImage_" + i + ".jpeg", ImageFormat.Jpeg);
        i++;
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load an existing Word document.
Using wordDocument As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Initialize the ChartToImageConverter for converting charts during Word to image conversion.
    wordDocument.ChartToImageConverter = New ChartToImageConverter()
    'Set the scaling mode for charts (Normal mode reduces the file size).
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
    'Convert the entire Word document to images.
    Dim images As Image() = wordDocument.RenderAsImages(ImageType.Bitmap)
    Dim i = 0
    For Each image As Image In images
        'Save the image as jpeg.
        image.Save("WordToImage_" & i & ".jpeg", ImageFormat.Jpeg)
        i += 1
    Next
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Convert-Word-to-image).

## Convert specific page of Word to image

You can convert a specific page of the Word document into an image and use it for a thumbnail.

The following code example illustrates how to convert a specific page in a Word document into an image.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
    //Load file stream into Word document.
    using (WordDocument wordDocument = new WordDocument(docStream, FormatType.Docx))
    {
        //Create a new instance of DocIORenderer class.
        using (DocIORenderer render = new DocIORenderer())
        {
            //Convert the first page of the Word document into an image.
            Stream imageStream = wordDocument.RenderAsImages(0, ExportImageFormat.Jpeg); 
            //Reset the stream position.
            imageStream.Position = 0;
            //Save the stream as file.
            using (FileStream fileStreamOutput = File.Create("WordToImage.jpeg"))
            {
                imageStream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load an existing Word document.
using(WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx))
{
    //Initialize the ChartToImageConverter for converting charts during Word to image conversion.
    wordDocument.ChartToImageConverter = new ChartToImageConverter();
    //Set the scaling mode for charts (Normal mode reduces the file size).
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
    //Convert the first page of the Word document into an image.
    Image image = wordDocument.RenderAsImages(0, ImageType.Bitmap);
    //Save the image as jpeg.
    image.Save("WordToImage.jpeg", ImageFormat.Jpeg);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load an existing Word document.
Using wordDocument As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Initialize the ChartToImageConverter for converting charts during Word to image conversion.
    wordDocument.ChartToImageConverter = New ChartToImageConverter()
    'Set the scaling mode for charts (Normal mode reduces the file size).
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
    'Convert the first page of the Word document into an image.
    Dim image As Image = wordDocument.RenderAsImages(0, ImageType.Bitmap)
    'Save the image as jpeg.
    image.Save("WordToImage.jpeg", ImageFormat.Jpeg)
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/First-page-of-Word-to-image).

## Convert a specific range of pages in Word to an image

Users can convert a specific range of pages in a Word document into images.

The following code example illustrates how to convert a specific range of pages in a Word document into images.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
    //Load file stream into Word document.
    using (WordDocument wordDocument = new WordDocument(docStream, FormatType.Docx))
    {
        //Create a new instance of DocIORenderer class.
        using (DocIORenderer render = new DocIORenderer())
        {
            //Convert a specific range of pages in Word document to images.
            Stream[] imageStreams = wordDocument.RenderAsImages(1, 2); 
            int i = 0;
            foreach (Stream stream in imageStreams)
            {
                //Reset the stream position.
                stream.Position = 0;
                //Save the stream as file.
                using (FileStream fileStreamOutput = File.Create("WordToImage_" + i + ".jpeg"))
                {
                    stream.CopyTo(fileStreamOutput);
                }
                i++;
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load an existing Word document.
using(WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx))
{
    //Initialize the ChartToImageConverter for converting charts during Word to image conversion.
    wordDocument.ChartToImageConverter = new ChartToImageConverter();
    //Set the scaling mode for charts (Normal mode reduces the file size).
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
    //Convert a specific range of pages in Word document to images.
    Image[] images = wordDocument.RenderAsImages(1, 2, ImageType.Bitmap);
    int i = 0;
    foreach (Image image in images)
    {
        //Save the image as jpeg.
        image.Save("WordToImage_" + i + ".jpeg", ImageFormat.Jpeg);
        i++;
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load an existing Word document.
Using wordDocument As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Initialize the ChartToImageConverter for converting charts during Word to image conversion.
    wordDocument.ChartToImageConverter = New ChartToImageConverter()
    'Set the scaling mode for charts (Normal mode reduces the file size).
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
    'Convert the entire Word document to images.
    Dim images As Image() = wordDocument.RenderAsImages(1, 2, ImageType.Bitmap)
    Dim i = 0
    For Each image As Image In images
        'Save the image as jpeg.
        image.Save("WordToImage_" & i & ".jpeg", ImageFormat.Jpeg)
        i += 1
    Next
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Specific-range-of-pages-Word-to-image).

## Custom image resolution

The following code snippet illustrates how to convert a Word document to an image using custom image resolution.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//DocIO only supports Word to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platform.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load an existing Word document.
using (WordDocument wordDocument = new WordDocument(@"Template.docx", FormatType.Docx))
{
    //Initialize the ChartToImageConverter for converting charts during Word to image conversion.
    wordDocument.ChartToImageConverter = new ChartToImageConverter();
    //Set the scaling mode for charts (Normal mode reduces the file size).
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
    //Convert the word document to images.
    Image[] images = wordDocument.RenderAsImages(ImageType.Metafile);
    //Declare the variables to hold custom width and height.
    int customWidth = 1500;
    int customHeight = 1500;
    foreach (Image image in images)
    {
        MemoryStream stream = new MemoryStream();
        image.Save(stream, ImageFormat.Png);
        //Create a bitmap of specific width and height.
        Bitmap bitmap = new Bitmap(customWidth, customHeight, PixelFormat.Format32bppPArgb);
        //Get the graphics from an image.
        Graphics graphics = Graphics.FromImage(bitmap);
        //Set the resolution.
        bitmap.SetResolution(300, 300);
        //Recreate the image in custom size.
        graphics.DrawImage(System.Drawing.Image.FromStream(stream), new Rectangle(0, 0, bitmap.Width, bitmap.Height));
        //Save the image as a bitmap.
        bitmap.Save(@"ImageOutput" + Guid.NewGuid().ToString() + ".png");
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load an existing Word document.
Using wordDocument As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Initialize the ChartToImageConverter for converting charts during Word to image conversion.
    wordDocument.ChartToImageConverter = New ChartToImageConverter()
    'Set the scaling mode for charts (Normal mode reduces the file size).
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
    'Convert the word document to images.
    Dim images() As Image = wordDocument.RenderAsImages(ImageType.Metafile)
    'Declare the variables to hold custom width and height.
    Dim customWidth As Integer = 1500
    Dim customHeight As Integer = 1500
    For Each image As Image In images
        Dim stream As MemoryStream = New MemoryStream
        image.Save(stream, ImageFormat.Png)
        'Create a bitmap of specific width and height.
        Dim bitmap As Bitmap = New Bitmap(customWidth, customHeight, PixelFormat.Format32bppPArgb)
        'Get the graphics from an image.
        Dim graphics As Graphics = Graphics.FromImage(bitmap)
        'Set the resolution.
        bitmap.SetResolution(300, 300)
        'Recreate the image in custom size.
        graphics.DrawImage(System.Drawing.Image.FromStream(stream), New Rectangle(0, 0, bitmap.Width, bitmap.Height))
        'Save the image as a bitmap.
        bitmap.Save(("ImageOutput" + (Guid.NewGuid.ToString + ".png")))
    Next

End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Custom-image-resolution).

N> 1. In Azure Web Service and Azure APP Service, .NET GDI+ (System.Drawing) does not support the Metafile image (vector image). So, the image will be generated as Bitmap (raster image).
N> 2. Creating an instance of the [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html) class is mandatory to convert the charts present in the Word document to Image. Otherwise, the charts are not preserved in the generated image.
N> 3. Total number of images may vary based on unsupported elements in the input Word document.
N> 4. Word to Image conversion has the same limitations and unsupported elements of Word to PDF conversion.
N> 5. Different styles of borders are known limitations in Word to Image conversion in ASP.NET Core, Xamarin, Blazor, WinUI, and .NET MAUI platforms.
N> 6. In ASP.NET Core, Blazor, Xamarin, WinUI and .NET MAUI platforms, to convert Word document to images we recommend you to use Word to image [assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-image) or [NuGet](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-image) as a reference in your application.
N> 7. DocIO supports Word to image conversion in UWP application using DocIORenderer.
N> 8. In addition to the previous NuGet packages, we recommend to use [SkiaSharp.NativeAssets.Linux v2.88.6](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.6) and [HarfBuzzSharp.NativeAssets.Linux v7.3.0](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/7.3.0) NuGets to perform Word to Image conversion in Linux environment.

## See Also

* [How to convert word to tiff using C#, VB.NET](https://support.syncfusion.com/kb/article/9541/how-to-convert-word-to-tiff-using-c-vb-net)
* [How to convert Word to Image in Blazor WebAssembly (WASM)?](https://support.syncfusion.com/kb/article/12123/how-to-convert-word-to-image-in-blazor-webassembly-wasm)