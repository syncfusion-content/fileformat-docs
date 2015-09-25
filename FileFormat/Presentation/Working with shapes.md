---
layout: Post
title: Working with shapes in PowerPoint Presentation
description: Working with shapes in PowerPoint Presentation
platform: FileFormats
control: Presentation
documentation: UG
---
# Working with Shapes

## Adding shapes to a slide

In every slide there will be a shape collection which can contain any form of graphical objects such as an [autoShape](https://msdn.microsoft.com/en-us/library/dd439450(v=office.12).aspx# ""), chart, text or picture.  You can add any shape elements to this collection. The [IShape](http://www.google.com/# "") is the base type for the shape elements.

The below code snippet demonstrates adding an autoshape and image to the shape collection of a slide.

{% highlight c# %}
[C#]

//Create an instance for PowerPoint

IPresentation presentation = Presentation.Create();

//Add a blank slide to presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank); 

//Add normal shape to slide

IShape autoShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);          

//Create an instance for image as stream

Stream imageStream = File.Open("Image.jpg", FileMode.Open);

//Add picture to the shape collection

IPicture picture = slide.Shapes.AddPicture(imageStream, 373, 83, 526, 382);            

//Save the presentation

presentation.Save("Sample.pptx");

//Close the stream

imageStream.Close();

//close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create an instance for PowerPoint

Dim presentation_1 As IPresentation = Presentation.Create()

'Add a blank slide to presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

'Add normal shape to slide

Dim autoShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)

'Create an instance for image as stream

Dim imageStream As Stream = File.Open("Image.jpg", FileMode.Open)

'Add picture to the shape collection

Dim picture As IPicture = slide.Shapes.AddPicture(imageStream, 373, 83, 500, 382)

'Save the presentation

presentation_1.Save("Sample.pptx")

'Close the stream

imageStream.Close()

'close the presentation

presentation_1.Close()



{% endhighlight %}

## Iterating through shapes

We can iterate through the shapes in a PowerPoint slide. The below code snippet demonstrates iterating through the shapes present in a slide for modifying its properties.

{% highlight c# %}
[C#]

//Open an existing presentation from the file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Iterate through shapes in a slide and set title

foreach(IShape shape in presentation.Slides[0].Shapes)

{

if (shape is IPicture)

shape.Title = "Picture";

else if (shape is IShape)

shape.Title = "AutoShape";

}

//Save the presentation

presentation.Save("Output.pptx");

//close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation from the file system.

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Iterate through shapes in a slide and set title

For Each shape As IShape In presentation_1.Slides(0).Shapes

If TypeOf shape Is IPicture Then

shape.Title = "Picture"

ElseIf TypeOf shape Is IShape Then

shape.Title = "AutoShape"

End If

Next

'Save the presentation

presentation_1.Save("Output.pptx")

'close the presentation

presentation_1.Close()



{% endhighlight %}

## Specifying shape properties

The shape properties can be used to format and modify the shapes in a slide. The following code snippet demonstrates applying formatting to a shape

{% highlight c# %}
[C#]

//Create instance for PowerPoint

IPresentation presentation = Presentation.Open("Sample.pptx");

//Get the first slide of the presentation

ISlide slide = presentation.Slides[0];

//Get the shape of the slide

IShape shape = slide.Shapes[0] as IShape;

//Set the shape name.

shape.ShapeName = "Shape1";

//Retrieve the lineformat instance of the shape.

ILineFormat lineFormat = shape.LineFormat;

//Set the dashstyle of the lineformat.

lineFormat.DashStyle = LineDashStyle.DashDotDot;

//Set the weight of the lineformat.

lineFormat.Weight = 3;

//Set the pattern fill type to shape

shape.Fill.FillType = FillType.Pattern;

//Choose the type of pattern 

shape.Fill.PatternFill.Pattern = PatternFillType.DashedDownwardDiagonal;

//Set the fore color

shape.Fill.PatternFill.ForeColor = ColorObject.AliceBlue;

//Set the back color

shape.Fill.PatternFill.BackColor = ColorObject.DarkSalmon;

//Save the presentation

presentation.Save("Output.pptx");           

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create instance for PowerPoint

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Get the first slide of the presentation

Dim slide As ISlide = presentation_1.Slides(0)

'Get the shape of the slide

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Set the shape name.

shape.ShapeName = "Shape1"

'Retrieve the lineformat instance of the shape.

Dim lineFormat As ILineFormat = shape.LineFormat

'Set the dashstyle of the lineformat.

lineFormat.DashStyle = LineDashStyle.DashDotDot

'Set the weight of the lineformat.

lineFormat.Weight = 3

'Set the pattern fill type to shape

shape.Fill.FillType = FillType.Pattern

'Choose the type of pattern 

shape.Fill.PatternFill.Pattern = PatternFillType.DashedDownwardDiagonal

'Set the fore color

shape.Fill.PatternFill.ForeColor = ColorObject.AliceBlue

'Set the back color

shape.Fill.PatternFill.BackColor = ColorObject.DarkSalmon

'Save the presentation

presentation_1.Save("Output.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Removing the shapes

The shapes can be removed from a slide by its instance or by its index position in the shape collection. The below code snippet demonstrates removing the shapes from a slide. 

{% highlight c# %}
[C#]

//Open an existing presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieve the first slide from presentation

ISlide slide = presentation.Slides[0];

//Retrieve the first shape.

IShape shape = slide.Shapes[0] as IShape;

//Remove the shape from the shape collection.

slide.Shapes.Remove(shape);

//Save the presentation to the file system.

presentation.Save("Result.pptx");

//Close the presentation.

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation from file system.

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Retrieve the first slide from presentation

Dim slide As ISlide = presentation_1.Slides(0)

'Retrieve the first shape.

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Remove the shape from the shape collection.

slide.Shapes.Remove(shape)

'Save the presentation to the file system.

presentation_1.Save("Result.pptx")

'Close the presentation.

presentation_1.Close()



{% endhighlight %}

