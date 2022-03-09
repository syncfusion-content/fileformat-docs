---
title: Working with XFA Forms | Syncfusion
description: This section explains how to create, fill, edit and modify the forms fields in the XFA document
platform: file-formats
control: PDF
documentation: UG
---
# Working with XFA

XFA stands for XML Forms Architecture, dynamic forms are based on a XML specification. Essential PDF supports both the dynamic and static XFA forms.

* In a static form the form’s appearance and layout is fixed, regardless of the field content.
* Dynamic forms can change in appearance in several ways in response to changes in the data.

## Creating a new XFA form

Essential PDF allows you to create and manipulate the XFA form in PDF document by using [PdfXfaDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaDocument.html) and [PdfXfaForm](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaForm.html) classes. The [PdfXfaFieldCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaFieldCollection.html) class represents the entire field collection of the XFA form.

### Adding a new page to the XFA document

The following code sample explains you on how to add a new page in a PDF XFA document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");           

//Add the field to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//Close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a text element and add the properties

Dim textElement As New PdfXfaTextElement("Hello World!")

'Add the field to the XFA form

mainForm.Fields.Add(textElement)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'Close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Add the field to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Add the field to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Add the field to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


N> XFA documents are created based on the flow layout, so the pages are sequentially added if the doesn’t have space to fit the field it will automatically move on the next page, so we can’t specify the page and page numbers.
N> PDF supports XFA forms only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, UWP platforms, Xamarin (.NETStandard 2.0 and above), and ASP.NET Core (.NETStandard 2.0 and above).


### Adding the XFA document settings

Essential PDF supports various XFA page setting options through [PdfXfaPageSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaPageSettings.html) class, to control the page display.

The below sample illustrates how to create a new PDF document with XFA page size.

{% tabs %}

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Set the page size

document.PageSettings.PageSize = PdfPageSize.A4

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a text element and add the properties

Dim textElement As New PdfXfaTextElement("Hello World!!!")

'Set font

textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)

'Add the text element to the XFA form

mainForm.Fields.Add(textElement)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document.

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document.

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


You can create a custom page size to the PDF document by using following code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = new SizeF(500,700);

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Set the page size

document.PageSettings.PageSize = New SizeF(500,700)

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a text element and add the properties

Dim textElement As New PdfXfaTextElement("Hello World!!!")

'Set font

textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)

'Add the text element to the XFA form

mainForm.Fields.Add(textElement)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = new SizeF(500, 700);

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = new SizeF(500, 700);

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = new SizeF(500, 700);

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


You can change page orientation from portrait to landscape by using the following code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = new SizeF(500,700);

//Change the page orientation to landscape

document.PageSettings. PageOrientation = PdfXfaPageOrientation.Landscape;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Set the page size

document.PageSettings.PageSize = New SizeF(500,700)

'Change the page orientation to landscape

document.PageSettings.PageOrientation = PdfXfaPageOrientation.Landscape

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a text element and add the properties

Dim textElement As New PdfXfaTextElement("Hello World!!!")

'Set font

textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)

'Add the text element to the XFA form

mainForm.Fields.Add(textElement)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = new SizeF(500, 700);

//Change the page orientation to landscape

document.PageSettings.PageOrientation = PdfXfaPageOrientation.Landscape;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = new SizeF(500, 700);

//Change the page orientation to landscape

document.PageSettings.PageOrientation = PdfXfaPageOrientation.Landscape;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = new SizeF(500, 700);

//Change the page orientation to landscape

document.PageSettings.PageOrientation = PdfXfaPageOrientation.Landscape;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Creating dynamic XFA forms

The below sample illustrates how to create a dynamic XFA forms.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document dynamic form

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Set the page size

document.PageSettings.PageSize = PdfPageSize.A4

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1", xfaPage,xfaPage.GetClientSize().Width)

'Create a text element and add the properties

Dim textElement As New PdfXfaTextElement("Hello World!!!")

'Set font

textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)

'Add the text element to the XFA form

mainForm.Fields.Add(textElement)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document dynamic form

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASp.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Creating static XFA forms

The below sample illustrates how to create a static XFA forms.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document with static form

document.Save("XfaForm.pdf",PdfXfaType.Static);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Set the page size

document.PageSettings.PageSize = PdfPageSize.A4

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a text element and add the properties

Dim textElement As New PdfXfaTextElement("Hello World!!!")

'Set font

textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)

'Add the text element to the XFA form

mainForm.Fields.Add(textElement)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document with static form

document.Save("XfaForm.pdf",PdfXfaType.Static)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Static);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Static);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file nam

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Set the page size

document.PageSettings.PageSize = PdfPageSize.A4;

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Static);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Creating XFA form fields

### Adding the XFA text box field.

