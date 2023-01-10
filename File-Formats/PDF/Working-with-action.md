---
title: Working with Action | Syncfusion
description: This section explains how to add actions to the document & form fields. Some supported actions are Sound, JavaScript, URI, Launch, Named, Submits & Resets.
platform: file-formats
control: PDF
documentation: UG
---
# Working with Actions

Essential PDF supports different actions that can be triggered by different events and user interactions.

## Adding an action to the PDF

The below code example illustrates how to add the action to the PDF document using [PdfLaunchAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLaunchAction.html) class. 

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create and add new launch action to the document
PdfLaunchAction action = new PdfLaunchAction("../../Data/logo.png");
document.Actions.AfterOpen = action;

//Save the document
document.Save("LaunchAction.pdf");
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document
Dim document As New PdfDocument()

'Create and add new launch action to the document
Dim action As New PdfLaunchAction("../../Data/logo.png")
document.Actions.AfterOpen = action

'Save the document
document.Save("LaunchAction.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//PDF supports adding Launch action to the PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//PDF supports adding Launch action to the PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//PDF supports adding Launch action to the PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Add-action-to-the-PDF-document/).

## Supported action types

Essential PDF supports the following types of actions.

* [PdfSoundAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfSoundAction.html) that plays the music file
* [PdfJavaScriptAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfJavaScriptAction.html) that executes PDF JavaScript code
* [PdfUriAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfUriAction.html) that launches the URI
* [PdfGoToAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfGoToAction.html) that goes to the specified page of the document
* [PdfLaunchAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLaunchAction.html) that launches the application or opens the document
* [PdfNamedAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfNamedAction.html) that goes to the named destination: next, previous, first or last page
* [PdfSubmitAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfSubmitAction.html) that submits the data that is entered into the PDF form
* [PdfResetAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfResetAction.html) that resets the fields of the PDF form

### Sound action

The [PdfSoundAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfSoundAction.html) plays a specified music file in the PDF document. Volume and repeat can be specified for the sound action.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add a page
PdfPage page = document.Pages.Add();

//Create a sound action
PdfSoundAction soundAction = new PdfSoundAction("../../Data/Startup.wav");
soundAction.Sound.Bits = 16;
soundAction.Sound.Channels = PdfSoundChannels.Stereo;
soundAction.Sound.Encoding = PdfSoundEncoding.Signed;
soundAction.Volume = 0.9f;

//Set the sound action
document.Actions.AfterOpen = soundAction;

//Save and close the PDF document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document
Dim document As New PdfDocument()
'Add a page
Dim page As PdfPage = document.Pages.Add()

'Create a sound action
Dim soundAction As New PdfSoundAction("../../Data/Startup.wav")
soundAction.Sound.Bits = 16
soundAction.Sound.Channels = PdfSoundChannels.Stereo
soundAction.Sound.Encoding = PdfSoundEncoding.Signed
soundAction.Volume = 0.9F

'Set the sound action
document.Actions.AfterOpen = soundAction

'Save and close the PDF document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//PDF supports sound action only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add a page
PdfPage page = document.Pages.Add();

//Create a sound action
FileStream fileStream = new FileStream("Startup.wav", FileMode.Open, FileAccess.Read);
PdfSoundAction soundAction = new PdfSoundAction(fileStream);
soundAction.Sound.Bits = 16;
soundAction.Sound.Channels = PdfSoundChannels.Stereo;
soundAction.Sound.Encoding = PdfSoundEncoding.Signed;
soundAction.Volume = 0.9f;

//Set the sound action
document.Actions.AfterOpen = soundAction;

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for pdf file
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

//Create a sound action
Stream stream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Startup.wav");
PdfSoundAction soundAction = new PdfSoundAction(stream);
soundAction.Sound.Bits = 16;
soundAction.Sound.Channels = PdfSoundChannels.Stereo;
soundAction.Sound.Encoding = PdfSoundEncoding.Signed;
soundAction.Volume = 0.9f;

//Set the sound action
document.Actions.AfterOpen = soundAction;

//Save the document into stream.
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Close the documents.
document.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Add-the-sound-action-to-PDF-document/).

### JavaScript action

The [PdfJavaScriptAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfJavaScriptAction.html) allows execution of **JavaScript** code embedded in the PDF document.

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

