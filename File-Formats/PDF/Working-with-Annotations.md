---
title: Working with Annotations
description: This section explains how to create different type of interactive Annotation by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Annotations

Essential PDF provides support for interactive annotations.

You can add, delete and modify the annotation from the PDF documents.

## Adding annotations to a PDF document

The following code example explains how to add a popup annotation to the page.

{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page 

PdfPage page = document.Pages.Add();

//Creates a rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new popup annotation.

PdfPopupAnnotation popupAnnotation = new PdfPopupAnnotation(rectangle,"Test popup annotation");

popupAnnotation.Border.Width = 4;

popupAnnotation.Border.HorizontalRadius = 20;

popupAnnotation.Border.VerticalRadius = 30;

//Sets the pdf popup icon.

popupAnnotation.Icon = PdfPopupIcon.NewParagraph;

//Adds this annotation to the created page.

page.Annotations.Add(popupAnnotation);

//Saves the document to disk.

document.Save("PopupAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Creates a new page 

Dim page As PdfPage = document.Pages.Add()

'Creates a new rectangle

Dim rectangle As New RectangleF(10, 40, 30, 30)

'Creates a new popup annotation.

Dim popupAnnotation As New PdfPopupAnnotation(rectangle, "Test popup annotation")

popupAnnotation.Border.Width = 4

popupAnnotation.Border.HorizontalRadius = 20

popupAnnotation.Border.VerticalRadius = 30

'Sets the pdf popup icon.

popupAnnotation.Icon = PdfPopupIcon.NewParagraph

'Adds this annotation to the created page.

page.Annotations.Add(popupAnnotation)

'Saves the document to disk.

document.Save("PopupAnnotation.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}
To add annotations to an existing PDF document, use the following code example.

{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfLoadedDocument document = new PdfLoadedDocument("input.pdf");

//Creates a rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new popup annotation.

PdfPopupAnnotation popupAnnotation = new PdfPopupAnnotation(rectangle, "Test popup annotation");

popupAnnotation.Border.Width = 4;

popupAnnotation.Border.HorizontalRadius = 20;

popupAnnotation.Border.VerticalRadius = 30;

//Sets the pdf popup icon.

popupAnnotation.Icon = PdfPopupIcon.NewParagraph;

//Adds the annotation to loaded page

document.Pages[0].Annotations.Add(popupAnnotation);

//Saves the document to disk.

document.Save("PopupAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}      

'Creates a new PDF document.

Dim document As New PdfLoadedDocument("input.pdf")

'Creates a rectangle

Dim rectangle As New RectangleF(10, 40, 30, 30)

'Creates a new popup annotation.

Dim popupAnnotation As New PdfPopupAnnotation(rectangle, "Test popup annotation")

popupAnnotation.Border.Width = 4

popupAnnotation.Border.HorizontalRadius = 20

popupAnnotation.Border.VerticalRadius = 30

'Sets the pdf popup icon.

popupAnnotation.Icon = PdfPopupIcon.NewParagraph

'Adds the annotation to loaded page

document.Pages(0).Annotations.Add(popupAnnotation)

'Saves the document to disk.

document.Save("PopupAnnotation.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

## Flatten annotation

Annotations can be flattened by removing the existing annotation and replacing it with graphics objects that would resemble the annotation and cannot be edited.

Please refer the sample for flattening all the annotations in the PDF document.

{% tabs %}
{% highlight c# %}
//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");
//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
//Flatten all the annotations in the page
loadedPage.Annotations.Flatten = true;
}
//Save and close the PDF document instance
loadedDocument.Save("output.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}      

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedDocument("input.pdf")
'Get all the pages
For Each loadedPage As PdfLoadedPage In loadedDocument.Pages
'Flatten all the annotations in the page
loadedPage.Annotations.Flatten = True
Next
'Save and close the PDF document instance
loadedDocument.Save("output.pdf")
loadedDocument.Close(True)

{% endhighlight %}
{% endtabs %}

To flatten the specific annotation in the PDF document, use the below code example.

{% tabs %}
{% highlight c# %}
//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");
//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
//Flatten all the annotations in the page
foreach (PdfLoadedAnnotation annotation in loadedPage.Annotations)
{
//Check for the circle annotation
if (annotation is PdfLoadedCircleAnnotation)
{
//Flatten the circle annoation
annotation.Flatten = true;
}
}
}
//Save and close the PDF document instance
loadedDocument.Save("Output.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}      

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedDocument("input.pdf")
'Get all the pages
For Each loadedPage As PdfLoadedPage In loadedDocument.Pages
	'Flatten all the annotations in the page
	For Each annotation As PdfLoadedAnnotation In loadedPage.Annotations
		'Check for the circle annotation
		If TypeOf annotation Is PdfLoadedCircleAnnotation Then
			'Flatten the circle annotation
			annotation.Flatten = True
		End If
	Next
Next
'Save and close the PDF document instance
loadedDocument.Save("Output.pdf")
loadedDocument.Close(True)

{% endhighlight %}
{% endtabs %}

## Supported annotation types

### 3D Annotation

3D Annotations are used to represent 3D artworks in a PDF document. Essential PDF provides support to embed 3D files (u3d) in PDF. 

The following example illustrates how to add 3D annotation in PDF document.
{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new pdf 3d annotation.

Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), @"3DAnnotation.U3D");

//Handles the activation of the 3d annotation

Pdf3DActivation activation = new Pdf3DActivation();

activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation;

activation.ShowToolbar = true;

pdf3dAnnotation.Activation = activation;

//Adds annotation to page

page.Annotations.Add(pdf3dAnnotation);

//Saves the document to disk.

document.Save("3DAnnotation.pdf");

document.Close(true);





{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Creates a new pdf 3d annotation.

Dim pdf3dAnnotation As New Pdf3DAnnotation(New RectangleF(10, 50, 300, 150), "3DAnnotation.U3D")

'Handles the activation of the 3d annotation

Dim activation As New Pdf3DActivation()

activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation

activation.ShowToolbar = True

pdf3dAnnotation.Activation = activation

'Adds annotation to page

page.Annotations.Add(pdf3dAnnotation)

'Saves the document to disk.

document.Save("3DAnnotation.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

### File Link Annotation 

Links for external files can be added in a PDF document by using the file link annotation.

The following code example explains how to add a file link annotation in PDF.
{% tabs %}
{% highlight c# %}


//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new pdf file link annotation.

PdfFileLinkAnnotation fileLinkAnnotation = new PdfFileLinkAnnotation(rectangle, @"logo.png");

//Adds this annotation to a new page.

page.Annotations.Add(fileLinkAnnotation);

//Saves the document to disk.

document.Save("FileLinkAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Creates a new rectangle

Dim rectangle As New RectangleF(10, 40, 30, 30)

'Creates a new pdf file link annotation.

Dim fileLinkAnnotation As New PdfFileLinkAnnotation(rectangle, "logo.png")

'Adds this annotation to a new page.

page.Annotations.Add(fileLinkAnnotation)

'Saves the document to disk.

document.Save("FileLinkAnnotation.pdf")

document.Close(True)





{% endhighlight %}
{% endtabs %}

### Free Text Annotation

Free text annotation enables you to display the text directly on the page. When you want to add a comment directly without placing it on a pop-up window, FreeTextAnnotation can be used.

The following code example explains how to add a free text annotation in the PDF document.

{% tabs %}
{% highlight c# %}


//Creates a new pdf document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates PDF free text annotation

PdfFreeTextAnnotation freeText = new PdfFreeTextAnnotation(new RectangleF(50, 100, 100, 50));

//Sets properties to the annotation

freeText.MarkupText = "Free Text with Callout";

freeText.TextMarkupColor = new PdfColor(Color.Black);

freeText.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 7f);

freeText.Color = new PdfColor(Color.Yellow);

freeText.BorderColor = new PdfColor(Color.Red);

freeText.Border = new PdfAnnotationBorder(.5f);

freeText.LineEndingStyle = PdfLineEndingStyle.OpenArrow;

freeText.AnnotationFlags = PdfAnnotationFlags.Default;

freeText.Text = "Free Text";

freeText.Opacity = 0.5f;

PointF[] points = { new PointF(100, 400), new PointF(100, 450) };

freeText.CalloutLines = points;

//Adds the annotation to page

page.Annotations.Add(freeText);

//Saves the document to disk.

document.Save("FreeTextAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new pdf document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Creates PDF free text annotation

Dim freeText As New PdfFreeTextAnnotation(New RectangleF(50, 100, 100, 50))

'Sets properties to the annotation

freeText.MarkupText = "Free Text with Callout"

freeText.TextMarkupColor = New PdfColor(Color.Black)

freeText.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 7.0F)

freeText.Color = New PdfColor(Color.Yellow)

freeText.BorderColor = New PdfColor(Color.Red)

freeText.Border = New PdfAnnotationBorder(0.5F)

freeText.LineEndingStyle = PdfLineEndingStyle.OpenArrow

freeText.AnnotationFlags = PdfAnnotationFlags.[Default]

freeText.Text = "Free Text"

freeText.Opacity = 0.5F

Dim points As PointF() = {New PointF(100, 400), New PointF(100, 450)}

freeText.CalloutLines = points

'Adds the annotation to page

page.Annotations.Add(freeText)

'Saves the document to disk.

document.Save("FreeTextAnnotation.pdf")

document.Close(True)





{% endhighlight %}
{% endtabs %}

### Line Annotation 

Line annotation displays a single straight line on the page. When you open it, it displays a pop-up window containing text of the associated note.

PdfLineAnnotation is used to create and set the properties of the Line annotation.
{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Specifies the line end points

int[] points = new int[] { 80, 420, 150, 420 };

//Creates a new line annotation.

PdfLineAnnotation lineAnnotation = new PdfLineAnnotation(points, "Line Annotation");

//Creates pdf line border

LineBorder lineBorder = new LineBorder();

lineBorder.BorderStyle = PdfBorderStyle.Solid;

lineBorder.BorderWidth = 1;

lineAnnotation.lineBorder = lineBorder;

lineAnnotation.LineIntent = PdfLineIntent.LineDimension;

//Assigns the line ending style

lineAnnotation.BeginLineStyle = PdfLineEndingStyle.Butt;

lineAnnotation.EndLineStyle = PdfLineEndingStyle.Diamond;

lineAnnotation.AnnotationFlags = PdfAnnotationFlags.Default;

//Assigns the line color

lineAnnotation.InnerLineColor = new PdfColor(Color.Green);

lineAnnotation.BackColor = new PdfColor(Color.Green);

//Assigns the leader line

lineAnnotation.LeaderLineExt = 0;

lineAnnotation.LeaderLine = 0;

//Assigns the Line caption type

lineAnnotation.LineCaption = true;

lineAnnotation.CaptionType = PdfLineCaptionType.Inline;

//Adds this annotation to a new page.

page.Annotations.Add(lineAnnotation);

//Saves the document to disk.

document.Save("LineAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Specifies the line end points

Dim points As Integer() = New Integer() {80, 420, 150, 420}

'Creates a new line annotation.

Dim lineAnnotation As New PdfLineAnnotation(points, "Line Annotation")

'Creates pdf line border

Dim lineBorder As New LineBorder()

lineBorder.BorderStyle = PdfBorderStyle.Solid

lineBorder.BorderWidth = 1

lineAnnotation.lineBorder = lineBorder

lineAnnotation.LineIntent = PdfLineIntent.LineDimension

'Assigns the line ending style

lineAnnotation.BeginLineStyle = PdfLineEndingStyle.Butt

lineAnnotation.EndLineStyle = PdfLineEndingStyle.Diamond

lineAnnotation.AnnotationFlags = PdfAnnotationFlags.[Default]

'Assigns the line color

lineAnnotation.InnerLineColor = New PdfColor(Color.Green)

lineAnnotation.BackColor = New PdfColor(Color.Green)

'Assigns the leader line

lineAnnotation.LeaderLineExt = 0

lineAnnotation.LeaderLine = 0

'Assigns the Line caption type

lineAnnotation.LineCaption = True

lineAnnotation.CaptionType = PdfLineCaptionType.Inline

'Adds this annotation to a new page.

page.Annotations.Add(lineAnnotation)

'Saves the document to disk.

document.Save("LineAnnotation.pdf")

document.Close(True)





{% endhighlight %}
{% endtabs %}
### Rubber stamp Annotation

Rubber stamp annotation displays text or graphics intended to look like it is stamped on the page with a rubber stamp. 

When opened, it displays a pop-up window containing the text of the associated note.

PdfRubberStampAnnotation is used to create rubber stamp annotation.

{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new pdf rubber stamp annotation.

RectangleF rectangle = new RectangleF(40, 60, 80, 20);

PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangle, " Text Rubber Stamp Annotation");

rubberStampAnnotation.Icon = PdfRubberStampAnnotationIcon.Draft;

rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Adds annotation to the page

page.Annotations.Add(rubberStampAnnotation);

//Saves the document to disk.

document.Save("Rubberstamp.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Creates a new pdf rubber stamp annotation.

Dim rectangle As New RectangleF(40, 60, 80, 20)

Dim rubberStampAnnotation As New PdfRubberStampAnnotation(rectangle, " Text Rubber Stamp Annotation")

rubberStampAnnotation.Icon = PdfRubberStampAnnotationIcon.Draft

rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation"

'Adds annotation to the page

page.Annotations.Add(rubberStampAnnotation)

'Saves the document to disk.

document.Save("RubberStamp.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

### Ink Annotation

Ink annotation represents freehand “scribble” comprising one or more disjoint paths. 

When you open it, it displays a pop-up window containing text of the associated note.

The following code example explains how to add ink annotation in a PDF document.

{% tabs %}
{% highlight c# %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

List<float> linePoints=new List<float>{40,300,60,100,40,50,40,300};

//Creates a new ink annotation

RectangleF rectangle = new RectangleF(0, 0, 300, 400);

PdfInkAnnotation inkAnnotation = new PdfInkAnnotation(rectangle,linePoints);

inkAnnotation.Color = new PdfColor(Color.Red);

//Adds annotation to the page

page.Annotations.Add(inkAnnotation);

//Saves the document to disk.

document.Save("InkAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

Dim linePoints As New List(Of Single)() From {40, 300, 60, 100, 40, 50, 40, 300}

'Creates a new ink annotation

Dim rectangle As New RectangleF(0, 0, 300, 400)

Dim inkAnnotation As New PdfInkAnnotation(rectangle, linePoints)

inkAnnotation.Color = New PdfColor(Color.Red)

'Adds annotation to the page

page.Annotations.Add(inkAnnotation)

'Saves the document to disk.

document.Save("InkAnnotation.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

### Pop-up Annotation

Pop-up annotation displays text in a pop-up window for entry and editing. 

It typically does not appear alone, but is associated with markup annotation, its parent annotation.

The following code example explains how to add pop-up annotation in a PDF document.

{% tabs %}
{% highlight c# %}

//Creates a new rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new popup annotation.

PdfPopupAnnotation popupAnnotation = new PdfPopupAnnotation(rectangle, "Test popup annotation");

popupAnnotation.Border.Width = 4;

popupAnnotation.Border.HorizontalRadius = 20;

popupAnnotation.Border.VerticalRadius = 30;

//Sets the PDF popup icon.

popupAnnotation.Icon = PdfPopupIcon.NewParagraph;

//Adds this annotation to a new page.

page.Annotations.Add(popupAnnotation);

//Saves the document to disk.

document.Save("PopupAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Creates a new rectangle

Dim rectangle As New RectangleF(10, 40, 30, 30)

'Creates a new popup annotation.

Dim popupAnnotation As New PdfPopupAnnotation(rectangle, "Test popup annotation")

popupAnnotation.Border.Width = 4

popupAnnotation.Border.HorizontalRadius = 20

popupAnnotation.Border.VerticalRadius = 30

'Sets the PDF popup icon.

popupAnnotation.Icon = PdfPopupIcon.NewParagraph

'Adds this annotation to a new page.

page.Annotations.Add(popupAnnotation)

'Saves the document to disk.

document.Save("PopupAnnotation.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

### File Attachment Annotation

File attachment annotation contains reference to a file that typically is embedded in the PDF file.

The following code example explains how to add a file attachment annotation in a PDF document.

{% tabs %}
{% highlight c# %}

//Creates a new PDF Document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new rectangle

RectangleF attachmentRectangle = new RectangleF(10, 40, 30, 30);

//Creates a new attachment annotation.

PdfAttachmentAnnotation attachmentAnnotation = new PdfAttachmentAnnotation(attachmentRectangle, @"logo.png");

//Sets the attachment icon to attachment annotation.

attachmentAnnotation.Icon = PdfAttachmentIcon.PushPin;

//Adds this annotation to a new page.

page.Annotations.Add(attachmentAnnotation);

//Saves the document to disk.

document.Save("AttachmentAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF Document.

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Creates a new rectangle

Dim attachmentRectangle As New RectangleF(10, 40, 30, 30)

'Creates a new attachment annotation.

Dim attachmentAnnotation As New PdfAttachmentAnnotation(attachmentRectangle, "logo.png")

'Sets the attachment icon to attachment annotation.

attachmentAnnotation.Icon = PdfAttachmentIcon.PushPin

'Adds this annotation to a new page.

page.Annotations.Add(attachmentAnnotation)

'Saves the document to disk.

document.Save("AttachmentAnnotation.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

### Sound Annotation

Sound annotation is used to play the sound clip in the PDF Document.

The following code example explains how to add a sound annotation in a PDF document.
{% tabs %}
{% highlight c# %}


//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new sound annotation.

PdfSoundAnnotation soundAnnotation = new PdfSoundAnnotation(rectangle, @"startup.wav");

soundAnnotation.Sound.Encoding = PdfSoundEncoding.Signed;

soundAnnotation.Sound.Channels = PdfSoundChannels.Stereo;

soundAnnotation.Sound.Bits = 16;

soundAnnotation.Color = new PdfColor(Color.Red);

//Sets the pdf sound icon.

soundAnnotation.Icon = PdfSoundIcon.Speaker;

//Adds this annotation to a new page.

page.Annotations.Add(soundAnnotation);

//Saves the document to disk.

document.Save("SoundIcon.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Creates a new rectangle

Dim rectangle As New RectangleF(10, 40, 30, 30)

'Creates a new sound annotation.

Dim soundAnnotation As New PdfSoundAnnotation(rectangle, "startup.wav")

soundAnnotation.Sound.Encoding = PdfSoundEncoding.Signed

soundAnnotation.Sound.Channels = PdfSoundChannels.Stereo

soundAnnotation.Sound.Bits = 16

soundAnnotation.Color = New PdfColor(Color.Red)

'Sets the pdf sound icon.

soundAnnotation.Icon = PdfSoundIcon.Speaker

'Adds this annotation to a new page.

page.Annotations.Add(soundAnnotation)

'Saves the document to disk.

document.Save("SoundIcon.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

### URI Annotation

URI annotation is used to navigate to a particular web URI

The following code example explains how to add URI annotation in a PDF document.
{% tabs %}
{% highlight c# %}


//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new Uri Annotation

PdfUriAnnotation uriAnnotation = new PdfUriAnnotation(rectangle, "http://www.google.com");

//Sets Text to uriAnnotation

uriAnnotation.Text = "Uri Annotation";

//Adds this annotation to a new page

page.Annotations.Add(uriAnnotation);

//Saves the document to disk

document.Save("UriAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Creates a new rectangle

Dim rectangle As New RectangleF(10, 40, 30, 30)

'Creates a new Uri Annotation

Dim uriAnnotation As New PdfUriAnnotation(rectangle, "http://www.google.com")

'Sets Text to uriAnnotation.

uriAnnotation.Text = "Uri Annotation"

'Adds this annotation to a new page

page.Annotations.Add(uriAnnotation)

'Saves the document to disk.

document.Save("UriAnnotation.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

### Document Link Annotation

This annotation is used to navigate to a specific destination within the document.

The following code example explains how to add a document link annotation in PDF document.
{% tabs %}
{% highlight c# %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a page

PdfPage page2 = document.Pages.Add();

//Creates a new rectangle

RectangleF docLinkAnnotationRectangle = new RectangleF(10, 40, 30, 30);

//Creates a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationRectangle);

documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate;

documentLinkAnnotation.Text = "Document link annotation";

documentLinkAnnotation.Color = new PdfColor(Color.Navy);

//Sets the destination.

documentLinkAnnotation.Destination = new PdfDestination(page2);

documentLinkAnnotation.Destination.Location = new Point(10, 0);

documentLinkAnnotation.Destination.Zoom = 5;

//Adds this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation);

//Saves the document to disk.

document.Save("DocumentLinkAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Creates a new PDF document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Creates a page

Dim page2 As PdfPage = document.Pages.Add()

'Creates a new rectangle

Dim docLinkAnnotationRectangle As New RectangleF(10, 40, 30, 30)

'Creates a new document link annotation.

Dim documentLinkAnnotation As New PdfDocumentLinkAnnotation(docLinkAnnotationRectangle)

documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate

documentLinkAnnotation.Text = "Document link annotation"

documentLinkAnnotation.Color = New PdfColor(Color.Navy)

'Sets the destination.

documentLinkAnnotation.Destination = New PdfDestination(page2)

documentLinkAnnotation.Destination.Location = New Point(10, 0)

documentLinkAnnotation.Destination.Zoom = 5

'Adds this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation)

'Saves the document to disk.

document.Save("DocumentLinkAnnotation.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}
## Modifying the annotations

Essential PDF allows you to modify the annotation of existing document. The following code illustrates this.

{% tabs %}
{% highlight c# %}


//Loads the document

PdfLoadedDocument lDoc = new PdfLoadedDocument("inputAnnotation.pdf");

//Gets the first page from the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Gets the first annotation and modify the properties

PdfLoadedPopupAnnotation popUp = annotations[0] as PdfLoadedPopupAnnotation;

popUp.Border = new PdfAnnotationBorder(4, 0, 0);

popUp.Color = new PdfColor(Color.Red);

popUp.Text = "Modified annotation";

//Saves the document

lDoc.Save("sample.pdf");

lDoc.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Loads the document

Dim lDoc As New PdfLoadedDocument("inputAnnotation.pdf")

'Gets the first page from the document

Dim page As PdfLoadedPage = TryCast(lDoc.Pages(0), PdfLoadedPage)

'Gets the annotation collections

Dim annotations As PdfLoadedAnnotationCollection = page.Annotations

'Gets the annotation at index 0 and modifying the properties

Dim popUp As PdfLoadedPopupAnnotation = TryCast(annotations(0), PdfLoadedPopupAnnotation)

popUp.Border = New PdfAnnotationBorder(4, 0, 0)

popUp.Color = New PdfColor(Color.Red)

popUp.Text = "Modified annotation"

'Saves the document

lDoc.Save("sample.pdf")

lDoc.Close(True)



{% endhighlight %}
{% endtabs %}

## Removing annotations from an existing PDF 

You can remove the annotation from the annotation collection, represented by the **PdfLoadedAnnotationCollection** of the loaded page. The following code illustrates this.

{% tabs %}
{% highlight c# %}


//Loads the document

PdfLoadedDocument lDoc = new PdfLoadedDocument("inputAnnotation.pdf");

//Gets the first page of the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Removes the first annotation

annotations.RemoveAt(0);

//Saves the document

lDoc.Save("sample.pdf");

lDoc.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Loads the document

Dim lDoc As New PdfLoadedDocument("inputAnnotation.pdf")

'Gets the first page from the document

Dim page As PdfLoadedPage = TryCast(lDoc.Pages(0), PdfLoadedPage)

'Gets the annotation collection

Dim annotations As PdfLoadedAnnotationCollection = page.Annotations

'Removes the first annotation

annotations.RemoveAt(0)

'Saves the document

lDoc.Save("sample.pdf")

lDoc.Close(True)



{% endhighlight %}
{% endtabs %}
