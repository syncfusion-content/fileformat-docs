---
title: Working with Annotations | Syncfusion
description: This section explains how to create or modify or remove different type of interactive Annotation by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Annotations

Essential PDF provides support for interactive [annotations](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library/pdf-annotation).

You can add, delete and modify the annotation from the PDF documents.

## Adding annotations to a PDF document

You can add a popup annotation to the page using [PdfPopupAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfPopupAnnotation.html) class. The following code example explains this.

{% tabs %}
{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page 

PdfPage page = document.Pages.Add();

//Creates a rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new popup annotation.

PdfPopupAnnotation popupAnnotation = new PdfPopupAnnotation(rectangle, "Test popup annotation");

popupAnnotation.Border.Width = 4;

popupAnnotation.Border.HorizontalRadius = 20;

popupAnnotation.Border.VerticalRadius = 30;

//Sets the pdf popup icon.

popupAnnotation.Icon = PdfPopupIcon.NewParagraph;

//Adds this annotation to the created page.

page.Annotations.Add(popupAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "PopupAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page 

PdfPage page = document.Pages.Add();

//Creates a rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new popup annotation.

PdfPopupAnnotation popupAnnotation = new PdfPopupAnnotation(rectangle, "Test popup annotation");

popupAnnotation.Border.Width = 4;

popupAnnotation.Border.HorizontalRadius = 20;

popupAnnotation.Border.VerticalRadius = 30;

//Sets the pdf popup icon.

popupAnnotation.Icon = PdfPopupIcon.NewParagraph;

//Adds this annotation to the created page.

page.Annotations.Add(popupAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "PopupAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page 

PdfPage page = document.Pages.Add();

//Creates a rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new popup annotation.

PdfPopupAnnotation popupAnnotation = new PdfPopupAnnotation();

popupAnnotation.Bounds = rectangle;

popupAnnotation.Text = "Test popup annotation";

popupAnnotation.Border.Width = 4;

popupAnnotation.Border.HorizontalRadius = 20;

popupAnnotation.Border.VerticalRadius = 30;

//Sets the pdf popup icon.

popupAnnotation.Icon = PdfPopupIcon.NewParagraph;

//Adds this annotation to the created page.

page.Annotations.Add(popupAnnotation);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("PopupAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("PopupAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}
To add annotations to an existing PDF document, use the following code example.

{% tabs %}
{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}      

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

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument document = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await document.OpenAsync(file);

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

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "PopupAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

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

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "PopupAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

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

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("PopupAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("PopupAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Flatten annotation

Annotations can be flattened by removing the existing annotation and replacing it with graphics objects that would resemble the annotation and cannot be edited.

This can be achieved by enabling the [Flatten](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedAnnotationCollection.html#Syncfusion_Pdf_Parsing_PdfLoadedAnnotationCollection_Flatten) property. Please refer the sample for flattening all the annotations in the PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}      

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

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    //Flatten all the annotations in the page
    loadedPage.Annotations.Flatten = true;
}

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    //Flatten all the annotations in the page
    loadedPage.Annotations.Flatten = true;
}

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    //Flatten all the annotations in the page
    loadedPage.Annotations.Flatten = true;
}

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("output.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

To flatten the specific annotation in the PDF document, use the below code example.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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
//Flatten the circle annotation
annotation.Flatten = true;
}
}
}
//Save and close the PDF document instance
loadedDocument.Save("Output.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}      

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

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    //Flatten all the annotations in the page
    foreach (PdfLoadedAnnotation annotation in loadedPage.Annotations)
    {
        //Check for the circle annotation
        if (annotation is PdfLoadedCircleAnnotation)
        {
            //Flatten the circle annotation
            annotation.Flatten = true;
        }
    }
}

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    //Flatten all the annotations in the page
    foreach (PdfLoadedAnnotation annotation in loadedPage.Annotations)
    {
        //Check for the circle annotation
        if (annotation is PdfLoadedCircleAnnotation)
        {
            //Flatten the circle annotation
            annotation.Flatten = true;
        }
    }
}

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    //Flatten all the annotations in the page
    foreach (PdfLoadedAnnotation annotation in loadedPage.Annotations)
    {
        //Check for the circle annotation
        if (annotation is PdfLoadedCircleAnnotation)
        {
            //Flatten the circle annotation
            annotation.Flatten = true;
        }
    }
}

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

To flatten pop-up annotation in the PDF document, use the following code example.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("PopupAnnotation.pdf");
//Get all the pages
foreach(PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    foreach(PdfLoadedAnnotation annotation in loadedPage.Annotations)
    {
        if(annotation is PdfLoadedPopupAnnotation)
        {
            //Enable the flatten annotation
            annotation.Flatten = true;
            //Enable flatten for the pop-up window annotation
            annotation.FlattenPopUps = true;
        }
    }
}
//Save the document
loadedDocument.Save("Output.pdf");
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedDocument("PopupAnnotation.pdf")
'Get all the pages
For Each loadedPage As PdfLoadedPage In loadedDocument.Pages
    For Each annotation As PdfLoadedAnnotation In loadedPage.Annotations
        If TypeOf annotation Is PdfLoadedPopupAnnotation Then
            'Enable the flatten annotation
            annotation.Flatten = True
            'Enable flatten for the pop-up window annotation
            annotation.FlattenPopUps = True
        End If
    Next
Next
'Save the document
loadedDocument.Save("Output.pdf")
'Close the document
loadedDocument.Close(True)


{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker
var picker = new FileOpenPicker();
picker.FileTypeFilter.Add(".pdf");
//Browse and choose the file
StorageFile file = await picker.PickSingleFileAsync();
//Creates an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument();
//Loads or opens an existing PDF document using Open method of the PdfLoadedDocument class
await loadedDocument.OpenAsync(file);
//Get all the page
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    foreach (PdfLoadedAnnotation annotation in loadedPage.Annotations)
    {
        if (annotation is PdfLoadedPopupAnnotation)
        {
            //Enable the flatten annotation
            annotation.Flatten = true;
            //Enable flatten for the pop-up window annotation
            annotation.FlattenPopUps = true;
        }
    }
}
//Save the document as stream
MemoryStream stream = new MemoryStream();
await loadedDocument.SaveAsync(stream);
//Close the document instances
loadedDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("PopupAnnotation.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    foreach (PdfLoadedAnnotation annotation in loadedPage.Annotations)
    {
        if (annotation is PdfLoadedPopupAnnotation)
        {
            //Enable the flatten annotation
            annotation.Flatten = true;
            //Enable flatten for the pop-up window annotation
            annotation.FlattenPopUps = true;
        }
    }
}
//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document as stream
loadedDocument.Save(stream);
//If the position is not set to '0', then the PDF will be empty
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates the FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PopupAnnotation.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Get all the pages
foreach (PdfLoadedPage loadedPage in loadedDocument.Pages)
{
    foreach (PdfLoadedAnnotation annotation in loadedPage.Annotations)
    {
        if (annotation is PdfLoadedPopupAnnotation)
        {
            //Enable the flatten annotation
            annotation.Flatten = true;
            //Enable flatten for the pop-up window annotation
            annotation.FlattenPopUps = true;
        }
    }
}
//Save the document as stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document instances
loadedDocument.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Supported annotation types

### 3D Annotation

3D Annotations are used to represent 3D artworks in a PDF document. Essential PDF provides support to embed 3D files (u3d) in PDF. 

You can add a 3D annotation in PDF document using [Pdf3DAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.Pdf3DAnnotation.html) class. The following example illustrates this.
{% tabs %}
{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//PDF supports 3D annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

FileStream inputStream = new FileStream("3DAnnotation.U3D", FileMode.Open, FileAccess.Read);

//Creates a new pdf 3d annotation.

Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), inputStream);

//Handles the activation of the 3d annotation

Pdf3DActivation activation = new Pdf3DActivation();

activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation;

activation.ShowToolbar = true;

pdf3dAnnotation.Activation = activation;

//Adds annotation to page

page.Annotations.Add(pdf3dAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "3DAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.3DAnnotation.u3d");

//Creates a new PDF 3d annotation

Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), inputStream);

//Handles the activation of the 3d annotation

Pdf3DActivation activation = new Pdf3DActivation();

activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation;

activation.ShowToolbar = true;

pdf3dAnnotation.Activation = activation;

//Adds annotation to page

page.Annotations.Add(pdf3dAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("3DAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("3DAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

You can add the JavaScript script to the 3D annotation using the [OnInstantiate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.Pdf3DAnnotation.html#Syncfusion_Pdf_Interactive_Pdf3DAnnotation_OnInstantiate) property, which is executed whenever a 3D stream is read to create an instance of the 3D artwork. The following code snippet illustrate this.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Create a new PDF 3D annotation

Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), @"Input.u3d");

//Assign JavaScript script

pdf3dAnnotation.OnInstantiate = "host.getURL(\"http://www.google.com\")";

//Adds annotation to page

page.Annotations.Add(pdf3dAnnotation);

//Save the document to disk

document.Save("3DAnnotation.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Create a new PDF 3D annotation

Dim pdf3dAnnotation As New Pdf3DAnnotation(New RectangleF(10, 50, 300, 150), "Input.u3d")

'Assign JavaScript script

pdf3dAnnotation.OnInstantiate = "host.getURL(""http://www.google.com"")"

'Adds annotation to page

page.Annotations.Add(pdf3dAnnotation)

'Save the document to disk

document.Save("3DAnnotation.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//PDF supports 3D annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, and ASP.NET Core platforms

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

FileStream inputStream = new FileStream("3DAnnotation.U3D", FileMode.Open, FileAccess.Read);

//Creates a new PDF 3D annotation

Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), inputStream);

//Assign JavaScript script

pdf3dAnnotation.OnInstantiate = "host.getURL(\"http://www.google.com\")";

//Adds annotation to page

page.Annotations.Add(pdf3dAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "3DAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.3DAnnotation.u3d");

//Creates a new PDF 3d annotation

Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), inputStream);

//Assign JavaScript script

pdf3dAnnotation.OnInstantiate = "host.getURL(\"http://www.google.com\")";          

//Adds annotation to page