//Save the document.
MemoryStream memoryStream = new MemoryStream();
await document.SaveAsync(memoryStream);
//Close the documents.
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
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
//Defining the ContentType for pdf file
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
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Add-JavaScript-action-to-the-PDF-document/).

N> You can refer more PDF JavaScript code in **PdfJavaScriptAction** from the below developer guide.
N> [http://www.adobe.com/content/dam/Adobe/en/devnet/acrobat/pdfs/js_developer_guide.pdf](http://www.adobe.com/content/dam/Adobe/en/devnet/acrobat/pdfs/js_developer_guide.pdf)

### URI action

The [PdfUriAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfUriAction.html) allows you to create a hyperlink that can open web page in a web browser.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/A standard
PdfDocument document = new PdfDocument();

//Create a uri action
PdfUriAction uriAction = new PdfUriAction("http://www.google.com");

//Add the action to the document
document.Actions.AfterOpen = uriAction;

//Save and close the PDF document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/A standard.
Dim document As New PdfDocument()

'Create a URI action
Dim uriAction As New PdfUriAction("http://www.google.com")

'Add the action to the document
document.Actions.AfterOpen = uriAction

'Save and close the PDF document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with PDF/A standard
PdfDocument document = new PdfDocument();

//Create a URI action
PdfUriAction uriAction = new PdfUriAction("http://www.google.com");

//Add the action to the document
document.Actions.AfterOpen = uriAction;

//Save the document
MemoryStream memoryStream = new MemoryStream();
await document.SaveAsync(memoryStream);
//Close the documents
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with PDF/A standard
PdfDocument document = new PdfDocument();

//Create a URI action
PdfUriAction uriAction = new PdfUriAction("http://www.google.com");

//Add the action to the document
document.Actions.AfterOpen = uriAction;

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

//Create a new document with PDF/A standard
PdfDocument document = new PdfDocument();

//Create a URI action
PdfUriAction uriAction = new PdfUriAction("http://www.google.com");

//Add the action to the document
document.Actions.AfterOpen = uriAction;

//Save the document into stream.
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Close the documents
document.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Add-URI-action-to-the-PDF-document/).

### GoTo action

The [PdfGoToAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfGoToAction.html) displays the specified page in the current document. The location can be specified for the destination page.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add first page
PdfPage page = document.Pages.Add();
//Add second page
PdfPage secondPage = document.Pages.Add();

//Set the goto action
PdfGoToAction gotoAction = new PdfGoToAction(secondPage);
//Set destination location
gotoAction.Destination = new PdfDestination(secondPage, new PointF(0, 100));

//Add the action to the document
document.Actions.AfterOpen = gotoAction;

//Save and close the PDF document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document
Dim document As New PdfDocument()
'Add first page
Dim page As PdfPage = document.Pages.Add()
'Add second page
Dim secondPage As PdfPage = document.Pages.Add()

'Set the goto action
Dim gotoAction As New PdfGoToAction(secondPage)
'Set destination location
gotoAction.Destination = New PdfDestination(secondPage, New PointF(0, 100))

'Add the action to the document
document.Actions.AfterOpen = gotoAction

'Save and close the PDF document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add first page
PdfPage page = document.Pages.Add();
//Add second page
PdfPage secondPage = document.Pages.Add();

//Set the goto action
PdfGoToAction gotoAction = new PdfGoToAction(secondPage);
//Set destination location
gotoAction.Destination = new PdfDestination(secondPage, new PointF(0, 100));
//Add the action to the document
document.Actions.AfterOpen = gotoAction;

//Save the document
MemoryStream memoryStream = new MemoryStream();
await document.SaveAsync(memoryStream);
//Close the documents
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add first page
PdfPage page = document.Pages.Add();
//Add second page
PdfPage secondPage = document.Pages.Add();

//Set the goto action
PdfGoToAction gotoAction = new PdfGoToAction(secondPage);
//Set destination location
gotoAction.Destination = new PdfDestination(secondPage, new PointF(0, 100));

//Add the action to the document
document.Actions.AfterOpen = gotoAction;

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
//Add first page
PdfPage page = document.Pages.Add();
//Add second page
PdfPage secondPage = document.Pages.Add();

//Set the goto action
PdfGoToAction gotoAction = new PdfGoToAction(secondPage);
//Set destination location
gotoAction.Destination = new PdfDestination(secondPage, new PointF(0, 100));