The below code snippet illustrates how to add a textbox field to a new PDF document using [PdfXfaTextBoxField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaTextBoxField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();   

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName",new SizeF(200,20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a textbox field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("FirstName",New SizeF(200,20))

'Set the caption text

textBoxField.Caption.Text = "First Name"

'Set the tool tip

textBoxField.ToolTip = "First Name"

'Add the field to the XFA form

mainForm.Fields.Add(textBoxField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add a textbox field to an existing PDF document

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the existing XFA form

loadedForm.Fields.Add(textBoxField);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a textbox field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("FirstName", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "First Name"

'Set the tool tip

textBoxField.ToolTip = "First Name"

'Add the field to the existing XFA form

loadedForm.Fields.Add(textBoxField)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the existing XFA form

loadedForm.Fields.Add(textBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASp.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the existing XFA form

loadedForm.Fields.Add(textBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the existing XFA form

loadedForm.Fields.Add(textBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA numeric field

The below code snippet illustrates how to add a numeric field to a new PDF document using [PdfXfaNumericField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaNumericField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField",new SizeF(200,20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Add the field to the XFA form

mainForm.Fields.Add(numericField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a numeric field and add the properties

Dim numericField As New PdfXfaNumericField("numericField",New SizeF(200,20))

'Set the caption text

numericField.Caption.Text = "Numeric Field"

'Add the field to the XFA form

mainForm.Fields.Add(numericField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Add the field to the XFA form

mainForm.Fields.Add(numericField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Add the field to the XFA form

mainForm.Fields.Add(numericField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Add the field to the XFA form

mainForm.Fields.Add(numericField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add the numeric field to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField",new SizeF(200,20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Add the field to the existing XFA form

loadedForm.Fields.Add(numericField);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a numeric field and add the properties

Dim numericField As New PdfXfaNumericField("numericField",New SizeF(200,20))

'Set the caption text

numericField.Caption.Text = "Numeric Field"

'Add the field to the existing XFA form

loadedForm.Fields.Add(numericField)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form
PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Add the field to the existing XFA form

loadedForm.Fields.Add(numericField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Add the field to the existing XFA form

loadedForm.Fields.Add(numericField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Add the field to the existing XFA form

loadedForm.Fields.Add(numericField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA combo box field

The below code snippet illustrates how to add a combo box field to a new PDF document using [PdfXfaComboBoxField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaComboBoxField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();   

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a combo box field and add the properties

PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));

//Set the caption text

comboBoxField.Caption.Text = "Job Title";

//Add the combo box items

comboBoxField.Items.Add("Development.");

comboBoxField.Items.Add("Support.");

comboBoxField.Items.Add("Documentation.");

//Add the field to the XFA form

mainForm.Fields.Add(comboBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a combo box field and add the properties

PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));

//Set the caption text

comboBoxField.Caption.Text = "Job Title";

//Add the combo box items

comboBoxField.Items.Add("Development.");

comboBoxField.Items.Add("Support.");

comboBoxField.Items.Add("Documentation.");

//Add the field to the XFA form

mainForm.Fields.Add(comboBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a combo box field and add the properties

PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));

//Set the caption text

comboBoxField.Caption.Text = "Job Title";

//Add the combo box items

comboBoxField.Items.Add("Development.");

comboBoxField.Items.Add("Support.");

comboBoxField.Items.Add("Documentation.");

//Add the field to the XFA form

mainForm.Fields.Add(comboBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a combo box field and add the properties

PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));

//Set the caption text

comboBoxField.Caption.Text = "Job Title";

//Add the combo box items

comboBoxField.Items.Add("Development.");

comboBoxField.Items.Add("Support.");

comboBoxField.Items.Add("Documentation.");

//Add the field to the XFA form

mainForm.Fields.Add(comboBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a combo box field and add the properties

PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));

//Set the caption text

comboBoxField.Caption.Text = "Job Title";

//Add the combo box items

comboBoxField.Items.Add("Development.");

comboBoxField.Items.Add("Support.");

comboBoxField.Items.Add("Documentation.");

//Add the field to the XFA form

mainForm.Fields.Add(comboBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add the combo box field to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a combo box field and add the properties

PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));

//Set the caption text

comboBoxField.Caption.Text = "Job Title";

//Add the combo box items

comboBoxField.Items.Add("Development.");

comboBoxField.Items.Add("Support.");

comboBoxField.Items.Add("Documentation.");

//Add the field to the existing XFA form

loadedForm.Fields.Add(comboBoxField);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a combo box field and add the properties

Dim comboBoxField As New PdfXfaComboBoxField("comboField", New SizeF(200, 20))

'Set the caption text

comboBoxField.Caption.Text = "Job Title"

'Add the combo box items

comboBoxField.Items.Add("Development.")

comboBoxField.Items.Add("Support.")

comboBoxField.Items.Add("Documentation.")

'Add the field to the existing XFA form

loadedForm.Fields.Add(comboBoxField)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a combo box field and add the properties

PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));

//Set the caption text

comboBoxField.Caption.Text = "Job Title";

//Add the combo box items

comboBoxField.Items.Add("Development.");

comboBoxField.Items.Add("Support.");

comboBoxField.Items.Add("Documentation.");

//Add the field to the existing XFA form

loadedForm.Fields.Add(comboBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASp.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a combo box field and add the properties

PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));

//Set the caption text

comboBoxField.Caption.Text = "Job Title";

//Add the combo box items

comboBoxField.Items.Add("Development.");

comboBoxField.Items.Add("Support.");

comboBoxField.Items.Add("Documentation.");

//Add the field to the existing XFA form

loadedForm.Fields.Add(comboBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a combo box field and add the properties

PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));

//Set the caption text

comboBoxField.Caption.Text = "Job Title";

//Add the combo box items

comboBoxField.Items.Add("Development.");

comboBoxField.Items.Add("Support.");

comboBoxField.Items.Add("Documentation.");

//Add the field to the existing XFA form

loadedForm.Fields.Add(comboBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA list box field

The below code snippet illustrates how to add a list box field to a new PDF document using [PdfXfaListBoxField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaListBoxField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a list box field and add the properties

PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("listBoxField", new SizeF(150, 50));

//Set the caption text

listBoxField.Caption.Text = "Known Languages";

listBoxField.Caption.Position = PdfXfaPosition.Top;

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;

//Add the list box items

listBoxField.Items.Add("English");

listBoxField.Items.Add("French");

listBoxField.Items.Add("German");

//Add the field to the XFA form

mainForm.Fields.Add(listBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a list box field and add the properties

Dim listBoxField As New PdfXfaListBoxField("listBoxField", New SizeF(150, 50))

'Set the caption text

listBoxField.Caption.Text = "Known Languages"

listBoxField.Caption.Position = PdfXfaPosition.Top

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center

'Add the list box items

listBoxField.Items.Add("English")

listBoxField.Items.Add("French")

listBoxField.Items.Add("German")

'Add the field to the XFA form

mainForm.Fields.Add(listBoxField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a list box field and add the properties

PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("listBoxField", new SizeF(150, 50));

//Set the caption text

listBoxField.Caption.Text = "Known Languages";

listBoxField.Caption.Position = PdfXfaPosition.Top;

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;

//Add the list box items

listBoxField.Items.Add("English");

listBoxField.Items.Add("French");

listBoxField.Items.Add("German");

//Add the field to the XFA form

mainForm.Fields.Add(listBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a list box field and add the properties

PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("listBoxField", new SizeF(150, 50));

//Set the caption text

listBoxField.Caption.Text = "Known Languages";

listBoxField.Caption.Position = PdfXfaPosition.Top;

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;

//Add the list box items

listBoxField.Items.Add("English");

listBoxField.Items.Add("French");

listBoxField.Items.Add("German");

//Add the field to the XFA form

mainForm.Fields.Add(listBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a list box field and add the properties

PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("listBoxField", new SizeF(150, 50));

//Set the caption text

listBoxField.Caption.Text = "Known Languages";

listBoxField.Caption.Position = PdfXfaPosition.Top;

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;

//Add the list box items

listBoxField.Items.Add("English");

listBoxField.Items.Add("French");

listBoxField.Items.Add("German");

//Add the field to the XFA form

mainForm.Fields.Add(listBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add the list box field to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a list box field and add the properties

PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("listBoxField", new SizeF(150, 50));

//Set the caption text

listBoxField.Caption.Text = "Known Languages";

listBoxField.Caption.Position = PdfXfaPosition.Top;

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;

//Add the list box items

listBoxField.Items.Add("English");

listBoxField.Items.Add("French");

listBoxField.Items.Add("German");

//Add the field to the existing XFA form

loadedForm.Fields.Add(listBoxField);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}



'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a list box field and add the properties

Dim listBoxField As New PdfXfaListBoxField("listBoxField", New SizeF(150, 50))

'Set the caption text

listBoxField.Caption.Text = "Known Languages"

listBoxField.Caption.Position = PdfXfaPosition.Top

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center

'Add the list box items

listBoxField.Items.Add("English")

listBoxField.Items.Add("French")

listBoxField.Items.Add("German")

'Add the field to the existing XFA form

loadedForm.Fields.Add(listBoxField)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a list box field and add the properties

PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("listBoxField", new SizeF(150, 50));

//Set the caption text

listBoxField.Caption.Text = "Known Languages";

listBoxField.Caption.Position = PdfXfaPosition.Top;

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;

//Add the list box items

listBoxField.Items.Add("English");

listBoxField.Items.Add("French");

listBoxField.Items.Add("German");

//Add the field to the existing XFA form

loadedForm.Fields.Add(listBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASp.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a list box field and add the properties

PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("listBoxField", new SizeF(150, 50));

//Set the caption text

listBoxField.Caption.Text = "Known Languages";

listBoxField.Caption.Position = PdfXfaPosition.Top;

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;

//Add the list box items

listBoxField.Items.Add("English");

listBoxField.Items.Add("French");

listBoxField.Items.Add("German");

//Add the field to the existing XFA form

loadedForm.Fields.Add(listBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a list box field and add the properties

PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("listBoxField", new SizeF(150, 50));

//Set the caption text

listBoxField.Caption.Text = "Known Languages";

listBoxField.Caption.Position = PdfXfaPosition.Top;

listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;

//Add the list box items

listBoxField.Items.Add("English");

listBoxField.Items.Add("French");

listBoxField.Items.Add("German");

//Add the field to the existing XFA form

loadedForm.Fields.Add(listBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding XFA check box field

The below code snippet illustrates how to add a check box field to a new PDF document using [PdfXfaCheckBoxField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaCheckBoxField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a check box field and add the properties

PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkBoxField", new SizeF(100, 20));

//Set the caption text

checkBoxField.Caption.Text = "Check box Field";

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;

//Add the field to the XFA form

mainForm.Fields.Add(checkBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a check box field and add the properties

Dim checkBoxField As New PdfXfaCheckBoxField("checkBoxField", New SizeF(100, 20))

'Set the caption text

checkBoxField.Caption.Text = "Check box Field"

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross

'Add the field to the XFA form

mainForm.Fields.Add(checkBoxField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a check box field and add the properties

PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkBoxField", new SizeF(100, 20));

//Set the caption text

checkBoxField.Caption.Text = "Check box Field";

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;

//Add the field to the XFA form

mainForm.Fields.Add(checkBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a check box field and add the properties

PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkBoxField", new SizeF(100, 20));

//Set the caption text

checkBoxField.Caption.Text = "Check box Field";

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;

//Add the field to the XFA form

mainForm.Fields.Add(checkBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a check box field and add the properties

PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkBoxField", new SizeF(100, 20));

//Set the caption text

checkBoxField.Caption.Text = "Check box Field";

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;

//Add the field to the XFA form

mainForm.Fields.Add(checkBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add the check box field to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a check box field and add the properties

PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkBoxField", new SizeF(100, 20));

//Set the caption text

checkBoxField.Caption.Text = "Check box Field";

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;

//Add the field to the existing XFA form

loadedForm.Fields.Add(checkBoxField);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a check box field and add the properties

Dim checkBoxField As New PdfXfaCheckBoxField("checkBoxField", New SizeF(100, 20))

'Set the caption text

checkBoxField.Caption.Text = "Check box Field"

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross

'Add the field to the existing XFA form

loadedForm.Fields.Add(checkBoxField)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a check box field and add the properties

PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkBoxField", new SizeF(100, 20));

//Set the caption text

checkBoxField.Caption.Text = "Check box Field";

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;

//Add the field to the existing XFA form

loadedForm.Fields.Add(checkBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a check box field and add the properties

PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkBoxField", new SizeF(100, 20));

//Set the caption text

checkBoxField.Caption.Text = "Check box Field";

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;

//Add the field to the existing XFA form

loadedForm.Fields.Add(checkBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a check box field and add the properties

PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkBoxField", new SizeF(100, 20));

//Set the caption text

checkBoxField.Caption.Text = "Check box Field";

checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;

//Add the field to the existing XFA form

loadedForm.Fields.Add(checkBoxField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}
 
 
### Adding the XFA radio button field

The below code snippet illustrates how to add a radio button field to a new PDF document using [PdfXfaRadioButtonField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaRadioButtonField.html) class and add it into [PdfXfaRadioButtonGroup](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaRadioButtonGroup.html).

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a radio button group

PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");

group.FlowDirection = PdfXfaFlowDirection.Vertical;

//Create a radio button field and add the properties

PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));

//Set the caption text

radioButtonField1.Caption.Text = "Male";

PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));

radioButtonField2.Caption.Text = "Female";

//Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1);

group.Items.Add(radioButtonField2);

//Add the field to the XFA form

mainForm.Fields.Add(group);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a radio button group

Dim group As New PdfXfaRadioButtonGroup("radioGroup")

group.FlowDirection = PdfXfaFlowDirection.Vertical

'Create a radio button field and add the properties

Dim radioButtonField1 As New PdfXfaRadioButtonField("r1", New SizeF(80, 20))

'Set the caption text

radioButtonField1.Caption.Text = "Male"

Dim radioButtonField2 As New PdfXfaRadioButtonField("r2", New SizeF(80, 20))

radioButtonField2.Caption.Text = "Female"

'Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1)

group.Items.Add(radioButtonField2)

'Add the field to the XFA form

mainForm.Fields.Add(group)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a radio button group

PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");

group.FlowDirection = PdfXfaFlowDirection.Vertical;

//Create a radio button field and add the properties

PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));

//Set the caption text

radioButtonField1.Caption.Text = "Male";

PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));

radioButtonField2.Caption.Text = "Female";

//Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1);

group.Items.Add(radioButtonField2);

//Add the field to the XFA form

mainForm.Fields.Add(group);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a radio button group

PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");

group.FlowDirection = PdfXfaFlowDirection.Vertical;

//Create a radio button field and add the properties

PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));

//Set the caption text

radioButtonField1.Caption.Text = "Male";

PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));

radioButtonField2.Caption.Text = "Female";

//Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1);

group.Items.Add(radioButtonField2);

//Add the field to the XFA form

mainForm.Fields.Add(group);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a radio button group

PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");

group.FlowDirection = PdfXfaFlowDirection.Vertical;

//Create a radio button field and add the properties

PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));

//Set the caption text

radioButtonField1.Caption.Text = "Male";

PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));

radioButtonField2.Caption.Text = "Female";

//Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1);

group.Items.Add(radioButtonField2);

//Add the field to the XFA form

mainForm.Fields.Add(group);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add the radio button field to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form.

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a radio button group

PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");

group.FlowDirection = PdfXfaFlowDirection.Vertical;

//Create a radio button field and add the properties

PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));

//Set the caption text

radioButtonField1.Caption.Text = "Male";

PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));

radioButtonField2.Caption.Text = "Female";

//Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1);

group.Items.Add(radioButtonField2);

//Add the field to the existing XFA form

loadedForm.Fields.Add(group);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a radio button group 

Dim group As New PdfXfaRadioButtonGroup("radioGroup")

group.FlowDirection = PdfXfaFlowDirection.Vertical

'Create a radio button field and add the properties

Dim radioButtonField1 As New PdfXfaRadioButtonField("r1", New SizeF(80, 20))

'Set the caption text

radioButtonField1.Caption.Text = "Male"

Dim radioButtonField2 As New PdfXfaRadioButtonField("r2", New SizeF(80, 20))

radioButtonField2.Caption.Text = "Female"

'Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1)

group.Items.Add(radioButtonField2)

'Add the field to the existing XFA form

loadedForm.Fields.Add(group)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a radio button group

PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");

group.FlowDirection = PdfXfaFlowDirection.Vertical;

//Create a radio button field and add the properties

PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));

