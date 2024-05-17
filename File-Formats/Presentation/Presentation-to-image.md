---
title: Converting PowerPoint Presentation to image in File Formats|Syncfusion
description: This section illustrates how to convert PowerPoint Presentation document to image; PowerPoint Presentation conversion
platform: file-formats
control: Presentation
documentation: UG
---
# Presentation to image conversion

To quickly start converting a PowerPoint Presentation to an Image using .NET PowerPoint library, please check out this video:
{% youtube "https://www.youtube.com/watch?v=DcH9CptpYHg" %}

## .NET Framework

This section covers converting an entire Presentation or a single slide to image in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms. The supported image formats are listed as follows.

* BMP
* EMF
* JPG
* JPEG
* PNG

## Assemblies Required

Refer to the following links for assemblies required based on platforms to convert the PowerPoint Presentation to image.

* [Assemblies Information](https://help.syncfusion.com/file-formats/presentation/assemblies-required) 
* [NuGet Information](https://help.syncfusion.com/file-formats/presentation/nuget-packages-required#converting-powerpoint-presentation-to-image)

T> When converting a slide to image, use 'Metafile' format for good image resolution.

## Convert a slide to image

The following code example demonstrates how to convert a slide to image.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-PowerPoint-slide-to-Image/.NET).

## Convert PowerPoint Presentation to images

The following code example demonstrates the conversion of an entire Presentation to images:

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
using (FileStream fileStream = new FileStream("Sample.pptx", FileMode.Open, FileAccess.Read))
{
   //Open the existing PowerPoint presentation.
   using (IPresentation pptxDoc = Presentation.Open(fileStream))
   {
       //Initialize the PresentationRenderer to perform image conversion.
       pptxDoc.PresentationRenderer = new PresentationRenderer();
       //Convert PowerPoint to image as stream.
       Stream[] images = pptxDoc.RenderAsImages(ExportImageFormat.Jpeg);
       //Saves the images to file system
       foreach (Stream stream in images)
       {
           //Create the output image file stream
           using (FileStream fileStreamOutput = File.Create("Output" + Guid.NewGuid().ToString() + ".jpg"))
           {
               //Copy the converted image stream into created output stream
               stream.CopyTo(fileStreamOutput);
           }
       }
   }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image).

## Image resolution

The following code snippet demonstrates how to convert a PowerPoint slide to image using custom image resolution,

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Change-resolution-of-converted-image).

## Convert PowerPoint Animations to Images

The .NET PowerPoint Library (Presentation) allows you to convert PowerPoint slides into images based on the sequence of entrance animation effects applied to each element.

For instance, if a slide includes bulleted paragraphs, each having entrance animation effects, the Presentation library converts every bulleted paragraph into a separate image.

N> 1. Only entrance animation effects are considered for generating separate images. Other animation effects and non-animated elements will be converted into images within the first image itself.
N> 2. Converting PowerPoint animations to images is not supported in the UWP platform. 

The following code example shows how to convert PowerPoint slides to images based on the sequence of animation effects using the [PresentationAnimationConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.PresentationAnimationConverter.html) API.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Open a PowerPoint Presentation.
IPresentation pptxDoc = Presentation.Open("Input.pptx");