//Add the action to the document
document.Actions.AfterOpen = gotoAction;

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Close the document
document.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Add-GoTo-action-to-the-PDF-document/).

### Launch action

The [PdfLaunchAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLaunchAction.html) allows execution of an external file. The following code example explains how to add a launch action in PDF document. 

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create and add new launch Action to the document
PdfLaunchAction action = new PdfLaunchAction("../../Data/logo.png");

//Add the action to the document. 
document.Actions.AfterOpen = action;

//Save and close the document
document.Save("LaunchAction.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document
Dim document As New PdfDocument()

'Create and add new launch Action to the document
Dim action As New PdfLaunchAction("../../Data/logo.png")

'Add the action to the document. 
document.Actions.AfterOpen = action

'Save and close the document
document.Save("LaunchAction.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//PDF supports launch action only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//PDF supports launch action only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//PDF supports launch action only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Add-lauch-action-to-PDF-document).

### Named action

The [PdfNamedAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfNamedAction.html) allows execution of below predefined **PDF** actions using [PdfActionDestination](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfActionDestination.html) Enum. 

* Go to next page
* Go to previous page 
* Go to first page and 
* Go to last page

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add the page
document.Pages.Add();
document.Pages.Add();

//Create a named action
PdfNamedAction namedAction = new PdfNamedAction(PdfActionDestination.LastPage);

//Add the named action
document.Actions.AfterOpen = namedAction;

//Save and close the PDF document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document
Dim document As New PdfDocument()
'Add the page
document.Pages.Add()
document.Pages.Add()

'Create a named action
Dim namedAction As New PdfNamedAction(PdfActionDestination.LastPage)

'Add the named action
document.Actions.AfterOpen = namedAction

'Save and close the PDF document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add the page
document.Pages.Add();
document.Pages.Add();

//Create a named action
PdfNamedAction namedAction = new PdfNamedAction(PdfActionDestination.LastPage);

//Add the named action
document.Actions.AfterOpen = namedAction;

//Save the document
MemoryStream memoryStream = new MemoryStream();
await document.SaveAsync(memoryStream);
//Close the documents
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add the page
document.Pages.Add();
document.Pages.Add();

//Create a named action
PdfNamedAction namedAction = new PdfNamedAction(PdfActionDestination.LastPage);

//Add the named action
document.Actions.AfterOpen = namedAction;

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add the page
document.Pages.Add();
document.Pages.Add();

//Create a named action
PdfNamedAction namedAction = new PdfNamedAction(PdfActionDestination.LastPage);

//Add the named action
document.Actions.AfterOpen = namedAction;

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Close the documents
document.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Add-named-action-to-PDF-document).

### Submit action

The [PdfSubmitAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfSubmitAction.html) allows submission of data that is entered in the PDF form using [PdfButtonField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfButtonField.html) form field. 

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPage page = document.Pages.Add();

//Create a Button field
PdfButtonField submitButton = new PdfButtonField(page, "Submit data");
submitButton.Bounds = new RectangleF(100, 60, 50, 20);
submitButton.ToolTip = "Submit";
//Add button field to the form
document.Form.Fields.Add(submitButton);

//Create a submit action. It submit the data of the form fields to the mentioned URL
PdfSubmitAction submitAction = new PdfSubmitAction("http://www.syncfusionforms.com/Submit.aspx");
submitAction.DataFormat = SubmitDataFormat.Html;
submitButton.Actions.GotFocus = submitAction;

//Save and close the PDF document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a PDF document
Dim document As New PdfDocument()
'Add a new page
Dim page As PdfPage = document.Pages.Add()

'Create a Button field.
Dim submitButton As New PdfButtonField(page, "Submit data")
submitButton.Bounds = New RectangleF(100, 60, 50, 20)
submitButton.ToolTip = "Submit"
'Add button field to the form
document.Form.Fields.Add(submitButton)

'Create a submit action. It submit the data of the form fields to the mentioned URL
Dim submitAction As New PdfSubmitAction("http:// www.example.com/Submit.aspx")
submitAction.DataFormat = SubmitDataFormat.Html
submitButton.Actions.GotFocus = submitAction

'Save and close the PDF document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPage page = document.Pages.Add();

//Create a Button field
PdfButtonField submitButton = new PdfButtonField(page, "Submit data");
submitButton.Bounds = new RectangleF(100, 60, 50, 20);
submitButton.ToolTip = "Submit";
//Add button field to the form
document.Form.Fields.Add(submitButton);

//Create a submit action. It submit the data of the form fields to the mentioned URL
PdfSubmitAction submitAction = new PdfSubmitAction("http://www.syncfusionforms.com/Submit.aspx");
submitAction.DataFormat = SubmitDataFormat.Html;
submitButton.Actions.GotFocus = submitAction;

//Save the document
MemoryStream memoryStream = new MemoryStream();
await document.SaveAsync(memoryStream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPage page = document.Pages.Add();

//Create a Button field
PdfButtonField submitButton = new PdfButtonField(page, "Submit data");
submitButton.Bounds = new RectangleF(100, 60, 50, 20);
submitButton.ToolTip = "Submit";
//Add button field to the form
document.Form.Fields.Add(submitButton);

//Create a submit action. It submit the data of the form fields to the mentioned URL
PdfSubmitAction submitAction = new PdfSubmitAction("http://www.syncfusionforms.com/Submit.aspx");
submitAction.DataFormat = SubmitDataFormat.Html;
submitButton.Actions.GotFocus = submitAction;

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

//Create a PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPage page = document.Pages.Add();

//Create a Button field
PdfButtonField submitButton = new PdfButtonField(page, "Submit data");
submitButton.Bounds = new RectangleF(100, 60, 50, 20);
submitButton.ToolTip = "Submit";
//Add button field to the form
document.Form.Fields.Add(submitButton);

//Create a submit action. It submit the data of the form fields to the mentioned URL
PdfSubmitAction submitAction = new PdfSubmitAction("http://www.google.com");
submitAction.DataFormat = SubmitDataFormat.Html;
submitButton.Actions.GotFocus = submitAction;

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Close the documents.
document.Close(true);
//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Add-submit-action-to-the-PDF-document).

### Reset action

The [PdfResetAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfResetAction.html) allows execution of reset of all the form fields in the PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPage page = document.Pages.Add();

//Create a Text box field
PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");
//Set properties to the textbox
textBoxField.BorderColor = new PdfColor(Color.Gray);
textBoxField.BorderStyle = PdfBorderStyle.Beveled;
textBoxField.Bounds = new RectangleF(80, 0, 100, 20);
textBoxField.Text = "First Name";

//Add the form field to the document
document.Form.Fields.Add(textBoxField);

//Create a Button field.
PdfButtonField clearButton = new PdfButtonField(page, "Clear");
clearButton.Bounds = new RectangleF(100, 60, 50, 20);
clearButton.ToolTip = "Clear";
//Add button field to the form
document.Form.Fields.Add(clearButton);

//Create an instance of reset action
PdfResetAction resetAction = new PdfResetAction();
clearButton.Actions.GotFocus = resetAction;

//Save and close the PDF document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a PDF document
Dim document As New PdfDocument()
'Add a new page
Dim page As PdfPage = document.Pages.Add()

'Create a Text box field.
Dim textBoxField As New PdfTextBoxField(page, "FirstName")
'Set properties to the textbox.
textBoxField.BorderColor = New PdfColor(Color.Gray)
textBoxField.BorderStyle = PdfBorderStyle.Beveled
textBoxField.Bounds = New RectangleF(80, 0, 100, 20)
textBoxField.Text = "First Name"

'Add the form field to the document
document.Form.Fields.Add(textBoxField)

'Create a Button field.
Dim clearButton As New PdfButtonField(page, "Clear")
clearButton.Bounds = New RectangleF(100, 60, 50, 20)
clearButton.ToolTip = "Clear"
'Add button field to the form
document.Form.Fields.Add(clearButton)

'Create an instance of reset action
Dim resetAction As New PdfResetAction()
clearButton.Actions.GotFocus = resetAction

'Save and close the PDF document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPage page = document.Pages.Add();

//Create a Text box field.
PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");
//Set properties to the textbox
textBoxField.BorderColor = new PdfColor(128, 128, 128);
textBoxField.BorderStyle = PdfBorderStyle.Beveled;
textBoxField.Bounds = new RectangleF(80, 0, 100, 20);
textBoxField.Text = "First Name";

//Add the form field to the document
document.Form.Fields.Add(textBoxField);

//Create a Button field
PdfButtonField clearButton = new PdfButtonField(page, "Clear");
clearButton.Bounds = new RectangleF(100, 60, 50, 20);
clearButton.ToolTip = "Clear";
//Add button field to the form 
document.Form.Fields.Add(clearButton);

//Create an instance of reset action
PdfResetAction resetAction = new PdfResetAction();
clearButton.Actions.GotFocus = resetAction;

//Save the document
MemoryStream memoryStream = new MemoryStream();
await document.SaveAsync(memoryStream);
//Close the documents
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPage page = document.Pages.Add();

//Create a Text box field
PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");
//Set properties to the textbox
textBoxField.BorderColor = new PdfColor(Color.Gray);
textBoxField.BorderStyle = PdfBorderStyle.Beveled;
textBoxField.Bounds = new RectangleF(80, 0, 100, 20);
textBoxField.Text = "First Name";

//Add the form field to the document
document.Form.Fields.Add(textBoxField);

//Create a Button field
PdfButtonField clearButton = new PdfButtonField(page, "Clear");
clearButton.Bounds = new RectangleF(100, 60, 50, 20);
clearButton.ToolTip = "Clear";
//Add button field to the form
document.Form.Fields.Add(clearButton);

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

//Create a PDF document
PdfDocument document = new PdfDocument();

//Add a new page
PdfPage page = document.Pages.Add();

//Create a Text box field.
PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");
//Set properties to the textbox
textBoxField.BorderColor = new PdfColor(Syncfusion.Drawing.Color.Gray);
textBoxField.BorderStyle = PdfBorderStyle.Beveled;
textBoxField.Bounds = new RectangleF(80, 0, 100, 20);
textBoxField.Text = "First Name";

//Add the form field to the document
document.Form.Fields.Add(textBoxField);

//Create a Button field
PdfButtonField clearButton = new PdfButtonField(page, "Clear");
clearButton.Bounds = new RectangleF(100, 60, 50, 20);
clearButton.ToolTip = "Clear";
//Add button field to the form
document.Form.Fields.Add(clearButton);

//Create an instance of reset action
PdfResetAction resetAction = new PdfResetAction();
clearButton.Actions.GotFocus = resetAction;

//Save the document into stream.
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Close the documents
document.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Reset-form-fields-in-the-PDF-document).

## Adding an action to the form field

Essential PDF provides support to add various actions to the form fields. The following code example illustrates how to add actions to the form field in PDF document using [PdfFieldActions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfFieldActions.html) class. 


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
//Set the scriptAction to submitButton
submitButton.Actions.MouseDown = scriptAction;

//Add the submit button to the new document
document.Form.Fields.Add(submitButton);

//Save document to disk
document.Save("fieldAction.pdf");
//Close the document
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

//Save the document
MemoryStream memoryStream = new MemoryStream();
await document.SaveAsync(memoryStream);
//Close the documents
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
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
PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"You are looking at Form field action of PD
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

//Add the submit button to the new document.
document.Form.Fields.Add(submitButton);

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Close the documents
document.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Adding-an-action-to-the-form-fields-in-PDF-document/).