//Set the caption text

radioButtonField1.Caption.Text = "Male";

PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));

radioButtonField2.Caption.Text = "Female";

//Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1);

group.Items.Add(radioButtonField2);

//Add the field to the existing XFA form

loadedForm.Fields.Add(group);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a radio button group

PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");

group.FlowDirection = PdfXfaFlowDirection.Vertical;

//Create a radio button field and add the properties

PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));

//Set the caption text

radioButtonField1.Caption.Text = "Male";

PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));

radioButtonField2.Caption.Text = "Female";

//Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1);

group.Items.Add(radioButtonField2);

//Add the field to the existing XFA form

loadedForm.Fields.Add(group);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a radio button group

PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");

group.FlowDirection = PdfXfaFlowDirection.Vertical;

//Create a radio button field and add the properties

PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));

//Set the caption text

radioButtonField1.Caption.Text = "Male";

PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));

radioButtonField2.Caption.Text = "Female";

//Add the radio button fields to the radio button group

group.Items.Add(radioButtonField1);

group.Items.Add(radioButtonField2);

//Add the field to the existing XFA form

loadedForm.Fields.Add(group);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA date time field

The below code snippet illustrates how to add a date time field to a new PDF document using [PdfXfaDateTimeField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaDateTimeField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();   

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date Time Field";

//Set the tool tip

dateTimeField.ToolTip = "Date Time";

//Add the field to the XFA form

mainForm.Fields.Add(dateTimeField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a date time field and add the properties

Dim dateTimeField As New PdfXfaDateTimeField("date", New SizeF(200, 20))

'Set the caption text

dateTimeField.Caption.Text = "Date Time Field"

'Set the tool tip

dateTimeField.ToolTip = "Date Time"

'Add the field to the XFA form

mainForm.Fields.Add(dateTimeField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date Time Field";

//Set the tool tip

dateTimeField.ToolTip = "Date Time";

//Add the field to the XFA form

mainForm.Fields.Add(dateTimeField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date Time Field";

//Set the tool tip

dateTimeField.ToolTip = "Date Time";

//Add the field to the XFA form

mainForm.Fields.Add(dateTimeField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date Time Field";

//Set the tool tip

dateTimeField.ToolTip = "Date Time";

//Add the field to the XFA form

mainForm.Fields.Add(dateTimeField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add the date time field to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date Time Field";

//Set the tool tip

dateTimeField.ToolTip = "Date Time";

//Add the field to the existing XFA form

loadedForm.Fields.Add(dateTimeField);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a date time field and add the properties

Dim dateTimeField As New PdfXfaDateTimeField("date", New SizeF(200, 20))

'Set the caption text

dateTimeField.Caption.Text = "Date Time Field"

'Set the tool tip

dateTimeField.ToolTip = "Date Time"

'Add the field to the existing XFA form

loadedForm.Fields.Add(dateTimeField)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date Time Field";

//Set the tool tip

dateTimeField.ToolTip = "Date Time";

//Add the field to the existing XFA form

loadedForm.Fields.Add(dateTimeField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date Time Field";

//Set the tool tip

dateTimeField.ToolTip = "Date Time";

//Add the field to the existing XFA form

loadedForm.Fields.Add(dateTimeField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date Time Field";

//Set the tool tip

dateTimeField.ToolTip = "Date Time";

//Add the field to the existing XFA form

loadedForm.Fields.Add(dateTimeField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA button field

The below code snippet illustrates how to add a button field to a new PDF document using [PdfXfaButtonField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaButtonField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();   

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a button field and add the properties

PdfXfaButtonField buttonField = new PdfXfaButtonField("buttonField", new SizeF(70, 20));

//Set the caption text

buttonField.Content = "Click";

//Add the field to the XFA form

mainForm.Fields.Add(buttonField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a button field and add the properties

Dim buttonField As New PdfXfaButtonField("buttonField", New SizeF(70, 20))

'Set the caption text

buttonField.Content = "Click"

'Add the field to the XFA form

mainForm.Fields.Add(buttonField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a button field and add the properties

PdfXfaButtonField buttonField = new PdfXfaButtonField("buttonField", new SizeF(70, 20));

//Set the caption text

buttonField.Content = "Click";

//Add the field to the XFA form

mainForm.Fields.Add(buttonField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a button field and add the properties

PdfXfaButtonField buttonField = new PdfXfaButtonField("buttonField", new SizeF(70, 20));

//Set the caption text

buttonField.Content = "Click";

//Add the field to the XFA form

mainForm.Fields.Add(buttonField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a button field and add the properties

PdfXfaButtonField buttonField = new PdfXfaButtonField("buttonField", new SizeF(70, 20));

//Set the caption text

buttonField.Content = "Click";

//Add the field to the XFA form

mainForm.Fields.Add(buttonField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add the button field to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a button field and add the properties

PdfXfaButtonField buttonField = new PdfXfaButtonField("buttonField", new SizeF(70, 20));

//Set the caption text

buttonField.Content = "Click";

//Add the field to the existing XFA form

loadedForm.Fields.Add(buttonField);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a button field and add the properties

Dim buttonField As New PdfXfaButtonField("buttonField", New SizeF(70, 20))

'Set the caption text

buttonField.Content = "Click"

'Add the field to the existing XFA form

loadedForm.Fields.Add(buttonField)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()


{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a button field and add the properties

PdfXfaButtonField buttonField = new PdfXfaButtonField("buttonField", new SizeF(70, 20));

//Set the caption text

buttonField.Content = "Click";

//Add the field to the existing XFA form

loadedForm.Fields.Add(buttonField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a button field and add the properties

PdfXfaButtonField buttonField = new PdfXfaButtonField("buttonField", new SizeF(70, 20));

//Set the caption text

buttonField.Content = "Click";

//Add the field to the existing XFA form

loadedForm.Fields.Add(buttonField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a button field and add the properties

PdfXfaButtonField buttonField = new PdfXfaButtonField("buttonField", new SizeF(70, 20));

//Set the caption text

buttonField.Content = "Click";

//Add the field to the existing XFA form

loadedForm.Fields.Add(buttonField);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA text element

The below code snippet illustrates how to add a text element to a new PDF document using [PdfXfaTextElement](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaTextElement.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();   

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a text element and add the properties

Dim textElement As New PdfXfaTextElement("Hello World!")

'Set font

textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)

'Add the text element to the XFA form

mainForm.Fields.Add(textElement)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form

mainForm.Fields.Add(textElement);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add a text element to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a text element and add the properties

PdfXfaTextElement textElement  = new PdfXfaTextElement("Hello World!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the existing XFA form

loadedForm.Fields.Add(textElement);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a text element and add the properties

Dim textElement As New PdfXfaTextElement("Hello World!")

'Set font

textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)


'Add the text element to the existing XFA form

loadedForm.Fields.Add(textElement)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the existing XFA form

loadedForm.Fields.Add(textElement);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the existing XFA form

loadedForm.Fields.Add(textElement);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a text element and add the properties

PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");

//Set font

textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the existing XFA form

loadedForm.Fields.Add(textElement);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA rectangle field

The below code snippet illustrates how to add the rectangle field to a new PDF document using [PdfXfaRectangleField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaRectangleField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();   

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a rectangle field and add the properties

PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1",new SizeF (100,50));

//Set the fill color

rectangle.Border.FillColor = new PdfXfaSolidBrush(Color.Red);

//Add the rectangle field to the XFA form

mainForm.Fields.Add(rectangle);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a rectangle field and add the properties

Dim rectangle As New PdfXfaRectangleField("rect1",New SizeF(100,50))

'Set the fill color

rectangle.Border.FillColor = New PdfXfaSolidBrush(Color.Red)

'Add the rectangle field to the XFA form

mainForm.Fields.Add(rectangle)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a rectangle field and add the properties

PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1", new SizeF(100, 50));

//Set the fill color

rectangle.Border.FillColor = new PdfXfaSolidBrush(Color.FromArgb(0,255,0,0));

//Add the rectangle field to the XFA form

mainForm.Fields.Add(rectangle);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf"); 



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a rectangle field and add the properties

PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1", new SizeF(100, 50));

//Set the fill color

rectangle.Border.FillColor = new PdfXfaSolidBrush(Color.FromArgb(0,255,0,0));

//Add the rectangle field to the XFA form

mainForm.Fields.Add(rectangle);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a rectangle field and add the properties

PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1", new SizeF(100, 50));

//Set the fill color

rectangle.Border.FillColor = new PdfXfaSolidBrush(Syncfusion.Drawing.Color.FromArgb(0,255,0,0));

//Add the rectangle field to the XFA form

mainForm.Fields.Add(rectangle);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add the rectangle field to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a rectangle field and add the properties

PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1", new SizeF(100, 50));

//Set the fill color

rectangle.Border.FillColor = new PdfXfaSolidBrush(Color.Red);

//Add the rectangle to the existing XFA form.

loadedForm.Fields.Add(rectangle);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a rectangle field and add the properties

Dim rectangle As New PdfXfaRectangleField("rect1", New SizeF(100, 50))

'Set the fill color

rectangle.Border.FillColor = New PdfXfaSolidBrush(Color.Red)

'Add the rectangle to the existing XFA form

loadedForm.Fields.Add(rectangle)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a rectangle field and add the properties

PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1", new SizeF(100, 50));

//Set the fill color

rectangle.Border.FillColor = new PdfXfaSolidBrush(Color.FromArgb(0,255,0,0));

//Add the rectangle to the existing XFA form

loadedForm.Fields.Add(rectangle);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a rectangle field and add the properties

PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1", new SizeF(100, 50));

//Set the fill color

rectangle.Border.FillColor = new PdfXfaSolidBrush(Color.FromArgb(0,255,0,0));

//Add the rectangle to the existing XFA form

loadedForm.Fields.Add(rectangle);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a rectangle field and add the properties

PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1", new SizeF(100, 50));

//Set the fill color

rectangle.Border.FillColor = new PdfXfaSolidBrush(Syncfusion.Drawing.Color.FromArgb(0,255,0,0));

//Add the rectangle to the existing XFA form

loadedForm.Fields.Add(rectangle);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA circle field

The below code snippet illustrates how to add the circle field to a new PDF document using [PdfXfaCircleField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaCircleField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();   

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a circle field and add the properties

PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));

//Set the fill color

circle.Border.FillColor = new PdfXfaSolidBrush(Color.Red);

//Add the text element to the XFA form

mainForm.Fields.Add(circle);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a circle field and add the properties

Dim circle As New PdfXfaCircleField("circle", New SizeF(100, 100))

'Set the fill color

circle.Border.FillColor = New PdfXfaSolidBrush(Color.Red)

'Add the text element to the XFA form

mainForm.Fields.Add(circle)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a circle field and add the properties

PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));

//Set the fill color

circle.Border.FillColor = new PdfXfaSolidBrush(Color.FromArgb(0,255,0,0));

//Add the text element to the XFA form

mainForm.Fields.Add(circle);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a circle field and add the properties

PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));

//Set the fill color

circle.Border.FillColor = new PdfXfaSolidBrush(Color.FromArgb(0,255,0,0));

//Add the text element to the XFA form

mainForm.Fields.Add(circle);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a circle field and add the properties

PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));

//Set the fill color

circle.Border.FillColor = new PdfXfaSolidBrush(Syncfusion.Drawing.Color.FromArgb(0,255,0,0));

//Add the text element to the XFA form

mainForm.Fields.Add(circle);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add the circle field to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a circle field and add the properties

PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));

//Set the fill color

circle.Border.FillColor = new PdfXfaSolidBrush(Color.Red);

//Add the circle to the existing XFA form

loadedForm.Fields.Add(circle);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a circle field and add the properties

Dim circle As New PdfXfaCircleField("circle", New SizeF(100, 100))

'Set the fill color

circle.Border.FillColor = New PdfXfaSolidBrush(Color.Red)

'Add the circle to the existing XFA form

loadedForm.Fields.Add(circle)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a circle field and add the properties

PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));

//Set the fill color

circle.Border.FillColor = new PdfXfaSolidBrush(Color.FromArgb(0,255,0,0));

//Add the circle to the existing XFA form

loadedForm.Fields.Add(circle);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a circle field and add the properties

PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));

//Set the fill color

circle.Border.FillColor = new PdfXfaSolidBrush(Color.FromArgb(0,255,0,0));

//Add the circle to the existing XFA form

loadedForm.Fields.Add(circle);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a circle field and add the properties

PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));

//Set the fill color

circle.Border.FillColor = new PdfXfaSolidBrush(Syncfusion.Drawing.Color.FromArgb(0,255,0,0));

//Add the circle to the existing XFA form

loadedForm.Fields.Add(circle);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA line

The below code snippet illustrates how to add a line to a new PDF document using [PdfXfaLine](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaLine.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();   

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a line and add the properties

PdfXfaLine line = new PdfXfaLine(new PointF(0,0),new PointF (200,0),3);

//Set the line color

line.Color = new PdfColor(Color.Red);

//Add the text line to the XFA form

mainForm.Fields.Add(line);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a line and add the properties

Dim line As New PdfXfaLine(New PointF(0,0),New PointF(200,0),3)

'Set the line color

line.Color = New PdfColor(Color.Red)

'Add the text line to the XFA form

mainForm.Fields.Add(line)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a line and add the properties

PdfXfaLine line = new PdfXfaLine(new PointF(0, 0), new PointF(200, 0), 3);

//Set the line color

line.Color = new PdfColor(Color.FromArgb(0,255,0,0));

//Add the text line to the XFA form

mainForm.Fields.Add(line);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf"); 



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a line and add the properties

PdfXfaLine line = new PdfXfaLine(new PointF(0, 0), new PointF(200, 0), 3);

//Set the line color

line.Color = new PdfColor(Color.FromArgb(0,255,0,0));

//Add the text line to the XFA form

mainForm.Fields.Add(line);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName); 



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Create a line and add the properties

PdfXfaLine line = new PdfXfaLine(new PointF(0, 0), new PointF(200, 0), 3);

//Set the line color

line.Color = new PdfColor(Syncfusion.Drawing.Color.FromArgb(0,255,0,0));

//Add the text line to the XFA form

mainForm.Fields.Add(line);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add a line to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a line and add the properties

PdfXfaLine line = new PdfXfaLine(new PointF(0, 0), new PointF(200, 0), 3);

//Set the line color

line.Color = new PdfColor(Color.Red);

//Add the line to the existing XFA form

loadedForm.Fields.Add(line);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a line and add the properties

Dim line As New PdfXfaLine(New PointF(0, 0), New PointF(200, 0), 3)

'Set the line color

line.Color = New PdfColor(Color.Red)

'Add the line to the existing XFA form

loadedForm.Fields.Add(line)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a line and add the properties

PdfXfaLine line = new PdfXfaLine(new PointF(0, 0), new PointF(200, 0), 3);

//Set the line color

line.Color = new PdfColor(Color.FromArgb(0,255,0,0));

//Add the line to the existing XFA form

loadedForm.Fields.Add(line);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a line and add the properties

PdfXfaLine line = new PdfXfaLine(new PointF(0, 0), new PointF(200, 0), 3);

//Set the line color

line.Color = new PdfColor(Color.FromArgb(0,255,0,0));

//Add the line to the existing XFA form

loadedForm.Fields.Add(line);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a line and add the properties

PdfXfaLine line = new PdfXfaLine(new PointF(0, 0), new PointF(200, 0), 3);

//Set the line color

line.Color = new PdfColor(Syncfusion.Drawing.Color.FromArgb(0,255,0,0));

//Add the line to the existing XFA form

loadedForm.Fields.Add(line);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding the XFA image

The below code snippet illustrates how to add an image to a new PDF document using [PdfXfaImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaImage.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();   

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a image and add the properties

PdfXfaImage image = new PdfXfaImage("image1", "image.jpg");

//Add the image to the XFA form

mainForm.Fields.Add(image);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add a new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form

Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)

'Create a image and add the properties

Dim image As New PdfXfaImage("image1", "image.jpg")

'Add the image to the XFA form

mainForm.Fields.Add(image)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf",PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Load the image as stream

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.image.jpg");

//Create a image and add the properties

PdfXfaImage image = new PdfXfaImage("image1", imageStream);

//Add the image to the XFA form

mainForm.Fields.Add(image);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Load the image as stream

MemoryStream imageStream = new MemoryStream(File.ReadAllBytes(imageFileName));

//Create a image and add the properties

PdfXfaImage image = new PdfXfaImage("image1", imageStream);

//Add the image to the XFA form

mainForm.Fields.Add(image);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add a new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form

PdfXfaForm mainForm = new PdfXfaForm("subform1", xfaPage, xfaPage.GetClientSize().Width);

//Load the image as stream

Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.image.jpg");

//Create a image and add the properties

PdfXfaImage image = new PdfXfaImage("image1", imageStream);

//Add the image to the XFA form

mainForm.Fields.Add(image);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream, PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to add an image to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("XfaForm1.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Create a image and add the properties

PdfXfaImage image = new PdfXfaImage("imgage1", "image.jpg");            

//Add the image to the existing XFA form

loadedForm.Fields.Add(image);

//Save the document

loadedDocument.Save("XfaForm.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA document

Dim loadedDocument As New PdfLoadedXfaDocument("XfaForm1.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Create a image and add the properties

Dim image As New PdfXfaImage("imgage1", "image.jpg")

'Add the image to the existing XFA form

loadedForm.Fields.Add(image)

'Save the document

loadedDocument.Save("XfaForm.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.XfaForm.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Load the image as stream

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.image.jpg");

//Create a image and add the properties

PdfXfaImage image = new PdfXfaImage("imgage1", imageStream);

//Add the image to the existing XFA form

loadedForm.Fields.Add(image);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Load the image as stream

MemoryStream imageStream = new MemoryStream(File.ReadAllBytes(imageFileName));

//Create a image and add the properties

PdfXfaImage image = new PdfXfaImage("imgage1", imageStream);

//Add the image to the existing XFA form

loadedForm.Fields.Add(image);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Load the image as stream

Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.image.jpg");

//Create a image and add the properties

PdfXfaImage image = new PdfXfaImage("imgage1", imageStream);

//Add the image to the existing XFA form

loadedForm.Fields.Add(image);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Working with XFA form flow directions

There are two types of flow directions available in XFA forms.

1. Horizontal
2. Vertical

### Horizontal flow direction

You can set the flow direction to an XFA form while creating, using [PdfXfaFlowDirection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaFlowDirection.html) Enum. The below sample illustrate how to set the horizontal flow direction in XFA forms.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));

//Set the caption text

textBoxField1.Caption.Text = "Last Name";

mainForm.Fields.Add(textBoxField1);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a textbox field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("FirstName", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "First Name"

'Set the tool tip

textBoxField.ToolTip = "First Name"

'Add the field to the XFA form

mainForm.Fields.Add(textBoxField)

Dim textBoxField1 As New PdfXfaTextBoxField("LastName", New SizeF(200, 20))

'Set the caption text

textBoxField1.Caption.Text = "Last Name"

mainForm.Fields.Add(textBoxField1)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));

//Set the caption text

textBoxField1.Caption.Text = "Last Name";

mainForm.Fields.Add(textBoxField1);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));

//Set the caption text

textBoxField1.Caption.Text = "Last Name";

mainForm.Fields.Add(textBoxField1);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));

//Set the caption text

textBoxField1.Caption.Text = "Last Name";

mainForm.Fields.Add(textBoxField1);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Vertical flow direction

You can set the flow direction to an XFA form while creating, using [PdfXfaFlowDirection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaFlowDirection.html) Enum. The below sample illustrate how to set the vertical flow direction in XFA forms.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with vertical flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Vertical, xfaPage.GetClientSize ().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));

