---
title: Working with shapes in PowerPoint Presentation
description: Working with shapes in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Shapes

## Adding shapes to a slide

In every slide, there is a shape collection that can contain any form of graphical objects such as autoShape, chart, text, or picture.  You can add any shape element to this collection. The IShape is the base type for the shape elements.

The following code example demonstrates how to add an autoshape and image to the shape collection of a slide.

{% tabs %}

{% highlight c# %}

//Creates an instance for PowerPoint

IPresentation presentation = Presentation.Create();

//Adds a blank slide to presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank); 

//Adds normal shape to slide

IShape autoShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);          

//Creates an instance for image as stream

Stream imageStream = File.Open("Image.jpg", FileMode.Open);

//Add picture to the shape collection

IPicture picture = slide.Shapes.AddPicture(imageStream, 373, 83, 526, 382);            

//Saves the presentation

presentation.Save("Sample.pptx");

//Closes the stream

imageStream.Close();

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates an instance for PowerPoint

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds a blank slide to presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds normal shape to slide

Dim autoShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)

'Creates an instance for image as stream

Dim imageStream As Stream = File.Open("Image.jpg", FileMode.Open)

'Adds picture to the shape collection

Dim picture As IPicture = slide.Shapes.AddPicture(imageStream, 373, 83, 500, 382)

'Saves the presentation

presentationDocument.Save("Sample.pptx")

'Closes the stream

imageStream.Close()

'closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Iterate through shapes

You can iterate through the shapes in a PowerPoint slide. The following code example demonstrates how to iterate through the shapes present in a slide for modifying its properties.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from the file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Iterates through shapes in a slide and sets title

foreach(IShape shape in presentation.Slides[0].Shapes)

{

	if (shape is IPicture)

		shape.Title = "Picture";

	else if (shape is IShape)

		shape.Title = "AutoShape";

}

//Saves the presentation

presentation.Save("Output.pptx");

//closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}


'Opens an existing presentation from the file system.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Iterates through shapes in a slide and sets title

For Each shape As IShape In presentationDocument.Slides(0).Shapes

If TypeOf shape Is IPicture Then

shape.Title = "Picture"

ElseIf TypeOf shape Is IShape Then

shape.Title = "AutoShape"

End If

Next

'Saves the presentation

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Specify shape properties

The shape properties can be used to format and modify the shapes in a slide. The following code example demonstrates how to apply formatting to a shape.

{% tabs %}

{% highlight c# %}

//Creates instance for PowerPoint

IPresentation presentation = Presentation.Open("Sample.pptx");

//Gets the first slide of the presentation

ISlide slide = presentation.Slides[0];

//Gets the shape of the slide

IShape shape = slide.Shapes[0] as IShape;

//Sets the shape name.

shape.ShapeName = "Shape1";

//Retrieves the lineformat instance of the shape.

ILineFormat lineFormat = shape.LineFormat;

//Sets the dashstyle of the lineformat.

lineFormat.DashStyle = LineDashStyle.DashDotDot;

//Sets the weight of the lineformat.

lineFormat.Weight = 3;

//Sets the pattern fill type to shape

shape.Fill.FillType = FillType.Pattern;

//Chooses the type of pattern 

shape.Fill.PatternFill.Pattern = PatternFillType.DashedDownwardDiagonal;

//Sets the fore color

shape.Fill.PatternFill.ForeColor = ColorObject.AliceBlue;

//Sets the back color

shape.Fill.PatternFill.BackColor = ColorObject.DarkSalmon;

//Saves the presentation

presentation.Save("Output.pptx");           

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}


'Creates instance for PowerPoint

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Gets the first slide of the presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Gets the shape of the slide

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Sets the shape name.

shape.ShapeName = "Shape1"

'Retrieves the lineformat instance of the shape.

Dim lineFormat As ILineFormat = shape.LineFormat

'Sets the dashstyle of the lineformat.

lineFormat.DashStyle = LineDashStyle.DashDotDot

'Sets the weight of the lineformat.

lineFormat.Weight = 3

'Sets the pattern fill type to shape

shape.Fill.FillType = FillType.Pattern

'Chooses the type of pattern 

shape.Fill.PatternFill.Pattern = PatternFillType.DashedDownwardDiagonal

'Sets the fore color

shape.Fill.PatternFill.ForeColor = ColorObject.AliceBlue

'Sets the back color

shape.Fill.PatternFill.BackColor = ColorObject.DarkSalmon

'Saves the presentation

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Remove the shapes

The shapes can be removed from a slide by its instance or by its index position in the shape collection. The following code example demonstrates how to remove the shapes from a slide. 

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieves the first slide from presentation

ISlide slide = presentation.Slides[0];

//Retrieves the first shape.

IShape shape = slide.Shapes[0] as IShape;

//Removes the shape from the shape collection.

slide.Shapes.Remove(shape);

//Saves the presentation to the file system.

presentation.Save("Result.pptx");

//Closes the presentation.

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation from file system.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Retrieves the first shape.

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Removes the shape from the shape collection.

slide.Shapes.Remove(shape)

'Saves the presentation to the file system.

presentationDocument.Save("Result.pptx")

'Closes the presentation.

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

