---
title: Getting Started with Essential Presentation library
description: Getting started with Essential Presentation library; Creating a PowerPoint presentation; Modifying the existing PowerPoint presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Getting Started

## Creating a simple PowerPoint presentation with basic elements from scratch

In this page, you can learn how to create a simple PowerPoint presentation by using Essential Presentation API.

For creating and manipulating a PowerPoint presentation, include the following assemblies in the application.

<table>
    <thead>
        <tr>
            <th>
                Assembly Name
            </th>
            <th>
                Short Description
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                Syncfusion.Presentation.Base
            </td>
            <td>
                This assembly contains the core features required for creating, reading, manipulating a Presentation file.
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.Compression.Base
            </td>
            <td>
                This assembly is used to package the Presentation contents.
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.OfficeChart.Base
            </td>
            <td>
                This assembly contains the Office Chart Object model and core features needed for chart creation.
            </td>
        </tr>
    </tbody>
</table>

Include the following namespace in your .cs or .vb code as shown below

{% tabs %}

{% highlight c# %}

using Syncfusion.Presentation;

{% endhighlight %}

{% highlight vb.net %}

Imports Syncfusion.Presentation

{% endhighlight %}

{% endtabs %}

An entire PowerPoint presentation is represented by an instance of IPresentation interface and it is the root element of Essential Presentation’s DOM.

The following code example demonstrates how to create an instance of IPresentation interface.

{% tabs %}

{% highlight c# %}

//Creates a new instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new instance of PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Create()

{% endhighlight %}

{% endtabs %}

IPresentation instance has a slide collection that represents the individual slides present within PowerPoint presentation. A slide may contain textual and other graphics contents like shapes, images, charts etc.

The following code example demonstrates how to add a blank slide to a PowerPoint presentation.

{% tabs %}

{% highlight c# %}

//Adds a slide to the PowerPoint presentation

ISlide firstSlide = presentation.Slides.Add(SlideLayoutType.Blank);

{% endhighlight %}

{% highlight vb.net %}

'Adds a slide to the PowerPoint presentation

Dim firstSlide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

{% endhighlight %}

{% endtabs %}

N> The “Point” typographic units are used to add or manipulate any element in a presentation. 

All the textual contents in a Presentation document are represented by Paragraphs. Within the paragraph, textual contents are grouped into one or more child elements as TextParts. Each TextPart represents a region of text with a common set of formatted text.

The following code example demonstrates how to add text into a presentation.

{% tabs %}

{% highlight c# %}

//Adds a textbox in a slide by specifying its position and size

IShape textShape = firstSlide.AddTextBox(100, 75, 756, 200);

//Adds a paragraph into the textShape

IParagraph paragraph = textShape.TextBody.AddParagraph();

//Set the horizontal alignment of paragraph
          
paragraph.HorizontalAlignment = HorizontalAlignmentType.Center;

//Adds a textPart in the paragraph

ITextPart textPart = paragraph.AddTextPart("Hello Presentation");

//Applies font formatting to the text

textPart.Font.FontSize = 80;

textPart.Font.Bold = true;

{% endhighlight %}

{% highlight vb.net %}

'Adds a textbox in a slide by specifying its position and size

Dim textShape As IShape  = firstSlide.AddTextBox(100, 75, 756, 200)

'Adds a paragraph into the textShape

Dim paragraph As IParagraph  = textShape.TextBody.AddParagraph()

'Set the horizontal alignment of paragraph

paragraph.HorizontalAlignment = HorizontalAlignmentType.Center

'Add a textPart in the paragraph

Dim textPart As ITextPart  = paragraph.AddTextPart("Hello Presentation")

'Applies font formatting to the text

textPart.Font.FontSize = 80

textPart.Font.Bold = True

{% endhighlight %}

{% endtabs %}

Essential Presentation allows you to create simple and multi-level lists that make the content easier for reading. The following code example demonstrates how to add a bulleted list in a paragraph.

{% tabs %}

{% highlight c# %}

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

{% endtabs %}


In PowerPoint presentation, the multilevel lists are used for presenting the content in a hierarchy. You can create a multi-level list by setting the indentation levels. By default, the level begins at 0 and increments by 1 for each level. The following code example demonstrates how to add multi-level list in a paragraph.

{% tabs %}

{% highlight c# %}

//Adds a new paragraph  

paragraph = textShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.");

//Sets the list type as bullet

paragraph.ListFormat.Type = ListType.Bulleted;

//Sets the list level as 2. Possible values can range from 0 to 8

paragraph.IndentLevelNumber = 2;

{% endhighlight %}

{% highlight vb.net %}

'Adds a new paragraph  

paragraph = textShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Sets the list type as bullet

paragraph.ListFormat.Type = ListType.Bulleted

'Sets the list level as 2. Possible values can range from 0 to 8

paragraph.IndentLevelNumber = 2

{% endhighlight %}

{% endtabs %}


You can add images to the presentation by adding them in the picture collection of a slide. The following code example demonstrates how to add an image in a presentation.

{% tabs %}

{% highlight c# %}

//Gets the image from file path

Image image = Image.FromFile(@"image.jpg");

// Adds the image to the slide by specifying position and size

firstSlide.Pictures.AddPicture(new MemoryStream(image.ImageData), 300, 270, 410, 250);

{% endhighlight %}

{% highlight vb.net %}

'Gets the image from file path

Dim image__1 As Image = Image.FromFile("image.jpg")

' Adds the image to the slide by specifying position and size 
firstSlide.Pictures.AddPicture(New MemoryStream (image__1.ImageData), 300, 270, 410, 250)

{% endhighlight %}

{% endtabs %}

Finally, save the presentation in file system and close its instance.

{% tabs %}

{% highlight c# %}

//Saves the presentation in the given name 

presentation.Save("Output.pptx");

//Releases the resources occupied

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Saves the presentation in the given name

Presentation_1.Save("Output.pptx")

'Releases the resources occupied

Presentation_1.Close()

{% endhighlight %}

{% endtabs %}


The resultant PowerPoint presentation looks as follows.

![](GettingStarted_images/GettingStarted_img1.jpeg)


## Converting PowerPoint presentation to PDF

Essential Presentation allows you to convert a PowerPoint presentation into PDF document. The following assemblies are required for the presentation to PDF conversion.

<table>
    <thead>
        <tr>
            <th>
                Assembly Name
            </th>
            <th>
                Short Description
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                Syncfusion.Presentation.Base
            </td>
            <td>
                This assembly contains the core features required for creating, reading, manipulating a Presentation file.
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.Compression.Base
            </td>
            <td>
                This assembly is used to pack the Presentation contents.
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.OfficeChart.Base
            </td>
            <td>
                This assembly contains the Office Chart Object model and core features needed for chart creation.
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.OfficeChartToImageConverter.WPF
            </td>
            <td>
                This assembly is used to convert Office Chart into Image. 
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.Pdf.Base
            </td>
            <td>
                This assembly is used for PDF file creation. 
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.PresentationToPDFConverter.Base
            </td>
            <td>
                This assembly is used to convert Presentation file into PDF. 
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.SfChart.WPF
            </td>
            <td>
                Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.Shared.WPF
            </td>
            <td>
                Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF
            </td>
        </tr>
    </tbody>
</table>

The following namespaces are required to compile the code in this topic.

* Syncfusion.OfficeChartToImageConverter;
* Syncfusion.Pdf;
* Syncfusion.Presentation;
* Syncfusion.PresentationToPdfConverter;

Include the following namespaces in your .cs or .vb code as shown below

{% tabs %}

{% highlight c# %}

using Syncfusion.Presentation;

using Syncfusion.OfficeChartToImageConverter;

using Syncfusion.Pdf;

using Syncfusion.PresentationToPdfConverter;

{% endhighlight %}

{% highlight vb.net %}

Imports Syncfusion.Presentation

Imports Syncfusion.OfficeChartToImageConverter

Imports Syncfusion.Pdf

Imports Syncfusion.PresentationToPdfConverter

{% endhighlight %}

{% endtabs %}

**PresentationToPdfConverter** class is responsible for converting an entire Presentation or a slide into PDF. The following code example demonstrates how to convert the PowerPoint presentation to PDF.

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

'Opens a PowerPoint presentation file

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentationDocument.ChartToImageConverter = New ChartToImageConverter ()

'Converts the PowerPoint presentation into PDF document

Dim PDFdocument As PdfDocument = PresentationToPdfConverter.Convert(presentationDocument)

'Saves the PDF document

PDFdocument.Save("SampleWithoutSetting.pdf")

'Closes the PDF document

PDFdocument.Close(True)

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}


N> * Creating an instance of **ChartToImageConverter** class is mandatory to convert the charts present in the presentation to PDF conversion. Otherwise, the charts are not exported to the converted PDF.
N> * **ChartToImageConverter** is supported from .NET Framework 4.0 onwards

**PresentationToPdfConverterSettings** can be used to customize the conversion of Presentation to PDF document. **ChartToImageConverter** class can be further used to improve the quality of converted charts in the PDF document. For more information about this, see [Conversion](/file-formats/presentation/conversion).