//Set the caption text

textBoxField1.Caption.Text = "Last Name";

mainForm.Fields.Add(textBoxField1);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with vertical flow direction

Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Vertical, xfaPage.GetClientSize().Width)

'Create a textbox field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("FirstName", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "First Name"

'Set the tool tip

textBoxField.ToolTip = "First Name"

'Add the field to the XFA form

mainForm.Fields.Add(textBoxField)

Dim textBoxField1 As New PdfXfaTextBoxField("LastName", New SizeF(200, 20))

'Set the caption text

textBoxField1.Caption.Text = "Last Name"

mainForm.Fields.Add(textBoxField1)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with vertical flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Vertical, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));

//Set the caption text

textBoxField1.Caption.Text = "Last Name";

mainForm.Fields.Add(textBoxField1);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with vertical flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Vertical, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));

//Set the caption text

textBoxField1.Caption.Text = "Last Name";

mainForm.Fields.Add(textBoxField1);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with vertical flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Vertical, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));

//Set the caption text

textBoxField1.Caption.Text = "Last Name";

mainForm.Fields.Add(textBoxField1);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Rotating XFA form fields

You can rotate a form field in XFA document, using [PdfXfaRotateAngle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaRotateAngle.html) Enum. The following code snippet explains this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Set the fields rotation

