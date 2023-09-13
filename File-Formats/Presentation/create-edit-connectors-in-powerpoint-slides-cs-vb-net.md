---
title: Add and edit connectors in PowerPoint slides | Syncfusion |
description: Code examples to create and edit PowerPoint connectors in .NET, C#, web, ASP.NET, UWP, MVC, Xamarin and .NET Core
platform: file-formats
control: Syncfusion PowerPoint presentation
documentation: 
keywords: PowerPoint, slide, connectors, pptx, shapes
---

# Adding connectors in PowerPoint slides

Essential Presentation library supports adding, editing, and removing the connectors in a PowerPoint file. The following code example demonstrates how to add a connector between two shapes.

The following code example demonstrates how to add a connector in PowerPoint slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
using (IPresentation pptxDoc = Presentation.Create())
{
    //Add a slide to the PowerPoint file
    ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
    //Add a rectangle shape on the slide
    IShape rectangle = slide.Shapes.AddShape(AutoShapeType.Rectangle, 200, 300, 100, 100);
    //Add an oval shape on the slide
    IShape oval = slide.Shapes.AddShape(AutoShapeType.Oval, 400, 10, 100, 100);
    //Add elbow connector on the slide and connect the end points of connector with specified port positions 0 and 4 of the beginning and end shapes
    IConnector connector = slide.Shapes.AddConnector(ConnectorType.Elbow, rectangle, 0, oval, 4);
    //Save the PowerPoint Presentation as stream
    FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
    pptxDoc.Save(outputStream);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create a new PowerPoint file
using (IPresentation pptxDoc = Presentation.Create())
{
    //Add a slide to the PowerPoint file
    ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
    //Add a rectangle shape on the slide
    IShape rectangle = slide.Shapes.AddShape(AutoShapeType.Rectangle, 200, 300, 100, 100);
    //Add an oval shape on the slide
    IShape oval = slide.Shapes.AddShape(AutoShapeType.Oval, 400, 10, 100, 100);
    //Add elbow connector on the slide and connect the end points of connector with specified port positions 0 and 4 of the beginning and end shapes
    IConnector connector = slide.Shapes.AddConnector(ConnectorType.Elbow, rectangle, 0, oval, 4);
    //Save the PowerPoint file
    pptxDoc.Save("Sample.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create a new PowerPoint file
Using pptxDoc As IPresentation = Presentation.Create
    'Add a slide to the PowerPoint file
    Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
    'Add a rectangle shape on the slide
    Dim rectangle As IShape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 200, 300, 100, 100)
    'Add an oval shape on the slide
    Dim oval As IShape = slide.Shapes.AddShape(AutoShapeType.Oval, 400, 10, 100, 100)
    'Add elbow connector on the slide and connect the end points of connector with specified port positions 0 and 4 of the beginning and end shapes
    Dim connector As IConnector = slide.Shapes.AddConnector(ConnectorType.Elbow, rectangle, 0, oval, 4)
    'Save the PowerPoint file
    pptxDoc.Save("Sample.pptx")
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Connectors/Add-PowerPoint-connectors).

## Adding a single point connector

You can also add a connector to a source shape without any destination shapes. The following code example demonstrates how to add a connector with single point connection.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create a new PowerPoint file
using (IPresentation pptxDoc = Presentation.Create())
{
    // Add a slide to the PowerPoint file.   
    ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
    //Add a rectangle shape on the slide
    IShape rectangle = slide.Shapes.AddShape(AutoShapeType.Rectangle, 420, 250, 100, 100);
    //Add connector with specified bounds
    IConnector connector = slide.Shapes.AddConnector(ConnectorType.Straight, 0, 0, 470, 150);
    //Connect the beginning point of the connector with rectangle shape
    connector.BeginConnect(rectangle, 0);
    //Set the beginning cap of the connector as arrow
    connector.LineFormat.BeginArrowheadStyle = ArrowheadStyle.Arrow;
    //Change the connector color
    //Set the connector fill type as solid
    connector.LineFormat.Fill.FillType = FillType.Solid;
    //Set the connector solid fill as black
    connector.LineFormat.Fill.SolidFill.Color = ColorObject.Black;
    //Save the PowerPoint Presentation as stream
    FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
    pptxDoc.Save(outputStream);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create a new PowerPoint file
using (IPresentation pptxDoc = Presentation.Create())
{
    // Add a slide to the PowerPoint file.   
    ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
    //Add a rectangle shape on the slide
    IShape rectangle = slide.Shapes.AddShape(AutoShapeType.Rectangle, 420, 250, 100, 100);
    //Add connector with specified bounds
    IConnector connector = slide.Shapes.AddConnector(ConnectorType.Straight, 0, 0, 470, 150);
    //Connect the beginning point of the connector with rectangle shape
    connector.BeginConnect(rectangle, 0);
    //Set the beginning cap of the connector as arrow
    connector.LineFormat.BeginArrowheadStyle = ArrowheadStyle.Arrow;
    //Change the connector color
    //Set the connector fill type as solid
    connector.LineFormat.Fill.FillType = FillType.Solid;
    //Set the connector solid fill as black
    connector.LineFormat.Fill.SolidFill.Color = ColorObject.Black;
    //Save the PowerPoint file
    pptxDoc.Save("Sample.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create a new PowerPoint file
Using pptxDoc As IPresentation = Presentation.Create
    'Add a slide to the PowerPoint file
    Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
    'Add a rectangle shape on the slide
    Dim rectangle As IShape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 420, 250, 100, 100)
    'Add connector with specified bounds
    Dim connector As IConnector = slide.Shapes.AddConnector(ConnectorType.Straight, 0, 0, 470, 150)
    'Connect the beginning point of the connector with rectangle shape
    connector.BeginConnect(rectangle, 0)
    'Set the beginning cap of the connector as arrow
    connector.LineFormat.BeginArrowheadStyle = ArrowheadStyle.Arrow
    'Change the connector color
    'Set the connector fill type as solid
    connector.LineFormat.Fill.FillType = FillType.Solid
    'Set the connector solid fill as black
    connector.LineFormat.Fill.SolidFill.Color = ColorObject.Black
    'Save the PowerPoint file
    pptxDoc.Save("Sample.pptx")
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Connectors/Add-single-point-connector).

## Editing a connector in PowerPoint slide

The following code example demonstrates how to edit an existing connector in a PowerPoint slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads an PowerPoint file in stream
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
//Opens the loaded PowerPoint file
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
    //Get the first slide of a PowerPoint file
    ISlide slide = pptxDoc.Slides[0];
    //Get the connector from a slide
    IConnector connector = slide.Shapes[2] as IConnector;
    //Set the begin cap for the connector
    connector.LineFormat.BeginArrowheadStyle = ArrowheadStyle.ArrowOpen;
    //Set the line format for the connector
    connector.LineFormat.DashStyle = LineDashStyle.DashDotDot;
    //Disconnect the end connection of the connector if end point get connected
    if (connector.EndConnectedShape != null)
        connector.EndDisconnect();
    //Insert a triangle shape into slide
    IShape triangle = slide.Shapes.AddShape(AutoShapeType.IsoscelesTriangle, 600, 500, 150, 150);
    //Declare the end connection site index
    int connectionSiteIndex = 4;
    //Reconnect the end point of connector with triangle shape if its connection site count is greater than 4
    if (connectionSiteIndex < triangle.ConnectionSiteCount)
        connector.EndConnect(triangle, connectionSiteIndex);
    //Save the PowerPoint Presentation as stream
    FileStream outputStream = new FileStream("Connector.pptx", FileMode.Create);
    pptxDoc.Save(outputStream);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Open an existing PowerPoint file
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
    //Get the first slide of a PowerPoint file
    ISlide slide = pptxDoc.Slides[0];
    //Get the connector from a slide
    IConnector connector = slide.Shapes[2] as IConnector;
    //Set the begin cap for the connector
    connector.LineFormat.BeginArrowheadStyle = ArrowheadStyle.ArrowOpen;
    //Set the line format for the connector
    connector.LineFormat.DashStyle = LineDashStyle.DashDotDot;
    //Disconnect the end connection of the connector if end point get connected
    if (connector.EndConnectedShape != null)
        connector.EndDisconnect();
    //Insert a triangle shape into slide
    IShape triangle = slide.Shapes.AddShape(AutoShapeType.IsoscelesTriangle, 600, 500, 150, 150);
    //Declare the end connection site index
    int connectionSiteIndex = 4;
    //Reconnect the end point of connector with triangle shape if its connection site count is greater than 4
    if (connectionSiteIndex < triangle.ConnectionSiteCount)
        connector.EndConnect(triangle, connectionSiteIndex);
    //Save the PowerPoint file
    pptxDoc.Save("Connector.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
' Open an existing PowerPoint file.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
    'Get the first slide of a PowerPoint file
    Dim slide As ISlide = pptxDoc.Slides(2)
    'Get the connector from a slide
    Dim connector As IConnector = CType(slide.Shapes(2), IConnector)
    'Set the beginning cap for the connector
    connector.LineFormat.BeginArrowheadStyle = ArrowheadStyle.ArrowOpen
    'Set the line format for the connector
    connector.LineFormat.DashStyle = LineDashStyle.DashDotDot
    'Disconnect the end connection of the connector if end point get connected
    If (Not (connector.EndConnectedShape) Is Nothing) Then
        connector.EndDisconnect()
    End If
    'Insert a triangle shape into slide
    Dim triangle As IShape = slide.Shapes.AddShape(AutoShapeType.IsoscelesTriangle, 600, 500, 150, 150)
    'Declare the end connection site index
    Dim connectionSiteIndex As Integer = 4
    'Reconnect the end point of connector with triangle shape if its connection site count is greater than 4
    If (connectionSiteIndex < triangle.ConnectionSiteCount) Then
        connector.EndConnect(triangle, connectionSiteIndex)
    End If
    'Save the PowerPoint file
    pptxDoc.Save("Connector.pptx")   
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Connectors/Modify-existing-connector).

## Updating the positions of the connector in PowerPoint slide

The following code example demonstrates how to update a connector’s position when a source shape position is changed.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads an PowerPoint file in stream
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
//Opens the loaded PowerPoint file
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
    //Get the first slide of a PowerPoint file
    ISlide slide = pptxDoc.Slides[0];
    //Get the rectangle shape from a slide
    IShape rectangle = slide.Shapes[0] as IShape;
    //Get the connector from a slide
    IConnector connector = slide.Shapes[2] as IConnector;
    //Change the X and Y position of the rectangle
    rectangle.Left = 600;
    rectangle.Top = 200;
    //Update the connector to connect with previously updated shape
    connector.Update();
   //Save the PowerPoint Presentation as stream
   FileStream outputStream = new FileStream("Connector.pptx", FileMode.Create);
   pptxDoc.Save(outputStream);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Open an existing PowerPoint file
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
    //Get the first slide of a PowerPoint file
    ISlide slide = pptxDoc.Slides[0];
    //Get the rectangle shape from a slide
    IShape rectangle = slide.Shapes[0] as IShape;
    //Get the connector from a slide
    IConnector connector = slide.Shapes[2] as IConnector;
    //Change the X and Y position of the rectangle
    rectangle.Left = 600;
    rectangle.Top = 200;
    //Update the connector to connect with previously updated shape
    connector.Update();
    //Save the PowerPoint file
    pptxDoc.Save("Connector.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Open an existing PowerPoint file
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
    'Get the first slide of a PowerPoint file
    Dim slide As ISlide = pptxDoc.Slides(0)
    'Get the rectangle shape from a slide
    Dim rectangle As IShape = CType(slide.Shapes(0), IShape)
    'Get the connector from a slide
    Dim connector As IConnector = CType(slide.Shapes(2), IConnector)
    'Change the X and Y position of the rectangle
    rectangle.Left = 600
    rectangle.Top = 200
    'Update the connector to connect with previously updated shape
    connector.Update()
    'Save the PowerPoint file
    pptxDoc.Save("Connector.pptx")
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Connectors/Update-connector-position).

## Removing a connector from PowerPoint shapes

The following code example demonstrates how to remove a connector from PowerPoint slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads an PowerPoint file in stream
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
//Opens the loaded PowerPoint file
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
    //Get the first slide of a PowerPoint file
    ISlide slide = pptxDoc.Slides[0];                
    //Get the connector from a slide
    IConnector connector = slide.Shapes[2] as IConnector;
    //Remove the connector from slide
    slide.Shapes.Remove(connector);
    //Save the PowerPoint Presentation as stream
    FileStream outputStream = new FileStream("Connector.pptx", FileMode.Create);
    pptxDoc.Save(outputStream);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Open an existing PowerPoint file
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
    //Get the first slide of a PowerPoint file
    ISlide slide = pptxDoc.Slides[0];
    //Get the connector from a slide
    IConnector connector = slide.Shapes[2] as IConnector;
    //Remove the connector from slide
    slide.Shapes.Remove(connector);
    //Save the PowerPoint file
    pptxDoc.Save("Connector.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Open an existing PowerPoint file
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
    'Get the first slide of a PowerPoint file
    Dim slide As ISlide = pptxDoc.Slides(0)
    'Get the connector from a slide
    Dim connector As IConnector = CType(slide.Shapes(2), IConnector)
    'Remove the connector from slide
    slide.Shapes.Remove(connector)
    'Save the PowerPoint file
    pptxDoc.Save("Connector.pptx")
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Connectors/Remove-connector-from-shapes).