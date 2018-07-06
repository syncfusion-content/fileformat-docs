---
title: Working with Animations
description: Working with Animations
platform: Windows Forms, WPF, ASP.NET Web, ASP.NET MVC, ASP.NET Core, JavaScript, UWP and Xamarin.
control: Essential Presentation
documentation: UG
keywords: PowerPoint animation, slide animation, shape animation, pptx animation
---
# Working with Animations

Animations are visual effects for the objects in PowerPoint presentation and animation helps to make a PowerPoint presentation more dynamic. Animation effects can be grouped into four categories.,

1. Entrance
2. Emphasis
3. Exit
4. Motion paths

Entrance effects can be set to enter the objects with animations during slide show. Emphasis effects animate the objects on the spot. Exit effects allow objects to leave the slide show with animations. Motion Paths allow objects to move around the slide show. Each effect contains variables such as start (On click, with previous and after previous), delay, speed, repeat, and trigger. This makes animations more flexible and interactive. 

Syncfusion Presentation library allows you to animate the text, pictures, shapes, tables, SmartArt graphics, and charts in PowerPoint presentation.

## Adding animation effect to shapes

Animation effects can be added to shapes, images, tables, charts and SmartArt diagrams. The following code example demonstrates how to add an animation effect to an shape.

{% tabs %}
{% highlight c# %}

//Create an instance for PowerPoint

using (IPresentation pptxDoc = Presentation.Create())

{

//Add a blank slide to Presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide

IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects

ISequence sequence = slide.Timeline.MainSequence;

//Add bounce effect to the shape

IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.Bounce, EffectSubtype.None, EffectTriggerType.OnClick);

//Save the Presentation

pptxDoc.Save("Sample.pptx");

}

{% endhighlight %}
{% highlight vb.net %}

'Create an instance for PowerPoint

Using pptxDoc As IPresentation = Presentation.Create()

   'Add a blank slide to Presentation

    Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

    'Add normal shape to slide

    Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)

    'Access the animation sequence to create effects

    Dim sequence As ISequence = slide.Timeline.MainSequence

    'Add bounce effect to the shape

    Dim bounceEffect As IEffect = sequence.AddEffect(cubeShape, EffectType.Bounce, EffectSubtype.None, EffectTriggerType.OnClick)

    'Save the Presentation

    pptxDoc.Save("Sample.pptx")

End Using

{% endhighlight %}

{% endtabs %}

## Adding interactive animation

Animations can be interactive when it depends on another slide element., for example, an animation associated with a rectangle is triggered when user clicks an oval shape in the slide. The following code example demonstrates how to set an interactive animation.

{% tabs %}