textBoxField.Rotate = PdfXfaRotateAngle.RotateAngle90;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a textbox field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("FirstName", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "First Name"

'Set the tool tip

textBoxField.ToolTip = "First Name"

'Set the fields rotation

textBoxField.Rotate = PdfXfaRotateAngle.RotateAngle90

'Add the field to the XFA form

mainForm.Fields.Add(textBoxField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Set the fields rotation

textBoxField.Rotate = PdfXfaRotateAngle.RotateAngle90;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Set the fields rotation

textBoxField.Rotate = PdfXfaRotateAngle.RotateAngle90;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a textbox field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "First Name";

//Set the tool tip

textBoxField.ToolTip = "First Name";

//Set the fields rotation

textBoxField.Rotate = PdfXfaRotateAngle.RotateAngle90;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Validating the date time field

You can validate the date time fields of the input text by enabling the [RequireValidation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaDateTimeField.html#Syncfusion_Pdf_Xfa_PdfXfaDateTimeField_RequireValidation) property of [PdfXfaDateTimeField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaDateTimeField.html). The following code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("dateTimeField", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date of Birth";

//Set the date pattern

dateTimeField.DatePattern = PdfXfaDatePattern.DDMMMMYYYY;

//Enable the validation

dateTimeField.RequireValidation = true;

//Add the field to the XFA form

mainForm.Fields.Add(dateTimeField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a date time field and add the properties

Dim dateTimeField As New PdfXfaDateTimeField("dateTimeField", New SizeF(200, 20))

'Set the caption text

dateTimeField.Caption.Text = "Date of Birth"

'Set the date pattern

dateTimeField.DatePattern = PdfXfaDatePattern.DDMMMMYYYY

'Enable the validation

dateTimeField.RequireValidation = True

'Add the field to the XFA form

mainForm.Fields.Add(dateTimeField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("dateTimeField", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date of Birth";

//Set the date pattern

dateTimeField.DatePattern = PdfXfaDatePattern.DDMMMMYYYY;

//Enable the validation

dateTimeField.RequireValidation = true;

//Add the field to the XFA form

mainForm.Fields.Add(dateTimeField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("dateTimeField", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date of Birth";

//Set the date pattern

dateTimeField.DatePattern = PdfXfaDatePattern.DDMMMMYYYY;

//Enable the validation

dateTimeField.RequireValidation = true;

//Add the field to the XFA form

mainForm.Fields.Add(dateTimeField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a date time field and add the properties

PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("dateTimeField", new SizeF(200, 20));

//Set the caption text

dateTimeField.Caption.Text = "Date of Birth";

//Set the date pattern

dateTimeField.DatePattern = PdfXfaDatePattern.DDMMMMYYYY;

//Enable the validation

dateTimeField.RequireValidation = true;

//Add the field to the XFA form

mainForm.Fields.Add(dateTimeField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Customizing the numeric field value

You can customize the numeric field input value to the specific pattern through [PatternString](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaNumericField.html#Syncfusion_Pdf_Xfa_PdfXfaNumericField_PatternString) property of [PdfXfaNumericField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaNumericField.html) class. The following code snippet explains this.
Please refer the below link for numeric pattern format in detail,
[http://help.adobe.com/en_US/livecycle/10.0/DesignerHelp/WS92d06802c76abadb-56c02439129b8b00ebc-7ecf.html](http://help.adobe.com/en_US/livecycle/10.0/DesignerHelp/WS92d06802c76abadb-56c02439129b8b00ebc-7ecf.html)

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Set the pattern string

numericField.PatternString = "zzzzzzzzz9";

//Add the field to the XFA form

mainForm.Fields.Add(numericField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a numeric field and add the properties

Dim numericField As New PdfXfaNumericField("numericField", New SizeF(200, 20))

'Set the caption text

numericField.Caption.Text = "Numeric Field"

'Set the pattern string

numericField.PatternString = "zzzzzzzzz9"

'Add the field to the XFA form

mainForm.Fields.Add(numericField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Set the pattern string

numericField.PatternString = "zzzzzzzzz9";

//Add the field to the XFA form

mainForm.Fields.Add(numericField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Set the pattern string

numericField.PatternString = "zzzzzzzzz9";

//Add the field to the XFA form

mainForm.Fields.Add(numericField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a numeric field and add the properties

PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));

//Set the caption text

numericField.Caption.Text = "Numeric Field";

//Set the pattern string

numericField.PatternString = "zzzzzzzzz9";

//Add the field to the XFA form

mainForm.Fields.Add(numericField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Adding nested sub forms

You can add the nested sub forms by using the following code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a font

PdfFont font = new PdfStandardFont(xfaPage,PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a text element

PdfXfaTextElement element = new PdfXfaTextElement("Main Form", font, 400, 20);                

//Add the field to the XFA form

mainForm.Fields.Add(element);

//Create a form

PdfXfaForm form1 = new PdfXfaForm(PdfXfaFlowDirection.Vertical, 400);

PdfXfaTextElement element1 = new PdfXfaTextElement("First Form", font, 400, 20);

form1.Fields.Add(element1);

PdfXfaForm form2 = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, 400);

PdfXfaTextElement element2 = new PdfXfaTextElement ("Second Form", font,400,20);

form2.Fields.Add(element2);

form1.Fields.Add(form2);

mainForm.Fields.Add(form1);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Static);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a font

Dim font As PdfFont = New PdfStandardFont(xfaPage,PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold)

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a text element

Dim element As New PdfXfaTextElement("Main Form", font, 400, 20)

'Add the field to the XFA form

mainForm.Fields.Add(element)

'Create a form

Dim form1 As New PdfXfaForm(PdfXfaFlowDirection.Vertical, 400)

Dim element1 As New PdfXfaTextElement("First Form", font, 400, 20)

form1.Fields.Add(element1)

Dim form2 As New PdfXfaForm(PdfXfaFlowDirection.Horizontal, 400)

Dim element2 As New PdfXfaTextElement("Second Form", font,400,20)

form2.Fields.Add(element2)

form1.Fields.Add(form2)

mainForm.Fields.Add(form1)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Static)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text element

PdfXfaTextElement element = new PdfXfaTextElement("Main Form", font, 400, 20);

//Add the field to the XFA form

mainForm.Fields.Add(element);

//Create a form

PdfXfaForm form1 = new PdfXfaForm(PdfXfaFlowDirection.Vertical, 400);

PdfXfaTextElement element1 = new PdfXfaTextElement("First Form", font, 400, 20);

form1.Fields.Add(element1);

PdfXfaForm form2 = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, 400);

PdfXfaTextElement element2 = new PdfXfaTextElement("Second Form", font, 400, 20);

form2.Fields.Add(element2);

form1.Fields.Add(form2);

mainForm.Fields.Add(form1);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text element

PdfXfaTextElement element = new PdfXfaTextElement("Main Form", font, 400, 20);

//Add the field to the XFA form

mainForm.Fields.Add(element);

//Create a form

PdfXfaForm form1 = new PdfXfaForm(PdfXfaFlowDirection.Vertical, 400);

PdfXfaTextElement element1 = new PdfXfaTextElement("First Form", font, 400, 20);

form1.Fields.Add(element1);

PdfXfaForm form2 = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, 400);

PdfXfaTextElement element2 = new PdfXfaTextElement("Second Form", font, 400, 20);

form2.Fields.Add(element2);

form1.Fields.Add(form2);

mainForm.Fields.Add(form1);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text element

PdfXfaTextElement element = new PdfXfaTextElement("Main Form", font, 400, 20);

//Add the field to the XFA form

mainForm.Fields.Add(element);

//Create a form

PdfXfaForm form1 = new PdfXfaForm(PdfXfaFlowDirection.Vertical, 400);

PdfXfaTextElement element1 = new PdfXfaTextElement("First Form", font, 400, 20);

form1.Fields.Add(element1);

PdfXfaForm form2 = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, 400);

PdfXfaTextElement element2 = new PdfXfaTextElement("Second Form", font, 400, 20);

form2.Fields.Add(element2);

form1.Fields.Add(form2);

mainForm.Fields.Add(form1);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Formatting XFA form fields

### Working with alignments

XFA support both the horizontal and vertical alignments.

### Horizontal alignment

You can add the horizontal alignments in XFA form fields through [HorizontalAlignment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaStyledField.html#Syncfusion_Pdf_Xfa_PdfXfaStyledField_HorizontalAlignment) property by using [PdfXfaHorizontalAlignment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaHorizontalAlignment.html) Enum. The below code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the horizontal alignment

textBoxField.HorizontalAlignment = PdfXfaHorizontalAlignment.Right;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a text box field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "Fist Name"

'Set the horizontal alignment 

textBoxField.HorizontalAlignment = PdfXfaHorizontalAlignment.Right

'Add the field to the XFA form

mainForm.Fields.Add(textBoxField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the horizontal alignment

textBoxField.HorizontalAlignment = PdfXfaHorizontalAlignment.Right;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the horizontal alignment

textBoxField.HorizontalAlignment = PdfXfaHorizontalAlignment.Right;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the horizontal alignment

textBoxField.HorizontalAlignment = PdfXfaHorizontalAlignment.Right;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Vertical alignment

You can add the vertical alignments in XFA form fields through [VerticalAlignment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaStyledField.html#Syncfusion_Pdf_Xfa_PdfXfaStyledField_VerticalAlignment) property by using [PdfXfaVerticalAlignment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaVerticalAlignment.html) Enum. The below code snippet explains this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(XfaPagePdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the vertical alignment

textBoxField.VerticalAlignment = PdfXfaVerticalAlignment.Bottom;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(XfaPagePdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a text box field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "Fist Name"

'Set the vertical alignment 

textBoxField.VerticalAlignment = PdfXfaVerticalAlignment.Bottom

'Add the field to the XFA form

mainForm.Fields.Add(textBoxField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the vertical alignment

textBoxField.VerticalAlignment = PdfXfaVerticalAlignment.Bottom;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the vertical alignment

textBoxField.VerticalAlignment = PdfXfaVerticalAlignment.Bottom;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the vertical alignment

textBoxField.VerticalAlignment = PdfXfaVerticalAlignment.Bottom;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding margins to the XFA fields

You can add margin to the XFA form fields by using [Margins](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaField.html#Syncfusion_Pdf_Xfa_PdfXfaField_Margins) property. The below code snippet explains this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the margins

textBoxField.Margins.Left = 10;

textBoxField.Margins.Right = 5;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a text box field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "Fist Name"

'Set the margins 

textBoxField.Margins.Left = 10

textBoxField.Margins.Right = 5

'Add the field to the XFA form

mainForm.Fields.Add(textBoxField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the margins

textBoxField.Margins.Left = 10;

textBoxField.Margins.Right = 5;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the margins

textBoxField.Margins.Left = 10;

textBoxField.Margins.Right = 5;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the margins

textBoxField.Margins.Left = 10;

textBoxField.Margins.Right = 5;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding padding to the XFA fields

You can add padding to the XFA form fields by using the below code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the paddings

textBoxField.Padding.All = 2;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a text box field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "Fist Name"

'Set the paddings 

textBoxField.Padding.All = 2

'Add the field to the XFA form

mainForm.Fields.Add(textBoxField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the paddings

textBoxField.Padding.All = 2;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the paddings

textBoxField.Padding.All = 2;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the paddings

textBoxField.Padding.All = 2;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Adding border to the XFA fields

You can add the fields border by using the below code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the border color and width

textBoxField.Border.Color = new PdfColor (200,123,0);

textBoxField.Border.Width = 2;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a text box field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "Fist Name"

'Set the border color and width 

textBoxField.Border.Color = New PdfColor(200,123,0)

textBoxField.Border.Width = 2

'Add the field to the XFA form

mainForm.Fields.Add(textBoxField)

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the border color and width

textBoxField.Border.Color = new PdfColor(200, 123, 0);

textBoxField.Border.Width = 2;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "XfaForm.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the border color and width

textBoxField.Border.Color = new PdfColor(200, 123, 0);

textBoxField.Border.Width = 2;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(xfaPage, PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Set the border color and width

textBoxField.Border.Color = new PdfColor(200, 123, 0);

textBoxField.Border.Width = 2;

//Add the field to the XFA form

mainForm.Fields.Add(textBoxField);

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Filling form fields in an existing XFA document

Essential PDF allows you to fill the XFA form fields using [PdfLoadedXfaform](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaForm.html) class.

### Filling the XFA text box field

Please refer the below sample for filling the XFA text box field using [PdfLoadedXfaTextBoxField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaTextBoxField.html) class.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded text box field

PdfLoadedXfaTextBoxField loadedTextBox = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//fill the text box

loadedTextBox.Text = "First Name";

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the loaded text box field

Dim loadedTextBox As PdfLoadedXfaTextBoxField = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("text[0]"), PdfLoadedXfaTextBoxField)

'fill the text box

loadedTextBox.Text = "First Name"

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded text box field

PdfLoadedXfaTextBoxField loadedTextBox = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//fill the text box

loadedTextBox.Text = "First Name";

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded text box field

PdfLoadedXfaTextBoxField loadedTextBox = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//fill the text box

loadedTextBox.Text = "First Name";

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded text box field

PdfLoadedXfaTextBoxField loadedTextBox = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//fill the text box

loadedTextBox.Text = "First Name";

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Filling the XFA numeric field

You can fill the XFA numeric field by using [PdfLoadedXfaNumericField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaNumericField.html) class. The below code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded numeric field

PdfLoadedXfaNumericField loadedNumericField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["numericField[0]"] as PdfLoadedXfaNumericField;

//fill the numeric field

loadedNumericField.NumericValue = 945322;

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the loaded numeric field

Dim loadedNumericField As PdfLoadedXfaNumericField = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("numericField[0]"), PdfLoadedXfaNumericField)

'fill the numeric field

loadedNumericField.NumericValue = 945322

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded numeric field

PdfLoadedXfaNumericField loadedNumericField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["numericField[0]"] as PdfLoadedXfaNumericField;

//fill the numeric field

loadedNumericField.NumericValue = 945322;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded numeric field

PdfLoadedXfaNumericField loadedNumericField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["numericField[0]"] as PdfLoadedXfaNumericField;

//fill the numeric field

loadedNumericField.NumericValue = 945322;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document.

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded numeric field

PdfLoadedXfaNumericField loadedNumericField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["numericField[0]"] as PdfLoadedXfaNumericField;

//fill the numeric field

loadedNumericField.NumericValue = 945322;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document.

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Filling the XFA combo box field

You can fill the XFA combo box field by using [PdfLoadedXfaComboBoxField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaComboBoxField.html) class. The below code snippet explains this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded combo box field

PdfLoadedXfaComboBoxField loadedComboBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["comboBoxField[0]"] as PdfLoadedXfaComboBoxField;

//Set the combo box selected index

loadedComboBoxField.SelectedIndex = 1;

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the loaded combo box field

Dim loadedComboBoxField As PdfLoadedXfaComboBoxField = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("comboBoxField[0]"), PdfLoadedXfaComboBoxField)

'Set the combo box selected index

loadedComboBoxField.SelectedIndex = 1

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded combo box field

PdfLoadedXfaComboBoxField loadedComboBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["comboBoxField[0]"] as PdfLoadedXfaComboBoxField;

//Set the combo box selected index

loadedComboBoxField.SelectedIndex = 1;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded combo box field.

PdfLoadedXfaComboBoxField loadedComboBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["comboBoxField[0]"] as PdfLoadedXfaComboBoxField;

//Set the combo box selected index

loadedComboBoxField.SelectedIndex = 1;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded combo box field.

PdfLoadedXfaComboBoxField loadedComboBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["comboBoxField[0]"] as PdfLoadedXfaComboBoxField;

//Set the combo box selected index

loadedComboBoxField.SelectedIndex = 1;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


You can fill and save hidden items in XFA combo box field by using the following code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("Input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded combo box field

PdfLoadedXfaComboBoxField loadedComboBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["comboBoxField[0]"] as PdfLoadedXfaComboBoxField;

//Set the combo box selected index using hidden items

loadedComboBoxField.SelectedValue = loadedComboBoxField.HiddenItems[0];

//Save the combo box field hidden values

List<string> hiddenValues = new List<string>();

hiddenValues = loadedComboBoxField.HiddenItems;

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedXfaDocument("Input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the loaded combo box field

Dim loadedComboBoxField As PdfLoadedXfaComboBoxField = TryCast(TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm).Fields("comboBoxField[0]"), PdfLoadedXfaComboBoxField)

'Set the combo box selected index using hidden items

loadedComboBoxField.SelectedValue = loadedComboBoxField.HiddenItems(0)

'Save the combo box field hidden values

Dim hiddenValues As New List(Of String)()

hiddenValues = loadedComboBoxField.HiddenItems

'Save the document

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded combo box field

PdfLoadedXfaComboBoxField loadedComboBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["comboBoxField[0]"] as PdfLoadedXfaComboBoxField;

//Set the combo box selected index using hidden items

loadedComboBoxField.SelectedValue = loadedComboBoxField.HiddenItems[0];

//Save the combo box field hidden values

List<string> hiddenValues = new List<string>();

hiddenValues = loadedComboBoxField.HiddenItems;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded combo box field

PdfLoadedXfaComboBoxField loadedComboBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["comboBoxField[0]"] as PdfLoadedXfaComboBoxField;

//Set the combo box selected index using hidden items

loadedComboBoxField.SelectedValue = loadedComboBoxField.HiddenItems[0];

//Save the combo box field hidden values

List<string> hiddenValues = new List<string>();

hiddenValues = loadedComboBoxField.HiddenItems;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded combo box field

PdfLoadedXfaComboBoxField loadedComboBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["comboBoxField[0]"] as PdfLoadedXfaComboBoxField;

//Set the combo box selected index using hidden items

loadedComboBoxField.SelectedValue = loadedComboBoxField.HiddenItems[0];

//Save the combo box field hidden values

List<string> hiddenValues = new List<string>();

hiddenValues = loadedComboBoxField.HiddenItems;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %} 


### Filling the XFA list box field

You can fill the XFA list box field by using [PdfLoadedXfaListBoxField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaListBoxField.html) class. The below code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded list box field

PdfLoadedXfaListBoxField loadedListBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;

//Set the list box selected index

loadedListBoxField.SelectedIndex = 1;

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the loaded list box field

Dim loadedListBoxField As PdfLoadedXfaListBoxField = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("listBoxField[0]"), PdfLoadedXfaListBoxField)

'Set the list box selected index

loadedListBoxField.SelectedIndex = 1

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded list box field

PdfLoadedXfaListBoxField loadedListBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;

//Set the list box selected index

loadedListBoxField.SelectedIndex = 1;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded list box field.

PdfLoadedXfaListBoxField loadedListBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;

//Set the list box selected index

loadedListBoxField.SelectedIndex = 1;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded list box field.

PdfLoadedXfaListBoxField loadedListBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;

//Set the list box selected index

loadedListBoxField.SelectedIndex = 1;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


You can also select the multiple values by using the below code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded list box field

PdfLoadedXfaListBoxField loadedListBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;

//Set the list box selected items

loadedListBoxField .SelectedItems =new string[] {"English","Spanish"};

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the loaded list box field

Dim loadedListBoxField As PdfLoadedXfaListBoxField = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("listBoxField[0]"), PdfLoadedXfaListBoxField)

'Set the list box selected items           

loadedListBoxField.SelectedItems = New String() {"English","Spanish"}

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded list box field

PdfLoadedXfaListBoxField loadedListBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;

//Set the list box selected items

loadedListBoxField.SelectedItems = new string[] { "English", "Spanish" };

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded list box field

PdfLoadedXfaListBoxField loadedListBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;

//Set the list box selected items

loadedListBoxField.SelectedItems = new string[] { "English", "Spanish" };

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document.

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded list box field

PdfLoadedXfaListBoxField loadedListBoxField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;

//Set the list box selected items

loadedListBoxField.SelectedItems = new string[] { "English", "Spanish" };

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document.

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Filling the XFA date time field

You can fill the XFA date time field by using [PdfLoadedXfaDateTimeField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaDateTimeField.html) class. The below code snippet explains this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded date time field

PdfLoadedXfaDateTimeField loadedDateTimeField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["dateTimeField[0]"] as PdfLoadedXfaDateTimeField;

//Set the value

loadedDateTimeField.Value = DateTime.Now;

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the loaded date time field

Dim loadedDateTimeField As PdfLoadedXfaDateTimeField = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("dateTimeField[0]"), PdfLoadedXfaDateTimeField)

'Set the value           

loadedDateTimeField.Value = Date.Now

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded date time field

PdfLoadedXfaDateTimeField loadedDateTimeField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["dateTimeField[0]"] as PdfLoadedXfaDateTimeField;

//Set the value

loadedDateTimeField.Value = DateTime.Now;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded date time field

PdfLoadedXfaDateTimeField loadedDateTimeField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["dateTimeField[0]"] as PdfLoadedXfaDateTimeField;

//Set the value

loadedDateTimeField.Value = DateTime.Now;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded date time field

PdfLoadedXfaDateTimeField loadedDateTimeField = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["dateTimeField[0]"] as PdfLoadedXfaDateTimeField;

//Set the value

loadedDateTimeField.Value = DateTime.Now;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Filling the XFA check box field

You can fill the XFA check box field by using [PdfLoadedXfaCheckBoxField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaCheckBoxField.html) class. The below code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded check box field

PdfLoadedXfaCheckBoxField loadedCheckBox = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["checkBox[0]"] as PdfLoadedXfaCheckBoxField;

//Check the check box          

loadedCheckBox.IsChecked = true;

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the loaded check box field

Dim loadedCheckBox As PdfLoadedXfaCheckBoxField = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("checkBox[0]"), PdfLoadedXfaCheckBoxField)

'Check the check box          

loadedCheckBox.IsChecked = True

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded check box field

PdfLoadedXfaCheckBoxField loadedCheckBox = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["checkBox[0]"] as PdfLoadedXfaCheckBoxField;

//Check the check box          

loadedCheckBox.IsChecked = true;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded check box field

PdfLoadedXfaCheckBoxField loadedCheckBox = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["checkBox[0]"] as PdfLoadedXfaCheckBoxField;

//Check the check box          

loadedCheckBox.IsChecked = true;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "XfaForm.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the loaded check box field

PdfLoadedXfaCheckBoxField loadedCheckBox = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["checkBox[0]"] as PdfLoadedXfaCheckBoxField;

//Check the check box          

loadedCheckBox.IsChecked = true;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Filling the XFA radio button field

You can fill the XFA radio button field by using [PdfLoadedXfaRadioButtonField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaRadioButtonField.html) class. The below code snippet explains this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the radio button group

PdfLoadedXfaRadioButtonGroup loadedRadioButtonGroup = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["radioButtonGroup[0]"] as PdfLoadedXfaRadioButtonGroup;

//Get the radio button field

PdfLoadedXfaRadioButtonField loadedRadioButtonField = loadedRadioButtonGroup.Fields[0] as PdfLoadedXfaRadioButtonField;

//Check the radio button

loadedRadioButtonField.IsChecked = true;

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the radio button group

Dim loadedRadioButtonGroup As PdfLoadedXfaRadioButtonGroup = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("radioButtonGroup[0]"), PdfLoadedXfaRadioButtonGroup)

'Get the radio button field

Dim loadedRadioButtonField As PdfLoadedXfaRadioButtonField = TryCast(loadedRadioButtonGroup.Fields(0), PdfLoadedXfaRadioButtonField)

'Check the radio button          

loadedRadioButtonField.IsChecked = True

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the radio button group

PdfLoadedXfaRadioButtonGroup loadedRadioButtonGroup = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["radioButtonGroup[0]"] as PdfLoadedXfaRadioButtonGroup;

//Get the radio button field

PdfLoadedXfaRadioButtonField loadedRadioButtonField = loadedRadioButtonGroup.Fields[0] as PdfLoadedXfaRadioButtonField;

//Check the radio button

loadedRadioButtonField.IsChecked = true;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the radio button group

PdfLoadedXfaRadioButtonGroup loadedRadioButtonGroup = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["radioButtonGroup[0]"] as PdfLoadedXfaRadioButtonGroup;

//Get the radio button field

PdfLoadedXfaRadioButtonField loadedRadioButtonField = loadedRadioButtonGroup.Fields[0] as PdfLoadedXfaRadioButtonField;

//Check the radio button

loadedRadioButtonField.IsChecked = true;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the radio button group

PdfLoadedXfaRadioButtonGroup loadedRadioButtonGroup = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["radioButtonGroup[0]"] as PdfLoadedXfaRadioButtonGroup;

//Get the radio button field

PdfLoadedXfaRadioButtonField loadedRadioButtonField = loadedRadioButtonGroup.Fields[0] as PdfLoadedXfaRadioButtonField;

//Check the radio button

loadedRadioButtonField.IsChecked = true;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


### Removing editing capability of form fields

The form field editing or filling capabilities can be removed by marking the form or field as read only. To prevent the user from changing the form field content, you can enable the [ReadOnly](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaForm.html#Syncfusion_Pdf_Xfa_PdfXfaForm_ReadOnly) property of [PdfXfaForm](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfXfaForm.html).
The below code snippet illustrates how to set the read only property to a new PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Add the text box to the XFA form

mainForm.Fields.Add(textBoxField);

//Set the form as read only

mainForm.ReadOnly = true;

//Add the XFA form to the document

document.XfaForm = mainForm;

//Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic);

//close the document

document.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Create a new PDF XFA document

Dim document As New PdfXfaDocument()

'Add new XFA page

Dim xfaPage As PdfXfaPage = document.Pages.Add()

'Create a new PDF XFA form with horizontal flow direction

Dim mainForm As New PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)

'Create a text box field and add the properties

Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))

'Set the caption text

textBoxField.Caption.Text = "Fist Name"

'Add the text box to the XFA form

mainForm.Fields.Add(textBoxField)

'Set the form as read only

mainForm.ReadOnly = True

'Add the XFA form to the document

document.XfaForm = mainForm

'Save the document

document.Save("XfaForm.pdf", PdfXfaType.Dynamic)

'close the document

document.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Add the text box to the XFA form

mainForm.Fields.Add(textBoxField);

//Set the form as read only

mainForm.ReadOnly = true;

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//Close the document

document.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Add the text box to the XFA form

mainForm.Fields.Add(textBoxField);

//Set the form as read only

mainForm.ReadOnly = true;

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Create a new PDF XFA document

PdfXfaDocument document = new PdfXfaDocument();

//Add new XFA page

PdfXfaPage xfaPage = document.Pages.Add();

//Create a new PDF XFA form with horizontal flow direction

PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);

//Create a text box field and add the properties

PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));

//Set the caption text

textBoxField.Caption.Text = "Fist Name";

//Add the text box to the XFA form

mainForm.Fields.Add(textBoxField);

//Set the form as read only

mainForm.ReadOnly = true;

//Add the XFA form to the document

document.XfaForm = mainForm;

MemoryStream stream = new MemoryStream();

document.Save(stream,PdfXfaType.Dynamic);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


The below code snippet illustrates how to set the ```ReadOnly``` property to an existing PDF document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Set the form as read only

loadedForm.ReadOnly = true;

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document 

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Set the form as read only

loadedForm.ReadOnly = True

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Set the form as read only

loadedForm.ReadOnly = true;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Set the form as read only

loadedForm.ReadOnly = true;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Set the form as read only

loadedForm.ReadOnly = true;

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Flattening XFA Form fields

The form field editing or filling capabilities can be removed by flattening the PDF document.
The Essential PDF flattens a form field by removing the existing form field and replacing it with graphical objects that will resemble the form field and cannot be edited. This can be achieved by enabling the [Flatten](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaDocument.html#Syncfusion_Pdf_Xfa_PdfLoadedXfaDocument_Flatten) property of [PdfLoadedXfaDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaDocument.html).
The following code snippet illustrates how to flatten the XFA form field.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing document

PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("input.pdf");

//Set flatten

ldoc.Flatten = true;

//Save the document

ldoc.Save("output.pdf");

//Close the document

ldoc.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing document

Dim ldoc As New PdfLoadedXfaDocument("input.pdf")

'Set flatten

ldoc.Flatten = True

'Save the document

ldoc.Save("output.pdf")

'Close the document

ldoc.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//PDF supports flattening XFA form fields only in Windows Forms, WPF, ASP.NET and ASP.NET MVC.



{% endhighlight %}

{% endtabs %}


## Removing the dynamic form fields from an existing XFA document

You can remove the dynamic XFA form fields by using [Remove](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaFieldCollection.html#Syncfusion_Pdf_Xfa_PdfLoadedXfaFieldCollection_Remove_Syncfusion_Pdf_Xfa_PdfLoadedXfaField_) method of [PdfLoadedXfaFieldCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaFieldCollection.html) class. The below code snippet explained this.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the existing field

PdfLoadedXfaTextBoxField loadedText = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//Remove the field

loadedForm.Fields.Remove(loadedText);

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document 

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the existing field

Dim loadedText As PdfLoadedXfaTextBoxField = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("text[0]"), PdfLoadedXfaTextBoxField)

'Remove the field

loadedForm.Fields.Remove(loadedText)

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the existing field

PdfLoadedXfaTextBoxField loadedText = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//Remove the field

loadedForm.Fields.Remove(loadedText);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the existing field

PdfLoadedXfaTextBoxField loadedText = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//Remove the field

loadedForm.Fields.Remove(loadedText);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the existing field

PdfLoadedXfaTextBoxField loadedText = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//Remove the field

loadedForm.Fields.Remove(loadedText);

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Modifying the existing fields in XFA document

You can modify the existing dynamic XFA fields by using the below code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the existing field

PdfLoadedXfaTextBoxField loadedText = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//Set the width and height of the field

loadedText.Width = 200;

loadedText.Height = 30;

//Set the caption text

loadedText.Caption.Text = "Second Name";

//Save the document

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close();



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing PDF document 

Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")

'Load the existing XFA form

Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm

'Get the existing field

Dim loadedText As PdfLoadedXfaTextBoxField = TryCast((TryCast(loadedForm.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("text[0]"), PdfLoadedXfaTextBoxField)

'Set the width and height of the field

loadedText.Width = 200

loadedText.Height = 30

'Set the caption text

loadedText.Caption.Text = "Second Name"

'Save the document 

loadedDocument.Save("output.pdf")

'Close the document

loadedDocument.Close()



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the existing field

PdfLoadedXfaTextBoxField loadedText = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//Set the width and height of the field

loadedText.Width = 200;

loadedText.Height = 30;

//Set the caption text

loadedText.Caption.Text = "Second Name";

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the existing field

PdfLoadedXfaTextBoxField loadedText = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//Set the width and height of the field

loadedText.Width = 200;

loadedText.Height = 30;

//Set the caption text

loadedText.Caption.Text = "Second Name";

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Load the existing XFA form

PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;

//Get the existing field

PdfLoadedXfaTextBoxField loadedText = (loadedForm.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;

//Set the width and height of the field

loadedText.Width = 200;

loadedText.Height = 30;

//Set the caption text

loadedText.Caption.Text = "Second Name";

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Clear XFA date time field value

The Essential PDF supports clearing XFA form date time fields values, you can clear the date time values by using the [ClearValue](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaDateTimeField.html#Syncfusion_Pdf_Xfa_PdfLoadedXfaDateTimeField_ClearValue) method available in the [PdfLoadedXfaDateTimeField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xfa.PdfLoadedXfaDateTimeField.html).
The following sample illustrates how to clear the date time field in an existing XFA document.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing XFA PDF document

PdfLoadedXfaDocument loadedXfaDocument = new PdfLoadedXfaDocument("input.pdf");

//Get the date time field

PdfLoadedXfaDateTimeField dateTimeField = loadedXfaDocument.XfaForm.TryGetFieldByCompleteName("form[0].subform[0].dateTime[0]") as PdfLoadedXfaDateTimeField;

//Clear the date time field value

dateTimeField.ClearValue(); 

//Save and close the document

loadedXfaDocument.Save("output.pdf");



{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Load the existing XFA PDF document

Dim loadedXfaDocument As PdfLoadedXfaDocument = New PdfLoadedXfaDocument("input.pdf")

'Get the date time field

Dim dateTimeField As PdfLoadedXfaDateTimeField = TryCast(loadedXfaDocument.XfaForm.TryGetFieldByCompleteName("form[0].subform[0].dateTime[0]"), PdfLoadedXfaDateTimeField)

'Clear the date time field value

dateTimeField.ClearValue()

'Save and close the document

loadedXfaDocument.Save("output.pdf")



{% endhighlight %}

  {% highlight c# tabtile="UWP" %}


//Load the PDF document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Get the date time field

PdfLoadedXfaDateTimeField dateTimeField = loadedDocument.XfaForm.TryGetFieldByCompleteName("form[0].subform[0].dateTime[0]") as PdfLoadedXfaDateTimeField;

//Clear the date time field value

dateTimeField.ClearValue();

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close();

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "output.pdf");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Get the date time field

PdfLoadedXfaDateTimeField dateTimeField = loadedDocument.XfaForm.TryGetFieldByCompleteName("form[0].subform[0].dateTime[0]") as PdfLoadedXfaDateTimeField;

//Clear the date time field value

dateTimeField.ClearValue();

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0', then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);



{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}


//Load the PDF document

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load the existing XFA document

PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument(docStream);

//Get the date time field

PdfLoadedXfaDateTimeField dateTimeField = loadedDocument.XfaForm.TryGetFieldByCompleteName("form[0].subform[0].dateTime[0]") as PdfLoadedXfaDateTimeField;

//Clear the date time field value

dateTimeField.ClearValue();

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0', then the PDF will be empty

stream.Position = 0;

//Close the document

loadedDocument.Close();

//Save the stream into XFDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("XfaForm.pdf", "application/pdf", fdfStream);
}



{% endhighlight %}

{% endtabs %}


## Supported fields for XFA form

The following XFA fields are supported in creating, filling, and flattening the PDF document.

* Text box field
* Numeric field
* DateTime field
* Combo box field
* Radio button field
* List box field
* Check box field
* Text Element
* Button
* Line
* Rectangle
* Circle
* Image 

N> Removing and modifying the form fields is not supported in **static** XFA forms.
