---
title: Create, read and edit Master and Layout slides in CSharp |Syncfusion|
description: Create, read, and edit Master slides and Layout slides using Syncfusion PowerPoint library (Essential Presentation).
platform: file-formats
control: PowerPoint
documentation: UG
---

# Create and edit Master and Layout slides

To get all the slides in same format, you should perform those changes in the Slide Master or Layout Master. The changes will be applied to all the slides, which inherits the master slide or layout slide.

The [Syncfusion PowerPoint library](https://www.syncfusion.com/powerpoint-framework/net) supports the following:

1. Access the [MasterSlide](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IMasterSlide.html) in PowerPoint file.
2. Add [LayoutSlide](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ILayoutSlide.html) to the [MasterSlide](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IMasterSlide.html).
3. Customize the [LayoutSlide](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ILayoutSlide.html).
4. Create a slide with 9 pre-defined layout slides.
5. Customize the layout slides to fit your own scenarios.

## Access the MasterSlide

In PowerPoint presentation, the [MasterSlide](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IMasterSlide.html) is the top slide that controls all information about the theme, layout, background, color, fonts, and positioning of all slides. Using this MasterSlide, you can easily adjust the look of an existing theme or make overall changes to all your slides.

The following code example demonstrates how to access the [MasterSlide](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IMasterSlide.html) in a PowerPoint presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Access the first master slide in PowerPoint file
IMasterSlide masterSlide = pptxDoc.Masters[0];
//Get the first shape name from the master slide
string shapeName = masterSlide.Shapes[0].ShapeName;
//Save the PowerPoint file
pptxDoc.Save("Sample.pptx");
//Close the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Access the first master slide in PowerPoint file.
Dim masterSlide As IMasterSlide = pptxDoc.Masters(0)
'Get the first shape name from the master slide
Dim shapeName As String = masterSlide.Shapes(0).ShapeName
'Save the PowerPoint file.
pptxDoc.Save("AccessMasterSlide.pptx")
'Close the Presentation instance
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Master-and-Layout-slides/Access-PowerPoint-master-slide).

## Change background of Master slide

You can change the background of the master slide, all slides in the presentation would receive the same background settings. The following code example demonstrates how to set the background for a master slide.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Create a PowerPoint presentation.
using (IPresentation pptxDoc = Presentation.Create())
{
    //Access the first master slide in PowerPoint file.
    IMasterSlide masterSlide = pptxDoc.Masters[0];
    //Retrieve the background instance.
    IBackground background = masterSlide.Background;
    //Set the fill type for background as Solid fill.
    background.Fill.FillType = FillType.Solid;
    //Get the instance for solid Fill.
    ISolidFill solidFill = background.Fill.SolidFill;
    //Set the color for solid fill object.
    solidFill.Color = ColorObject.Green;
    //Save the PowerPoint file.
    pptxDoc.Save("Sample.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a PowerPoint presentation.
Using pptxDoc As IPresentation = Presentation.Create()
    'Access the first master slide in PowerPoint file.
    Dim masterSlide As IMasterSlide = pptxDoc.Masters(0)
    'Retrieve the background instance.
    Dim background As IBackground = masterSlide.Background
    'Set the fill type for background as Solid fill.
    background.Fill.FillType = FillType.Solid
    'Get the instance for solid Fill.
    Dim solidFill As ISolidFill = background.Fill.SolidFill
    'Set the color for solid fill object.
    solidFill.Color = ColorObject.Green
    'Save the PowerPoint file.
    pptxDoc.Save("Sample.pptx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a PowerPoint presentation.
using (IPresentation pptxDoc = Presentation.Create())
{
    //Access the first master slide in PowerPoint file.
    IMasterSlide masterSlide = pptxDoc.Masters[0];
    //Retrieve the background instance.
    IBackground background = masterSlide.Background;
    //Set the fill type for background as Solid fill.
    background.Fill.FillType = FillType.Solid;
    //Get the instance for solid Fill.
    ISolidFill solidFill = background.Fill.SolidFill;
    //Set the color for solid fill object.
    solidFill.Color = ColorObject.Green;
    //Initialize FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "Sample";
    savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
    //Create a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();
    //Save changes to the specified storage file
    await pptxDoc.SaveAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Create a PowerPoint presentation.
using (IPresentation pptxDoc = Presentation.Create())
{
    //Access the first master slide in PowerPoint file.
    IMasterSlide masterSlide = pptxDoc.Masters[0];
    //Retrieve the background instance.
    IBackground background = masterSlide.Background;
    //Set the fill type for background as Solid fill.
    background.Fill.FillType = FillType.Solid;
    //Get the instance for solid Fill.
    ISolidFill solidFill = background.Fill.SolidFill;
    //Set the color for solid fill object.
    solidFill.Color = ColorObject.Green;
    //Save the PowerPoint Presentation to MemoryStream.
    MemoryStream outputStream = new MemoryStream();
    pptxDoc.Save(outputStream);
    outputStream.Position = 0;
    //Download PowerPoint Presentation in the browser.
    return File(outputStream, "application/vnd.openxmlformats-officedocument.presentationml.presentation", "Sample.pptx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a PowerPoint presentation.
using (IPresentation pptxDoc = Presentation.Create())
{
    //Access the first master slide in PowerPoint file.
    IMasterSlide masterSlide = pptxDoc.Masters[0];
    //Retrieve the background instance.
    IBackground background = masterSlide.Background;
    //Set the fill type for background as Solid fill.
    background.Fill.FillType = FillType.Solid;
    //Get the instance for solid Fill.
    ISolidFill solidFill = background.Fill.SolidFill;
    //Set the color for solid fill object.
    solidFill.Color = ColorObject.Green;
    //Save the PowerPoint Presentation to MemoryStream.
    MemoryStream outputStream = new MemoryStream();
    pptxDoc.Save(outputStream);
    outputStream.Position = 0;
    //The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer presentation/xamarin section for respective code samples.
    if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
        Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", outputStream);
    else
        Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", outputStream);
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Master-and-Layout-slides/Modify-PowerPoint-master-slide-background).

## Create a custom LayoutSlide

The real-world scenarios always require more predefined templates. The Syncfusion PowerPoint library lets you build your own custom layout designs and use them to create individual slides.

The following code example demonstrates how to create new custom layout slide and access layout slide in Presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Create a PowerPoint instance
IPresentation pptxDoc = Presentation.Create();
//Add a new LayoutSlide to the PowerPoint file
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");
//Add a shape to the LayoutSlide
IShape shape = layoutSlide.Shapes.AddShape(AutoShapeType.Diamond, 30, 20, 400, 300);
//Change the background color for LayoutSlide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);
//Save the PowerPoint file
pptxDoc.Save("LayoutSlide.pptx");
//Close the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a PowerPoint instance
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a new LayoutSlide to the PowerPoint file
Dim layoutSlide As ILayoutSlide = pptxDoc.Masters(0).LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout")
'Add a shape to the LayoutSlide
Dim shape As IShape = layoutSlide.Shapes.AddShape(AutoShapeType.Diamond, 30, 20, 400, 300)
'Change the background color for LayoutSlide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90)
'Save the PowerPoint file
pptxDoc.Save("LayoutSlide.pptx")
'Close the Presentation instance
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Master-and-Layout-slides/Create-custom-layout-slide).