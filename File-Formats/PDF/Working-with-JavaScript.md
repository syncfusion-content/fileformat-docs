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

{% highlight c# tabtitle="C# [Cross-platform]" %}

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
//Defining the content type for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/JavaScript/Add-the-JavaScript-action-to-the-PDF-document).

## JavaScript action to the form fields

You can add the JavaScript actions to various form fields using [PdfJavaScriptAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfJavaScriptAction.html) instance. The [PdfFieldActions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfFieldActions.html) class is used to create form field actions. 

The following code snippet illustrate this.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}	

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

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/JavaScript/Add-JavaScript-action-to-the-form-fields-in-a-PDF).

## JavaScript in 3D Annotation

The 3D Annotations are used to represent 3D artworks in a PDF document. You can add a JavaScript code to 3D annotation using the [OnInstantiate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.Pdf3DAnnotation.html#Syncfusion_Pdf_Interactive_Pdf3DAnnotation_OnInstantiate) property in [Pdf3DAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.Pdf3DAnnotation.html) instance. The JavaScript script is executed when the 3D artwork is instantiated. The following code snippet illustrate this.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Creates a new page
PdfPage page = document.Pages.Add();

//Load 3D annotation as stream
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
//Defining the content type for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "3DAnnotation.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}

## Add/Modify JavaScript actions to the PDF

Add or modify the JavaScript action in a [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html). The below code example shows how to add/modify JavaScript code using [PdfJavaScriptAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfJavaScriptAction.html) class to an existing PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Change the javascript action in a pdf document.
loadedDocument.Actions.AfterOpen= new PdfJavaScriptAction("app.alert(\"Modified Script!\")");

//Save the document.
loadedDocument.Save("Output.pdf");
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/JavaScript/Add-JavaScript-to-3D-annotation-in-a-PDF-document).

## Types of JavaScript actions

The pdf will generate trigger with the javascript actions in the following places.

<table>
<tr>
<th style="font-size:14px">Action Type 
</th>
<th style="font-size:14px">Description
</th>
</tr>
<tr>
<td>document.Actions.AfterOpen	</td>
<td>A JavaScript action will be performed after opening the document</td>
</tr>
<tr>
<td>document.Actions.BeforeClose</td>
<td>A JavaScript action will be performed before closing the document</td>
</tr>
<tr>
<td>document.Actions.AfterSave</td>
<td>	A JavaScript action will be performed after saving the document</td>
</tr>
<tr>
<td>document.Actions.BeforeSave</td>
<td>	A JavaScript action will be performed before saving the document</td>
</tr>
<tr>
<td>document.Actions.AfterPrint	</td>
<td>A JavaScript action will be performed after printing the document</td>
</tr>
<tr>
<td>document.Actions.BeforePrint</td>
<td>	A JavaScript action will be performed before printing the document</td>
</tr>
</table>

## Types of Mouseover actions

The pdf will generate trigger with the javascript actions on the form fields in the places listed below.

<table>
<tr>
<th style="font-size:14px">Action Type 
</th>
<th style="font-size:14px">Description
</th>
</tr>
<tr>
<td>
submitButton.Actions.MouseDown</td>
<td>Gets or sets the action to be performed when the mouse button is pressed inside the annotation’s active area.</td>
</tr>
<tr>
<td>submitButton.Actions.MouseUp</td>
<td>	Gets or sets the action to be performed when the mouse button is released inside the annotation’s active area.</td>
</tr>
<tr>
<td>submitButton.Actions.MouseEnter</td>
<td>	Gets or sets the action to be performed when the cursor enters the annotation’s active area.</td>
</tr>
<tr>
<td>submitButton.Actions.MouseLeave</td>
<td>	Gets or sets the action to be performed when the cursor exits the annotation’s active area.</td>
</tr>
<tr>
<td>submitButton.Actions.GotFocus</td>
<td>	Gets or sets the action to be performed when the annotation receives the input focus.</td>
</tr>
<tr>
<td>submitButton.Actions.LostFocus</td>
<td>	Gets or sets the action to be performed when the annotation loses the input focus.</td>
</tr>
</table>