//Initialize the PresentationAnimationConverter to perform slide to image conversion based on animation order.
using (PresentationAnimationConverter animationConverter = new PresentationAnimationConverter())
{
    int i = 0;
    foreach (ISlide slide in pptxDoc.Slides)
    {
        //Convert the PowerPoint slide to a series of images based on entrance animation effects.
        Stream[] imageStreams = animationConverter.Convert(slide, ExportImageFormat.Png);

        //Save the image stream.
        foreach (Stream stream in imageStreams)
        {
            i++;
            //Reset the stream position.
            stream.Position = 0;

            //Create the output image file stream.
            using (FileStream fileStreamOutput = File.Create("Output" + i + ".png"))
            {
                //Copy the converted image stream into created output stream.
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Open a PowerPoint Presentation.
IPresentation pptxDoc = Presentation.Open("Input.pptx");

//Initialize the PresentationAnimationConverter to perform slide to image conversion based on animation order.
using (PresentationAnimationConverter animationConverter = new PresentationAnimationConverter())
{
    int i = 0;
    foreach (ISlide slide in pptxDoc.Slides)
    {
        //Convert the PowerPoint slide to a series of images based on entrance animation effects.
        Stream[] imageStreams = animationConverter.Convert(slide, Syncfusion.Drawing.ImageFormat.Png);

        //Save the image stream.
        foreach (Stream stream in imageStreams)
        {
            i++;
            //Reset the stream position.
            stream.Position = 0;

            //Create the output image file stream.
            using (FileStream fileStreamOutput = File.Create("Output" + i + ".png"))
            {
                //Copy the converted image stream into created output stream.
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Open a PowerPoint Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Input.pptx")

' Initialize the PresentationAnimationConverter to perform slide to image conversion based on animation order.
Using animationConverter As New PresentationAnimationConverter()
    Dim i As Integer = 0
    For Each slide As ISlide In pptxDoc.Slides
        ' Convert the PowerPoint slide to a series of images based on entrance animation effects.
        Dim imageStreams As Stream() = animationConverter.Convert(slide, Syncfusion.Drawing.ImageFormat.Png)

        ' Save the image stream.
        For Each stream As Stream In imageStreams
            i += 1
            ' Reset the stream position.
            stream.Position = 0

            ' Create the output image file stream.
            Using fileStreamOutput As FileStream = File.Create("Output" & i & ".png")
                ' Copy the converted image stream into created output stream.
                stream.CopyTo(fileStreamOutput)
            End Using
        Next
    Next
End Using

{% endhighlight %}
{% endtabs %}

![Convert PowerPoint slides to images with animation sequence](PPTXtoImage_images/PowerPoint-Animations-to-Images-output.png)

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Based-on-Entrance-animation-effects/.NET).

T> With this, you can showcase the converted images as a slideshow in your [custom PowerPoint Viewer](https://ej2.syncfusion.com/aspnetcore/PowerPoint/AnimationConverter#/material).

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

### Convert a slide to image

The following code example demonstrates how to convert a slide to image in UWP.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-PowerPoint-slide-to-Image/UWP).

### Convert PowerPoint Presentation to images

The following code snippet demonstrates how to convert a PowerPoint slide to image using custom image resolution.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Change-resolution-of-converted-image/UWP).

### Convert a slide to image by CancellationToken

The following code snippet demonstrates how to convert a PowerPoint slide to image by passing ‘CancellationToken’.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-with-UWP-cancellation-token).

N> 1. Instance of [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html) class is mandatory to convert the charts present in the Presentation to image. Otherwise, the charts in the presentation are not exported to the converted image
N> 2. The assembly "Syncfusion.SfChart.WPF" is non compliance with FIPS(Federal Information Processing Standard) algorithm policy.
N> 3. EMF images in the PowerPoint slides will not be converted in UWP due to platform limitation.
N> 4. Radial gradient, rectangular gradient and path gradient brushes are not supported in UWP due to platform limitation. These brushes are rendered as linear gradient brush in our UWP slide to image conversion.

## Font substitution for unavailable fonts

When a font used in a PowerPoint presentation is unavailable in the environment where it is converted to image, then the library substitutes the ‘Microsoft Sans Serif’ as a default font for text rendering. This leads to a difference in text layouts of PowerPoint presentation and the converted image.  To avoid this, the Essential Presentation library allows you to set an alternate font for the missing font used in the PowerPoint presentation.

N> Font substitution for Unavailable fonts is not supported in UWP platform.

The following code sample demonstrates how to set a substitute font for a missing font while converting a PowerPoint presentation to image.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Load the PowerPoint presentation and convert to image
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
    //Initialize the PresentationRenderer to perform image conversion.
    pptxDoc.PresentationRenderer = new PresentationRenderer();
    // Initializes the 'SubstituteFont' event to set the replacement font
    pptxDoc.FontSettings.SubstituteFont += FontSettings_SubstituteFont;
    //Convert PowerPoint slide to image as stream.
    using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
    {
        //Create the output image file stream
        using (FileStream fileStreamOutput = File.Create("Output.jpg"))
        {
         //Copy the converted image stream into created output stream
         stream.CopyTo(fileStreamOutput);
        }
     }        
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Add-font-substitution).

## Fallback fonts

During PowerPoint to Image conversions, if a glyph of the input text is unavailable in the specified font, the text will not be rendered properly. To address this, the Syncfusion PowerPoint (Presentation) library allows users to specify fallback fonts. When a glyph is missing, the library will use one of the fallback fonts to render the text correctly in the output image.

Users can configure fallback fonts in the following ways:
* Initialize default fallback fonts.
* Set custom fonts as fallback fonts for specific script types, including Arabic, Hebrew, Chinese, Japanese, and more.
* Set custom fonts as fallback fonts for a particular range of Unicode text.

N> Presentation internally uses user-initialized or specified fallback fonts for Unicode characters during PowerPoint to Image conversion. Therefore, the specified fallback fonts must be installed in the production environment. Otherwise, it will not render the text properly using the fallback fonts.

### Initialize default fallback fonts

The following code example demonstrates how to initialize a default fallback font while converting a PowerPoint presentation to an Image. The *InitializeDefault* API sets the default fallback fonts for specific script types like Arabic, Hebrew, Chinese, Japanese etc.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream("Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Initialize the PresentationRenderer to perform image conversion.
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Use a sets of default FallbackFont collection to IPresentation.
        pptxDoc.FontSettings.FallbackFonts.InitializeDefault();
        //Convert PowerPoint slide to image as stream.
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position.
            stream.Position = 0;
            //Create the output image file stream.
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream.
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Initialize-default-fallback-fonts).

### Fallback fonts based on script type

The following code example demonstrates how a user can add fallback fonts based on the script types, which Presentation considers internally when converting a PowerPoint presentation to an Image.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream("Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Adds fallback font for "Arabic" script type.
        pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Arabic, "Arial, Times New Roman");
        //Adds fallback font for "Hebrew" script type.
        pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Hebrew, "Arial, Courier New");
        //Adds fallback font for "Hindi" script type.
        pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Hindi, "Mangal, Nirmala UI");
        //Adds fallback font for "Chinese" script type.
        pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Chinese, "DengXian, MingLiU");
        //Adds fallback font for "Japanese" script type.
        pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Japanese, "Yu Mincho, MS Mincho");
        //Adds fallback font for "Thai" script type.
        pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Thai, "Tahoma, Microsoft Sans Serif");
        //Adds fallback font for "Korean" script type.
        pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Korean, "Malgun Gothic, Batang");
        //Initialize the PresentationRenderer to perform image conversion.
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Convert PowerPoint slide to image as stream.
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position.
            stream.Position = 0;
            //Create the output image file stream.
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream.
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Fallback-fonts-based-on-scripttype).