## Adding an action to the bookmarks

Essential PDF provides support to add the various actions to the [Bookmarks](https://help.syncfusion.com/file-formats/pdf/working-with-bookmarks). The code snippet below shows how to add an URI action to bookmark.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add a page
PdfPage page = document.Pages.Add();

//Create document bookmarks
PdfBookmark bookmark = document.Bookmarks.Add("Page 1");
//Set the text style and color
bookmark.TextStyle = PdfTextStyle.Bold;
bookmark.Color = Color.Red;

//Create a Uri action
PdfUriAction uriAction = new PdfUriAction("http://www.google.com");
//Set the Uri action to bookmark
bookmark.Action = uriAction;

//Save and close the PDF document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document
Dim document As New PdfDocument()
'Add a page
Dim page As PdfPage = document.Pages.Add()

'Create document bookmarks
Dim bookmark As PdfBookmark = document.Bookmarks.Add("Page 1")
'Set the text style and color
bookmark.TextStyle = PdfTextStyle.Bold
bookmark.Color = Color.Red

'Create a Uri action
Dim uriAction As New PdfUriAction("http://www.google.com")
'Set the Uri action to the bookmark
bookmark.Action = uriAction

'Save and close the PDF document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add a page
PdfPage page = document.Pages.Add();

//Create document bookmarks
PdfBookmark bookmark = document.Bookmarks.Add("Page 1");
//Set the text style and color
bookmark.TextStyle = PdfTextStyle.Bold;
bookmark.Color = Color.FromArgb(0,255,0,0);

//Create a Uri action
PdfUriAction uriAction = new PdfUriAction("http://www.google.com");
//Set the Uri action to the bookmark 
bookmark.Action = uriAction;

//Save the document
MemoryStream memoryStream = new MemoryStream();
await document.SaveAsync(memoryStream);
//Close the documents
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(memoryStream, "fieldAction.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Add a page
PdfPage page = document.Pages.Add();

//Create document bookmarks
PdfBookmark bookmark = document.Bookmarks.Add("Page 1");
//Set the text style and color
bookmark.TextStyle = PdfTextStyle.Bold;
bookmark.Color = Color.Red;

//Create a Uri action
PdfUriAction uriAction = new PdfUriAction("http://www.google.com");
//Set the Uri action to the bookmark 
bookmark.Action = uriAction;

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document.
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

//Create document bookmarks
PdfBookmark bookmark = document.Bookmarks.Add("Page 1");
//Set the text style and color
bookmark.TextStyle = PdfTextStyle.Bold;
bookmark.Color = Syncfusion.Drawing.Color.Red;

//Create a Uri action
PdfUriAction uriAction = new PdfUriAction("http://www.google.com");
//Set the Uri action to the bookmark
bookmark.Action = uriAction;

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Close the document
document.Close(true);
//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Adding-an-action-to-the-bookmark-in-the-PDF-document).

## Add actions to the existing PDF document

To add actions to an existing PDF document, use the following code example.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Load a document from the disk.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Create JavaScript action.
PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"Hello World!!!\")");

//Add the JavaScript action.
loadedDocument.Actions.AfterOpen = scriptAction;
           
// Save and close the document.
loadedDocument.Save("Output.pdf");
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}      

