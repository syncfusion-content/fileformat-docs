---
title: Getting Started with Essential Presentation library
description: Getting started with Essential Presentation library; Creating a PowerPoint presentation; Modifying the existing PowerPoint presentation
platform: FileFormats
control: Presentation
documentation: UG
---
# Getting Started

## Create a simple PowerPoint presentation with basic elements from scratch

In this page, you can learn how to create a simple PowerPoint presentation by using Essential Presentation API.

For creating and manipulating a PowerPoint presentation, include the following assemblies in the application.

<table>
<tr>
<td>
Assembly Name<br/><br/></td><td>
Short Description<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Presentation.Base<br/><br/></td><td>
This assembly contains the core features required for creating, reading, manipulating a Presentation file.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to package the Presentation contents.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChart.Base<br/><br/></td><td>
This assembly contains the Office Chart Object model and core features needed for chart creation.<br/><br/></td></tr>
</table>
The following namespaces are required to compile the code discussed in this topic.

* using Syncfusion.Presentation

An entire PowerPoint presentation is represented by an instance of IPresentation interface and it is the root element of Essential Presentation’s DOM.

The following code example demonstrates how to create an instance of IPresentation interface.

{% highlight c# %}
[C#]

//Creates a new instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Creates a new instance of PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Create()



{% endhighlight %}

IPresentation instance has a slide collection that represents the individual slides present within PowerPoint presentation. A slide may contain textual and other graphics contents like shapes, images, charts etc.

The following code example demonstrates how to add a blank slide to a PowerPoint presentation.

{% highlight c# %}
[C#]

//Adds a slide to the PowerPoint presentation

ISlide firstSlide = presentation.Slides.Add(SlideLayoutType.Blank);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Adds a slide to the PowerPoint presentation

Dim firstSlide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)



{% endhighlight %}

Note: The “Point” typographic units are used to add or manipulate any element in a presentation. 

All the textual contents in a Presentation document are represented by Paragraphs. Within the paragraph, textual contents are grouped into one or more child elements as TextParts. Each TextPart represents a region of text with a common set of formatted text.

The following code example demonstrates how to add text into a presentation.

{% highlight c# %}
[C#]

//Adds a textbox in a slide by specifying its position and size

IShape textShape = firstSlide.AddTextBox(100, 75, 756, 200);

//Adds a paragraph into the textShape

IParagraph paragraph = textShape.TextBody.AddParagraph();

//Adds a textPart in the paragraph

ITextPart textPart = paragraph.AddTextPart("Hello Presentation");

//Applies font formatting to the text

textPart.Font.FontSize = 80;

textPart.Font.Bold = true;



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Adds a textbox in a slide by specifying its position and size

Dim textShape As IShape  = firstSlide.AddTextBox(100, 75, 756, 200)

'Adds a paragraph into the textShape

Dim paragraph As IParagraph  = textShape.TextBody.AddParagraph()

'Add a textPart in the paragraph

Dim textPart As ITextPart  = paragraph.AddTextPart("Hello Presentation")

'Applies font formatting to the text

textPart.Font.FontSize = 80

textPart.Font.Bold = True



{% endhighlight %}

Essential Presentation allows you to create simple and multi-level lists that make the content easier for reading. The following code example demonstrates how to add a bulleted list in a paragraph.

{% highlight c# %}
[C#]

//Adds a new paragraph with text.

paragraph = textShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");

//Sets the list type as bullet

paragraph.ListFormat.Type = ListType.Bulleted;

//Sets the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183);

//Sets the font of the bullet character

paragraph.ListFormat.FontName = "Symbol";

//Sets the hanging value as 20

paragraph.FirstLineIndent = -20;



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Adds a new paragraph with text.

paragraph = textShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.")

'Sets the list type as bullet

paragraph.ListFormat.Type = ListType.Bulleted

'Sets the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183)

'Sets the font of the bullet character

paragraph.ListFormat.FontName = "Symbol"

'Sets the hanging value as 20

paragraph.FirstLineIndent = -20



{% endhighlight %}

In PowerPoint presentation, the multilevel lists are used for presenting the content in a hierarchy. You can create a multi-level list by setting the indentation levels. By default, the level begins at 0 and increments by 1 for each level. The following code example demonstrates how to add multi-level list in a paragraph.

{% highlight vb.net %}
[C#]

//Adds a new paragraph  

paragraph = textShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.");

//Sets the list type as bullet

paragraph.ListFormat.Type = ListType.Bulleted;

//Sets the list level as 2. Possible values can range from 0 to 8

paragraph.IndentLevelNumber = 2;



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Adds a new paragraph  

paragraph = textShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Sets the list type as bullet

paragraph.ListFormat.Type = ListType.Bulleted

'Sets the list level as 2. Possible values can range from 0 to 8

paragraph.IndentLevelNumber = 2



{% endhighlight %}

You can add images to the presentation by adding them in the picture collection of a slide. The following code example demonstrates how to add an image in a presentation.

{% highlight c# %}
[C#]

//Gets the image from file path

Image image = Image.FromFile(@"image.jpg");

// Adds the image to the slide by specifying position and size

firstSlide.Pictures.AddPicture(new MemoryStream(image.ImageData), 300, 270, 410, 250);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Gets the image from file path

Dim image__1 As Image = Image.FromFile("image.jpg")

' Adds the image to the slide by specifying position and size 
firstSlide.Pictures.AddPicture(New MemoryStream (image__1.ImageData), 300, 270, 410, 250)



{% endhighlight %}

Finally, save the presentation in file system and close its instance.

{% highlight c# %}
[C#]

//Saves the presentation in the given name 

presentation.Save("Output.pptx");

//Releases the resources occupied

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Saves the presentation in the given name

Presentation_1.Save("Output.pptx")

'Releases the resources occupied

Presentation_1.Close()



{% endhighlight %}

The resultant PowerPoint presentation looks as follows.

![](GettingStarted_images/GettingStarted_img1.jpeg)


## Convert PowerPoint presentation to PDF

Essential Presentation allows you to convert a PowerPoint presentation into PDF document. The following assemblies are required for the presentation to PDF conversion.

<table>
<tr>
<td>
Assembly Name<br/><br/></td><td>
Short Description<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Presentation.Base<br/><br/></td><td>
This assembly contains the core features required for creating, reading, manipulating a Presentation file.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to pack the Presentation contents.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChart.Base<br/><br/></td><td>
This assembly contains the Office Chart Object model and core features needed for chart creation.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td><td>
This assembly is used to convert Office Chart into Image. <br/><br/></td></tr>
<tr>
<td>
Syncfusion.Pdf.Base<br/><br/></td><td>
This assembly is used for PDF file creation. <br/><br/></td></tr>
<tr>
<td>
Syncfusion.PresentationToPDFConverter.Base<br/><br/></td><td>
This assembly is used to convert Presentation file into PDF. <br/><br/></td></tr>
<tr>
<td>
Syncfusion.SfChart.WPF<br/><br/></td><td>
Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Shared.WPF<br/><br/></td><td>
Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
</table>
The following namespaces are required to compile the code in this topic.

* Syncfusion.OfficeChartToImageConverter;
* Syncfusion.Pdf;
* Syncfusion.Presentation;
* Syncfusion.PresentationToPdfConverter;

**PresentationToPdfConverter** class is responsible for converting an entire Presentation or a slide into PDF. The following code example demonstrates how to convert the PowerPoint presentation to PDF.

{% highlight c# %}
[C#]

//Opens a PowerPoint presentation file

IPresentation presentation = Presentation.Open(fileName);

//Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation.ChartToImageConverter = new ChartToImageConverter();

//Converts the PowerPoint presentation into PDF document

PdfDocument PDFdocument = PresentationToPdfConverter.Convert(presentation);

//Saves the PDF document

PDFdocument.Save(@"SampleWithoutSetting.pdf");

//Closes the PDF document

PDFdocument.Close(true);

//Closes the presentation

presentation.Close();



{% endhighlight %}

{% highlight c# %}
[VB.NET]

'Opens a PowerPoint presentation file

Dim presentation_1 As IPresentation = Presentation.Open(fileName)

'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation_1.ChartToImageConverter = New ChartToImageConverter ()

'Converts the PowerPoint presentation into PDF document

Dim PDFdocument As PdfDocument = PresentationToPdfConverter.Convert(presentation_1)

'Saves the PDF document

PDFdocument.Save("SampleWithoutSetting.pdf")

'Closes the PDF document

PDFdocument.Close(True)

'Closes the presentation

presentation_1.Close()



{% endhighlight %}

**Note****:**

* Creating an instance of **ChartToImageConverter** class is mandatory to convert the charts present in the presentation to PDF conversion. Otherwise, the charts are not exported to the converted PDF.
* **ChartToImageConverter** is supported from .NET Framework 4.0 onwards

**PresentationToPdfConverterSettings** can be used to customize the conversion of Presentation to PDF document. **ChartToImageConverter** class can be further used to improve the quality of converted charts in the PDF document. For more information about this, see [Conversion](http://www.google.com/# "").

