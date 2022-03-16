---
title: Create, read and edit Master and Layout slides in CSharp |Syncfusion|
description: Create, read and edit Master slides and Layout slides in CSharp
platform: file-formats
control: PowerPoint
documentation: UG
---

# Create and edit Master and Layout slides

To get all the slides in same format, you should perform those changes in the Slide Master or Layout Master. The changes will be applied to all the slides, which inherits the master slide or layout slide.

The [Syncfusion PowerPoint library](https://www.syncfusion.com/powerpoint-framework/net) supports the following:
<ol>
<li>Access the <b>MasterSlide</b> in PowerPoint file.</li>
<li>Add <b>LayoutSlide</b> to the <b>MasterSlide</b>.</li>
<li>Customize the <b>LayoutSlide</b>.</li>
<li>Create a slide with 9 pre-defined layout slides.</li>
<li>Customize the layout slides to fit your own scenarios.</li>
</ol>

## Access the MasterSlide

In PowerPoint presentation, the **MasterSlide** is the top slide that controls all information about the theme, layout, background, color, fonts, and positioning of all slides. Using this MasterSlide, you can easily adjust the look of an existing theme or make overall changes to all your slides.

The following code example demonstrates how to access the **MasterSlide** in a PowerPoint presentation.

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