'Create a new PDF document. 
Dim document As New PdfLoadedDocument("input.pdf")

'Create JavaScript action. 
Dim scriptAction As New PdfJavaScriptAction("app.alert(""Hello World!!!"")") 

'Add the JavaScript action.
 document.Actions.AfterOpen = scriptAction

'Save the document to disk.
 document.Save("PopupAnnotation.pdf") 
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a file open picker
 var picker = new FileOpenPicker();
 picker.FileTypeFilter.Add(".pdf"); 
//Browse and chose the file
 StorageFile file = await picker.PickSingleFileAsync(); 
//Create an empty PDF loaded document instance
PdfLoadedDocument document = new PdfLoadedDocument(); 
//Load or open an existing PDF document through the Open method of the PdfLoadedDocument class
await document.OpenAsync(file);

//Create JavaScript action.
PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"Hello World!!!\")"); 
//Add the JavaScript action
document.Actions.AfterOpen = scriptAction;

//Save the PDF document to stream
MemoryStream stream = new MemoryStream(); 
await document.SaveAsync(stream);
//Close the document
document.Close(true); 
//Save the stream as a PDF document file in the local machine. Refer to the PDF/UWP section for respected code samples
Save(stream, "PopupAnnotation.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document.
FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read); PdfLoadedDocument document = new PdfLoadedDocument(docStream); 

//Create JavaScript action
PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"Hello World!!!\")"); 

//Add the JavaScript action
document.Actions.AfterOpen = scriptAction;

//Save the document into stream
MemoryStream stream = new MemoryStream(); 
document.Save(stream); stream.Position = 0;
//Close the document.
document.Close(true);
//Define the ContentType for a pdf file
string contentType = "application/pdf"; 
//Define the file name.
string fileName = "output.pdf"; 
//Create a FileContentResult object by using the file contents, content type, and file name. 
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream. 
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf"); PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Create JavaScript action 
PdfJavaScriptAction scriptAction = new PdfJavaScriptAction("app.alert(\"Hello World!!!\")"); 
//Add the JavaScript action
document.Actions.AfterOpen = scriptAction;

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true); 
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer to the PDF/Xamarin section for the respective code samples
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Actions/Add-actions-to-the-existing-PDF-document).

N> The action assigned to the bookmark works only when destination of bookmark is not set.

