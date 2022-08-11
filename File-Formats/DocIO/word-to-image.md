---
title: Converting Word document to Image | Word Library | Syncfusion
description: Learn here all about rendering and converting word document to image of Syncfusion's Word (DocIO) Library and more.
platform: file-formats
control: DocIO
documentation: UG
---

# Rendering / Converting Word document to Image in Word Library

The Essential DocIO converts the Word document to images using the `RenderAsImages` method.

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

The following code illustrates how to convert the Word document to image.


{% tabs %}
{% highlight c# tabtitle="C#" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to image conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode for charts (Normal mode reduces the file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
//Converts word document to image
Image[] images = wordDocument.RenderAsImages(ImageType.Bitmap);
int i = 0;
foreach (Image image in images)
{
    //Saves the images as jpeg
    image.Save("WordToImage_" + i + ".jpeg", ImageFormat.Jpeg);
    i++;
}
//Closes the document
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to image conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode for charts (Normal mode reduces the file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
'Converts word document to image
Dim images As Image() = wordDocument.RenderAsImages(ImageType.Bitmap)
Dim i As Integer = 0
For Each image As Image In images
	'Saves the images as jpeg
	image.Save("WordToImage_" & i & ".jpeg", ImageFormat.Jpeg)
	i += 1
Next
'Closes the document
wordDocument.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO supports Word to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens the file as Stream.
using (FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
    //Loads file stream into Word document.
    using (WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic))
    {
        //Creates a new instance of DocIORenderer class.
        using (DocIORenderer render = new DocIORenderer())
        {
            //Converts Word document to images.
            Stream[] imageStreams = wordDocument.RenderAsImages(); 
            int i = 0;
            foreach (Stream stream in imageStreams)
            {
                //Resets the stream position.
                stream.Position = 0;
                //Creates the output image file stream.
                using (FileStream fileStreamOutput = File.Create("WordToImage_" + i + ".jpeg"))
                {
                    //Copies the converted image stream into created output stream.
                    stream.CopyTo(fileStreamOutput);
                }
                i++;
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Opens the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx"))
{
    //Loads file stream into Word document.
    using (WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic))
    {
        //Creates a new instance of DocIORenderer class.
        using (DocIORenderer render = new DocIORenderer())
        {
            //Converts Word document to images.
            Stream[] imageStreams = wordDocument.RenderAsImages();
            int i = 0;
            foreach (Stream stream in imageStreams)
            {
                //Resets the stream position.
                stream.Position = 0;
                //Saves the stream as a file in the device and invoke it for viewing.
                Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WordToImage_" + i + ".jpeg", "image/jpeg", stream as MemoryStream);
                i++;
            }
        }
    }
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Convert-Word-to-image).

The following code snippet illustrates how to convert a Word document to an image using custom image resolution.


{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//DocIO only supports Word to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platform.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//DocIO only supports Word to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platform.
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//DocIO only supports Word to image conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platform.
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Custom-image-resolution).

N> 1. Word to Image conversion is not supported in Silverlight, Windows Phone, WinRT, Universal and Universal Windows Platform applications.
N> 2. In Azure Web Service and Azure APP Service, .NET GDI+ (System.Drawing) does not support the Metafile image (vector image). So, the image will be generated as Bitmap (raster image).
N> 3. Creating an instance of the ChartToImageConverter class is mandatory to convert the charts present in the Word document to Image. Otherwise, the charts are not preserved in the generated image.
N> 4. The ChartToImageConverter is supported from .NET Framework 4.0 onwards.
N> 5. Total number of images may vary based on unsupported elements in the input Word document.
N> 6. Word to Image conversion has the same limitations and unsupported elements of Word to PDF conversion.
N> 7. Different styles of underlines and borders are known limitations in Word to Image conversion in ASP.NET Core, Xamarin, Blazor, WinUI, and .NET MAUI platforms.
N> 8. In ASP.NET Core, Blazor, Xamarin, WinUI and .NET MAUI platforms, to convert Word document to images we recommend you to use Word to image [assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-image) or [NuGet](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-image) as a reference in your application.