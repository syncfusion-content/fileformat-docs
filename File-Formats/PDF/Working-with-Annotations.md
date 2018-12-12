---
title: Working with Annotations | Syncfusion
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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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
//Flatten the circle annotation
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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight c# %}

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

{% highlight vb.net %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

//PDF supports 3D annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core.

{% endhighlight %}

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

You can add the JavaScript script to the 3D annotation using the ```OnInstantiate``` property, which is executed whenever a 3D stream is read to create an instance of the 3D artwork. The following code snippet illustrate this.

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

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

{% highlight UWP %}

//PDF supports 3D annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, and ASP.NET Core platforms

{% endhighlight %}

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

//PDF supports File Link Annotation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports File Link Annotation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports File Link Annotation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC.

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

{% highlight UWP %}

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

PointF[] points = { new PointF(100, 400), new PointF(100, 450) };

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

PointF[] points = { new PointF(100, 400), new PointF(100, 450) };

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

document.Save("RubberStamp.pdf");

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

You can get ink list points from the ```PdfLoadedInkAnnotation```, represented by ```InkPointsCollection```. The following code illustrate this.

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

//PDF supports Sound Annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Web.

{% endhighlight %}

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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
## Measurement Annotations

Essential PDF supports interactive measurement annotations, which measures the distance, area, and angle of the line segments.

The following measurement annotation types are supported in Essential PDF:

### Line measurement annotation

The line measurement annotation is displayed as the straight line in the page. The distance of the line is measured automatically when you change the position of the line and is displayed in the pop-up window.

The following code example explains how to add a line measurement annotation to the page.

{% tabs %}
{% highlight c# %}

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

{% highlight vb.net %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

The following code example explains how to add a square measurement annotation to the page.

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

The following code example explains how to add a circle measurement annotation to the page.

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

The following code example explains how to add angle measurement annotation to the page.

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

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

{% highlight UWP %}

//PDF supports angle measurement annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Web.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports angle measurement annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Web.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports angle measurement annotation only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Web.

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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

{% highlight UWP %}

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

{% highlight ASP.NET Core %}

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

{% highlight Xamarin %}

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