page.Annotations.Add(pdf3dAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("3DAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("3DAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### File Link Annotation 

Links for external files can be added in a PDF document by using the [PdfFileLinkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfFileLinkAnnotation.html) class.

The following code example explains how to add a file link annotation in PDF.
{% tabs %}
{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//PDF supports File Link Annotation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//PDF supports File Link Annotation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC.

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//PDF supports File Link Annotation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC.

{% endhighlight %}

{% endtabs %}

### Free Text Annotation

Free text annotation enables you to display the text directly on the page. When you want to add a comment directly without placing it on a pop-up window, [PdfFreeTextAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfFreeTextAnnotation.html) can be used.

The following code example explains how to add a free text annotation in the PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}


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

PointF[] points = { new PointF(100, 450), new PointF(100, 200), new PointF(100, 150) };

freeText.CalloutLines = points;

//Adds the annotation to page

page.Annotations.Add(freeText);

//Saves the document to disk.

document.Save("FreeTextAnnotation.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

Dim points As PointF() = { New PointF(100, 450), New PointF(100, 200), New PointF(100, 150) }

freeText.CalloutLines = points

'Adds the annotation to page

page.Annotations.Add(freeText)

'Saves the document to disk.

document.Save("FreeTextAnnotation.pdf")

document.Close(True)





{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Creates a new pdf document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates PDF free text annotation

PdfFreeTextAnnotation freeText = new PdfFreeTextAnnotation(new RectangleF(50, 100, 100, 50));

//Sets properties to the annotation

freeText.MarkupText = "Free Text with Callout";

freeText.TextMarkupColor = new PdfColor(0, 0, 0);

freeText.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 7f);

freeText.Color = new PdfColor(255, 255, 0);

freeText.BorderColor = new PdfColor(255, 0, 0);

freeText.Border = new PdfAnnotationBorder(.5f);

freeText.LineEndingStyle = PdfLineEndingStyle.OpenArrow;

freeText.AnnotationFlags = PdfAnnotationFlags.Default;

freeText.Text = "Free Text";

freeText.Opacity = 0.5f;

PointF[] points = { new PointF(100, 450), new PointF(100, 200), new PointF(100, 150) };

freeText.CalloutLines = points;

//Adds the annotation to page

page.Annotations.Add(freeText);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respect

Save(stream, "FreeTextAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

PointF[] points = { new PointF(100, 450), new PointF(100, 200), new PointF(100, 150) };

freeText.CalloutLines = points;

//Adds the annotation to page

page.Annotations.Add(freeText);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "FreeTextAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new pdf document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates PDF free text annotation

PdfFreeTextAnnotation freeText = new PdfFreeTextAnnotation(new RectangleF(50, 100, 100, 50));

//Sets properties to the annotation

freeText.MarkupText = "Free Text with Callout";

freeText.TextMarkupColor = new PdfColor(Syncfusion.Drawing.Color.Black);

freeText.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 7f);

freeText.Color = new PdfColor(Syncfusion.Drawing.Color.Yellow);

freeText.BorderColor = new PdfColor(Syncfusion.Drawing.Color.Red);

freeText.Border = new PdfAnnotationBorder(.5f);

freeText.LineEndingStyle = PdfLineEndingStyle.OpenArrow;

freeText.AnnotationFlags = PdfAnnotationFlags.Default;

freeText.Text = "Free Text";

freeText.Opacity = 0.5f;

PointF[] points = { new PointF(100, 450), new PointF(100, 200), new PointF(100, 150) };

freeText.CalloutLines = points;

//Adds the annotation to page

page.Annotations.Add(freeText);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("FreeTextAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("FreeTextAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Line Annotation 

Line annotation displays a single straight line on the page. When you open it, it displays a pop-up window containing text of the associated note.

[PdfLineAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLineAnnotation.html) is used to create and set the properties of the Line annotation.
{% tabs %}
{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

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

lineAnnotation.InnerLineColor = new PdfColor(0, 128, 0);

lineAnnotation.BackColor = new PdfColor(0, 128, 0);

//Assigns the leader line

lineAnnotation.LeaderLineExt = 0;

lineAnnotation.LeaderLine = 0;

//Assigns the Line caption type

lineAnnotation.LineCaption = true;

lineAnnotation.CaptionType = PdfLineCaptionType.Inline;

//Adds this annotation to a new page.

page.Annotations.Add(lineAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "LineAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "LineAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

lineAnnotation.InnerLineColor = new PdfColor(Syncfusion.Drawing.Color.Green);

lineAnnotation.BackColor = new PdfColor(Syncfusion.Drawing.Color.Green);

//Assigns the leader line

lineAnnotation.LeaderLineExt = 0;

lineAnnotation.LeaderLine = 0;

//Assigns the Line caption type

lineAnnotation.LineCaption = true;

lineAnnotation.CaptionType = PdfLineCaptionType.Inline;

//Adds this annotation to a new page.

page.Annotations.Add(lineAnnotation);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("LineAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("LineAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}
### Rubber stamp Annotation

Rubber stamp annotation displays text or graphics intended to look like it is stamped on the page with a rubber stamp. 

When opened, it displays a pop-up window containing the text of the associated note.

[PdfRubberStampAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfRubberStampAnnotation.html) is used to create rubber stamp annotation.

{% tabs %}
{% highlight c# tabtitle="C#" %}


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

document.Save("RubberStamp.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new pdf rubber stamp annotation.

RectangleF rectangle = new RectangleF(40, 60, 80, 20);

PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangle, " Text Rubber Stamp

rubberStampAnnotation.Icon = PdfRubberStampAnnotationIcon.Draft;

rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Adds annotation to the page

page.Annotations.Add(rubberStampAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "RubberStamp.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "RubberStamp.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("RubberStamp.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("RubberStamp.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Ink Annotation

Ink annotation represents freehand “scribble” comprising one or more disjoint paths. 

When you open it, it displays a pop-up window containing text of the associated note.

[PdfInkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfInkAnnotation.html) is used to create ink annotation in a PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

List<float> linePoints = new List<float> { 40, 300, 60, 100, 40, 50, 40, 300 };

//Creates a new ink annotation

RectangleF rectangle = new RectangleF(0, 0, 300, 400);

PdfInkAnnotation inkAnnotation = new PdfInkAnnotation(rectangle, linePoints);

inkAnnotation.Color = new PdfColor(Color.FromArgb(0,255,0,0));

//Adds annotation to the page

page.Annotations.Add(inkAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "InkAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

List<float> linePoints = new List<float> { 40, 300, 60, 100, 40, 50, 40, 300 };

//Creates a new ink annotation

RectangleF rectangle = new RectangleF(0, 0, 300, 400);

PdfInkAnnotation inkAnnotation = new PdfInkAnnotation(rectangle, linePoints);

inkAnnotation.Color = new PdfColor(Color.Red);

//Adds annotation to the page

page.Annotations.Add(inkAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "InkAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

List<float> linePoints = new List<float> { 40, 300, 60, 100, 40, 50, 40, 300 };

//Creates a new ink annotation

RectangleF rectangle = new RectangleF(0, 0, 300, 400);

PdfInkAnnotation inkAnnotation = new PdfInkAnnotation(rectangle, linePoints);

inkAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);

//Adds annotation to the page

page.Annotations.Add(inkAnnotation);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("InkAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("InkAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

You can get ink list points from the [PdfLoadedInkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLoadedInkAnnotation.html), represented by [InkPointsCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLoadedInkAnnotation.html#Syncfusion_Pdf_Interactive_PdfLoadedInkAnnotation_InkPointsCollection). The following code illustrate this.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Loads the document

PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");

//Gets the first page from the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Gets the first ink annotation

PdfLoadedInkAnnotation inkAnnotation = annotations[0] as PdfLoadedInkAnnotation;

//Gets the ink points collection

List<List<float>> points = inkAnnotation.InkPointsCollection;

//Save the document

lDoc.Save("Output.pdf");

//Close the document

lDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads the document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Gets the first page from the document

Dim page As PdfLoadedPage = TryCast(lDoc.Pages(0), PdfLoadedPage)

'Gets the annotation collection

Dim annotations As PdfLoadedAnnotationCollection = page.Annotations

'Gets the first ink annotation

Dim inkAnnotation As PdfLoadedInkAnnotation = TryCast(annotations(0), PdfLoadedInkAnnotation)

'Gets the ink points collection

Dim points As List(Of List(Of Single)) = inkAnnotation.InkPointsCollection

'Save the document

lDoc.Save("Output.pdf")

'Close the document

lDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document using the Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Gets the first page from the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Gets the first ink annotation

PdfLoadedInkAnnotation inkAnnotation = annotations[0] as PdfLoadedInkAnnotation;

//Gets the ink points collection

List<List<float>> points = inkAnnotation.InkPointsCollection;

//Save the document as stream

MemoryStream stream = new MemoryStream();

await lDoc.SaveAsync(stream);

//Close the document instances

lDoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Gets the first page from the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Gets the first ink annotation

PdfLoadedInkAnnotation inkAnnotation = annotations[0] as PdfLoadedInkAnnotation;

//Gets the ink points collection

List<List<float>> points = inkAnnotation.InkPointsCollection;

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

lDoc.Save(stream);

//If the position is not set to '0', the PDF will be empty.

stream.Position = 0;

//Close the document

lDoc.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Gets the first page from the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Gets the first ink annotation

PdfLoadedInkAnnotation inkAnnotation = annotations[0] as PdfLoadedInkAnnotation;

//Gets the ink points collection

List<List<float>> points = inkAnnotation.InkPointsCollection;

//Save the document as stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

//Close the document instances

lDoc.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Pop-up Annotation

Pop-up annotation displays text in a pop-up window for entry and editing. 

It typically does not appear alone, but is associated with markup annotation, its parent annotation.

[PdfPopupAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfPopupAnnotation.html) is used to add pop-up annotation in a PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//Create new PDF document

PdfDocument document = new PdfDocument();

//Create a new PDF page

PdfPage page = document.Pages.Add();

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

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected c

Save(stream, "PopupAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create new PDF document

PdfDocument document = new PdfDocument();

//Create a new PDF page

PdfPage page = document.Pages.Add();

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

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "PopupAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create new PDF document

PdfDocument document = new PdfDocument();

//Create a new PDF page

PdfPage page = document.Pages.Add();

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

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("PopupAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("PopupAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### File Attachment Annotation

File attachment annotation contains reference to a file that typically is embedded in the PDF file.

[PdfAttachmentAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachmentAnnotation.html) is used to add a file attachment annotation in a PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF Document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new rectangle

RectangleF attachmentRectangle = new RectangleF(10, 40, 30, 30);

//Load the file as stream

Stream inputStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Logo.png");

//Creates a new attachment annotation.

PdfAttachmentAnnotation attachmentAnnotation = new PdfAttachmentAnnotation(attachmentRectangle, @"logo.png", inputStream);

//Sets the attachment icon to attachment annotation.

attachmentAnnotation.Icon = PdfAttachmentIcon.PushPin;

//Adds this annotation to a new page.

page.Annotations.Add(attachmentAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "AttachmentAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF Document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new rectangle

RectangleF attachmentRectangle = new RectangleF(10, 40, 30, 30);

//Load the PDF document

FileStream inputStream = new FileStream("logo.png", FileMode.Open, FileAccess.Read);

//Creates a new attachment annotation.

PdfAttachmentAnnotation attachmentAnnotation = new PdfAttachmentAnnotation(attachmentRectangle, @"logo.png", inputStream);

//Sets the attachment icon to attachment annotation.

attachmentAnnotation.Icon = PdfAttachmentIcon.PushPin;

//Adds this annotation to a new page.

page.Annotations.Add(attachmentAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "PopupAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF Document.

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new rectangle

RectangleF attachmentRectangle = new RectangleF(10, 40, 30, 30);

//Load the file as stream

Stream inputStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Logo.png");

//Creates a new attachment annotation.

PdfAttachmentAnnotation attachmentAnnotation = new PdfAttachmentAnnotation(attachmentRectangle, @"logo.png", inputStream);

//Sets the attachment icon to attachment annotation.

attachmentAnnotation.Icon = PdfAttachmentIcon.PushPin;

//Adds this annotation to a new page.

page.Annotations.Add(attachmentAnnotation);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("AttachmentAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("AttachmentAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Sound Annotation

Sound annotation is used to play the sound clip in the PDF Document.

The following code example explains how to add a sound annotation in a PDF document using [PdfSoundAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfSoundAnnotation.html).
{% tabs %}
{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//PDF supports Sound Annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Web.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new sound annotation.

FileStream inputStream = new FileStream("Startup.wav", FileMode.Open, FileAccess.Read);

PdfSoundAnnotation soundAnnotation = new PdfSoundAnnotation(rectangle, inputStream);

soundAnnotation.Sound.Encoding = PdfSoundEncoding.Signed;

soundAnnotation.Sound.Channels = PdfSoundChannels.Stereo;

soundAnnotation.Sound.Bits = 16;

soundAnnotation.Color = new PdfColor(Color.Red);

//Sets the pdf sound icon.

soundAnnotation.Icon = PdfSoundIcon.Speaker;

//Adds this annotation to a new page.

page.Annotations.Add(soundAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "SoundIcon.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a new rectangle

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

//Creates a new sound annotation.

//Load the file as stream

Stream inputStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Signature.Assets.Startup.wav");

PdfSoundAnnotation soundAnnotation = new PdfSoundAnnotation(rectangle, inputStream);

soundAnnotation.Sound.Encoding = PdfSoundEncoding.Signed;

soundAnnotation.Sound.Channels = PdfSoundChannels.Stereo;

soundAnnotation.Sound.Bits = 16;

soundAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);

//Sets the pdf sound icon.

soundAnnotation.Icon = PdfSoundIcon.Speaker;

//Adds this annotation to a new page.

page.Annotations.Add(soundAnnotation);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SoundIcon.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SoundIcon.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### URI Annotation

URI annotation is used to navigate to a particular web URI

The following code example explains how to add URI annotation in a PDF document using [PdfUriAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfUriAnnotation.html).
{% tabs %}
{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

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

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code sample.

Save(stream, "UriAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "UriAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("UriAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("UriAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Document Link Annotation

This annotation is used to navigate to a specific destination within the document.

[PdfDocumentLinkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfDocumentLinkAnnotation.html) is used to add a document link annotation in PDF document.
{% tabs %}
{% highlight c# tabtitle="C#" %}

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

{% highlight vb.net tabtitle="VB.NET" %}


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

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Creates a page

PdfPage page2 = document.Pages.Add();

//Creates a new rectangle

RectangleF docLinkAnnotationRectangle = new RectangleF(10, 40, 30, 30);

//Creates a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationRectangle)

documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate;

documentLinkAnnotation.Text = "Document link annotation";

documentLinkAnnotation.Color = new PdfColor(Color.FromArgb(0,0,0,128));

//Sets the destination.

documentLinkAnnotation.Destination = new PdfDestination(page2);

documentLinkAnnotation.Destination.Location = new PointF(10, 0);

documentLinkAnnotation.Destination.Zoom = 5;

//Adds this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "DocumentLinkAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

documentLinkAnnotation.Destination.Location = new PointF(10, 0);

documentLinkAnnotation.Destination.Zoom = 5;

//Adds this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentLinkAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

documentLinkAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Navy);

//Sets the destination.

documentLinkAnnotation.Destination = new PdfDestination(page2);

documentLinkAnnotation.Destination.Location = new Syncfusion.Drawing.PointF(10, 0);

documentLinkAnnotation.Destination.Zoom = 5;

//Adds this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation); 

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentLinkAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentLinkAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Pdf Redaction Annotation

The essential PDF supports removing or redacting the sensitive text and images from the PDF documents. The redaction is the process of permanently removing sensitive information from the PDF document, use the [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class to remove content. Using the [PdfRedactionAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfRedactionAnnotation.html) class, you can mark the content to redact or remove it from the PDF pages. The content will be redacted when performing the [Flatten](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedAnnotationCollection.html#Syncfusion_Pdf_Parsing_PdfLoadedAnnotationCollection_Flatten) operation.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page.

PdfPage page = document.Pages.Add();

//Create a new Redaction annotation.

PdfRedactionAnnotation annot = new PdfRedactionAnnotation();

//Assign the Bounds value

annot.Bounds = new Rectangle(100, 120, 100, 100);

//Assign the InnerColor

annot.InnerColor = Color.Black;

//Assign the Bordercolor

annot.BorderColor = Color.Yellow;

//Assign the Textcolor

annot.TextColor = Color.Blue;

//Assign the font

annot.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 10);

//Assign the OverlayText

annot.OverlayText = "REDACTION";

//Assign the TextAlignment

annot.TextAlignment = PdfTextAlignment.Right;

//Assign the RepeatText

annot.RepeatText = true;

annot.SetAppearance(true);

//Add the annotation to the page.

page.Annotations.Add(annot);

//Save the document to disk.

document.Save("output.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
       
Dim document As PdfDocument = New PdfDocument()

'Create a new page.
	
Dim page As PdfPage = document.Pages.Add()
		
'Create a New Redaction annotation.
		
Dim annot As PdfRedactionAnnotation = New PdfRedactionAnnotation()
		
'Assign the Bounds value
		
annot.Bounds = New Rectangle(100, 120, 100, 100)
		
'Assign the InnerColor 
		
annot.InnerColor = Color.Black
		
'Assign the BorderColor
		
annot.BorderColor = Color.Yellow
		
'Assign the TextColor 
		
annot.TextColor = Color.Blue
		
'Assign the font value
		
annot.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 10)
		
'Assign the OverlayText
		
annot.OverlayText = "REDACTION"
		
'Assign the TextAlignment
		
annot.TextAlignment = PdfTextAlignment.Right
		
'Assign the RepeatText
		
annot.RepeatText = True
		
annot.SetAppearance(True)
		
'Add the annotation to the page.
		
page.Annotations.Add(annot)
		
'Save the document to disk.
		
document.Save("output.pdf")
		
'Close the document
		
document.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page.

PdfPage page = document.Pages.Add();

//Create a new Redaction annotation.

PdfRedactionAnnotation annot = new PdfRedactionAnnotation();

//Assign the Bounds value

annot.Bounds = new Rectangle(100, 120, 100, 100);

//Assign the InnerColor

annot.InnerColor = Color.Black;

//Assign the Bordercolor

annot.BorderColor = Color.Yellow;

//Assign the Textcolor

annot.TextColor = Color.Blue;

//Assign the font

annot.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 10);

//Assign the OverlayText

annot.OverlayText = "REDACTION";

//Assign the TextAlignment

annot.TextAlignment = PdfTextAlignment.Right;

//Assign the RepeatText

annot.RepeatText = true;

annot.SetAppearance(true);

//Add the annotation to the page.

page.Annotations.Add(annot);

//Save the PDF document to stream 

MemoryStream stream = new MemoryStream(); 

document.Save(stream); 

//Close the document 

document.Close(true); 

Save(stream, "RedactionAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();
			
//Create a new page.
			
PdfPage page = document.Pages.Add();
			
//Create a new Redaction annotation.
			
PdfRedactionAnnotation annot = new PdfRedactionAnnotation();
			
//Assign the Bounds value
			
annot.Bounds = new Rectangle(100, 120, 100, 100);
			
//Assign the InnerColor
			
annot.InnerColor = Color.Black;
			
//Assign the Bordercolor
			
annot.BorderColor = Color.Yellow;
			
//Assign the Textcolor
			
annot.TextColor = Color.Blue;
			
//Assign the font
			
annot.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 10);
			
//Assign the OverlayText
			
annot.OverlayText = "REDACTION";
			
//Assign the TextAlignment
			
annot.TextAlignment = PdfTextAlignment.Right;
			
//Assign the RepeatText
			
annot.RepeatText = true;
			
annot.SetAppearance(true);
			
//Add the annotation to the page.
	
page.Annotations.Add(annot);
			
//Save the document into stream 
			
MemoryStream stream = new MemoryStream();
			
document.Save(stream);
			
stream.Position = 0;
			
//Close the document 
			
document.Close(true);
			
//Defining the ContentType for pdf file 
			
string contentType = "application/pdf";
			
//Define the file name 
			
String fileName = "RedactionAnnotation.pdf";
			
//Create a FileContentResult object by using the file contents, content type, and file name 
			
return File(stream, contentType, fileName);
			
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page.

PdfPage page = document.Pages.Add();

//Create a new Redaction annotation.

PdfRedactionAnnotation annot = new PdfRedactionAnnotation();

//Assign the Bounds value

annot.Bounds = new Rectangle(100, 120, 100, 100);

//Assign the InnerColor

annot.InnerColor = Color.Black;

//Assign the Bordercolor

annot.BorderColor = Color.Yellow;

//Assign the Textcolor

annot.TextColor = Color.Blue;

//Assign the font

annot.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 10);

//Assign the OverlayText

annot.OverlayText = "REDACTION";

//Assign the TextAlignment

annot.TextAlignment = PdfTextAlignment.Right;

//Assign the RepeatText

annot.RepeatText = true;

annot.SetAppearance(true);

//Add the annotation to the page.

page.Annotations.Add(annot);

//Save the document into stream.
 
MemoryStream stream = new MemoryStream(); 

document.Save(stream);

//Close the document. 

document.Close(true); 

//Save the stream into pdf file 

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("RedactionAnnotation.pdf", "application/pdf", stream);

{% endhighlight %}

{% endtabs %}

N>The redaction annotation flatten operation is currently supported in the .NET Framework and ASP.NET Core platforms only, it is not supported in the UWP, Xamarin platforms.

## Cloud border style Annotation

### PdfRectangleAnnotation

Cloud border style can be added to the [PdfRectangleAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfRectangleAnnotation.html) by using the [PdfBorderEffect](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfBorderEffect.html) class. 
The following code sample explains how to add cloud border styled rectangle annotation in the PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument ();

//Create a new page

PdfPage page = document.Pages.Add();

//Create a new rectangle annotation.

PdfRectangleAnnotation annotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 200, 100), "rectangle");

//Assign the borderWidth value.

annotation. Border. BorderWidth = 1;

//Assign the color

annotation. Color = Color.Red;

//Assign the InnerColor

annotation.InnerColor = Color.Blue;

//Create a new PdfBorderEffect class.

PdfBorderEffect bordereffect = new PdfBorderEffect();

//Assign the intensity value

bordereffect.Intensity =2;

//Assign the cloud style

bordereffect.Style = PdfBorderEffectStyle.Cloudy;

//Assign the BorderEffect.

annotation.BorderEffect = bordereffect;

//Add the annotation to the page.

page.Annotations.Add(annotation);

//Save the document to disk.

document.Save("Output.pdf");

//close the document to disk.

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.

Dim document As PdfDocument = New PdfDocument()
		
'Create a new page.
		
Dim page As PdfPage = document.Pages.Add()
		
'Create a new Redaction annotation
		
Dim annotation As PdfRectangleAnnotation = New PdfRectangleAnnotation(New RectangleF(0, 0, 200, 100), "rectangle")
		
'Assign the borderWidth value.
		
annotation.Border.BorderWidth = 1
		
'Assign the color
		
annotation.Color = Color.Red
		
'Assign the InnerColor
		
annotation.InnerColor = Color.Blue
		
'Create a new PdfBorderEffect class.
		
Dim bordereffect As PdfBorderEffect = New PdfBorderEffect()
		
'Assign the intensity value
		
bordereffect.Intensity = 2
		
'Assign the cloud style
		
bordereffect.Style = PdfBorderEffectStyle.Cloudy
		
'Assign the BorderEffect.
		
annotation.BorderEffect = bordereffect
		
'Add the annotation to the page.
		
page.Annotations.Add(annotation)
		
'Save the document to disk.
		
document.Save("Output.pdf")
		
'close the document to disk.
		
document.Close(True) 

{% endhighlight %}
  {% highlight c# tabtitle="UWP" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create a new rectangle annotation.

PdfRectangleAnnotation annotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 200, 100), "rectangle");

//Assign the borderWidth value.

annotation.Border.BorderWidth = 1;

//Assign the color

annotation.Color = Color.Red;

//Assign the InnerColor

annotation.InnerColor = Color.Blue;

//Create a new PdfBorderEffect class.

PdfBorderEffect bordereffect = new PdfBorderEffect();

//Assign the intensity value

bordereffect.Intensity =2;

//Assign the cloud style

bordereffect.Style = PdfBorderEffectStyle.Cloudy;

//Assign the BorderEffect.

annotation.BorderEffect = bordereffect;

//Add the annotation to the page.

page.Annotations.Add(annotation);

//Save the PDF document to stream 

MemoryStream stream = new MemoryStream(); 

await document.SaveAsync(stream);
 
//Close the document
 
document.Close(true); 

//save the stream

Save(stream, "CloudRectangleAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

// create a rectangle annotation

PdfRectangleAnnotation annotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 200, 100), "rectangle");

//Assign the borderWidth value.

annotation.Border.BorderWidth = 1;

//Assign the color

annotation.Color = Color.Red;

//Assign the InnerColor

annotation.InnerColor = Color.Blue;

//Create a new PdfBorderEffect class.

PdfBorderEffect bordereffect = new PdfBorderEffect();

//Assign the intensity value

bordereffect.Intensity = 2;

//Assign the cloud style

bordereffect.Style = PdfBorderEffectStyle.Cloudy;

//Assign the BorderEffect.

annotation.BorderEffect = bordereffect;

// Adds the annotation to the page.

page.Annotations.Add(annotation);

//Save the document into stream 

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document 

document.Close(true);

//Defining the ContentType for pdf file 

string contentType = "application/pdf";

//Define the file name 

String fileName = "cloudRectangleAnnotation.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name
 
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page.

PdfPage page = document.Pages.Add();

//Create a new rectangle annotation.

PdfRectangleAnnotation annotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 200, 100), "rectangle");

//Assign the borderWidth value.

annotation.Border.BorderWidth = 1;

//Assign the color

annotation.Color = Color.Red;

//Assign the InnerColor

annotation.InnerColor = Color.Blue;

//Create a new PdfBorderEffect class.

PdfBorderEffect bordereffect = new PdfBorderEffect();

//Assign the intensity value

bordereffect.Intensity =2;

//Assign the cloud style

bordereffect.Style = PdfBorderEffectStyle.Cloudy;

//Assign the BorderEffect.

annotation.BorderEffect = bordereffect;

//Add the annotation to the page.

page.Annotations.Add(annotation);

//Save the document into stream.
 
MemoryStream stream = new MemoryStream(); 

document.Save(stream);

//Close the document.
 
document.Close(true); 

//Save the stream into pdf file 

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("rectangleAnnotation.pdf", "application/pdf", stream);

{% endhighlight %}
{% endtabs %}

### Polygon Annotation

Cloud border style can be added to the [PdfPolygonAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfPolygonAnnotation.html) by using the [PdfBorderEffect](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfBorderEffect.html) class. 
The following code sample explains how to add cloud border styled polygon annotation in the PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create points
   
int[] points = new int[] { 100, 300, 150, 200, 300, 200, 350, 300, 300, 400, 150, 400 };
   
//Create a new polygon annotation.
   
PdfPolygonAnnotation annotation = new PdfPolygonAnnotation(points,"polygon");

//Assign the borderWidth value.

annotation.Border.BorderWidth = 1;

//Assign the color

annotation.Color = Color.Red;

//Assign the InnerColor

annotation.InnerColor = Color.Blue;

//Create a new PdfBorderEffect class.

PdfBorderEffect bordereffect = new PdfBorderEffect();

//Assign the intensity value

bordereffect.Intensity =2;

//Assign the cloud style

bordereffect.Style = PdfBorderEffectStyle.Cloudy;

//Assign the BorderEffect.

annotation.BorderEffect = bordereffect;

//Add the annotation to the page.

page.Annotations.Add(annotation);

//Save the document to disk.

document.Save("Output.pdf");

//close the document to disk.

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a New PDF document.

Dim document As PdfDocument = New PdfDocument()
		
'Create a new page.
		
Dim page As PdfPage = document.Pages.Add()
		
'Create points
		
Dim points As Integer() = New Integer() {100, 300, 150, 200, 300, 200, 350, 300, 300, 400, 150, 400}
		
'Create a new polygon annotation
		
Dim annotation As PdfPolygonAnnotation = New PdfPolygonAnnotation(points, "polygon")
		
'Assign the borderWidth value.
		
annotation.Border.BorderWidth = 1
		
'Assign the color
		
annotation.Color = Color.Red
		
'Assign the InnerColor
		
annotation.InnerColor = Color.Blue
		
'Create a new PdfBorderEffect class.
		
Dim bordereffect As PdfBorderEffect = New PdfBorderEffect()
		
'Assign the intensity value
		
bordereffect.Intensity = 2
		
'Assign the cloud style
		
bordereffect.Style = PdfBorderEffectStyle.Cloudy
		
'Assign the BorderEffect.
		
annotation.BorderEffect = bordereffect
		
'Add the annotation to the page.
		
page.Annotations.Add(annotation)
		
'Save the document to disk.
		
 document.Save("Output.pdf")
		
'close the document to disk.
		
document.Close(True)
		
{% endhighlight %}		

  {% highlight c# tabtitle="UWP" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create points

int[] points = new int[] { 100, 300, 150, 200, 300, 200, 350, 300, 300, 400, 150, 400 };

//Create a new polygon annotation.

PdfPolygonAnnotation annotation = new PdfPolygonAnnotation(points,"polygon");

//Assign the borderWidth value.

annotation.Border.BorderWidth = 1;

//Assign the color

annotation.Color = Color.Red;

//Assign the InnerColor

annotation.InnerColor = Color.Blue;

//Create a new PdfBorderEffect class.

PdfBorderEffect bordereffect = new PdfBorderEffect();

//Assign the intensity value

bordereffect.Intensity =2;

//Assign the cloud style

bordereffect.Style = PdfBorderEffectStyle.Cloudy;

//Assign the BorderEffect.

annotation.BorderEffect = bordereffect;

/Add the annotation to the page.

page.Annotations.Add(annotation);

//Save the PDF document to stream 

MemoryStream stream = new MemoryStream();
 
await document.SaveAsync(stream); 

//Close the document 

document.Close(true);
 
//saves the stream

Save(stream, "CloudPolygonAnnotation.pdf");

//Create a new PDF document.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document. Pages. Add ();

//Create points

int[] points = new int[] { 100, 300, 150, 200, 300, 200, 350, 300, 300, 400, 150, 400 };

//Create a new polygon annotation.

PdfPolygonAnnotation annotation = new PdfPolygonAnnotation(points,"polygon");

//Assign the borderWidth value.

annotation.Border.BorderWidth = 1;

//Assign the color

annotation.Color = Color.Red;

//Assign the InnerColor

annotation.InnerColor = Color.Blue;

//Create a new PdfBorderEffect class.

PdfBorderEffect bordereffect = new PdfBorderEffect();

//Assign the intensity value

bordereffect.Intensity =2;

//Assign the cloud style

bordereffect.Style = PdfBorderEffectStyle.Cloudy;

//Assign the BorderEffect.

annotation.BorderEffect = bordereffect;

//Add the annotation to the page.

page.Annotations.Add(annotation);

//Save the document into stream 

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document 

document.Close(true);

//Defining the ContentType for pdf file 

string contentType = "application/pdf"; 

//Define the file name 

String fileName = "cloudpolygonAnnotation.pdf"; 

//Create a FileContentResult object by using the file contents, content type, and file name 

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create points

int[] points = new int[] { 100, 300, 150, 200, 300, 200, 350, 300, 300, 400, 150, 400 };

//Create a new polygon annotation

PdfPolygonAnnotation annotation = new PdfPolygonAnnotation(points, "polygon");

//Assign the borderWidth value.

annotation.Border.BorderWidth = 1;

//Assign the color

annotation.Color = Color.Red;

//Assign the InnerColor

annotation.InnerColor = Color.Blue;

//Create a new PdfBorderEffect class.

PdfBorderEffect bordereffect = new PdfBorderEffect();

//Assign the intensity value

bordereffect.Intensity =2;

//Assign the cloud style

bordereffect.Style = PdfBorderEffectStyle.Cloudy;

//Assign the BorderEffect.

annotation.BorderEffect = bordereffect;

//Adds the annotation to the page.

page.Annotations.Add(annotation);

//Save the PDF document to stream 

MemoryStream stream = new MemoryStream(); 

document.Save(stream);

//Close the document. 

document.Close(true); 

//Save the stream into pdf file 

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("polygonAnnotation.pdf", "application/pdf", stream);

{% endhighlight %}

{% endtabs %}

### Watermark Annotation

A watermark annotation is used to represent graphics that are expected to be printed at a fixed size and position on a page, regardless of the dimensions of the printed page., [PdfWatermarkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfWatermarkAnnotation.html) can be used.
The following code example explains how to add a watermark annotation in the PDF document
*C#
*VB.NET
*UWP
*ASP.NET Core
*Xamarin

{% tabs %}
{% highlight c# tabtitle="C#" %}


//Load the existing PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

 //Get the page 
 
PdfLoadedPage lpage = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates PDF watermark annotation 

PdfWatermarkAnnotation watermark = new PdfWatermarkAnnotation(new RectangleF(50, 100, 100, 50));

 //Sets properties to the annotation 
 
watermark.Opacity = 0.5f; 

//Create the appearance of watermark 

watermark.Appearance.Normal.Graphics.DrawString("Watermark Text",new PdfStandardFont(PdfFontFamily.Helvetica,20),PdfBrushes.Red,new RectangleF(0,0,200,50), new PdfStringFormat(PdfTextAlignment.Center,PdfVerticalAlignment.Middle));

//Adds the annotation to page 

lpage.Annotations.Add(watermark); 

//Saves the document to disk. 

loadedDocument.Save("WatermarkAnnotation.pdf"); 

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the existing PDF document

 Dim loadedDocument As New PdfLoadedDocument("input.pdf");
 
'Get the page 
Dim lpage As PdfLoadedPage = TryCast(loadedDocument.Pages(0),PdfLoadedPage)

'Creates PDF watermark annotation

Dim watermark As New PdfWatermarkAnnotation(New RectangleF(50, 100, 100, 50)) 

watermark.Opacity = 0.5f; 

'Creates the appearance of watermark

watermark.Appearance.Normal.Graphics.DrawString("Watermark Text",new PdfStandardFont(PdfFontFamily.Helvetica,20),PdfBrushes.Red,new RectangleF(0,0,200,50), new PdfStringFormat(PdfTextAlignment.Center,PdfVerticalAlignment.Middle))

'Adds annotation to the page 

lpage.Annotations.Add(watermark)

'Saves the document to disk. 
 
loadedDocument.Save("WatermarkAnnotation.pdf")
 
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load the existing PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Get the page 
 
PdfLoadedPage lpage = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates PDF watermark annotation 

PdfWatermarkAnnotation watermark = new PdfWatermarkAnnotation(new RectangleF(50, 100, 100, 50));

//Sets properties to the annotation 
 
watermark.Opacity = 0.5f; 

//Create the appearance of watermark 

watermark.Appearance.Normal.Graphics.DrawString("Watermark Text",new PdfStandardFont(PdfFontFamily.Helvetica,20),PdfBrushes.Red,new RectangleF(0,0,200,50), new PdfStringFormat(PdfTextAlignment.Center,PdfVerticalAlignment.Middle));

//Adds the annotation to page 

lpage.Annotations.Add(watermark);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream(); 

await loadedDocument.SaveAsync(stream);

//Close the document 

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples 

Save(stream, "WatermarkAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the existing PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Get the page 
 
PdfLoadedPage lpage = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates PDF watermark annotation 

PdfWatermarkAnnotation watermark = new PdfWatermarkAnnotation(new RectangleF(50, 100, 100, 50));

//Sets properties to the annotation 
 
watermark.Opacity = 0.5f; 

//Create the appearance of watermark 

watermark.Appearance.Normal.Graphics.DrawString("Watermark Text",new PdfStandardFont(PdfFontFamily.Helvetica,20),PdfBrushes.Red,new RectangleF(0,0,200,50), new PdfStringFormat(PdfTextAlignment.Center,PdfVerticalAlignment.Middle));

//Adds the annotation to page 

lpage.Annotations.Add(watermark);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document 
loadedDocument.Close(true); 

//Defining the ContentType for pdf file

 string contentType = "application/pdf"; 
 
//Define the file name

 string fileName = "WatermarkAnnotation.pdf";
 
//Creates a FileContentResult object by using the file contents, content type, and file name
 
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the existing PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Get the page 
 
PdfLoadedPage lpage = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates PDF watermark annotation 

PdfWatermarkAnnotation watermark = new PdfWatermarkAnnotation(new RectangleF(50, 100, 100, 50));

//Sets properties to the annotation 
 
watermark.Opacity = 0.5f; 

//Create the appearance of watermark 

watermark.Appearance.Normal.Graphics.DrawString("Watermark Text",new PdfStandardFont(PdfFontFamily.Helvetica,20),PdfBrushes.Red,new RectangleF(0,0,200,50), new PdfStringFormat(PdfTextAlignment.Center,PdfVerticalAlignment.Middle));

//Adds the annotation to page
 
lpage.Annotations.Add(watermark);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document 

loadedDocument.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows) { 
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("WatermarkAnnotation.pdf", "application/pdf", stream);
 }
 else {
 Xamarin.Forms.DependencyService.Get<ISave>().Save("WatermarkAnnotation.pdf", "application/pdf", stream);
 }


## Measurement Annotations

Essential PDF supports interactive measurement annotations, which measures the distance, area, and angle of the line segments.

The following measurement annotation types are supported in Essential PDF:

### Line measurement annotation

The line measurement annotation is displayed as the straight line in the page. The distance of the line is measured automatically when you change the position of the line and is displayed in the pop-up window.

[PdfLineMeasurementAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLineMeasurementAnnotation.html) to add a line measurement annotation to the page.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Creates a new PDF document.

PdfDocument document= new PdfDocument();

//Creates a new page.

PdfPage page = document.Pages.Add();

PdfFont font= new PdfStandardFont(PdfFontFamily.Helvetica, 10f, PdfFontStyle.Regular);

//Specifies the line end points.

int[]  points = new int[] { 100, 750, 500, 750 };

//Creates the line measurement annotation

PdfLineMeasurementAnnotation lineMeasureAnnotation = new PdfLineMeasurementAnnotation(points);

//Assign author to the line measurement annotation.

lineMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the line measurement annotation

lineMeasureAnnotation.Subject = "LineAnnotation";

//Assign unit to the line measurement annotation

lineMeasureAnnotation.Unit = PdfMeasurementUnit.Inch;

//Assign borderWidth to the line measurement annotation.

lineMeasureAnnotation.lineBorder.BorderWidth = 2;

//Assign font to the line measurement annotation.

lineMeasureAnnotation.Font = font;

//Assign color to the line measurement annotation.

lineMeasureAnnotation.Color = new PdfColor(Color.Red);

//Adds the line measurement annotation to a new page.

page.Annotations.Add(lineMeasureAnnotation);

//Saves the document to disk.

document.Save("LineMeasurementAnnotation.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

//Creates a new PDF document

Dim document As PdfDocument = New PdfDocument

//Creates a new page

Dim page As PdfPage = document.Pages.Add

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 10.0!, PdfFontStyle.Regular)

//Specifies the line end points.

Dim points() As Integer = New Integer() {100, 750, 500, 750}

//Creates the line measurement annotation

Dim lineMeasureAnnotation As PdfLineMeasurementAnnotation = New PdfLineMeasurementAnnotation(points)

'Assign author to the line measurement annotation

lineMeasureAnnotation.Author = "Syncfusion"

'Assign subject to the line measurement annotation

lineMeasureAnnotation.Subject = "LineAnnotation"

'Assign unit to the line measurement annotation

lineMeasureAnnotation.Unit = PdfMeasurementUnit.Inch

'Assign borderWidth to the line measurement annotation

lineMeasureAnnotation.lineBorder.BorderWidth = 2

'Assign font to the line measurement annotation

lineMeasureAnnotation.Font = font

'Assign color to the line measurement annotation

lineMeasureAnnotation.Color = New PdfColor(Color.Red)

'Adds the line measurement annotation to a new page

page.Annotations.Add(lineMeasureAnnotation)

'Saves the document to disk

document.Save("LineMeasurementAnnotation.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 10f, PdfFontStyle.Regular);

//Specifies the line end points

int[] points = new int[] { 100, 750, 500, 750 };

//Creates the line measurement annotation

PdfLineMeasurementAnnotation lineMeasureAnnotation = new PdfLineMeasurementAnnotation(points);

//Assign author to the line measurement annotation

lineMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the line measurement annotation

lineMeasureAnnotation.Subject = "LineAnnotation";

//Assign unit to the line measurement annotation

lineMeasureAnnotation.Unit = PdfMeasurementUnit.Inch;

//Assign borderWidth to the line measurement annotation

lineMeasureAnnotation.lineBorder.BorderWidth = 2;

//Assign font to the line measurement annotation

lineMeasureAnnotation.Font = font;

//Assign color to the line measurement annotation

lineMeasureAnnotation.Color = new PdfColor(Color.FromArgb(255, 255, 0, 0));

//Adds the line measurement annotation to a new page

page.Annotations.Add(lineMeasureAnnotation);

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

document.Save(stream);

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 10f, PdfFontStyle.Regular);

//Specifies the line end points

int[] points = new int[] { 100, 750, 500, 750 };

//Creates the line measurement annotation

PdfLineMeasurementAnnotation lineMeasureAnnotation = new PdfLineMeasurementAnnotation(points);

//Assign author to the line measurement annotation

lineMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the line measurement annotation

lineMeasureAnnotation.Subject = "LineAnnotation";

//Assign unit to the line measurement annotation

lineMeasureAnnotation.Unit = PdfMeasurementUnit.Inch;

//Assign borderWidth to the line measurement annotation

lineMeasureAnnotation.lineBorder.BorderWidth = 2;

//Assign font to the line measurement annotation

lineMeasureAnnotation.Font = font;

//Assign color to the line measurement annotation

lineMeasureAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);

//Adds the line measurement annotation to a new page

page.Annotations.Add(lineMeasureAnnotation);

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

document.Save(stream);

stream.Position=0;

//Close the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "LineMeasurementAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 10f, PdfFontStyle.Regular);

//Specifies the line end points

int[] points = new int[] { 100, 750, 500, 750 };

//Creates the line measurement annotation

PdfLineMeasurementAnnotation lineMeasureAnnotation = new PdfLineMeasurementAnnotation(points);

//Assign author to the line measurement annotation

lineMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the line measurement annotation

lineMeasureAnnotation.Subject = "LineAnnotation";

//Assign unit to the line measurement annotation

lineMeasureAnnotation.Unit = PdfMeasurementUnit.Inch;

//Assign borderWidth to the line measurement annotation

lineMeasureAnnotation.lineBorder.BorderWidth = 2;

//Assign font to the line measurement annotation

lineMeasureAnnotation.Font = font;

//Assign color to the line measurement annotation

lineMeasureAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);

//Adds the line measurement annotation to a new page

page.Annotations.Add(lineMeasureAnnotation);

MemoryStream stream = new MemoryStream();

//Save the document into stream.

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("LineMeasurementAnnotation.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("LineMeasurementAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Square measurement annotation

The square measurement annotation is displayed as square shape in the page. The area of the square is measured when you change the square bound and is displayed in the pop-up window.

[PdfSquareMeasurementAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfSquareMeasurementAnnotation.html) is used to add a square measurement annotation to the page.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document

PdfDocument document= new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

RectangleF rect = new RectangleF(10, 100, 100,100);

//Creates the square measurement annotation

PdfSquareMeasurementAnnotation squareMeasureAnnotation = new PdfSquareMeasurementAnnotation(rect);

//Assign author to the square measurement annotation

squareMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the square measurement annotation

squareMeasureAnnotation.Subject = "Square measurement annotation";

//Assign color to the square measurement annotation

squareMeasureAnnotation.Color = new PdfColor(Color.Red);

//Assign measurement unit to the square measurement annotation

squareMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter;

//Adds the square measurement annotation to a page

page.Annotations.Add(squareMeasureAnnotation);

//Saves the document to disk

document.Save("SquareMeasurementAnnotation.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

Dim rect As New RectangleF(10, 100, 100, 100)

'Creates the square measurement annotation

Dim squareMeasureAnnotation As New PdfSquareMeasurementAnnotation(rect)

'Assign author to the square measurement annotation

squareMeasureAnnotation.Author = "Syncfusion"

'Assign subject to the square measurement annotation

squareMeasureAnnotation.Subject = "Square measurement annotation"

'Assign color to the square measurement annotation

squareMeasureAnnotation.Color = New PdfColor(Color.Red)

'Assign measurement unit to the square measurement annotation

squareMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter

'Adds the square measurement annotation to a page

page.Annotations.Add(squareMeasureAnnotation)

'Saves the document to disk

document.Save("SquareMeasurementAnnotation.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

RectangleF rect = new RectangleF(10, 100, 100, 100);

//Creates the square measurement annotation

PdfSquareMeasurementAnnotation squareMeasureAnnotation = new PdfSquareMeasurementAnnotation(rect);

//Assign author to the square measurement annotation

squareMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the square measurement annotation

squareMeasureAnnotation.Subject = "Square measurement annotation";

//Assign color to the square measurement annotation

squareMeasureAnnotation.Color = new PdfColor(Color.FromArgb(255, 255, 0, 0));

//Assign measurement unit to the square measurement annotation

squareMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter;

//Adds the square measurement annotation to a page

page.Annotations.Add(squareMeasureAnnotation);

MemoryStream stream = new MemoryStream();

//Save the document into stream.

document.Save(stream);

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

Syncfusion.Drawing.RectangleF rect = new Syncfusion.Drawing.RectangleF(10, 100, 100, 100);

//Creates the square measurement annotation

PdfSquareMeasurementAnnotation squareMeasureAnnotation = new PdfSquareMeasurementAnnotation(rect);

//Assign author to the square measurement annotation

squareMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the square measurement annotation

squareMeasureAnnotation.Subject = "Square measurement annotation";

//Assign color to the square measurement annotation

squareMeasureAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);

//Assign measurement unit to the square measurement annotation

squareMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter;

//Adds the square measurement annotation to a page

page.Annotations.Add(squareMeasureAnnotation);

MemoryStream stream = new MemoryStream();

//Save the document into stream

document.Save(stream);

stream.Position=0;

//Close the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "SquareMeasurementAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

Syncfusion.Drawing.RectangleF rect = new Syncfusion.Drawing.RectangleF(10, 100, 100, 100);

//Creates the square measurement annotation

PdfSquareMeasurementAnnotation squareMeasureAnnotation = new PdfSquareMeasurementAnnotation(rect);

//Assign author to the square measurement annotation

squareMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the square measurement annotation

squareMeasureAnnotation.Subject = "Square measurement annotation";

//Assign color to the square measurement annotation

squareMeasureAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);

//Assign measurement unit to the square measurement annotation

squareMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter;

//Adds the square measurement annotation to a page

page.Annotations.Add(squareMeasureAnnotation);

MemoryStream stream = new MemoryStream();

//Saves the document to disk

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SquareMeasurementAnnotation.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("SquareMeasurementAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Circle measurement annotation

The circle measurement annotation is displayed as circle shape in the page. The radius or diameter distance of the circle is measured and the value is displayed in the pop-up window.

[PdfCircleMeasurementAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfCircleMeasurementAnnotation.html) is used to add a circle measurement annotation to the page.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

RectangleF rect = new RectangleF(10, 100, 100, 100);

//Creates the circle measurement annotation

PdfCircleMeasurementAnnotation circleMeasureAnnotation = new PdfCircleMeasurementAnnotation(rect);

//Assign author to the circle measurement annotation

circleMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the circle measurement annotation

circleMeasureAnnotation.Subject = "Circle measurement annotation";

//Assign color to the square measurement annotation

circleMeasureAnnotation.Color = new PdfColor(Color.Red);

//Assign measurement unit to the circle measurement annotation

circleMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter;

//Sets the measurementType to the circle measurement annotation

circleMeasureAnnotation.MeasurementType = PdfCircleMeasurementType.Diameter;

//Adds the circle measurement annotation to a page

page.Annotations.Add(circleMeasureAnnotation);

//Saves the document to disk

document.Save("CircleMeasurementAnnotation.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

Dim rect As New RectangleF(10, 100, 100, 100)

'Creates the circle measurement annotation

Dim circleMeasureAnnotation As New PdfCircleMeasurementAnnotation(rect)

'Assign author to the circle measurement annotation

circleMeasureAnnotation.Author = "Syncfusion"

'Assign subject to the circle measurement annotation

circleMeasureAnnotation.Subject = "Circle measurement annotation"

'Assign color to the square measurement annotation

circleMeasureAnnotation.Color = New PdfColor(Color.Red)

'Assign measurement unit to the circle measurement annotation

circleMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter

'Sets the measurementType to the circle measurement annotation

circleMeasureAnnotation.MeasurementType = PdfCircleMeasurementType.Diameter

'Adds the circle measurement annotation to a page

page.Annotations.Add(circleMeasureAnnotation)

'Saves the document to disk

document.Save("CircleMeasurementAnnotation.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

RectangleF rect = new RectangleF(10, 100, 100, 100);

//Creates the circle measurement annotation

PdfCircleMeasurementAnnotation circleMeasureAnnotation = new PdfCircleMeasurementAnnotation(rect);

//Assign author to the circle measurement annotation

circleMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the circle measurement annotation

circleMeasureAnnotation.Subject = "Circle measurement annotation";

//Assign color to the square measurement annotation

circleMeasureAnnotation.Color = new PdfColor(Color.FromArgb(255, 255, 0, 0));

//Assign measurement unit to the circle measurement annotation

circleMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter;

//Sets the measurementType to the circle measurement annotation

circleMeasureAnnotation.MeasurementType = PdfCircleMeasurementType.Diameter;

//Adds the circle measurement annotation to a page

page.Annotations.Add(circleMeasureAnnotation);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

Syncfusion.Drawing.RectangleF rect = new Syncfusion.Drawing.RectangleF(10, 100, 100, 100);

//Creates the circle measurement annotation

PdfCircleMeasurementAnnotation circleMeasureAnnotation = new PdfCircleMeasurementAnnotation(rect);

//Assign author to the circle measurement annotation

circleMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the circle measurement annotation

circleMeasureAnnotation.Subject = "Circle measurement annotation";

//Assign color to the square measurement annotation

circleMeasureAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);

//Assign measurement unit to the circle measurement annotation

circleMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter;

//Sets the measurementType to the circle measurement annotation

circleMeasureAnnotation.MeasurementType = PdfCircleMeasurementType.Diameter;

//Adds the circle measurement annotation to a page

page.Annotations.Add(circleMeasureAnnotation);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "CircleMeasurementAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

Syncfusion.Drawing.RectangleF rect = new Syncfusion.Drawing.RectangleF(10, 100, 100, 100);

//Creates the circle measurement annotation

PdfCircleMeasurementAnnotation circleMeasureAnnotation = new PdfCircleMeasurementAnnotation(rect);

//Assign author to the circle measurement annotation

circleMeasureAnnotation.Author = "Syncfusion";

//Assign subject to the circle measurement annotation

circleMeasureAnnotation.Subject = "Circle measurement annotation";

//Assign color to the square measurement annotation

circleMeasureAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);

//Assign measurement unit to the circle measurement annotation

circleMeasureAnnotation.Unit = PdfMeasurementUnit.Centimeter;

//Sets the measurementType to the circle measurement annotation

circleMeasureAnnotation.MeasurementType = PdfCircleMeasurementType.Diameter;

//Adds the circle measurement annotation to a page

page.Annotations.Add(circleMeasureAnnotation);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("CircleMeasurementAnnotation.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("CircleMeasurementAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Angle measurement annotation

The angle measurement annotation calculates the angle between three points and draws arc between three points. The angle of the annotation is displayed in the pop-up window.

[PdfAngleMeasurementAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAngleMeasurementAnnotation.html) helps you to add angle measurement annotation to the page.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

PointF[] points = new PointF[] { new PointF(100, 700), new PointF(150, 650), new PointF(100, 600) };

//Creates the angel measurement annotation

PdfAngleMeasurementAnnotation angleMeasureAnnotation = new PdfAngleMeasurementAnnotation(points);

//Set font to the angle measurement annotation

angleMeasureAnnotation.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f, PdfFontStyle.Regular);

//Assign color to the angle measurement annotation
angleMeasureAnnotation.Color = Color.Red;

//Adds angle measurement annotation

page.Annotations.Add(angleMeasureAnnotation);

//Saves the document to disk

document.Save("AngleMeasurementAnnotation.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

Dim points As PointF() = New PointF() {New PointF(100, 700), New PointF(150, 650), New PointF(100, 600)}

'Creates the angel measurement annotation

Dim angleMeasureAnnotation As New PdfAngleMeasurementAnnotation(points)

'Set font to the angle measurement annotation

angleMeasureAnnotation.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 12.0F, PdfFontStyle.Regular)

'Assign color to the angle measurement annotation
angleMeasureAnnotation.Color = Color.Red

'Adds angle measurement annotation

page.Annotations.Add(angleMeasureAnnotation)

'Saves the document to disk

document.Save("AngleMeasurementAnnotation.pdf")

document.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//PDF supports angle measurement annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Web.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//PDF supports angle measurement annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Web.

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//PDF supports angle measurement annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Web.

{% endhighlight %}

{% endtabs %}
## Modifying the annotations

Essential PDF allows you to modify the annotation of existing document. The following code illustrates this.

{% tabs %}
{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Gets the first page from the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Gets the first annotation and modify the properties

PdfLoadedPopupAnnotation popUp = annotations[0] as PdfLoadedPopupAnnotation;

popUp.Border = new PdfAnnotationBorder(4, 0, 0);

popUp.Color = new PdfColor(Color.FromArgb(0,255,0,0));

popUp.Text = "Modified annotation";

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await lDoc.SaveAsync(stream);

//Close the document

lDoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("inputAnnotation.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Gets the first page from the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Gets the first annotation and modify the properties

PdfLoadedPopupAnnotation popUp = annotations[0] as PdfLoadedPopupAnnotation;

popUp.Border = new PdfAnnotationBorder(4, 0, 0);

popUp.Color = new PdfColor(Color.Red);

popUp.Text = "Modified annotation";

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

stream.Position = 0;

//Closes the document

lDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.inputAnnotation.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Gets the first page from the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Gets the first annotation and modify the properties

PdfLoadedPopupAnnotation popUp = annotations[0] as PdfLoadedPopupAnnotation;

popUp.Border = new PdfAnnotationBorder(4, 0, 0);

popUp.Color = new PdfColor(Syncfusion.Drawing.Color.Red);

popUp.Text = "Modified annotation";

//Save the document into stream.

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

//Close the document.

lDoc.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Modifying the redaction annotations   

The redaction annotations from the existing document can be modified using the Essential PDF library. You can add, remove, or modify the redaction annotation in the existing PDF documents. 
The following code sample explains this.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Load the existing PDF document

PdfLoadedDocument ldoc = new PdfLoadedDocument("input.pdf");

//Get the pages

foreach (PdfAnnotation annot in ldoc.Pages[0].Annotations)

{

//Check for the Redaction annotation

if (annot is PdfLoadedRedactionAnnotation)
{

PdfLoadedRedactionAnnotation redactAnnot = annot as PdfLoadedRedactionAnnotation;

//Assign the Bounds values

redactAnnot.Bounds = new RectangleF(50, 50, 100, 100);

//Assign the OverlayText

redactAnnot.OverlayText = "Redaction";

//Assign the InnerColor

redactAnnot.InnerColor = Color.Yellow;

//Assign the BorderColor

redactAnnot.BorderColor = Color.Green;

//Assign the TextColor

redactAnnot.TextColor = Color.Red;
 
//Assign the TextAlignment

redactAnnot.TextAlignment = PdfTextAlignment.Right;

//Assign the RepeatText

redactAnnot.RepeatText = true;

//Flatten the annotations in the page

redactAnnot.Flatten = true;
    
}

}

//save the document

ldoc.Save("output.pdf");

//Close the document

ldoc.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the existing PDF document

Dim ldoc As PdfLoadedDocument = New PdfLoadedDocument("output.pdf")
		
'Get the pages
		
For Each annot As PdfAnnotation In ldoc.Pages(0).Annotations
		
'Check for the Redaction annotation
			
If TypeOf annot Is PdfLoadedRedactionAnnotation Then
			
Dim redactAnnot As PdfLoadedRedactionAnnotation = TryCast(annot, PdfLoadedRedactionAnnotation)
				
'Assign the Bounds values
				
redactAnnot.Bounds = New RectangleF(50, 50, 100, 100)
				
'Assign the OverlayText
				
redactAnnot.OverlayText = "Redaction"
				
'Assign the InnerColor
				
redactAnnot.InnerColor = Color.Yellow
				
'Assign the BorderColor 
				
redactAnnot.BorderColor = Color.Green
				
'Assign the TextColor
				
redactAnnot.TextColor = Color.Red
				
'Assign the TextAlignment
				
redactAnnot.TextAlignment = PdfTextAlignment.Right
				
'Assign the RepeatText
				
redactAnnot.RepeatText = True
				
'Flatten the annotations in the page
				
redactAnnot.Flatten = True
				
End If
			
Next
		
'save the document
		
ldoc.Save("output.pdf")
		
'Close the document
		
ldoc.Close()
		
{% endhighlight %}		
  {% highlight c# tabtitle="UWP" %}

//Create the file open picker 

var picker = new FileOpenPicker(); 

picker.FileTypeFilter.Add(".pdf");
 
//Browse and choose the file 

StorageFile file = await picker.PickSingleFileAsync();
 
//Create an empty PDF loaded document instance 

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Load or open an existing PDF document through Open method of PdfLoadedDocument class 

await loadedDocument.OpenAsync(file);

foreach (PdfAnnotation annot in loadedDocument.Pages[0].Annotations)

{

//Check for the Redaction annotation

if (annot is PdfLoadedRedactionAnnotation)
{

PdfLoadedRedactionAnnotation redactAnnot = annot as PdfLoadedRedactionAnnotation;

//Assign the Bounds values

redactAnnot.Bounds = new RectangleF(50, 50, 100, 100);

//Assign the OverlayText

redactAnnot.OverlayText = "Redaction";

//Assign the InnerColor

redactAnnot.InnerColor = Color.Yellow;

//Assign the BorderColor

redactAnnot.BorderColor = Color.Green;

//Assign the TextColor

redactAnnot.TextColor = Color.Red;
 
//Assign the TextAlignment

redactAnnot.TextAlignment = PdfTextAlignment.Right;

//Assign the RepeatText

redactAnnot.RepeatText = true;

//Flatten the annotations in the page

redactAnnot.Flatten = true;

}
}
//Save the PDF document to stream 

MemoryStream stream = new MemoryStream(); 

loadedDocument.Save(stream); 

//Close the document loadedDocument.Close(true); 

//Save the stream as PDF document file in the local machine. Refer to PDF or UWP section for respective code samples 
Save(stream, "output.pdf");

{% endhighlight %}
{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document 

FileStream docStream = new FileStream("input.pdf", FileMode.Open,FileAccess.Read);
 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

foreach (PdfAnnotation annot in loadedDocument.Pages[0].Annotations)

{
//Check for the Redaction annotation

if (annot is PdfLoadedRedactionAnnotation)

{

PdfLoadedRedactionAnnotation redactAnnot = annot as PdfLoadedRedactionAnnotation;

//Assign the Bounds values

redactAnnot.Bounds = new RectangleF(50, 50, 100, 100);

//Assign the OverlayText

redactAnnot.OverlayText = "Redaction";

//Assign the InnerColor

redactAnnot.InnerColor = Color.Yellow;

//Assign the BorderColor

redactAnnot.BorderColor = Color.Green;

//Assign the TextColor

redactAnnot.TextColor = Color.Red; 

//Assign the TextAlignment

redactAnnot.TextAlignment = PdfTextAlignment.Right;

//Assign the RepeatText

redactAnnot.RepeatText = true;

//Flatten the annotations in the page

redactAnnot.Flatten = true;

}
}
//Save the document into stream 

MemoryStream stream = new MemoryStream(); 

loadedDocument.Save(stream); 

stream.Position = 0; 

//Close the document 

loadedDocument.Close(true);
 
//Defining the ContentType for pdf file 

string contentType = "application/pdf"; 

//Define the file name 

string fileName = "output.pdf";
 
//Create a FileContentResult object by using the file contents, content type, and file name 

return File(stream, contentType, fileName);

{% endhighlight %}
{% highlight c# tabtitle="Xamarin" %}

//Load the file as a stream 

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf"); 

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

foreach (PdfAnnotation annot in ldoadedDocument.Pages[0].Annotations)

{
//Check for the Redaction annotation

if (annot is PdfLoadedRedactionAnnotation)
{

PdfLoadedRedactionAnnotation redactAnnot = annot as PdfLoadedRedactionAnnotation;

//Assign the Bounds values

redactAnnot.Bounds = new RectangleF(50, 50, 100, 100);

//Assign the OverlayText

redactAnnot.OverlayText = "Redaction";

//Assign the InnerColor

redactAnnot.InnerColor = Color.Yellow;

//Assign the BorderColor

redactAnnot.BorderColor = Color.Green;

//Assign the TextColor

redactAnnot.TextColor = Color.Red; 

//Assign the TextAlignment

redactAnnot.TextAlignment = PdfTextAlignment.Right;

//Assign the RepeatText

redactAnnot.RepeatText = true;

//Flatten the annotations in the page

redactAnnot.Flatten = true;

}
}
//Save the document into a stream.
 
MemoryStream stream = new MemoryStream(); 

loadedDocument.Save(stream); 

//Close the document. 

loadedDocument.Close(true); 

//Save the stream into pdf file

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("rectangleAnnotation.pdf", "application/pdf", stream);

{% endhighlight %}

{% endtabs %}


## Removing annotations from an existing PDF 

You can remove the annotation from the annotation collection, represented by the [PdfLoadedAnnotationCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedAnnotationCollection.html) of the loaded page. The following code illustrates this.

{% tabs %}
{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}

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

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Gets the first page of the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Removes the first annotation

annotations.RemoveAt(0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await lDoc.SaveAsync(stream);

//Close the document

lDoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("inputAnnotation.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Gets the first page of the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Removes the first annotation

annotations.RemoveAt(0);

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

stream.Position = 0;

//Closes the document

lDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.inputAnnotation.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Gets the first page of the document

PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Gets the annotation collection

PdfLoadedAnnotationCollection annotations = page.Annotations;

//Removes the first annotation

annotations.RemoveAt(0);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

//Close the document.

lDoc.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Importing annotations from FDF file

FDF stands for Forms Data Format. FDF is a file format for representing annotations present in a PDF document. You can import annotation data from the FDF file to PDF using the [ImportAnnotations](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_ImportAnnotations_System_IO_Stream_Syncfusion_Pdf_Parsing_AnnotationDataFormat_) method in [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}


//Loads the document

PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf");

//Import annotation data from FDF file

lDoc.ImportAnnotations("Annotations.fdf", AnnotationDataFormat.Fdf);

//Saves the document

lDoc.Save("Annotation.pdf");

lDoc.Close(true);



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads the document

Dim lDoc As New PdfLoadedDocument("input.pdf")

'Import annotation data from FDF file

lDoc.ImportAnnotations("Annotations.fdf", AnnotationDataFormat.Fdf)

'Saves the document

lDoc.Save("Annotation.pdf")

lDoc.Close(True)



{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through the Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Load the FDF file stream from the disk

Stream fdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Annotations.fdf");

'Import annotation data from FDF stream

lDoc.ImportAnnotations(fdfStream, AnnotationDataFormat.Fdf)

MemoryStream stream = new MemoryStream();

await lDoc.SaveAsync(stream);

//Close the document

lDoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Annotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Import annotation data from FDF stream

FileStream fdfStream = new FileStream("Annotations.fdf", FileMode.Open, FileAccess.Read);

lDoc.ImportAnnotations(fdfStream, AnnotationDataFormat.Fdf)

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

stream.Position = 0;

//Closes the document

lDoc.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Annotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Import annotation data from FDF stream

Stream fdfStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Annotations.fdf");

lDoc.ImportAnnotations(fdfStream, AnnotationDataFormat.Fdf)

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

//Close the document

lDoc.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Annotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Annotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Importing annotations from XFDF file

XFDF stands for XML Forms Data Format. XFDF is the XML version of FDF for representing annotations that are contained in a PDF document. You can import annotation data from the XFDF file to PDF using the [ImportAnnotations](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_ImportAnnotations_System_IO_Stream_Syncfusion_Pdf_Parsing_AnnotationDataFormat_) method in [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}


//Loads the document

PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf");

//Import annotation data from XFDF file

lDoc.ImportAnnotations("Annotations.xfdf", AnnotationDataFormat.XFdf);

//Saves the document

lDoc.Save("Annotation.pdf");

lDoc.Close(true);



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads the document

Dim lDoc As New PdfLoadedDocument("input.pdf")

'Import annotation data from XFDF file

lDoc.ImportAnnotations("Annotations.xfdf", AnnotationDataFormat.XFdf)

'Saves the document

lDoc.Save("Annotation.pdf")

lDoc.Close(True)



{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through the Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Load the XFDF file stream from the disk

Stream xfdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Annotations.xfdf");

'Import annotation data from XFDF stream

lDoc.ImportAnnotations(xfdfStream, AnnotationDataFormat.XFdf);

MemoryStream stream = new MemoryStream();

await lDoc.SaveAsync(stream);

//Close the document

lDoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Annotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Import annotation data from XFDF stream

FileStream xfdfStream = new FileStream("Annotations.xfdf", FileMode.Open, FileAccess.Read);

lDoc.ImportAnnotations(xfdfStream, AnnotationDataFormat.XFdf);

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

stream.Position = 0;

//Closes the document

lDoc.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Annotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Import annotation data from XFDF stream

Stream xfdfStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Annotations.xfdf");

lDoc.ImportAnnotations(xfdfStream, AnnotationDataFormat.XFdf);

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

//Close the document

lDoc.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Annotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Annotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Importing annotations from JSON file

JSON stands for JavaScript Object Notation. It is a collection of key or value pairs and it is used for serializing and transmitting the structured data over a network connection. You can import the annotation data from the JSON file to PDF using the [ImportAnnotations](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_ImportAnnotations_System_IO_Stream_Syncfusion_Pdf_Parsing_AnnotationDataFormat_) method in [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Loads the document 

PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf"); 

//Import the annotation data from the JSON file 

lDoc.ImportAnnotations("Annotations.Json", AnnotationDataFormat.Json); 

//Saves the document 

lDoc.Save("Annotation.pdf"); 

lDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads the document 

Dim lDoc As New PdfLoadedDocument("input.pdf") 

'Import the annotation data from the JSON file 

lDoc.ImportAnnotations("Annotations.Json", AnnotationDataFormat.Json) 

'Saves the document 

lDoc.Save("Annotation.pdf") 

'close the document 

lDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker 

var picker = new FileOpenPicker(); 

picker.FileTypeFilter.Add(".pdf"); 

//Browse and choose the file 

StorageFile file = await picker.PickSingleFileAsync(); 

//Creates an empty PDF loaded document instance 

PdfLoadedDocument lDoc = new PdfLoadedDocument(); 

//Loads or opens an existing PDF document through the Open method of PdfLoadedDocument class 

await lDoc.OpenAsync(file); 

//Load the JSON file stream from the disk 

Stream jsonStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Annotations.Json"); 

//Import annotation data from json stream 

lDoc.ImportAnnotations(jsonStream, AnnotationDataFormat.Json) 

MemoryStream stream = new MemoryStream(); 

await lDoc.SaveAsync(stream); 

//Close the document 

lDoc.Close(true); 

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for the respective code samples 

Save(stream, "Annotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document 

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read); 

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream); 

//Import the annotation data from the JSON stream 

FileStream jsonStream = new FileStream("Annotations.Json", FileMode.Open, FileAccess.Read); 

lDoc.ImportAnnotations(jsonStream, AnnotationDataFormat.Json); 

//Save the document into the stream 

MemoryStream stream = new MemoryStream(); 

lDoc.Save(stream); 

stream.Position = 0; 

//Closes the document 

lDoc.Close(true); 

//Defining the ContentType for PDF file 

string contentType = "application/pdf"; 

//Define the file name 

string fileName = "Annotation.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name 

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as a stream 

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf"); 

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream); 

//Import the annotation data from the JSON stream 

Stream jsonStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Annotations.Json"); 

lDoc.ImportAnnotations(jsonStream, AnnotationDataFormat.Json); 

//Save the document into the stream 

MemoryStream stream = new MemoryStream(); 

lDoc.Save(stream); 

//Close the document 

lDoc.Close(true); 

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ImportAnnotation.pdf", "application/pdf", stream);

{% endhighlight %}

{% endtabs %}

## Exporting annotations to FDF file

To export annotation data to the FDF file from PDF document, you can use the [ExportAnnotations](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_ExportAnnotations_System_IO_Stream_Syncfusion_Pdf_Parsing_AnnotationDataFormat_) method in [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}


//Loads the document

PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf");

//Export annotation data to FDF file

lDoc.ExportAnnotations("Annotations.fdf", AnnotationDataFormat.Fdf);

//Close the document

lDoc.Close(true);



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads the document

Dim lDoc As New PdfLoadedDocument("input.pdf")

'Export annotation data to FDF file

lDoc.ExportAnnotations("Annotations.fdf", AnnotationDataFormat.Fdf)

'Close the document

lDoc.Close(True)



{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through the Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Load the FDF file stream from the disk

Stream fdfStream = new MemoryStream();

//Export annotation data from FDF stream

lDoc.ExportAnnotations(fdfStream, AnnotationDataFormat.Fdf)

//Save the fdfStream as FDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(fdfStream, "Annotations.fdf");

//Close the document

lDoc.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Export annotation data from FDF stream

Stream fdfStream = new MemoryStream();

lDoc.ExportAnnotations(fdfStream, AnnotationDataFormat.Fdf)

//Close the document

lDoc.Close(true);

fdfStream.Position = 0;

//Defining the ContentType for FDF file

string contentType = "application/fdf";

//Define the file name

string fileName = "Annotations.fdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(fdfStream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Export annotation data from FDF stream

Stream fdfStream = new MemoryStream();

lDoc.ExportAnnotations(fdfStream, AnnotationDataFormat.Fdf)

//Close the document

lDoc.Close(true);

//Save the stream into FDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Annotations.fdf", "application/fdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Annotations.fdf", "application/fdf", fdfStream);
}

{% endhighlight %}

{% endtabs %}

## Exporting annotations to XFDF file

To export annotation data to the XFDF file from PDF document, you can use the [ExportAnnotations](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_ExportAnnotations_System_IO_Stream_Syncfusion_Pdf_Parsing_AnnotationDataFormat_) method in [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}


//Loads the document

PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf");

//Export annotation data to XFDF file

lDoc.ExportAnnotations("Annotations.xfdf", AnnotationDataFormat.XFdf);

//Close the document

lDoc.Close(true);



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads the document

Dim lDoc As New PdfLoadedDocument("input.pdf")

'Export annotation data to XFDF file

lDoc.ExportAnnotations("Annotations.xfdf", AnnotationDataFormat.XFdf)

'Close the document

lDoc.Close(True)



{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through the Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Load the XFDF file stream from the disk

Stream xfdfStream = new MemoryStream();

//Export annotation data from XFDF stream

lDoc.ExportAnnotations(xfdfStream, AnnotationDataFormat.XFdf);

//Save the xfdfStream as XFDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(xfdfStream, "Annotations.xfdf");

//Close the document

lDoc.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Export annotation data from XFDF stream

Stream xfdfStream = new MemoryStream();

lDoc.ExportAnnotations(xfdfStream, AnnotationDataFormat.XFdf);

//Close the document

lDoc.Close(true);

xfdfStream.Position = 0;

//Defining the ContentType for XFDF file

string contentType = "application/xfdf";

//Define the file name

string fileName = "Annotations.xfdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(xfdfStream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Export annotation data from XFDF stream

Stream xfdfStream = new MemoryStream();

lDoc.ExportAnnotations(xfdfStream, AnnotationDataFormat.XFdf);

//Close the document

lDoc.Close(true);

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Annotations.xfdf", "application/xfdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Annotations.xfdf", "application/xfdf", fdfStream);
}

{% endhighlight %}

{% endtabs %}

## Exporting annotations to JSON file

To export annotation data to the JSON file from PDF document, you can use the [ExportAnnotations](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_ExportAnnotations_System_IO_Stream_Syncfusion_Pdf_Parsing_AnnotationDataFormat_) method in [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Loads the document 

PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf"); 

//Export the annotation data to the JSON file 

lDoc.ExportAnnotations("Annotations.Json", AnnotationDataFormat.Json); 

//Close the document 

lDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads the document 

Dim lDoc As New PdfLoadedDocument("input.pdf") 

'Export the annotation data to the JSON file 

lDoc.ExportAnnotations("Annotations.Json", AnnotationDataFormat.Json) 

'Close the document 

lDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker 

var picker = new FileOpenPicker(); 

picker.FileTypeFilter.Add(".pdf"); 

//Browse and choose the file 

StorageFile file = await picker.PickSingleFileAsync(); 

//Creates an empty PDF loaded document instance 

PdfLoadedDocument lDoc = new PdfLoadedDocument(); 

//Loads or opens an existing PDF document through the Open method of PdfLoadedDocument class 

await lDoc.OpenAsync(file); 

//Load the JSON file stream from the disk 

Stream jsonStream = new MemoryStream(); 

//Export the annotation data from the JSON stream 

lDoc.ExportAnnotations(jsonStream, AnnotationDataFormat.Json) 

//Save the jsonStream as a JSON document file in the local machine. Refer to the PDF/UWP section for the respective code samples 

Save(jsonStream, "Annotations.Json"); 

//Close the document 

lDoc.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document 

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read); 

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream); 

//Export the annotation data from the JSON stream 

Stream jsonStream = new MemoryStream(); 

lDoc.ExportAnnotations(jsonStream, AnnotationDataFormat.Json) 

//Close the document 

lDoc.Close(true); 

jsonStream.Position = 0; 

//Defining the ContentType for Json file 

string contentType = "application/Json"; 

//Define the file name 

string fileName = "Annotations.Json"; 

//Creates a FileContentResult object by using the file contents, content type, and file name 

return File(jsonStream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as a stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Export the annotation data from the JSON stream

Stream jsonStream = new MemoryStream();

lDoc.ExportAnnotations(jsonStream, AnnotationDataFormat.Json);

//Save the document into the stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

//Close the document

lDoc.Close(true);

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ExportAnnotation.pdf", "application/pdf", stream);

{% endhighlight %}

{% endtabs %}

## Adding comments and review status to the PDF annotation

The PDF annotations may have an author-specific state associated with them. The state is not specified in the annotation itself, but it represents a separate text annotation ([Popup Annotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.Interactive.PdfPopupAnnotation.html)).

The Essential PDF supports adding the annotation comments and review status to the PDF document annotations.

### Adding comments to the PDF annotation

The following code example explains how to add comments to the PDF annotation.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create new rectangle annotation

PdfRectangleAnnotation rectangleAnnotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 100, 50), "Rectangle Annotation");

//Set author

rectangleAnnotation.Author = "Syncfusion";

rectangleAnnotation.Border.BorderWidth = 1;

rectangleAnnotation.Color = Color.Red;

rectangleAnnotation.ModifiedDate = DateTime.Now;

//Create a new comment annotation

PdfPopupAnnotation comment = new PdfPopupAnnotation();

//Set author

comment.Author = "John";

//Set comment text

comment.Text = "This is first comment";

//Set modification date

comment.ModifiedDate = DateTime.Now;

//Set subject

comment.Subject = "Annotation Comments";

//Add the comments to the annotation

rectangleAnnotation.Comments.Add(comment);

//Add the annotation to the PDF page

page.Annotations.Add(rectangleAnnotation);

//Save the document to disk

document.Save("Output.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document

Dim document As PdfDocument = New PdfDocument

'Create a new page

Dim page As PdfPage = document.Pages.Add

'Create new rectangle annotation

Dim rectangleAnnotation As PdfRectangleAnnotation = New PdfRectangleAnnotation(New RectangleF(0, 0, 100, 50), "Rectangle Annotation")

'Set author

rectangleAnnotation.Author = "Syncfusion"

rectangleAnnotation.Border.BorderWidth = 1

rectangleAnnotation.Color = Color.Red

rectangleAnnotation.ModifiedDate = DateTime.Now

Dim comment As PdfPopupAnnotation = New PdfPopupAnnotation

'Set author

comment.Author = "John"

'Set Text

comment.Text = "This is first comment"

'Set modification date.

comment.ModifiedDate = DateTime.Now

'Set subject

comment.Subject = "Annotation Comments"

'Add the  comment to the annotation.

rectangleAnnotation.Comments.Add(comment)

'Add the annotation to the PDF page.

page.Annotations.Add(rectangleAnnotation)

'Save the document to disk.

document.Save("Output.pdf")

'Close the document

document.Close(true)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create new rectangle annotation

PdfRectangleAnnotation rectangleAnnotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 100, 50), "Rectangle Annotation");

//Set author

rectangleAnnotation.Author = "Syncfusion";

rectangleAnnotation.Border.BorderWidth = 1;

rectangleAnnotation.Color = Color.Red;

rectangleAnnotation.ModifiedDate = DateTime.Now;

//Create a new comment annotation

PdfPopupAnnotation comment = new PdfPopupAnnotation();

//Set author

comment.Author = "John";

//Set Text

comment.Text = "This is first comment";

//Set modification date

comment.ModifiedDate = DateTime.Now;

//Set subject

comment.Subject = "Annotation Comments";

//Add the comment to the annotation

rectangleAnnotation.Comments.Add(comment);

//Add the annotation to the PDF page

page.Annotations.Add(rectangleAnnotation);

//Saves the document

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create new rectangle annotation

PdfRectangleAnnotation rectangleAnnotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 100, 50), "Rectangle Annotation");

//Set author

rectangleAnnotation.Author = "Syncfusion";

rectangleAnnotation.Border.BorderWidth = 1;

rectangleAnnotation.Color = Color.Red;

rectangleAnnotation.ModifiedDate = DateTime.Now;

//Create a new comment annotation

PdfPopupAnnotation comment = new PdfPopupAnnotation();

//Set author

comment.Author = "John";

//Set Text

comment.Text = "This is first comment";

//Set modification date

comment.ModifiedDate = DateTime.Now;

//Set subject

comment.Subject = "Annotation Comments";

//Add the comment to the annotation

rectangleAnnotation.Comments.Add(comment);

//Add the annotation to the PDF page

page.Annotations.Add(rectangleAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create new rectangle annotation

PdfRectangleAnnotation rectangleAnnotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 100, 50), "Rectangle Annotation");

//Set author

rectangleAnnotation.Author = "Syncfusion";

rectangleAnnotation.Border.BorderWidth = 1;

rectangleAnnotation.Color = Color.Red;

rectangleAnnotation.ModifiedDate = DateTime.Now;

//Create a new comments annotation

PdfPopupAnnotation comment = new PdfPopupAnnotation();

//Set author

comment.Author = "John";

//Set Text

comment.Text = "This is first comment";

//Set modification date

comment.ModifiedDate = DateTime.Now;

//Set subject

comment.Subject = "Annotation Comments";

//Add the comment to the annotation

rectangleAnnotation.Comments.Add(comment);

//Add the annotation to the PDF page

page.Annotations.Add(rectangleAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}



The following code example explains how to add comments to the existing PDF annotation.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document

PdfLoadedDocument ldoc = new PdfLoadedDocument("Input.pdf");

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing PDF annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Create a new comment annotation

PdfPopupAnnotation comment = new PdfPopupAnnotation();

//Set author

comment.Author = "John";

//Set Text

comment.Text = "This is first comment";

//Set modification date

comment.ModifiedDate = DateTime.Now;

//Set subject

comment.Subject = "Annotation Comments";

//Add the comment to the annotation

loadedRectangleAnnotation.Comments.Add(comment);

//Save the document

ldoc.Save("Output.pdf");

//Close the document

ldoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the PDF document

Dim ldoc As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the existing PDF page

Dim lpage As PdfLoadedPage = CType(ldoc.Pages(0),PdfLoadedPage)

'Get the existing annotations

Dim annots As PdfLoadedAnnotationCollection = lpage.Annotations

'Get the existing rectangle annotation

Dim loadedRectangleAnnotation As PdfLoadedRectangleAnnotation = CType(annots(0),PdfLoadedRectangleAnnotation)

'Get the existing rectangle annotation

Dim comment As PdfPopupAnnotation = New PdfPopupAnnotation

'Set author

comment.Author = "John"

'Set Text

comment.Text = "This is first comment"

'Set modification date

comment.ModifiedDate = DateTime.Now

'Set subject

comment.Subject = "Annotation Comments"

'Add the comment to the annotation.

loadedRectangleAnnotation.Comments.Add(comment)

'Save the document

ldoc.Save("Output.pdf")

'Close the document

ldoc.Close(true)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}


//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Get the existing PDF page

PdfLoadedPage lpage = lDoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Create a new comment annotation

PdfPopupAnnotation comment = new PdfPopupAnnotation();

//Set author

comment.Author = "John";

//Set Text

comment.Text = "This is first comment";

//Set modification date

comment.ModifiedDate = DateTime.Now;

//Set subject

comment.Subject = "Annotation Comments";

//Add the comments to the annotation

loadedRectangleAnnotation.Comments.Add(comment);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await lDoc.SaveAsync(stream);

//Close the document

lDoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("inputAnnotation.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = lDoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Create a new comment annotation

PdfPopupAnnotation comment = new PdfPopupAnnotation();

//Set author

comment.Author = "John";

//Set Text

comment.Text = "This is first comment";

//Set modification date

comment.ModifiedDate = DateTime.Now;

//Set subject

comment.Subject = "Annotation Comments";

//Add the comments to the annotation

loadedRectangleAnnotation.Comments.Add(comment);

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

stream.Position = 0;

//Closes the document

lDoc.Close(true);

//Defining the Content Type for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);


{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.inputAnnotation.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = lDoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Create a new comment annotation

PdfPopupAnnotation comment = new PdfPopupAnnotation();

//Set author

comment.Author = "John";

//Set Text

comment.Text = "This is first comment";

//Set modification date

comment.ModifiedDate = DateTime.Now;

//Set subject

comment.Subject = "Annotation Comments";

//Add the comment to the annotation

loadedRectangleAnnotation.Comments.Add(comment);

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

//Close the document

lDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Adding review status to the PDF annotation

The following code example explains how to add a review status in a newly created PDF annotation.

{% tabs %}

{% highlight c# tabtitle="C#" %}


//Create a new PDF document

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create new rectangle annotation

PdfRectangleAnnotation rectangleAnnotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 100, 50), "Rectangle Annotation");

//Set author

rectangleAnnotation.Author = "Syncfusion";

rectangleAnnotation.Border.BorderWidth = 1;

rectangleAnnotation.Color = Color.Red;

rectangleAnnotation.ModifiedDate = DateTime.Now;

//Create a new review annotation

PdfPopupAnnotation review = new PdfPopupAnnotation();

//Set author

review.Author = "John";

//Set review state model

review.StateModel = PdfAnnotationStateModel.Review;

//Set review state

review.State = PdfAnnotationState.Accepted;

//Set modification date

review.ModifiedDate = DateTime.Now;

//Add the review to the annotation

rectangleAnnotation.ReviewHistory.Add(review);

//Add the annotation to the PDF page

page.Annotations.Add(rectangleAnnotation);

//Save the document to disk

document.Save("Output.pdf");

//Close the document

document.Close(true);


{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document

Dim document As PdfDocument = New PdfDocument

'Create a new page

Dim page As PdfPage = document.Pages.Add

'Create new rectangle annotation

Dim rectangleAnnotation As PdfRectangleAnnotation = New PdfRectangleAnnotation(New RectangleF(0, 0, 100, 50), "Rectangle Annotation")

'Set author

rectangleAnnotation.Author = "Syncfusion"

rectangleAnnotation.Border.BorderWidth = 1

rectangleAnnotation.Color = Color.Red

rectangleAnnotation.ModifiedDate = DateTime.Now

Dim review As PdfPopupAnnotation = New PdfPopupAnnotation

'Set author

review.Author = "John"

'Set review state model

review.StateModel = PdfAnnotationStateModel.Review

'Set review state

review.State = PdfAnnotationState.Accepted

'Set modification date.

review.ModifiedDate = DateTime.Now

'Add the review to the annotation.

rectangleAnnotation.ReviewHistory.Add(review)

'Add the annotation to the PDF page.

page.Annotations.Add(rectangleAnnotation)

'Save the document to disk.

document.Save("Output.pdf")

'Close the document

document.Close(true)


{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create a new PDF document 

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create new rectangle annotation

PdfRectangleAnnotation rectangleAnnotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 100, 50), "Rectangle Annotation");

//Set author

rectangleAnnotation.Author = "Syncfusion";

rectangleAnnotation.Border.BorderWidth = 1;

rectangleAnnotation.Color = Color.Red;

rectangleAnnotation.ModifiedDate = DateTime.Now;

//Create a new review annotation

PdfPopupAnnotation review = new PdfPopupAnnotation();

//Set author

review.Author = "John";

//Set review state model

review.StateModel = PdfAnnotationStateModel.Review;

//Set review state

review.State = PdfAnnotationState.Accepted;

//Set modification date

review.ModifiedDate = DateTime.Now;

//Add the review to the annotation

rectangleAnnotation.ReviewHistory.Add(review);

//Add the annotation to the PDF page

page.Annotations.Add(rectangleAnnotation);

//Save the document

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples 

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create new rectangle annotation

PdfRectangleAnnotation rectangleAnnotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 100, 50), "Rectangle Annotation");

//Set author

rectangleAnnotation.Author = "Syncfusion";

rectangleAnnotation.Border.BorderWidth = 1;

rectangleAnnotation.Color = Color.Red;

rectangleAnnotation.ModifiedDate = DateTime.Now;

//Create a new review annotation

PdfPopupAnnotation review = new PdfPopupAnnotation();

//Set author

review.Author = "John";

//Set review state model

review.StateModel = PdfAnnotationStateModel.Review;

//Set review state

review.State = PdfAnnotationState.Accepted;

//Set modification date

review.ModifiedDate = DateTime.Now;

//Add the review to the annotation

rectangleAnnotation.ReviewHistory.Add(review);

//Add the annotation to the PDF page

page.Annotations.Add(rectangleAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the Content Type for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "PopupAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create new rectangle annotation

PdfRectangleAnnotation rectangleAnnotation = new PdfRectangleAnnotation(new RectangleF(0, 0, 100, 50), "Rectangle Annotation");

//Set author

rectangleAnnotation.Author = "Syncfusion";

rectangleAnnotation.Border.BorderWidth = 1;

rectangleAnnotation.Color = Color.Red;

rectangleAnnotation.ModifiedDate = DateTime.Now;

//Create a new review annotation

PdfPopupAnnotation review = new PdfPopupAnnotation();

//Set author

review.Author = "John";

//Set review state model

review.StateModel = PdfAnnotationStateModel.Review;

//Set review state

review.State = PdfAnnotationState.Accepted;

//Set modification date

review.ModifiedDate = DateTime.Now;

//Add the review to the annotation

rectangleAnnotation.ReviewHistory.Add(review);

//Add the annotation to the PDF page

page.Annotations.Add(rectangleAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}


The following code example explains how to add the review status to the existing PDF annotation. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document

PdfLoadedDocument ldoc = new PdfLoadedDocument("Input.pdf");

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Create a new review annotation

PdfPopupAnnotation review = new PdfPopupAnnotation();

//Set author

review.Author = "John";

//Set review state model

review.StateModel = PdfAnnotationStateModel.Review;

//Set review state

review.State = PdfAnnotationState.Accepted;

//Set modification date

review.ModifiedDate = DateTime.Now;

//Add the review to the annotation

loadedRectangleAnnotation.ReviewHistory.Add(review);

//Save the document

ldoc.Save("Output.pdf");

//Close the document

ldoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the existing PDF document

Dim ldoc As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the existing PDF page

Dim lpage As PdfLoadedPage = CType(ldoc.Pages(0),PdfLoadedPage)

'Get the existing annotations

Dim annots As PdfLoadedAnnotationCollection = lpage.Annotations

'Get the existing rectangle annotation

Dim loadedRectangleAnnotation As PdfLoadedRectangleAnnotation = CType(annots(0),PdfLoadedRectangleAnnotation)

'Get the existing rectangle annotation

Dim review As PdfPopupAnnotation = New PdfPopupAnnotation

'Set author

review.Author = "John"

'Set review state model

review.StateModel = PdfAnnotationStateModel.Review

'Set review state

review.State = PdfAnnotationState.Accepted

'Set modification date

review.ModifiedDate = DateTime.Now

'Add the review to the annotation.

loadedRectangleAnnotation.ReviewHistory.Add(review)

'Save the document

ldoc.Save("Output.pdf")

'Close the document

ldoc.Close(true)


{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}


//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Get the existing PDF page

PdfLoadedPage lpage = lDoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Create a new review annotation

PdfPopupAnnotation review = new PdfPopupAnnotation();

//Set author

review.Author = "John";

//Set review state model

review.StateModel = PdfAnnotationStateModel.Review;

//Set review state

review.State = PdfAnnotationState.Accepted;

//Set modification date

review.ModifiedDate = DateTime.Now;

//Add the review to the annotation

loadedRectangleAnnotation.ReviewHistory.Add(review);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await lDoc.SaveAsync(stream);

//Close the document

lDoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("inputAnnotation.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = lDoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Create a new review annotation

PdfPopupAnnotation review = new PdfPopupAnnotation();

//Set author

review.Author = "John";

//Set review state model

review.StateModel = PdfAnnotationStateModel.Review;

//Set review state

review.State = PdfAnnotationState.Accepted;

//Set modification date

review.ModifiedDate = DateTime.Now;

//Add the review to the annotation

loadedRectangleAnnotation.ReviewHistory.Add(review);

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

stream.Position = 0;

//Closes the document

lDoc.Close(true);

//Defining the Content Type for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.inputAnnotation.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = lDoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Create a new review annotation

PdfPopupAnnotation review = new PdfPopupAnnotation();

//Set author

review.Author = "John";

//Set review state model

review.StateModel = PdfAnnotationStateModel.Review;

//Set review state

review.State = PdfAnnotationState.Accepted;

//Set modification date

review.ModifiedDate = DateTime.Now;

//Add the review to the annotation

loadedRectangleAnnotation.ReviewHistory.Add(review);

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

//Close the document

lDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}



## Removing comments and review status from PDF annotation

The Essential PDF supports removing comments and reviewing status from the PDF annotation.

The following code example explains how to remove comments from the existing PDF annotation.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document

PdfLoadedDocument ldoc = new PdfLoadedDocument("Input.pdf");

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation comments collection

PdfLoadedPopupAnnotationCollection commentsCollection = loadedRectangleAnnotation.Comments;

// Remove comments by index 

commentsCollection.RemoveAt(0);

//Save the document

ldoc.Save("Output.pdf");

//Close the document

ldoc.Close(true);


{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the PDF document

Dim ldoc As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")'Load the PDF page

'Get the existing PDF page

Dim lpage As PdfLoadedPage = CType(ldoc.Pages(0),PdfLoadedPage)

'Get the existing annotations 

Dim annots As PdfLoadedAnnotationCollection = lpage.Annotations

'Get the existing rectangle annotation

Dim loadedRectangleAnnotation As PdfLoadedRectangleAnnotation =CType(annots(0),PdfLoadedRectangleAnnotation)

'Get the annotation comments collection

Dim commentsCollection As PdfLoadedPopupAnnotationCollection = loadedRectangleAnnotation.Comments

' Remove comments by index 

commentsCollection.RemoveAt(0)

'Save the document

ldoc.Save("Output.pdf")

'Close the document

ldoc.Close(true)


{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}


//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument ldoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await ldoc.OpenAsync(file);

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation comments collection

PdfLoadedPopupAnnotationCollection commentsCollection = loadedRectangleAnnotation.Comments;

// Remove comments by index 

commentsCollection.RemoveAt(0);


//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await ldoc.SaveAsync(stream);

//Close the document

ldoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("inputAnnotation.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument ldoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation comments collection

PdfLoadedPopupAnnotationCollection commentsCollection = loadedRectangleAnnotation.Comments;

// Remove comments by index 

commentsCollection.RemoveAt(0);

//Save the document into stream

MemoryStream stream = new MemoryStream();

ldoc.Save(stream);

stream.Position = 0;

//Closes the document

ldoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.inputAnnotation.pdf");

PdfLoadedDocument ldoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation comments collection

PdfLoadedPopupAnnotationCollection commentsCollection = loadedRectangleAnnotation.Comments;

// Remove comments by index 

commentsCollection.RemoveAt(0);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}


{% endhighlight %}

{% endtabs %}

The following code example explains how to remove review status to the existing PDF annotation.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document

PdfLoadedDocument ldoc = new PdfLoadedDocument("Input.pdf");

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation review collection

PdfLoadedPopupAnnotationCollection reviewCollection = loadedRectangleAnnotation.ReviewHistory;

// Remove review status by index 

reviewCollection.RemoveAt(0);

ldoc.Save("Output.pdf");

//Close the document

ldoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loaded the PDF document

Dim ldoc As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the existing PDF page

Dim lpage As PdfLoadedPage = CType(ldoc.Pages(0),PdfLoadedPage)

'Get the existing annotations 

Dim annots As PdfLoadedAnnotationCollection = lpage.Annotations

'Get the existing rectangle annotation

Dim loadedRectangleAnnotation As PdfLoadedRectangleAnnotation = CType(annots(0),PdfLoadedRectangleAnnotation)

'Get the annotation review collection

Dim reviewCollection As PdfLoadedPopupAnnotationCollection = loadedRectangleAnnotation.ReviewHistory

' Remove review status by index 

reviewCollection.RemoveAt(0)

ldoc.Save("Output.pdf")

'Close the document

ldoc.Close(true)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}


//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument ldoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await ldoc.OpenAsync(file);

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

// Get the annotation review collection

PdfLoadedPopupAnnotationCollection reviewCollection = loadedRectangleAnnotation.ReviewHistory;

//Remove review status by index 

reviewCollection.RemoveAt(0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await ldoc.SaveAsync(stream);

//Close the document

ldoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("inputAnnotation.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument ldoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation  reviewcollection

PdfLoadedPopupAnnotationCollection reviewCollection = loadedRectangleAnnotation.ReviewHistory;

//Remove review status by index 

reviewCollection.RemoveAt(0);

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

stream.Position = 0;

//Closes the document

ldoc.Close(true);

//Defining the Content Type for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.inputAnnotation.pdf");

PdfLoadedDocument ldoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation review collection

PdfLoadedPopupAnnotationCollection reviewCollection = loadedRectangleAnnotation.ReviewHistory;

//Remove review status by index 

reviewCollection.RemoveAt(0);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}


## Modifying comments and review status 

The Essential PDF supports modifying comments and reviewing status in the PDF annotation.

The following code example explains how to modify comments in the existing PDF annotation.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document

PdfLoadedDocument ldoc = new PdfLoadedDocument("Input.pdf");

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation comments collection

PdfLoadedPopupAnnotationCollection commentsCollection = loadedRectangleAnnotation.Comments;

//Get the modified comments

PdfLoadedPopupAnnotation loadedComments = commentsCollection[0];

//Modify the comments Text

loadedComments.Text = "This is the modified comment";

//Save the document

ldoc.Save("Output.pdf");

//Close the document

ldoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the PDF document

Dim ldoc As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the existing PDF page

Dim lpage As PdfLoadedPage = CType(ldoc.Pages(0),PdfLoadedPage)

'Get the existing annotations

Dim annots As PdfLoadedAnnotationCollection = lpage.Annotations

'Get the existing rectangle annotation

Dim loadedRectangleAnnotation As PdfLoadedRectangleAnnotation = CType(annots(0),PdfLoadedRectangleAnnotation)

'Get the annotation comments collection

Dim commentsCollection As PdfLoadedPopupAnnotationCollection = loadedRectangleAnnotation.Comments

'Get the modified comment

Dim loadedComments As PdfLoadedPopupAnnotation = commentsCollection(0)

' Modify the comment Text

loadedComments.Text = "This is the modified comment"

'Save the document

ldoc.Save("Output.pdf")

'Close the document

ldoc.Close(true)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument ldoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await ldoc.OpenAsync(file);

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Load the annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the existing rectangle annotation

PdfLoadedPopupAnnotationCollection commentsCollection = loadedRectangleAnnotation.Comments;

// Get the modified comment

PdfLoadedPopupAnnotation loadedComments = commentsCollection[0];

// Modify the comment Text

loadedComments.Text = "This is the modified comment";

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await ldoc.SaveAsync(stream);

//Close the document

ldoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("inputAnnotation.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument ldoc = new PdfLoadedDocument(docStream);

//Load the PDF document page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Load the annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation comments collection

PdfLoadedPopupAnnotationCollection commentsCollection = loadedRectangleAnnotation.Comments;

//Get the modified comment

PdfLoadedPopupAnnotation loadedComments = commentsCollection[0];

//Modify the comment Text

loadedComments.Text = "This is the modified comments";

//Save the document into stream

MemoryStream stream = new MemoryStream();

ldoc.Save(stream);

stream.Position = 0;

//Closes the document

ldoc.Close(true);

//Defining the Content Type for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}


//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.inputAnnotation.pdf");

PdfLoadedDocument ldoc = new PdfLoadedDocument(docStream);

//Load the PDF document page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Load the annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation comments collection

PdfLoadedPopupAnnotationCollection commentsCollection = loadedRectangleAnnotation.Comments;

//Get the modified comment

PdfLoadedPopupAnnotation loadedComments = commentsCollection[0];

//Modify the comments Text

loadedComments.Text = "This is Modify comments";

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

The following code example explains how to modify review status to the existing PDF annotation.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document

PdfLoadedDocument ldoc = new PdfLoadedDocument("Input.pdf");

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation review collection

PdfLoadedPopupAnnotationCollection reviewCollection = loadedRectangleAnnotation.ReviewHistory;

// Get the modified review state

PdfLoadedPopupAnnotation loadedReview = reviewCollection[0];

// Modify the review State

loadedReview.State = PdfAnnotationState.Rejected;

//Save the document

ldoc.Save("Output.pdf");

//Close the document

ldoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loaded the PDF document

Dim ldoc As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the existing PDF page

Dim lpage As PdfLoadedPage = CType(ldoc.Pages(0),PdfLoadedPage)

'Get the existing annotations

Dim annots As PdfLoadedAnnotationCollection = lpage.Annotations

'Get the existing rectangle annotation

Dim loadedRectangleAnnotation As PdfLoadedRectangleAnnotation = CType(annots(0),PdfLoadedRectangleAnnotation)

'Get annotation review collection

Dim reviewCollection As PdfLoadedPopupAnnotationCollection = loadedRectangleAnnotation.ReviewHistory

Dim loadedReview As PdfLoadedPopupAnnotation = reviewCollection(0)

' Modify the review State

loadedReview.State = PdfAnnotationState.Rejected

'Save the document

ldoc.Save("Output.pdf")

'Close the document

ldoc.Close(true)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument ldoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await ldoc.OpenAsync(file);

//Get the existing annotations

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing PDF page

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation review collection

PdfLoadedPopupAnnotationCollection reviewCollection = loadedRectangleAnnotation.ReviewHistory;

// Get the modified review state

PdfLoadedPopupAnnotation loadedReview = reviewCollection[0];

// Modify the review State

loadedReview.State = PdfAnnotationState.Rejected;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await ldoc.SaveAsync(stream);

//Close the document

ldoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("inputAnnotation.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument ldoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation review collection

PdfLoadedPopupAnnotationCollection reviewCollection = loadedRectangleAnnotation.ReviewHistory;

// Get the modified review state

PdfLoadedPopupAnnotation loadedReview = reviewCollection[0];

// Modify the review State

loadedReview.State = PdfAnnotationState.Rejected;

//Save the document into stream

MemoryStream stream = new MemoryStream();

lDoc.Save(stream);

stream.Position = 0;

//Closes the document

ldoc.Close(true);

//Defining the Content Type for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.inputAnnotation.pdf");

PdfLoadedDocument ldoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage lpage = ldoc.Pages[0] as PdfLoadedPage;

//Get the existing annotations

PdfLoadedAnnotationCollection annots = lpage.Annotations;

//Get the existing rectangle annotation

PdfLoadedRectangleAnnotation loadedRectangleAnnotation = annots[0] as PdfLoadedRectangleAnnotation;

//Get the annotation review collection

PdfLoadedPopupAnnotationCollection reviewCollection = loadedRectangleAnnotation.ReviewHistory;

// Get the modified review state

PdfLoadedPopupAnnotation loadedReview = reviewCollection[0];

// Modify the review State

loadedReview.State = PdfAnnotationState.Rejected;

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Retrieve review status and comments from PDF annotation

The PDF annotations may have an author-specific state associated with them. The state is not specified in the annotation itself, but it represents a separate text annotation ([Popup Annotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.Interactive.PdfPopupAnnotation.html)).

The Essential PDF supports retrieving the annotation comments and review history from the existing PDF document annotations.

### Retrieve review status from PDF annotation

You can retrieve the annotation review history from the existing PDF document annotations through the [ReviewHistory](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLoadedPopupAnnotation.html#Syncfusion_Pdf_Interactive_PdfLoadedPopupAnnotation_ReviewHistory) property.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the existing PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Get the existing PDF page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage; 

//Get the annotation

PdfLoadedTextMarkupAnnotation loadedMarkup = loadedPage.Annotations[0] as PdfLoadedTextMarkupAnnotation;

//Get the review history collection for the annotation

PdfLoadedPopupAnnotationCollection reviewCollection = loadedMarkup.ReviewHistory;

//Get annotation state

PdfAnnotationState state = reviewCollection[0].State;

//Get annotation state model

PdfAnnotationStateModel model = reviewCollection[0].StateModel;

//Get the comments of the annotation

PdfLoadedPopupAnnotationCollection commentsCollection = loadedMarkup.Comments;

//Get the review history of the comment

PdfLoadedPopupAnnotationCollection reviewCollection1 = commentsCollection[0].ReviewHistory;

//Close the PDF document

loadedDocument.Close(true);


{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the existing PDF document

Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")

'Get the existing PDF page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Get the annotation

Dim loadedMarkup As PdfLoadedTextMarkupAnnotation = TryCast(loadedPage.Annotations(0), PdfLoadedTextMarkupAnnotation)

'Get the review history collection for the annotation

Dim reviewCollection As PdfLoadedPopupAnnotationCollection = loadedMarkup.ReviewHistory

'Get annotation state

Dim state As PdfAnnotationState = reviewCollection(0).State

'Get annotation state model

Dim model As PdfAnnotationStateModel = reviewCollection(0).StateModel

'Get the comments of the annotation

Dim commentsCollection As PdfLoadedPopupAnnotationCollection = loadedMarkup.Comments

'Get the review history of the comment

Dim reviewCollection1 As PdfLoadedPopupAnnotationCollection = commentsCollection(0).ReviewHistory

'Close the PDF document

loadedDocument.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Get the existing PDF page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage; 

//Get the annotation

PdfLoadedTextMarkupAnnotation loadedMarkup = loadedPage.Annotations[0] as PdfLoadedTextMarkupAnnotation;

//Get the review history collection for the annotation

PdfLoadedPopupAnnotationCollection reviewCollection = loadedMarkup.ReviewHistory;

//Get annotation state

PdfAnnotationState state = reviewCollection[0].State;

//Get annotation state model

PdfAnnotationStateModel model = reviewCollection[0].StateModel;

//Get the comments of the annotation

PdfLoadedPopupAnnotationCollection commentsCollection = loadedMarkup.Comments;

//Get the review history of the comment

PdfLoadedPopupAnnotationCollection reviewCollection1 = commentsCollection[0].ReviewHistory;

//Close the document

loadedDocument.Close(true);


{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage; 

//Get the annotation

PdfLoadedTextMarkupAnnotation loadedMarkup = loadedPage.Annotations[0] as PdfLoadedTextMarkupAnnotation;

//Get the review history collection for the annotation

PdfLoadedPopupAnnotationCollection reviewCollection = loadedMarkup.ReviewHistory;

//Get annotation state

PdfAnnotationState state = reviewCollection[0].State;

//Get annotation state model

PdfAnnotationStateModel model = reviewCollection[0].StateModel;

//Get the comments of the annotation

PdfLoadedPopupAnnotationCollection commentsCollection = loadedMarkup.Comments;

//Get the review history of the comment

PdfLoadedPopupAnnotationCollection reviewCollection1 = commentsCollection[0].ReviewHistory;

//Closes the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage; 

//Get the annotation

PdfLoadedTextMarkupAnnotation loadedMarkup = loadedPage.Annotations[0] as PdfLoadedTextMarkupAnnotation;

//Get the review history collection for the annotation

PdfLoadedPopupAnnotationCollection reviewCollection = loadedMarkup.ReviewHistory;

//Get annotation state

PdfAnnotationState state = reviewCollection[0].State;

//Get annotation state model

PdfAnnotationStateModel model = reviewCollection[0].StateModel;

//Get the comments of the annotation

PdfLoadedPopupAnnotationCollection commentsCollection = loadedMarkup.Comments;

//Get the review history of the comment

PdfLoadedPopupAnnotationCollection reviewCollection1 = commentsCollection[0].ReviewHistory;

//Closes the document

loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %}

### Retrieve comments from PDF annotation

The following code example explains how to retrieve the annotation comments from the existing PDF document annotations.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the existing PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Get the existing PDF page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage; 

//Get the annotation

PdfLoadedTextMarkupAnnotation loadedMarkup = loadedPage.Annotations[0] as PdfLoadedTextMarkupAnnotation;

//Get the comments of the annotation

PdfLoadedPopupAnnotationCollection commentsCollection = loadedMarkup.Comments;

//Close the PDF document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the existing PDF document

Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")

'Get the existing PDF page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Get the annotation

Dim loadedMarkup As PdfLoadedTextMarkupAnnotation = TryCast(loadedPage.Annotations(0), PdfLoadedTextMarkupAnnotation)

'Get the comments of the annotation

Dim commentsCollection As PdfLoadedPopupAnnotationCollection = loadedMarkup.Comments

'Close the PDF document

loadedDocument.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Get the existing PDF page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage; 

//Get the annotation

PdfLoadedTextMarkupAnnotation loadedMarkup = loadedPage.Annotations[0] as PdfLoadedTextMarkupAnnotation;

//Get the comments of the annotation

PdfLoadedPopupAnnotationCollection commentsCollection = loadedMarkup.Comments;

//Close the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage; 

//Get the annotation

PdfLoadedTextMarkupAnnotation loadedMarkup = loadedPage.Annotations[0] as PdfLoadedTextMarkupAnnotation;

//Get the comments of the annotation

PdfLoadedPopupAnnotationCollection commentsCollection = loadedMarkup.Comments;

//Closes the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the existing PDF page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage; 

//Get the annotation

PdfLoadedTextMarkupAnnotation loadedMarkup = loadedPage.Annotations[0] as PdfLoadedTextMarkupAnnotation;

//Get the comments of the annotation

PdfLoadedPopupAnnotationCollection commentsCollection = loadedMarkup.Comments;

//Closes the document

loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %}

## Printing Annotations

The Essential PDF supports printing the annotation in a PDF document by setting the annotation flag to ```Print``` using the [AnnotationFlags](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLoadedStyledAnnotation.html#Syncfusion_Pdf_Interactive_PdfLoadedStyledAnnotation_AnnotationFlags) property.

The following code example illustrates how to print annotation in the PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page 

PdfPage page = document.Pages.Add();

//Creates a new PDF rubber stamp annotation

RectangleF rectangle = new RectangleF(40, 60, 80, 20);

PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangle, " Text Rubber Stamp Annotation");

rubberStampAnnotation.Icon = PdfRubberStampAnnotationIcon.Draft;

rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Set the AnnotationFlags to print 

rubberStampAnnotation.AnnotationFlags = PdfAnnotationFlags.Print;

//Adds annotation to the page 

page.Annotations.Add(rubberStampAnnotation);

//Saves the document

document.Save("RubberStamp.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document

Dim document As PdfDocument = New PdfDocument()

'Creates a new page 

Dim page As PdfPage = document.Pages.Add()

'Creates a new PDF rubber stamp annotation

Dim rectangle As RectangleF = New RectangleF(40, 60, 80, 20)

Dim rubberStampAnnotation As PdfRubberStampAnnotation = New 

PdfRubberStampAnnotation(rectangle, " Text Rubber Stamp Annotation")

rubberStampAnnotation.Icon = PdfRubberStampAnnotationIcon.Draft

rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation"

'Set the AnnotationFlags to print 

rubberStampAnnotation.AnnotationFlags = PdfAnnotationFlags.Print

'Adds annotation to the page 

page.Annotations.Add(rubberStampAnnotation)

'Saves the document

document.Save("RubberStamp.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page 

PdfPage page = document.Pages.Add();

//Creates a new PDF rubber stamp annotation

RectangleF rectangle = new RectangleF(40, 60, 80, 20);

PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangle, " Text Rubber Stamp Annotation");

rubberStampAnnotation.Icon = PdfRubberStampAnnotationIcon.Draft;

rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Set the AnnotationFlags to print 

rubberStampAnnotation.AnnotationFlags = PdfAnnotationFlags.Print;

//Adds annotation to the page 

page.Annotations.Add(rubberStampAnnotation);

//Saves the document
MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page 

PdfPage page = document.Pages.Add();

//Creates a new PDF rubber stamp annotation

RectangleF rectangle = new RectangleF(40, 60, 80, 20);

PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangle, " Text Rubber Stamp Annotation");

rubberStampAnnotation.Icon = PdfRubberStampAnnotationIcon.Draft;

rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Set the AnnotationFlags to print 

rubberStampAnnotation.AnnotationFlags = PdfAnnotationFlags.Print;

//Adds annotation to the page 

page.Annotations.Add(rubberStampAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "RubberStamp.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page 

PdfPage page = document.Pages.Add();

//Creates a new PDF rubber stamp annotation

RectangleF rectangle = new RectangleF(40, 60, 80, 20);

PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangle, " Text Rubber Stamp Annotation");

rubberStampAnnotation.Icon = PdfRubberStampAnnotationIcon.Draft;

rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Set the AnnotationFlags to print 

rubberStampAnnotation.AnnotationFlags = PdfAnnotationFlags.Print;

//Adds annotation to the page 

page.Annotations.Add(rubberStampAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
   Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("RubberStamp.pdf", "application/pdf", stream);
}
else
{
   Xamarin.Forms.DependencyService.Get<ISave>().Save("RubberStamp.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

The following table explains annotation flags.

<table>
<thead>
<tr>
<th>
Member<br/><br/></th><th>
Meaning<br/><br/></th></tr>
</thead>
<tbody>
<tr>
<td>
Invisible<br/><br/></td><td>
If set, do not display the annotation if it does not belong to one of the standard annotation types and no annotation handler is available.<br/><br/></td></tr>
<tr>
<td>
Hidden<br/><br/></td><td>
If set, do not display or print the annotation, or allow user interact with annotation, regardless of annotation type or annotation handler.<br/><br/></td></tr>
<tr>
<td>
Print<br/><br/></td><td>
If set, prints the annotation when the page is printed.<br/><br/></td></tr>
<tr>
<td>
NoZoom<br/><br/></td><td>
If set, do not scale the annotation’s appearance to match the magnification of the page.<br/><br/></td></tr>
<tr>
<td>
NoRotate<br/><br/></td><td>
If set, do not rotate the annotation’s appearance to match the rotation of the page.<br/><br/></td></tr>
<tr>
<td>
NoView<br/><br/></td><td>
If set, do not display the annotation on the screens or allow user interact with annotation.<br/><br/></td></tr>
<tr>
<td>
ReadOnly<br/><br/></td><td>
If set, do not allow user interact with annotation.<br/><br/></td></tr>
<tr>
<td>
Locked<br/><br/></td><td>
If set, do not allow the annotation to be deleted or its properties to be modified by the user.<br/><br/></td></tr>
<tr>
<td>
ToggleNoView<br/><br/></td><td>
If set, inverts the interpretation of the NoView flat for certain events.<br/><br/></td></tr>
</tbody>
</table>

## Add Custom Stamp using Rubber Stamp Annotation

Essential PDF supports adding custom stamp in an existing PDF document by using the [PdfRubberStampAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfRubberStampAnnotation.html) class along with different appearance settings through [PdfAppearance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAppearance.html). This custom stamp is movable and resizable.

Rubber stamp annotation displays text or graphics intended to look like it is stamped on the page with a rubber stamp. When opened, it displays a pop-up window containing the text of the associated note. 

The following code snippet explains how to add custom stamp in an existing PDF document using rubber stamp annotation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Get the page from loaded PDF document
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new pdf rubber stamp annotation
RectangleF rectangleF = new RectangleF(350, 20, 200, 80);
PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangleF);

//Custom stamp the rubber stamp annotation
PdfSolidBrush brush = new PdfSolidBrush(new PdfColor(Color.LightBlue));
PdfPath path = RoundedRect(new RectangleF(0, 0, 200, 80), 20);
rubberStampAnnotation.Appearance.Normal.Graphics.DrawPath(brush, path);

//Add text in rubber stamp annotation
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString("DD/2018/1234567890", font, PdfBrushes.Black, new PointF(10, 20));
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString(DateTime.Now.ToString("dd-MM-yyyy HH:mm:ss"), font, PdfBrushes.Black, new PointF(10, 40));

//Set the content of annotation
rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Add annotation to the page
loadedPage.Annotations.Add(rubberStampAnnotation);

//Save the PDF document
loadedDocument.Save("Output.pdf");

//Close the instance of PdfLoadedDocument
loadedDocument.Close(true);

public static PdfPath RoundedRect(RectangleF bounds, int radius)
{
    int diameter = radius * 2;
    SizeF size = new SizeF(diameter, diameter);
    RectangleF arc = new RectangleF(bounds.Location, size);
    PdfPath path = new PdfPath();

    if (radius == 0)
    {
        path.AddRectangle(bounds);
        return path;
    }

    //Draw the top left arc  
    path.AddArc(arc, 180, 90);

    //Draw the top right arc  
    arc.X = bounds.Right - diameter;
    path.AddArc(arc, 270, 90);

    //Draw the bottom right arc  
    arc.Y = bounds.Bottom - diameter;
    path.AddArc(arc, 0, 90);

    //Draw the bottom left arc 
    arc.X = bounds.Left;
    path.AddArc(arc, 90, 90);

    //Close the figure
    path.CloseFigure();

    //Return the path
    return path;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the page from loaded PDF document
Dim loadedPage As PdfLoadedPage = CType(loadedDocument.Pages(0), PdfLoadedPage)

'Create a new pdf rubber stamp annotation
Dim rectangleF As RectangleF = New RectangleF(350, 20, 200, 80)
Dim rubberStampAnnotation As PdfRubberStampAnnotation = New PdfRubberStampAnnotation(rectangleF)

'Custom stamp the rubber stamp annotation
Dim brush As PdfSolidBrush = New PdfSolidBrush(New PdfColor(Color.LightBlue))
Dim path As PdfPath = RoundedRect(New RectangleF(0, 0, 200, 80), 20)
rubberStampAnnotation.Appearance.Normal.Graphics.DrawPath(brush, path)

'Add text in rubber stamp annotation
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold)
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString("DD/2018/1234567890", font, PdfBrushes.Black, New PointF(10, 20))
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString(DateTime.Now.ToString("dd-MM-yyyy HH:mm:ss"), font, PdfBrushes.Black, New PointF(10, 40))

'Set the content of annotation
rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation"

'Adds annotation to the page
loadedPage.Annotations.Add(rubberStampAnnotation)

'Save the PDF document
loadedDocument.Save("Output.pdf")

'Close the instance of PdfLoadedDocument
loadedDocument.Close(True)

Private Function RoundedRect(bounds As RectangleF, radius As Integer) As PdfPath
    Dim diameter As Integer = (radius * 2)
    Dim size As SizeF = New SizeF(diameter, diameter)
    Dim arc As RectangleF = New RectangleF(bounds.Location, size)
    Dim path As PdfPath = New PdfPath
    If (radius = 0) Then
        path.AddRectangle(bounds)
        Return path
    End If

    'Draw the top left arc  
    path.AddArc(arc, 180, 90)

    'Draw the top right arc  
    arc.X = (bounds.Right - diameter)
    path.AddArc(arc, 270, 90)

    'Draw the bottom right arc  
    arc.Y = (bounds.Bottom - diameter)
    path.AddArc(arc, 0, 90)

    'Draw the bottom left arc 
    arc.X = bounds.Left
    path.AddArc(arc, 90, 90)

    'Close the figure
    path.CloseFigure()

    'Return the path
    Return path
End Function
{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}
//Load an existing PDF document
Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(inputStream);

//Get the page from loaded PDF document
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new pdf rubber stamp annotation
RectangleF rectangleF = new RectangleF(350, 20, 200, 80);
PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangleF);

//Custom stamp the rubber stamp annotation
PdfSolidBrush brush = new PdfSolidBrush(new PdfColor(Color.FromArgb(255, 173, 216, 230)));
PdfPath path = RoundedRect(new RectangleF(0, 0, 200, 80), 20);
rubberStampAnnotation.Appearance.Normal.Graphics.DrawPath(brush, path);

//Add text in rubber stamp annotation
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString("DD/2018/1234567890", font, PdfBrushes.Black, new PointF(10, 20));
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString(DateTime.Now.ToString("dd-MM-yyyy HH:mm:ss"), font, PdfBrushes.Black, new PointF(10, 40));

//Set the content of annotation
rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Add annotation to the page
loadedPage.Annotations.Add(rubberStampAnnotation);

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
loadedDocument.Save(ms);

//Close the document
loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code sample
Save(ms, "Output.pdf");

private PdfPath RoundedRect(RectangleF bounds, int radius)
{
    int diameter = radius * 2;
    SizeF size = new SizeF(diameter, diameter);
    RectangleF arc = new RectangleF(bounds.Location, size);
    PdfPath path = new PdfPath();

    if (radius == 0)
    {
        path.AddRectangle(bounds);
        return path;
    }

    //Draw the top left arc  
    path.AddArc(arc, 180, 90);

    //Draw the top right arc  
    arc.X = bounds.Right - diameter;
    path.AddArc(arc, 270, 90);

    //Draw the bottom right arc  
    arc.Y = bounds.Bottom - diameter;
    path.AddArc(arc, 0, 90);

    //Draw the bottom left arc 
    arc.X = bounds.Left;
    path.AddArc(arc, 90, 90);

    //Close the figure
    path.CloseFigure();

    //Return the path
    return path;
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Load an existing PDF document
FileStream inputStream = new FileStream("Input.pdf", FileMode.Open);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(inputStream);

//Get the page from loaded PDF document
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new pdf rubber stamp annotation
RectangleF rectangleF = new RectangleF(350, 20, 200, 80);
PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangleF);

//Custom stamp the rubber stamp annotation
PdfSolidBrush brush = new PdfSolidBrush(new PdfColor(Color.FromArgb(255, 173, 216, 230)));
PdfPath path = RoundedRect(new RectangleF(0, 0, 200, 80), 20);
rubberStampAnnotation.Appearance.Normal.Graphics.DrawPath(brush, path);

//Add text in rubber stamp annotation
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString("DD/2018/1234567890", font, PdfBrushes.Black, new PointF(10, 20));
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString(DateTime.Now.ToString("dd-MM-yyyy HH:mm:ss"), font, PdfBrushes.Black, new PointF(10, 40));

//Set the content of annotation
rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Add annotation to the page
loadedPage.Annotations.Add(rubberStampAnnotation);

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;

private PdfPath RoundedRect(RectangleF bounds, int radius)
{
    int diameter = radius * 2;
    SizeF size = new SizeF(diameter, diameter);
    RectangleF arc = new RectangleF(bounds.Location, size);
    PdfPath path = new PdfPath();

    if (radius == 0)
    {
        path.AddRectangle(bounds);
        return path;
    }

    //Draw the top left arc  
    path.AddArc(arc, 180, 90);

    //Draw the top right arc  
    arc.X = bounds.Right - diameter;
    path.AddArc(arc, 270, 90);

    //Draw the bottom right arc  
    arc.Y = bounds.Bottom - diameter;
    path.AddArc(arc, 0, 90);

    //Draw the bottom left arc 
    arc.X = bounds.Left;
    path.AddArc(arc, 90, 90);

    //Close the figure
    path.CloseFigure();

    //Return the path
    return path;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Load an existing PDF document
Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(inputStream);

//Get the page from loaded PDF document
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new pdf rubber stamp annotation
RectangleF rectangleF = new RectangleF(350, 20, 200, 80);
PdfRubberStampAnnotation rubberStampAnnotation = new PdfRubberStampAnnotation(rectangleF);

//Custom stamp the rubber stamp annotation
PdfSolidBrush brush = new PdfSolidBrush(new PdfColor(Syncfusion.Drawing.Color.FromArgb(255, 173, 216, 230)));
PdfPath path = RoundedRect(new RectangleF(0, 0, 200, 80), 20);
rubberStampAnnotation.Appearance.Normal.Graphics.DrawPath(brush, path);

//Add text in rubber stamp annotation
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString("DD/2018/1234567890", font, PdfBrushes.Black, new PointF(10, 20));
rubberStampAnnotation.Appearance.Normal.Graphics.DrawString(DateTime.Now.ToString("dd-MM-yyyy HH:mm:ss"), font, PdfBrushes.Black, new PointF(10, 40));

//Set the content of annotation
rubberStampAnnotation.Text = "Text Properties Rubber Stamp Annotation";

//Add annotation to the page
loadedPage.Annotations.Add(rubberStampAnnotation);

//Save the document to the stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Close the document
loadedDocument.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

private PdfPath RoundedRect(RectangleF bounds, int radius)
{
    int diameter = radius * 2;
    SizeF size = new SizeF(diameter, diameter);
    RectangleF arc = new RectangleF(bounds.Location, size);
    PdfPath path = new PdfPath();

    if (radius == 0)
    {
        path.AddRectangle(bounds);
        return path;
    }

    //Draw the top left arc  
    path.AddArc(arc, 180, 90);

    //Draw the top right arc  
    arc.X = bounds.Right - diameter;
    path.AddArc(arc, 270, 90);

    //Draw the bottom right arc  
    arc.Y = bounds.Bottom - diameter;
    path.AddArc(arc, 0, 90);

    //Draw the bottom left arc 
    arc.X = bounds.Left;
    path.AddArc(arc, 90, 90);

    //Close the figure
    path.CloseFigure();

    //Return the path
    return path;
}
{% endhighlight %}
{% endtabs %}

## Text Markup Annotation

You can highlight the Markup Text using the [PdfTextMarkupAnnotationType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfTextMarkupAnnotationType.html) enum of the [TextMarkupAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfTextMarkupAnnotation.html) class. This is explained in the following code example.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Create a new page.
PdfPage page = document.Pages.Add();

//Create a PDF font and font style.
Font font = new Font("Calibri", 10, FontStyle.Bold);
PdfFont pdfFont = new PdfTrueTypeFont(font, false);

//Create a new PDF brush.
PdfBrush pdfBrush = new PdfSolidBrush(Color.Black);

//Draw text in the new page.
page.Graphics.DrawString("Text Markup Annotation Demo", pdfFont, pdfBrush, new PointF(150, 10));
string markupText = "Text Markup";
SizeF size = pdfFont.MeasureString(markupText);
RectangleF rectangle = new RectangleF(175, 40, size.Width, size.Height);
page.Graphics.DrawString(markupText, pdfFont, pdfBrush, rectangle);

//Create a PDF text markup annotation.
PdfTextMarkupAnnotation markupAnnotation = new PdfTextMarkupAnnotation("Markup annotation", "Markup annotation with highlight style", markupText, new PointF(175, 40), pdfFont);
markupAnnotation.TextMarkupColor = new PdfColor(Color.BlueViolet);
markupAnnotation.TextMarkupAnnotationType = PdfTextMarkupAnnotationType.Highlight;

//Add this annotation to a new page.
page.Annotations.Add(markupAnnotation);

//Save the document to disk.
document.Save("Output.pdf");
//close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a new PDF document.
Dim document As New PdfDocument()

'Create a new page.
Dim page As PdfPage = document.Pages.Add()

'Create a pdf font and pdf font style.
Dim font As New Font("Calibri", 10, FontStyle.Bold)
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, False)

'Create a new PdfBrush.
Dim pdfBrush As PdfBrush = New PdfSolidBrush(Color.Black)

'Draw text in the new page.
page.Graphics.DrawString("Text Markup Annotation Demo", pdfFont, pdfBrush, New PointF(150, 10))
Dim markupText As String = "Text Markup"
Dim size As SizeF = pdfFont.MeasureString(markupText)
Dim rectangle As New RectangleF(175, 40, size.Width, size.Height)
page.Graphics.DrawString(markupText, pdfFont, pdfBrush, rectangle)

'Create a pdf text markup annotation.
Dim markupAnnotation As New PdfTextMarkupAnnotation("Markup annotation", "Markup annotation with highlight style", markupText, New PointF(175, 40), pdfFont)
markupAnnotation.TextMarkupColor = New PdfColor(Color.BlueViolet)
markupAnnotation.TextMarkupAnnotationType = PdfTextMarkupAnnotationType.Highlight

'Add this annotation to a new page.
page.Annotations.Add(markupAnnotation)

'Save the document to disk.
document.Save("Output.pdf")

'close the document.
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page. 

PdfPage page = document.Pages.Add();

//Create a PDF font and font style.
Font font = new Font("Calibri", 10, FontStyle.Bold);
PdfFont pdfFont = new PdfTrueTypeFont(font, false);

//Create a new PDF brush.
PdfBrush pdfBrush = new PdfSolidBrush(Color.Black);

//Draw text in the new page.
page.Graphics.DrawString("Text Markup Annotation Demo", pdfFont, pdfBrush, new PointF(150, 10));
string markupText = "Text Markup";
SizeF size = pdfFont.MeasureString(markupText);
RectangleF rectangle = new RectangleF(175, 40, size.Width, size.Height);
page.Graphics.DrawString(markupText, pdfFont, pdfBrush, rectangle);

//Create a PDF text markup annotation.
PdfTextMarkupAnnotation markupAnnotation = new PdfTextMarkupAnnotation("Markup annotation", "Markup annotation with highlight style", markupText, new PointF(175, 40), pdfFont);
markupAnnotation.TextMarkupColor = new PdfColor(Color.BlueViolet);
markupAnnotation.TextMarkupAnnotationType = PdfTextMarkupAnnotationType.Highlight;

//Add this annotation to a new page.
page.Annotations.Add(markupAnnotation);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Create a new page.
PdfPage page = document.Pages.Add();
FileStream fontStream = new FileStream("arial.ttf", FileMode.Open, FileAccess.Read);

PdfFont pdfFont = new PdfTrueTypeFont(fontStream, 14);

//Create a new PDF brush.
PdfBrush pdfBrush = new PdfSolidBrush(Color.Black);

//Draw text in the new page.
page.Graphics.DrawString("Text Markup Annotation Demo", pdfFont, pdfBrush, new PointF(150, 10));
string markupText = "Text Markup";
SizeF size = pdfFont.MeasureString(markupText);
RectangleF rectangle = new RectangleF(175, 40, size.Width, size.Height);
page.Graphics.DrawString(markupText, pdfFont, pdfBrush, rectangle);

//Create a PDF text markup annotation.
PdfTextMarkupAnnotation markupAnnotation = new PdfTextMarkupAnnotation("Markup annotation", "Markup annotation with highlight style", markupText, new PointF(175, 40), pdfFont);
markupAnnotation.TextMarkupColor = new PdfColor(Color.BlueViolet);
markupAnnotation.TextMarkupAnnotationType = PdfTextMarkupAnnotationType.Highlight;

//Add this annotation to a new page.
page.Annotations.Add(markupAnnotation);

//Save the document to disk.
Save(document, "Output.pdf");
//close the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page. 

PdfPage page = document.Pages.Add();

//Create a PDF font and font style .
Font font = new Font("Calibri", 10, FontStyle.Bold);
PdfFont pdfFont = new PdfTrueTypeFont(font, false);

//Create a new PDF brush.
PdfBrush pdfBrush = new PdfSolidBrush(Color.Black);

//Draw text in the new page.
page.Graphics.DrawString("Text Markup Annotation Demo", pdfFont, pdfBrush, new PointF(150, 10));
string markupText = "Text Markup";
SizeF size = pdfFont.MeasureString(markupText);
RectangleF rectangle = new RectangleF(175, 40, size.Width, size.Height);
page.Graphics.DrawString(markupText, pdfFont, pdfBrush, rectangle);

//Create a PDF text markup annotation.
PdfTextMarkupAnnotation markupAnnotation = new PdfTextMarkupAnnotation("Markup annotation", "Markup annotation with highlight style", markupText, new PointF(175, 40), pdfFont);
markupAnnotation.TextMarkupColor = new PdfColor(Color.BlueViolet);
markupAnnotation.TextMarkupAnnotationType = PdfTextMarkupAnnotationType.Highlight;

//Add this annotation to a new page.
page.Annotations.Add(markupAnnotation);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer to the PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("PopupAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("PopupAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

## Troubleshooting

<table>
<th style="font-size:14px">Annotations are sometimes missing in the acrobat and the other Pdf Viewer applications.
</th>


<table>
<tr>
<th style="font-size:14px">Reason
</th>
<td style="font-size:14px">
<b>Due to the absence of the appearance dictionary, Annotation may sometimes disappear in adobe reader and other pdf viewer. 
</td>
</tr>
<tr>
<th style="font-size:14px">Solution
</th>
<td>By enabling the appearance [Graphical representation] for the annotation by using the “SetAppearance” method as below, PDF Annotations will be preserved properly on saving the file.
{% tabs %}

{% highlight c# tabtitle="C#" %}

//Enable the appearance of free text annotation.
freeText.SetAppearance(true);

{% endhighlight %}
{% endtabs %}
</td>
</tr>
</table>
</table>