{% highlight c# %}

//Create an instance for PowerPoint

using (IPresentation pptxDoc = Presentation.Create())

{

//Add a blank slide to Presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide

IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Add a shape to act as button

IShape buttonShape = slide.Shapes.AddShape(AutoShapeType.Oval, 100,100,50,50);

//Create the interactive sequence to make the animation effects interactive by triggering with button click

ISequence interactiveSequence = slide.Timeline.InteractiveSequences.Add(buttonShape);

//Add Fly effect with top subtype to animate the shape as fly from top

IEffect bounceEffect = interactiveSequence.AddEffect(cubeShape, EffectType.Fly, EffectSubtype.Top, EffectTriggerType.OnClick);

//Save the Presentation

pptxDoc.Save("Sample.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Create an instance for PowerPoint

Using pptxDoc As IPresentation = Presentation.Create()

   'Add a blank slide to Presentation

   Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

   'Add normal shape to slide

   Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)

   'Add a shape to act as button

   Dim buttonShape As IShape = slide.Shapes.AddShape(AutoShapeType.Oval, 100, 100, 50, 50)

   'Create the interactive sequence to make the animation effects interactive by triggering with button click

   Dim interactiveSequence As ISequence = slide.Timeline.InteractiveSequences.Add(buttonShape)

   'Add Fly effect with top subtype to animate the shape as fly from top

   Dim bounceEffect As IEffect = interactiveSequence.AddEffect(cubeShape, EffectType.Fly, EffectSubtype.Top, EffectTriggerType.OnClick)

   'Save the Presentation

   pptxDoc.Save("Sample.pptx")

End Using

{% endhighlight %}

{% endtabs %}

## Adding animation to text

Animation effects can be applied to text. The following code example demonstrated how to set an animation effect to a text.

{% tabs %}

{% highlight c# %}

//Open an existing Presentation from file system

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Retrieve the first slide from Presentation

ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape

IShape shape = slide.Shapes[0] as IShape;

//Access the animation sequence to create effects

ISequence sequence = slide.Timeline.MainSequence;

//Add swivel effect with vertical subtype to the shape, build type is used to represent the animate level of the paragraph

IEffect bounceEffect = sequence.AddEffect(shape, EffectType.Swivel, EffectSubtype.Vertical, EffectTriggerType.OnClick, BuildType.ByLevelParagraphs1);

//Save the Presentation to the file system

pptxDoc.Save("Result.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Retrieve the first slide from Presentation

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieve the first shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Access the animation sequence to create effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Add swivel effect with vertical subtype to the shape, build type is used to represent the animate level of the paragraph

   Dim bounceEffect As IEffect = sequence.AddEffect(shape, EffectType.Swivel, EffectSubtype.Vertical, EffectTriggerType.OnClick, BuildType.ByLevelParagraphs1)

   'Save the Presentation to the file system

   pptxDoc.Save("Result.pptx")

End Using

{% endhighlight %}

{% endtabs %}

## Adding exit animation effect

When you add common animation effects for both entrance and exit types, animation is applied with entrance effect by default. The following code example demonstrates how to set exist type animation for a shape.

{% tabs %}

{% highlight c# %}

//Create an instance for PowerPoint

using (IPresentation pptxDoc = Presentation.Create())

{

//Add a blank slide to Presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide

IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects

ISequence sequence = slide.Timeline.MainSequence;

//Add random bars effect to the shape

IEffect effect = sequence.AddEffect(cubeShape, EffectType.RandomBars, EffectSubtype.None, EffectTriggerType.OnClick);

//Change the preset class type of the effect from default entrance to exit

effect.PresetClassType = EffectPresetClassType.Exit;

//Save the Presentation

pptxDoc.Save("Sample.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Create an instance for PowerPoint

Using pptxDoc As IPresentation = Presentation.Create()

   'Add a blank slide to Presentation

   Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

   'Add normal shape to slide

   Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)

   'Access the animation sequence to create effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Add random bars effect to the shape

   Dim effect As IEffect = sequence.AddEffect(cubeShape, EffectType.RandomBars, EffectSubtype.None, EffectTriggerType.OnClick)

   'Change the preset class type of the effect from default entrance to exit

   effect.PresetClassType = EffectPresetClassType.[Exit]

   'Save the Presentation

   pptxDoc.Save("Sample.pptx")

End Using

{% endhighlight %}

{% endtabs %}

## Edit existing animation effect

The Presentation library allows you to edit the animations in existing presentations. The following example demonstrates how to modify an existing animation applied to a shape.

{% tabs %}

{% highlight c# %}

//Open an existing Presentation from file system

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Retrieve the first slide from Presentation

ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape

IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects

ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the particular shape

IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Iterate the animation effect to make the change

IEffect animationEffect = animationEffects[0];

//Change the animation effect type from swivel to GrowAndTurn

animationEffect.Type = EffectType.GrowAndTurn;

//Save the Presentation to the file system

pptxDoc.Save("Animation.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Open an existing Presentation from file system

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Retrieve the first slide from Presentation

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieve the first shape.

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Access the animation main sequence to modify the effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Get the animation effects of the particular shape

   Dim animationEffects As IEffect() = sequence.GetEffectsByShape(shape)

   'Iterate the animation effect to make the change

   Dim animationEffect As IEffect = animationEffects(0)

   'Change the animation effect type from swivel to GrowAndTurn

   animationEffect.Type = EffectType.GrowAndTurn

   'Save the Presentation to the file system

   pptxDoc.Save("Animation.pptx")

End Using

{% endhighlight %}

{% endtabs %}

## Modifying animation effect sub type

Presentation library allows you to edit the sub type of animations effects in existing presentations. The following example demonstrates how to modify a sub type applied to the existing animation.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from file system

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Retrieves the first slide from Presentation

ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape

IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects

ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide            

IEffect wheelEffect = sequence[0] as IEffect;

//Change the wheel animation effect sub type from 2 spoke to 4 spoke

wheelEffect.Subtype = EffectSubtype.Wheel4;

//Saves the Presentation to the file system

pptxDoc.Save("Result.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Retrieves the first slide from Presentation

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieves the first shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Access the animation main sequence to modify the effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Get the required animation effect from the slide            

   Dim wheelEffect As IEffect = TryCast(sequence(0), IEffect)

   'Change the wheel animation effect sub type from 2 spoke to 4 spoke

   wheelEffect.Subtype = EffectSubtype.Wheel4

   'Saves the Presentation to the file system

   pptxDoc.Save("Result.pptx")

End Using

{% endhighlight %}

{% endtabs %}

## Modifying timing of animation effect

Presentation library allows you to edit the animation timing in the existing presentations. The following example demonstrates how to modify an existing animation timing applied to a shape.

{% tabs %}

{% highlight c# %}

//Open an existing Presentation from file system

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Retrieves the first slide from Presentation

ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape

IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects

ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide            

IEffect pathEffect = sequence[0] as IEffect;

//Increase the duration of the animation effect

pathEffect.Behaviors[0].Timing.Duration = 5;

//Saves the Presentation to the file system

pptxDoc.Save("Result.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Open an existing Presentation from file system

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Retrieves the first slide from Presentation

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieves the first shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Access the animation main sequence to modify the effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Get the required animation effect from the slide            

   Dim pathEffect As IEffect = TryCast(sequence(0), IEffect)

   'Increase the duration of the animation effect

   pathEffect.Behaviors(0).Timing.Duration = 5

   'Save the Presentation to the file system.

   pptxDoc.Save("Result.pptx")

End Using

{% endhighlight %}


{% endtabs %}

## Reordering the animation effects

Presentation library allows you to reorder the animation effects in existing presentations. The following example demonstrates how to modify an existing animation order applied to a shape.

{% tabs %}

{% highlight c# %}

//Open the existing presentation

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Iterate the slide

ISlide slide = pptxDoc.Slides[0];

//Iterate the shape

IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence

ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the shape

IEffect[] shapeAnimationEffects = sequence.GetEffectsByShape(shape);

//Get the second animation effect of the shape

IEffect effect = shapeAnimationEffects[1];

//Remove the animation effect from the sequence

sequence.Remove(effect);

//Insert the removed animation effect as first

sequence.Insert(0, effect);

//Save the created presentation

pptxDoc.Save("Output.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Open the existing presentation

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Iterate the slide

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Iterate the shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Iterate the sequence

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Get the animation effects of the shape

   Dim shapeAnimationEffects As IEffect() = sequence.GetEffectsByShape(shape)

   'Get the second animation effect of the shape

   Dim effect As IEffect = shapeAnimationEffects(1)

   'Remove the animation effect from the sequence

   sequence.Remove(effect)

   'Insert the removed animation effect as first

   sequence.Insert(0, effect)

   'Save the created presentation

   pptxDoc.Save("Output.pptx")

End Using

{% endhighlight %}

{% endtabs %}

## Creating custom path animation effect

Presentation library allows you to create and modify the custom animations in presentations. The following example demonstrates how to apply a custom animation to a shape.

{% tabs %}

{% highlight c# %}

//Creates an instance for PowerPoint

using (IPresentation pptxDoc = Presentation.Create())

{

//Adds a blank slide to Presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds normal shape to slide

IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 200, 0, 300, 300);

//Access the animation sequence to create effects

ISequence sequence = slide.Timeline.MainSequence;

//Add user path effect to the shape

IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.PathUser, EffectSubtype.None, EffectTriggerType.OnClick);

//Add commands to the empty path for moving

IMotionEffect motionBehavior = ((IMotionEffect)bounceEffect.Behaviors[0]);

PointF[] points = new PointF[1];

//Add the move command to move the position of the shape

points[0] = new PointF(0, 0);

motionBehavior.Path.Add(MotionCommandPathType.MoveTo, points, MotionPathPointsType.Auto, false);

//Add the line command to move the shape in straight line

points[0] = new PointF(0, 0.25f);

motionBehavior.Path.Add(MotionCommandPathType.LineTo, points, MotionPathPointsType.Auto, false);

//Add the end command to finish the path animation

motionBehavior.Path.Add(MotionCommandPathType.End, null, MotionPathPointsType.Auto, false);

//Saves the Presentation

pptxDoc.Save("Sample.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Creates an instance for PowerPoint

Using pptxDoc As IPresentation = Presentation.Create()

   'Adds a blank slide to Presentation

   Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

   'Adds normal shape to slide

   Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 200, 0, 300, 300)

   'Access the animation sequence to create effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Add user path effect to the shape

   Dim bounceEffect As IEffect = sequence.AddEffect(cubeShape, EffectType.PathUser, EffectSubtype.None, EffectTriggerType.OnClick)

   'Add commands to the empty path for moving

   Dim motionBehavior As IMotionEffect = DirectCast(bounceEffect.Behaviors(0), IMotionEffect)

   Dim points As PointF() = New PointF(0) {}

   'Add the move command to move the position of the shape

   points(0) = New PointF(0, 0)

   motionBehavior.Path.Add(MotionCommandPathType.MoveTo, points, MotionPathPointsType.Auto, False)

   'Add the line command to move the shape in straight line

   points(0) = New PointF(0, 0.25F)

   motionBehavior.Path.Add(MotionCommandPathType.LineTo, points, MotionPathPointsType.Auto, False)

   'Add the end command to finish the path animation

   motionBehavior.Path.Add(MotionCommandPathType.[End], Nothing, MotionPathPointsType.Auto, False)

   'Saves the Presentation

   pptxDoc.Save("Sample.pptx")

End Using

{% endhighlight %}

{% endtabs %}

## Removing animation effect

Presentation library allows you to remove the animation effects from a shape. The following example demonstrates how to remove an animation effect from a shape.

{% tabs %}

{% highlight c# %}

//Open the existing presentation

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Iterate the slide

ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape

IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence

ISequence sequence = slide.Timeline.MainSequence;

//To Remove the animation effects from the shape

//Get the animation effects of the particular shape

IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Remove the animation effect from the main sequence

foreach (IEffect effect in animationEffects)
{
   sequence.Remove(effect);
}

//Save the created presentation

pptxDoc.Save("Result.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Open the existing presentation

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Iterate the slide

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieves the first shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Iterate the sequence

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'To Remove the animation effects from the shape

   'Get the animation effects of the particular shape

   Dim animationEffects As IEffect() = sequence.GetEffectsByShape(shape)

   'Remove the animation effect from the main sequence

   For Each effect As IEffect In animationEffects
      sequence.Remove(effect)
   Next

   'Save the created presentation

   pptxDoc.Save("Result.pptx")

End Using

{% endhighlight %}

{% endtabs %}

## Supported animation effects type

Syncfusion Presentation library supports the following predefined animation effects with the sub types like Microsoft PowerPoint.

<table>
<tr>
<td>
{{'**Effect type**'| markdownify }}
</td>
<td>
{{'**Valid PresetClass type**'| markdownify }}
</td>
<td>
{{'**Valid subtype**'| markdownify }}
</td>
</tr>
<tr>
<td>
Appear
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
CurveUpDown
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Ascend
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Blast
</td>
<td>
Emphasis
</td>
<td>
EffectSubtype.None

</td>
</tr>
<tr>
<td>
Blinds
</td>
<td>
Entrance or Exit

</td>
<td>

EffectSubtype.Horizontal

EffectSubtype.Vertical

</td>
</tr>
<tr>
<td>
Blink
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
BoldFlash
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
BoldReveal
</td>
<td>
Emphasis
</td>
<td>
EffectSubtype.None

</td>
</tr>
<tr>
<td>
Boomerang
</td>
<td>
Entrance or Exit
</td>
<td>
EffectSubtype.None

</td>
</tr>
<tr>
<td>
Bounce
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Box
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.In

EffectSubtype.Out

</td>
</tr>
<tr>
<td>
BrushOnColor
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
BrushOnUnderline
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
CenterRevolve
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
ChangeFillColor
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.Instant

EffectSubtype.Gradual

EffectSubtype.GradualAndCycleClockwise

EffectSubtype.GradualAndCycleCounterClockwise

</td>
</tr>
<tr>
<td>
ChangeFont
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.Instant

EffectSubtype.Gradual

</td>
</tr>
<tr>
<td>
ChangeFontColor
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.Instant

EffectSubtype.Gradual

EffectSubtype.GradualAndCycleClockwise

EffectSubtype.GradualAndCycleCounterClockwise

</td>
</tr>
<tr>
<td>
ChangeFontSize
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.Instant
EffectSubtype.Gradual

</td>
</tr>
<tr>
<td>
ChangeFontStyle
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.FontBold

EffectSubtype.FontItalic

EffectSubtype.FontUnderline


</td>
</tr>
<tr>
<td>
ChangeLineColor
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.Instant

EffectSubtype.Gradual

EffectSubtype.GradualAndCycleClockwise

EffectSubtype.GradualAndCycleCounterClockwise


</td>
</tr>
<tr>
<td>
Checkerboard
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.Vertical

EffectSubtype.Across

</td>
</tr>
<tr>
<td>
Circle
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.In

EffectSubtype.Out

</td>
</tr>
<tr>
<td>
ColorBlend
</td>
<td>
Emphasis
</td>
<td>
EffectSubtype.None

</td>
</tr>
<tr>
<td>
ColorTypewriter
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
ColorWave
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
ComplementaryColor
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
ComplementaryColor2
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Compress
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
ContrastingColor
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Crawl
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.Right

EffectSubtype.Left

EffectSubtype.Top

EffectSubtype.Bottom

</td>
</tr>
<tr>
<td>
Credits
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Custom
</td>
<td>
-
</td>
<td>
-
</td>
</tr>
<tr>
<td>
Darken
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Desaturate
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Descend
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Diamond
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.In
EffectSubtype.Out

</td>
</tr>
<tr>
<td>
Dissolve
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
EaseInOut
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Expand
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Fade
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
FadedSwivel
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
FadedZoom
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
EffectSubtype.Center

</td>
</tr>
<tr>
<td>
FlashBulb
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
FlashOnce
</td>
<td>
Entrance or Exit
</td>
<td>
EffectSubtype.None

</td>
</tr>
<tr>
<td>
Flicker
</td>
<td>
Emphasis
</td>
<td>
EffectSubtype.None

</td>
</tr>
<tr>
<td>
Flip
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Float
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Fly
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.Right

EffectSubtype.Left

EffectSubtype.Top

EffectSubtype.Bottom

EffectSubtype.TopLeft

EffectSubtype.TopRight

EffectSubtype.BottomLeft

EffectSubtype.BottomRight

</td>
</tr>
<tr>
<td>
Fold
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Glide
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
GrowAndTurn
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
GrowShrink
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
GrowWithColor
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Lighten
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
LightSpeed
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Path4PointStar
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Path5PointStar
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Path6PointStar
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Path8PointStar
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathArcDown
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathArcLeft
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathArcRight
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathArcUp
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathBean
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathBounceLeft
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathBounceRight
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathBuzzsaw
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathCircle
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathCrescentMoon
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathCurvedSquare
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathCurvedX
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathCurvyLeft
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathCurvyRight
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathCurvyStar
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathDecayingWave
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathDiagonalDownRight
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathDiagonalUpRight
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathDiamond
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathDown
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathEqualTriangle
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathFigure8Four
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathFootball
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathFunnel
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathHeart
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathHeartbeat
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathHexagon
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathHorizontalFigure8
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathInvertedSquare
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathInvertedTriangle
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathLeft
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathLoopdeLoop
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathNeutron
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathOctagon
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathParallelogram
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathPeanut
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathPentagon
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathPlus
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathPointyStar
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathRight
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathRightTriangle
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathSCurve1
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathSCurve2
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathSineWave
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathSpiralLeft
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathSpiralRight
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathSpring
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathSquare
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathStairsDown
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathSwoosh
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathTeardrop
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathTrapezoid
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathTurnDown
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathTurnRight
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathTurnUp
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathTurnUpRight
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathUp
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathUser
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathVerticalFigure8
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathWave
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
PathZigzag
</td>
<td>
Path

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Peek
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.Bottom

EffectSubtype.Left

EffectSubtype.Right

EffectSubtype.Top

</td>
</tr>
<tr>
<td>
Pinwheel
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Plus
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.In

EffectSubtype.Out

</td>
</tr>
<tr>
<td>
RandomBars
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.Horizontal

EffectSubtype.Vertical

</td>
</tr>
<tr>
<td>
RandomEffects
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
RiseUp
</td>
<td>
Entrance
</td>
<td>
EffectSubtype.None

</td>
</tr>
<tr>
<td>
Shimmer
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Sling
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Spin
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Spinner
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Spiral
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Split
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.HorizontalIn

EffectSubtype.HorizontalOut

EffectSubtype.VerticalIn

EffectSubtype.VerticalOut

</td>
</tr>
<tr>
<td>
Stretch
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.Right

EffectSubtype.Left

EffectSubtype.Top

EffectSubtype.Bottom

EffectSubtype.Across

</td>
</tr>
<tr>
<td>
Strips
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.UpLeft

EffectSubtype.UpRight

EffectSubtype.DownLeft

EffectSubtype.DownRight

</td>
</tr>
<tr>
<td>
StyleEmphasis
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Swish
</td>
<td>
Entrance or Exit
</td>
<td>
EffectSubtype.None

</td>
</tr>
<tr>
<td>
Swivel
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.Horizontal

EffectSubtype.Vertical

</td>
</tr>
<tr>
<td>
Teeter
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Thread
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Transparency
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Unfold
</td>
<td>
Entrance or Exit
</td>
<td>
EffectSubtype.None

</td>
</tr>
<tr>
<td>
VerticalGrow
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Wave
</td>
<td>
Emphasis

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Wedge
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Wheel
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.Wheel1

EffectSubtype.Wheel2

EffectSubtype.Wheel3

EffectSubtype.Wheel4

EffectSubtype.Wheel8

</td>
</tr>
<tr>
<td>
Whip
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Wipe
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.Top

EffectSubtype.Right

EffectSubtype.Bottom

EffectSubtype.Left

</td>
</tr>
<tr>
<td>
Magnify
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.None
</td>
</tr>
<tr>
<td>
Zoom
</td>
<td>
Entrance or Exit

</td>
<td>
EffectSubtype.In

EffectSubtype.Out

EffectSubtype.InCenter - only for Entrance type

EffectSubtype.OutBottom - only for Entrance type

EffectSubtype.OutSlightly

EffectSubtype.InSlightly

EffectSubtype.OutCenter - only for Exit type

EffectSubtype.InBottom - only for Exit type

</td>
</tr>
</table>
