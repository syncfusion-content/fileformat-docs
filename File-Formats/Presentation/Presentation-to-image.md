---
title: Converting PowerPoint Presentation to image in File Formats|Syncfusion
description: This section illustrates how to convert PowerPoint Presentation document to image; PowerPoint Presentation conversion
platform: file-formats
control: Presentation
documentation: UG
---
# Presentation to image conversion

## .NET Framework

This section covers converting an entire Presentation or a single slide to image in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms. The supported image formats are listed as follows.

* BMP
* EMF
* JPG
* JPEG
* PNG

## Assemblies Required

Refer to the following links for assemblies required based on platforms to convert the worksheet to image.

* [Assemblies Information](https://help.syncfusion.com/file-formats/presentation/assemblies-required) 
* [NuGet Information](https://help.syncfusion.com/file-formats/presentation/nuget-packages-required#converting-powerpoint-presentation-to-image)

T> When converting a slide to image, use 'Metafile' format for good image resolution.

The following code example demonstrates how to convert a slide to image.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Namespaces to perform PPTX to Image conversion
using Syncfusion.Presentation;
using Syncfusion.OfficeChartToImageConverter;
using System.IO;
using Syncfusion.Drawing;

//Opens a PowerPoint Presentation file
IPresentation pptxDoc = Presentation.Open(fileName);
//Creates an instance of ChartToImageConverter
pptxDoc.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode as best
pptxDoc.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best;
//Converts the first slide into image
Image image = pptxDoc.Slides[0].ConvertToImage(Syncfusion.Drawing.ImageType.Metafile);
//Saves the image as file
image.Save("slide1.png");
//Disposes the image
image.Dispose();
//Closes the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Namespaces to perform PPTX to Image conversion
Imports Syncfusion.Presentation
Imports Syncfusion.OfficeChartToImageConverter
Imports Syncfusion.Drawing
Imports System.IO

'Opens a PowerPoint Presentation file
Dim pptxDoc As IPresentation = Presentation.Open(fileName)
'Creates an instance of ChartToImageConverter
pptxDoc.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode as best
pptxDoc.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best
'Converts the first slide into image
Dim image As Image = pptxDoc.Slides(0).ConvertToImage(Syncfusion.Drawing.ImageType.Metafile)
'Saves the image as file
image.Save("slide1.png")
'Disposes the image
image.Dispose()
'Closes the Presentation instance
Presentation_1.Close()
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Namespaces to perform PPTX to Image conversion
using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;
using System.IO;

//Open the existing PowerPoint presentation with stream.
using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
{
    //Initialize the PresentationRenderer to perform image conversion.
    pptxDoc.PresentationRenderer = new PresentationRenderer();
    //Convert PowerPoint slide to image as stream.
    using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
    {
        //Reset the stream position
        stream.Position = 0;
        //Create the output image file stream
        using (FileStream fileStreamOutput = File.Create("Output.jpg"))
        {
            //Copy the converted image stream into created output stream
            stream.CopyTo(fileStreamOutput);
        }
    }
}

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Namespaces to perform PPTX to Image conversion
using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;
using System.IO;

//Open the existing PowerPoint presentation with stream.
using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
{
    //Initialize the PresentationRenderer to perform image conversion.
    pptxDoc.PresentationRenderer = new PresentationRenderer();
    //Convert PowerPoint slide to image as stream.
    using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
    {
        //Reset the stream position
        stream.Position = 0;
        //Create the output image file stream
        using (FileStream fileStreamOutput = File.Create("Output.jpg"))
        {
            //Copy the converted image stream into created output stream
            stream.CopyTo(fileStreamOutput);
        }
    }
}
{% endhighlight %}

{% endtabs %}

The following code example demonstrates the conversion of an entire Presentation to images:

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads the PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Creates instance of ChartToImageConverter
pptxDoc.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode as best
pptxDoc.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best;
//Converts entire Presentation to images
Image[] images = pptxDoc.RenderAsImages(Syncfusion.Drawing.ImageType.Metafile);
//Saves the image to file system
foreach (Image image in images)
{ 
    image.Save("ImageOutput" + Guid.NewGuid().ToString()+ ".png");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Creates instance of ChartToImageConverter
pptxDoc.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode as best
pptxDoc.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best
'Converts entire Presentation to images
Dim images As Image() = pptxDoc.RenderAsImages(Syncfusion.Drawing.ImageType.Metafile)
'Saves the image to file system
For Each image As Image In images
    image.Save("ImageOutput" + Guid.NewGuid().ToString() + ".png")
Next
{% endhighlight %}

{% endtabs %}

The following code snippet demonstrates how to convert a PowerPoint slide to image using custom image resolution,

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads the PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Output.pptx");
//Declare variables to hold custom width and height
int customWidth = 1500;
int customHeight = 1000;
//Converts the slide as image and returns the image stream
Stream stream = pptxDoc.Slides[0].ConvertToImage(Syncfusion.Drawing.ImageFormat.Emf);
//Creates a bitmap of specific width and height
Bitmap bitmap = new Bitmap(customWidth, customHeight, PixelFormat.Format32bppPArgb);
//Gets the graphics from image
Graphics graphics = Graphics.FromImage(bitmap);
//Sets the resolution
bitmap.SetResolution(graphics.DpiX, graphics.DpiY);
//Recreates the image in custom size
graphics.DrawImage(System.Drawing.Image.FromStream(stream), new Rectangle(0, 0, bitmap.Width, bitmap.Height));
//Saves the image as bitmap 
bitmap.Save("ImageOutput" + Guid.NewGuid().ToString() + ".jpeg");
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Output.pptx")
'Declare variables to hold custom width and height
Dim customWidth As Integer = 1500
Dim customHeight As Integer = 1000
'Converts the slide as image and returns the image stream
Dim stream As Stream = pptxDoc.Slides(0).ConvertToImage(Syncfusion.Drawing.ImageFormat.Emf)
'Creates a bitmap of specific width and height
Dim bitmap As New Bitmap(customWidth, customHeight, PixelFormat.Format32bppPArgb)
'Gets the graphics from image
Dim imageGraphics As Graphics = Graphics.FromImage(bitmap)
'Sets the resolution
bitmap.SetResolution(imageGraphics.DpiX, imageGraphics.DpiY)
'Recreates the image in custom size
imageGraphics.DrawImage(System.Drawing.Image.FromStream(stream), New Rectangle(0, 0, bitmap.Width, bitmap.Height))
'Saves the image as bitmap
bitmap.Save("ImageOutput" + Guid.NewGuid().ToString() + ".jpeg")
'Closes the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

## UWP

PowerPoint slides can be converted to images in UWP by using Essential Presentation library. The following assemblies are required in the UWP application to convert the slides as images.

<table>
    <thead>
        <tr>
            <th>
                Assembly Name</th>
            <th>
                Short Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Syncfusion.Presentation.UWP</td>
            <td>This assembly contains the core features needed for creating, reading, manipulating a Presentation file.</td>
        </tr>
        <tr>
            <td>Syncfusion.OfficeChart.UWP</td>
            <td>This assembly contains the Office Chart Object model and core features needed for chart creation.</td>
        </tr>
        <tr>
            <td>Syncfusion.OfficeChartToImageConverter.UWP</td>
            <td>This assembly is used to convert Office Chart into Image. </td>
        </tr>
        <tr>
            <td>Syncfusion.SfChart.UWP</td>
            <td>Supporting assembly for Syncfusion.OfficeChartToImageConverter.UWP</td>
        </tr>       
    </tbody>
</table>

The following code example demonstrates how to convert a slide to image in UWP.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load the presentation file using open picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.FileTypeFilter.Add(".pptx");
StorageFile inputFile = await openPicker.PickSingleFileAsync();
pptxDoc = await Presentation.OpenAsync(inputFile);
//Initialize the ‘ChartToImageConverter’ instance to convert the charts in the slides
pptxDoc.ChartToImageConverter = new ChartToImageConverter();
//Pick the folder to save the converted images.
FolderPicker folderPicker = new FolderPicker();
folderPicker.ViewMode = PickerViewMode.Thumbnail;
folderPicker.FileTypeFilter.Add("*");
StorageFolder storageFolder = await folderPicker.PickSingleFolderAsync();
StorageFile imageFile = await storageFolder.CreateFileAsync("Slide1.jpg", CreationCollisionOption.ReplaceExisting);
//Convert the slide to image.
await slide.SaveAsImageAsync(imageFile);
//Closes the presentation instance
pptxDoc.Close();
{% endhighlight %}

{% endtabs %}

The following code snippet demonstrates how to convert a PowerPoint slide to image using custom image resolution.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load the presentation file using open picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.FileTypeFilter.Add(".pptx");
StorageFile inputFile = await openPicker.PickSingleFileAsync();
pptxDoc = await Presentation.OpenAsync(inputFile);
//Initialize the ‘ChartToImageConverter’ instance to convert the charts in the slides.
pptxDoc.ChartToImageConverter = new ChartToImageConverter();
//Pick the folder to save the converted images.
FolderPicker folderPicker = new FolderPicker();
folderPicker.ViewMode = PickerViewMode.Thumbnail;
folderPicker.FileTypeFilter.Add("*");
StorageFolder storageFolder = await folderPicker.PickSingleFolderAsync();
StorageFile imageFile = await storageFolder.CreateFileAsync("Slide1.jpg", CreationCollisionOption.ReplaceExisting);
//Get the stream of the created image file.
StorageFile imageStream = await imageFile.OpenStreamForWriteAsync()
//Creates a new instance for the rendering options to customize the image resolution.
RenderingOptions renderingOptions = new RenderingOptions();
//Sets the horizontal scaling value for the converted image. The default value is 1.
renderingOptions.ScaleX = 10F;
//Sets the vertical scaling value for the converted image. The default value is 1.
renderingOptions.ScaleY = 10F;
//Convert the slide to image with specified resolution.
await slide.SaveAsImageAsync(imageStream, renderingOptions);
//Closes the presentation instance
pptxDoc.Close();
{% endhighlight %}

{% endtabs %}

The following code snippet demonstrates how to convert a PowerPoint slide to image by passing ‘CancellationToken’.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load the presentation file using open picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.FileTypeFilter.Add(".pptx");
StorageFile inputFile = await openPicker.PickSingleFileAsync();
pptxDoc = await Presentation.OpenAsync(inputFile);
//Initialize the ChartToImageConverter instance to convert the charts in the slides.
pptxDoc.ChartToImageConverter = new ChartToImageConverter();
//Pick the folder to save the converted images.
FolderPicker folderPicker = new FolderPicker();                    
folderPicker.ViewMode = PickerViewMode.Thumbnail;
folderPicker.FileTypeFilter.Add("*");
StorageFolder storageFolder = await folderPicker.PickSingleFolderAsync();
//Create a cancellation token to cancel the image rendering instantly.
CancellationTokenSource cancellationToken = new CancellationTokenSource();
//Convert the slide to image.
int slideNumber = 1;
foreach (ISlide slide in pptxDoc.Slides)
{
    StorageFile imageFile = await storageFolder.CreateFileAsync("Slide" + slideNumber++ + ".jpg", CreationCollisionOption.ReplaceExisting);
    await slide.SaveAsImageAsync(imageFile, cancellationToken.Token);
}
//Close the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% endtabs %}

N> 1. PowerPoint Presentation to image conversion is supported in Blazor server-side application alone and is not supported in Blazor client-side application. 
N> 2. Instance of **ChartToImageConverter** class is mandatory to convert the charts present in the Presentation to image. Otherwise, the charts in the presentation are not exported to the converted image
N> 3. **ChartToImageConverter** is supported from .NET Framework 4.0 onward
N> 4. The assembly "Syncfusion.SfChart.WPF" is non compliance with FIPS(Federal Information Processing Standard) algorithm policy.
N> 5. EMF images in the PowerPoint slides will not be converted in UWP due to platform limitation.
N> 6. Radial gradient, rectangular gradient and path gradient brushes are not supported in UWP due to platform limitation. These brushes are rendered as linear gradient brush in our UWP slide to image conversion.

## Font substitution for unavailable fonts

When a font used in a PowerPoint presentation is unavailable in the environment where it is converted to image, then the library substitutes the ‘Microsoft Sans Serif’ as a default font for text rendering. This leads to a difference in text layouts of PowerPoint presentation and the converted image.  To avoid this, the Essential Presentation library allows you to set an alternate font for the missing font used in the PowerPoint presentation.

N> Font substitution for Unavailable fonts is not supported in UWP platform.

The following code sample demonstrates how to set a substitute font for a missing font while converting a PowerPoint presentation to image.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load the PowerPoint presentation and convert to image
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
    //Initialize 'ChartToImageConverter' to convert charts in the slides, and this is optional
    pptxDoc.ChartToImageConverter = new ChartToImageConverter();
    // Initializes the 'SubstituteFont' event to set the replacement font
    pptxDoc.FontSettings.SubstituteFont += FontSettings_SubstituteFont;
    //Converts the first slide into image
    Image image = pptxDoc.Slides[0].ConvertToImage(Syncfusion.Drawing.ImageType.Metafile);
    //Saves the image as file
    image.Save("slide1.png");
    //Disposes the image
    image.Dispose();
}
/// <summary>
/// Sets the alternate font when a specified font is unavailable in the production environment
/// </summary>
/// <param name="sender">FontSettings type of the Presentation in which the specified font is used but unavailable in production environment. </param>
/// <param name="args">Retrieves the unavailable font name and receives the substitute font name for conversion. </param>
private static void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    if (args.OriginalFontName == "Arial Unicode MS")
        args.AlternateFontName = "Arial";
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation and convert to image
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize 'ChartToImageConverter' to convert charts in the slides, and this is optional
pptxDoc.ChartToImageConverter = New ChartToImageConverter()
'Initializes the 'SubstituteFont' event to set the replacement font
AddHandler pptxDoc.FontSettings.SubstituteFont, AddressOf SubstituteFont
'Convert the PowerPoint presentation to image.
Dim image As Image = pptxDoc.Slides(0).ConvertToImage(Syncfusion.Drawing.ImageType.Metafile)
'Save the image.
image.Save("slide1.png")
'Dispose the Presentation instance
pptxDoc.Dispose()
'Dispose the image
image.Dispose()
''' <summary>
''' Sets the alternate font when a specified font is unavailable in the production environment
''' </summary>
''' <param name="sender">FontSettings type of the Presentation in which the specified font is used but unavailable in production environment. </param>
''' <param name="args">Retrieves the unavailable font name and receives the substitute font name for conversion. </param>
Private Sub SubstituteFont(ByVal sender As Object, ByVal args As SubstituteFontEventArgs)
    ' Sets the alternate font when a specified font is not installed in the production environment
    If args.OriginalFontName = "Arial Unicode MS" Then
        args.AlternateFontName = "Arial"
    Else
        args.AlternateFontName = "Times New Roman"
    End If
End Sub
{% endhighlight %}

{% endtabs %}

## Fallback fonts

When a glyph of input text is unavailable in mentioned font, text will not be preserved in PPTX to Image conversion. To avoid this, Syncfusion PowerPoint library allows you to use a fallback font to preserve the text properly in PPTX to Image conversion.

### Initialize Fallback Fonts

The following code example demonstrates how to initialize a default fallback font while converting a PowerPoint presentation to Image.

{% tabs %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Initialize the PresentationRenderer to perform image conversion
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Use a sets of default FallbackFont collection to IPresentation
        pptxDoc.FontSettings.InitializeFallbackFonts();
        //Convert PowerPoint slide to image as stream
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position
            stream.Position = 0;
            //Create the output image file stream
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Use a sets of default FallbackFont collection to IPresentation
        pptxDoc.FontSettings.InitializeFallbackFonts();
        //Initialize the PresentationRenderer to perform image conversion
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Convert PowerPoint slide to image as stream
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position
            stream.Position = 0;
            //Create the output image file stream
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% endtabs %}

### Customize Default Fallback Fonts

The following code example demonstrates how to customize default fallback font while converting a PowerPoint presentation to Image.

{% tabs %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Initialize the PresentationRenderer to perform image conversion
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Use a sets of default FallbackFont collection to IPresentation
        pptxDoc.FontSettings.InitializeFallbackFonts();
        // Customize a default fallback font name
        // Modify the Hebrew script default font name as "David"
        pptxDoc.FontSettings.FallbackFonts[5].FontNames = "David";
        //Convert PowerPoint slide to image as stream
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position
            stream.Position = 0;
            //Create the output image file stream
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Use a sets of default FallbackFont collection to IPresentation
        pptxDoc.FontSettings.InitializeFallbackFonts();
        // Customize a default fallback font name
        // Modify the Hebrew script default font name as "David"
        pptxDoc.FontSettings.FallbackFonts[5].FontNames = "David";
        //Initialize the PresentationRenderer to perform image conversion
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Convert PowerPoint slide to image as stream
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position
            stream.Position = 0;
            //Create the output image file stream
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% endtabs %}

### Add Custom Fallback Fonts

The following code example demonstrates how to add custom fallback fonts while converting a PowerPoint presentation to Image.

{% tabs %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Add custom fallback font names
        // Arabic
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
        // Hebrew
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Arial"));
        // Hindi
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Mangal"));
        // Chinese
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
        // Japanese
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Mincho"));
        // Korean
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"));
        //Initialize the PresentationRenderer to perform image conversion
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Convert PowerPoint slide to image as stream
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position
            stream.Position = 0;
            //Create the output image file stream
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Add custom fallback font names
        // Arabic
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
        // Hebrew
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Arial"));
        // Hindi
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Mangal"));
        // Chinese
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
        // Japanese
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Mincho"));
        // Korean
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"));
        //Initialize the PresentationRenderer to perform image conversion
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Convert PowerPoint slide to image as stream
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position
            stream.Position = 0;
            //Create the output image file stream
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% endtabs %}

N> 1. Fallback fonts only supported for Arabic, Hebrew, Hindi, Chinese, Japanese and Korean languages.
N> 2. Its only supported in [Portable PPTX to Image](https://help.syncfusion.com/file-formats/presentation/presentation-to-image) conversion.