---
title: Working with JavaScript | Syncfusion
description: This section explains how to add/modify JavaScript action in the existing PDF document by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---

# Working with JavaScript

A JavaScript action allows execution of JavaScript code embedded in the PDF document. Essential PDF supports adding JavaScript action to the PDF document in the following:

* Document level JavaScript action
* JavaScript action to the form fields
* JavaScript in 3D Annotation

## Document level JavaScript action

You can add the JavaScript action to the PDF document by using [PdfJavaScriptAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfJavaScriptAction.html) class. The following code sample illustrates this. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create JavaScript action

PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"Hello World!!!\")");

//Add the JavaScript action

document.Actions.AfterOpen = scriptAction;

//Save and close the PDF document

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document

Dim document As New PdfDocument()

'Add a page

Dim page As PdfPage = document.Pages.Add()

'Create JavaScript action

Dim scriptAction As New PdfJavaScriptAction("app.alert(""Hello World!!!"")")

'Add the JavaScript action

document.Actions.AfterOpen = scriptAction

'Save and close the PDF document

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create JavaScript action

PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"Hello World!!!\")");

//Add the JavaScript action

document.Actions.AfterOpen = scriptAction;

MemoryStream memoryStream = new MemoryStream();

//Save the document

await document.SaveAsync(memoryStream);

//Close the documents

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create JavaScript action

PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"Hello World!!!\")");

//Add the JavaScript action

document.Actions.AfterOpen = scriptAction;

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create JavaScript action

PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"Hello World!!!\")");

//Add the JavaScript action

document.Actions.AfterOpen = scriptAction;

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

document.Save(memoryStream);

//Close the documents

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

## JavaScript action to the form fields

You can add the JavaScript actions to various form fields using [PdfJavaScriptAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfJavaScriptAction.html) instance. The [PdfFieldActions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfFieldActions.html) class is used to create form field actions. 

The following code snippet illustrate this.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Create a new PdfButtonField

PdfButtonField submitButton = new PdfButtonField(page, "submitButton");

submitButton.Bounds = new RectangleF(25, 160, 100, 20);

submitButton.Text = "Apply";

submitButton.BackColor = new PdfColor(181, 191, 203);

//Create a new PdfJavaScriptAction

PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"You are looking at Form field action of PDF \")");

//Set the script action to submitButton

submitButton.Actions.MouseDown = scriptAction;

//Add the submit button to the new document

document.Form.Fields.Add(submitButton);

//Save document to disk

document.Save("fieldAction.pdf");

//Save document to disk

document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document

Dim document As New PdfDocument()

'Creates a new page

Dim page As PdfPage = document.Pages.Add()

'Create a new PdfButtonField

Dim submitButton As New PdfButtonField(page, "submitButton")

submitButton.Bounds = New RectangleF(25, 160, 100, 20)

submitButton.Text = "Apply"

submitButton.BackColor = New PdfColor(181, 191, 203)

'Create a new PdfJavaScriptAction

Dim scriptAction As New PdfJavaScriptAction("app.alert(""You are looking at Form field action of PDF "")")

'Set the scriptAction to submitButton

submitButton.Actions.MouseDown = scriptAction

'Add the submit button to the new document

document.Form.Fields.Add(submitButton)

'Save document to disk

document.Save("fieldAction.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Create a new PdfButtonField

PdfButtonField submitButton = new PdfButtonField(page, "submitButton");

submitButton.Bounds = new RectangleF(25, 160, 100, 20);

submitButton.Text = "Apply";

submitButton.BackColor = new PdfColor(181, 191, 203);

//Create a new PdfJavaScriptAction

PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"You are looking at Form field action of PDF \")");

//Set the scriptAction to submitButton

submitButton.Actions.MouseDown = scriptAction;

//Add the submit button to the new document

document.Form.Fields.Add(submitButton);

MemoryStream memoryStream = new MemoryStream();

//Save the document

await document.SaveAsync(memoryStream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Create a new PdfButtonField

PdfButtonField submitButton = new PdfButtonField(page, "submitButton");

submitButton.Bounds = new RectangleF(25, 160, 100, 20);

submitButton.Text = "Apply";

submitButton.BackColor = new PdfColor(181, 191, 203);

//Create a new PdfJavaScriptAction

PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"You are looking at Form field action of PDF \")");

//Set the scriptAction to submitButton

submitButton.Actions.MouseDown = scriptAction;

//Add the submit button to the new document

document.Form.Fields.Add(submitButton);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

//Create a new PdfButtonField

PdfButtonField submitButton = new PdfButtonField(page, "submitButton");

submitButton.Bounds = new RectangleF(25, 160, 100, 20);

submitButton.Text = "Apply";

submitButton.BackColor = new PdfColor(181, 191, 203);

//Create a new PdfJavaScriptAction

PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"You are looking at Form field action of PDF \")");

//Set the scriptAction to submitButton

submitButton.Actions.MouseDown = scriptAction;

//Add the submit button to the new document

document.Form.Fields.Add(submitButton);

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

document.Save(memoryStream);

//Close the documents

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}


{% endhighlight %}

{% endtabs %}

## JavaScript in 3D Annotation

3D Annotations are used to represent 3D artworks in a PDF document. You can add a JavaScript code to 3D annotation using the [OnInstantiate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.Pdf3DAnnotation.html#Syncfusion_Pdf_Interactive_Pdf3DAnnotation_OnInstantiate) property in [Pdf3DAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.Pdf3DAnnotation.html) instance. The JavaScript script is executed when the 3D artwork is instantiated. The following code snippet illustrate this.

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

//Handles the activation of the 3D annotation

Pdf3DActivation activation = new Pdf3DActivation();

activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation;

activation.ShowToolbar = true;

pdf3dAnnotation.Activation = activation;

//Adds annotation to page

page.Annotations.Add(pdf3dAnnotation);

//Save the document to disk

document.Save("Output.pdf");

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

'Handles the activation of the 3D annotation

Dim activation As New Pdf3DActivation()

activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation

activation.ShowToolbar = True

pdf3dAnnotation.Activation = activation

'Adds annotation to page

page.Annotations.Add(pdf3dAnnotation)

'Save the document to disk

document.Save("Output.pdf")

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

//Handles the activation of the 3D annotation

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

## Add/Modify JavaScript actions to the PDF

you can add or modify the JavaScript action in existing PDF document. The below code snippet shows how to add/modify JavaScript code using [PdfJavaScriptAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfJavaScriptAction.html) class to a PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load a PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Change the javascript action in a pdf document.

loadedDocument.Actions.AfterOpen= new PdfJavaScriptAction("app.alert(\"Modified Script!\")");

//Save the document.

loadedDocument.Save("Output.pdf");

//Close the document.

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the PDF document.

Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")
 
'Change the javascript Action in a pdf document.

loadedDocument.Actions.AfterOpen = new PdfJavaScriptAction("app.alert(\"Modified Script!\")")

'Save the document.

loadedDocument.Save("Output.pdf")

'Close the document.

loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}