### Fallback fonts for range of Unicode text

Users can set fallback fonts for specific Unicode range of text to be used in Presentation to Image conversion.

The following code example demonstrates how users can add fallback fonts by using a specific Unicode range of text that Presentation considers internally while converting a PowerPoint presentation to an Image.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Adds fallback font for specific unicode range.
        // Arabic.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
        // Hebrew.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Arial"));
        // Hindi.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Mangal"));
        // Chinese.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
        // Japanese.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Mincho"));
        // Korean.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"));
        //Initialize the PresentationRenderer to perform image conversion.
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Convert PowerPoint slide to image as stream.
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position.
            stream.Position = 0;
            //Create the output image file stream.
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream.
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Fallback-fonts-for-Unicode-range).

### Modify the exiting fallback fonts

The following code example demonstrates how user can modify or customize the existing fallback fonts using *FontNames* API while converting a PowerPoint presentation to an Image.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Initialize the PresentationRenderer to perform image conversion.
        pptxDoc.PresentationRenderer = new PresentationRenderer();
        //Use a sets of default FallbackFont collection to IPresentation.
        pptxDoc.FontSettings.FallbackFonts.InitializeDefault();
        // Customize a default fallback font name.
        FallbackFonts fallbackFonts = pptxDoc.FontSettings.FallbackFonts;
        foreach (FallbackFont fallbackFont in fallbackFonts) 
        {
           //Customize a default fallback font name as "David" for the Hebrew script.
           if (fallbackFont.ScriptType == ScriptType.Hebrew)
              fallbackFont.FontNames = "David";
        }
        //Convert PowerPoint slide to image as stream.
        using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
        {
            //Reset the stream position.
            stream.Position = 0;
            //Create the output image file stream.
            using (FileStream fileStreamOutput = File.Create("Output.jpg"))
            {
                //Copy the converted image stream into created output stream.
                stream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Modify-the-exiting-fallback-fonts).

### Supported script types

The following table illustrates the supported script types by the .NET PowerPoint library (Presentation) in Presentation to Image conversion.

<table>
<thead> 
<tr>
<th>Script types</th>
<th>Ranges</th>
<th>Default fallback fonts considered in InitializeDefault() API</th>
</tr>
</thead>
<tr>
<td>
Arabic
</td>
<td>
0x0600 - 0x06ff<br>
0x0750 - 0x077f<br>
0x08a0 - 0x08ff<br>
0xfb50 - 0xfdff<br>
0xfe70 - 0xfeff<br>
</td>
<td>
Arial, Times New Roman, Microsoft Uighur
</td>
</tr>
<tr>
<td>
Hebrew
</td>
<td>
0x0590 - 0x05ff<br>
0xfb1d - 0xfb4f<br>
</td>
<td>
Arial, Times New Roman, David
</td>
</tr>
<tr>
<td>
Hindi
</td>
<td>
0x0900 - 0x097F<br>
0xa8e0 - 0xa8ff<br>
0x1cd0 - 0x1cff<br>
</td>
<td>
Mangal, Utsaah
</td>
</tr>
<tr>
<td>
Chinese
</td>
<td>
0x4E00 - 0x9FFF<br>
0x3400 - 0x4DBF<br>
0xd840 - 0xd869<br>
0xdc00 - 0xdedf<br>
0xA960 - 0xA97F<br>
0xFF00 - 0xFFEF<br>
0x3000 - 0x303F<br>
</td>
<td>
DengXian, MingLiU, MS Gothic
</td>
</tr>
<tr>
<td>
Japanese
</td>
<td>
0x30A0 - 0x30FF<br>
0x3040 - 0x309F<br>
</td>
<td>
Yu Mincho, MS Mincho
</td>
</tr>
<tr>
<td>
Thai 
</td>
<td>
0x0E00 - 0x0E7F
</td>
<td>
Tahoma, Microsoft Sans Serif
</td>
</tr>
<tr>
<td>
Korean 
</td>
<td>
0xAC00 - 0xD7A3<br>
0x1100 - 0x11FF<br>
0x3130 - 0x318F<br>
0xA960 - 0xA97F<br>
0xD7B0 - 0xD7FF<br>
0xAC00 - 0xD7AF<br>
</td>
<td>
Malgun Gothic, Batang
</td>
</tr>
</table>

N> The .NET PowerPoint Library (Presentation) uses System.Drawing functionalities for PowerPoint to image conversion conversion in .NET Framework applications. And System.Drawing itself uses a fallback font to preserve the Unicode text while drawing the text in the image. So, these Fallback fonts APIs are **not supported in .NET Framework**.

## See Also

* [How to convert PPTX to Image in Blazor WebAssembly (WASM)?](https://support.syncfusion.com/kb/article/12122/how-to-convert-pptx-to-image-in-blazor-webassembly-wasm)
* [How custom resolution supported in WinForms PowerPoint slide to image conversion?](https://support.syncfusion.com/kb/article/6685/how-custom-resolution-supported-in-winforms-powerpoint-slide-to-image-conversion)
* [How to convert and replace EMF image to PNG with same size during PowerPoint to PDF conversion?](https://support.syncfusion.com/kb/article/15641/how-to-convert-and-replace-emf-image-to-png-with-same-size-during-powerpoint-to-pdf-conversion)
