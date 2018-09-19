---
title: Working with Forms
description: This section explains how to create, fill and flatten form fields in the PDF document
platform: file-formats
control: PDF
documentation: UG
---
# Working with Forms 

An interactive form, sometimes referred to as an AcroForm is a collection of fields for gathering information. A PDF document can contain any number of fields appearing on any combination of pages, all of that make a single, globally interactive form spanning the entire document.

## Creating a new PDF form

Essential PDF allows you to create and manage the form (AcroForm) in PDF document by using PdfForm class. The PdfFormFieldCollection class represents the entire field collection of the form.

### Adding the text box field 

The below code snippet illustrates how to add a textbox field to a new PDF document.

{% tabs %}

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to the PDF document.

PdfPage page = document.Pages.Add();

//Create a textbox field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Save the document.

document.Save("Form.pdf");

//close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As PdfDocument = New PdfDocument()

'Add a new page to the PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create a textbox field and add the properties.

Dim textBoxField As PdfTextBoxField = New PdfTextBoxField(page, "FirstName")

textBoxField.Bounds = New RectangleF(0, 0, 100, 20)

textBoxField.ToolTip = "First Name"

'Add the form field to the document.

document.Form.Fields.Add(textBoxField)

'Save the document.

document.Save("Form.pdf")

'close the document

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to the PDF document.

PdfPage page = document.Pages.Add();

//Create a textbox field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to the PDF document.

PdfPage page = document.Pages.Add();

//Create a textbox field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to the PDF document.

PdfPage page = document.Pages.Add();

//Create a textbox field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
        Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
        Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

The below code snippet illustrates how to add the textbox to an existing PDF document:

{% tabs %}  

{% highlight c# %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Create the form if the form does not exist in the loaded document

if(loadedDocument.Form==null)

loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a textbox field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(loadedPage, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the existing PDF document.

loadedDocument.Form.Fields.Add(textBoxField);

//Save the document.

loadedDocument.Save("Form.pdf");

//close the document

loadedDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Create the form if the form does not exist in the loaded document

If loadedDocument.Form Is Nothing Then

loadedDocument.CreateForm()

End If

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create a text box field and add the properties.

Dim textBoxField As New PdfTextBoxField(loadedPage, "FirstName")

textBoxField.Bounds = New RectangleF(0, 0, 100, 20)

textBoxField.ToolTip = "First Name"

'Add the form field to the existing PDF document.

loadedDocument.Form.Fields.Add(textBoxField)

'Save the document.

loadedDocument.Save("Form.pdf")

'close the document

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

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a textbox field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(loadedPage, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the existing PDF document.

loadedDocument.Form.Fields.Add(textBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a textbox field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(loadedPage, "FirstName");

textBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the existing PDF document.

loadedDocument.Form.Fields.Add(textBoxField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a textbox field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(loadedPage, "FirstName");

textBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the existing PDF document.

loadedDocument.Form.Fields.Add(textBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}


{% endhighlight %}

{% endtabs %}  


### Adding the combo box field

PdfComboBoxField class is used to create a combo box field in PDF forms. You can add a list of items to the combo box by using the PdfListFieldItem class.

Please refer the below code snippet for adding the combo box in new PDF document:

{% tabs %} 

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a combo box for the first page.

PdfComboBoxField comboBoxField = new PdfComboBoxField(page, "JobTitle");

//Set the combo box properties.

comboBoxField.Bounds = new RectangleF(0, 40, 100, 20);

//Set tooltip.

comboBoxField.ToolTip = "Job Title";

//Add list items.

comboBoxField.Items.Add(new PdfListFieldItem("Development", "accounts"));

comboBoxField.Items.Add(new PdfListFieldItem("Support", "advertise"));

comboBoxField.Items.Add(new PdfListFieldItem("Documentation", "content"));

//Add combo box to the form.

document.Form.Fields.Add(comboBoxField);

//Save the document.

document.Save("Form.pdf");

//Close the document.

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
     

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create a combo box for the first page.

Dim comboBoxField As New PdfComboBoxField(page, "JobTitle")

'Set the combo box properties.

comboBoxField.Bounds = New RectangleF(0, 40, 100, 20)

'Set tooltip

comboBoxField.ToolTip = "Job Title"

'Add list items.

comboBoxField.Items.Add(New PdfListFieldItem("Development", "accounts"))

comboBoxField.Items.Add(New PdfListFieldItem("Support", "advertise"))

comboBoxField.Items.Add(New PdfListFieldItem("Documentation", "content"))

'Add combo box to the form.

document.Form.Fields.Add(comboBoxField)

'Save the PDF document.

document.Save("Form.pdf")

'Close the document                       

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a combo box for the first page.

PdfComboBoxField comboBoxField = new PdfComboBoxField(page, "JobTitle");

//Set the combo box properties.

comboBoxField.Bounds = new RectangleF(0, 40, 100, 20);

//Set tooltip.

comboBoxField.ToolTip = "Job Title";

//Add list items.

comboBoxField.Items.Add(new PdfListFieldItem("Development", "accounts"));

comboBoxField.Items.Add(new PdfListFieldItem("Support", "advertise"));

comboBoxField.Items.Add(new PdfListFieldItem("Documentation", "content"));

//Add combo box to the form.

document.Form.Fields.Add(comboBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a combo box for the first page.

PdfComboBoxField comboBoxField = new PdfComboBoxField(page, "JobTitle");

//Set the combo box properties.

comboBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 40, 100, 20);

//Set tooltip.

comboBoxField.ToolTip = "Job Title";

//Add list items.

comboBoxField.Items.Add(new PdfListFieldItem("Development", "accounts"));

comboBoxField.Items.Add(new PdfListFieldItem("Support", "advertise"));

comboBoxField.Items.Add(new PdfListFieldItem("Documentation", "content"));

//Add combo box to the form.

document.Form.Fields.Add(comboBoxField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a combo box for the first page.

PdfComboBoxField comboBoxField = new PdfComboBoxField(page, "JobTitle");

//Set the combo box properties.

comboBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 40, 100, 20);

//Set tooltip.

comboBoxField.ToolTip = "Job Title";

//Add list items.

comboBoxField.Items.Add(new PdfListFieldItem("Development", "accounts"));

comboBoxField.Items.Add(new PdfListFieldItem("Support", "advertise"));

comboBoxField.Items.Add(new PdfListFieldItem("Documentation", "content"));

//Add combo box to the form.

document.Form.Fields.Add(comboBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}


{% endhighlight %}

{% endtabs %}  

Please refer the below code snippet for adding the combo box in existing PDF document.

{% tabs %} 

{% highlight c# %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Create the form if the form does not exist in the loaded document

if(loadedDocument.Form==null)

loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a combo box for the first page.

PdfComboBoxField comboBoxField = new PdfComboBoxField(loadedPage, "JobTitle");

//Set the combo box properties.

comboBoxField.Bounds = new RectangleF(0, 40, 100, 20);

//Set tooltip.

comboBoxField.ToolTip = "Job Title";

//Add list items.

comboBoxField.Items.Add(new PdfListFieldItem("Development", "accounts"));

comboBoxField.Items.Add(new PdfListFieldItem("Support", "advertise"));

comboBoxField.Items.Add(new PdfListFieldItem("Documentation", "content"));

//Add combo box to the form.

loadedDocument.Form.Fields.Add(comboBoxField);

//Save the document.

loadedDocument.Save("Form.pdf");

//Close the document.

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Create the form if the form does not exist in the loaded document

If loadedDocument.Form Is Nothing Then

loadedDocument.CreateForm()

End If

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create a combo box for the first page.

Dim comboBoxField As New PdfComboBoxField(loadedPage, "JobTitle")

'Set the combo box properties.

comboBoxField.Bounds = New RectangleF(0, 40, 100, 20)

'Set tooltip.

comboBoxField.ToolTip = "Job Title"

'Add list items.

comboBoxField.Items.Add(New PdfListFieldItem("Development", "accounts"))

comboBoxField.Items.Add(New PdfListFieldItem("Support", "advertise"))

comboBoxField.Items.Add(New PdfListFieldItem("Documentation", "content"))

'Add combo box to the form.

loadedDocument.Form.Fields.Add(comboBoxField)

'Save the document.

loadedDocument.Save("Form.pdf")

'Close the document.

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

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a combo box for the first page.

PdfComboBoxField comboBoxField = new PdfComboBoxField(loadedPage, "JobTitle");

//Set the combo box properties.

comboBoxField.Bounds = new RectangleF(0, 40, 100, 20);

//Set tooltip.

comboBoxField.ToolTip = "Job Title";

//Add list items.

comboBoxField.Items.Add(new PdfListFieldItem("Development", "accounts"));

comboBoxField.Items.Add(new PdfListFieldItem("Support", "advertise"));

comboBoxField.Items.Add(new PdfListFieldItem("Documentation", "content"));

//Add combo box to the form.

loadedDocument.Form.Fields.Add(comboBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a combo box for the first page.

PdfComboBoxField comboBoxField = new PdfComboBoxField(loadedPage, "JobTitle");

//Set the combo box properties.

comboBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 40, 100, 20);

//Set tooltip.

comboBoxField.ToolTip = "Job Title";

//Add list items.

comboBoxField.Items.Add(new PdfListFieldItem("Development", "accounts"));

comboBoxField.Items.Add(new PdfListFieldItem("Support", "advertise"));

comboBoxField.Items.Add(new PdfListFieldItem("Documentation", "content"));

//Add combo box to the form.

loadedDocument.Form.Fields.Add(comboBoxField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a combo box for the first page.

PdfComboBoxField comboBoxField = new PdfComboBoxField(loadedPage, "JobTitle");

//Set the combo box properties.

comboBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 40, 100, 20);

//Set tooltip.

comboBoxField.ToolTip = "Job Title";

//Add list items.

comboBoxField.Items.Add(new PdfListFieldItem("Development", "accounts"));

comboBoxField.Items.Add(new PdfListFieldItem("Support", "advertise"));

comboBoxField.Items.Add(new PdfListFieldItem("Documentation", "content"));

//Add combo box to the form.

loadedDocument.Form.Fields.Add(comboBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
        Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
        Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

### Adding the radio button field

To create the radio button in the PDF Forms, you can use PdfRadioButtonListField class and you can create the radio button list items by using the PdfRadioButtonListItem class.

Please refer the below code snippet for adding the radio button in new PDF document:

{% tabs %} 

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Radio button.

PdfRadioButtonListField employeesRadioList = new PdfRadioButtonListField(page, "employeesRadioList");

//Add the radio button into form

document.Form.Fields.Add(employeesRadioList);

//Create radio button items.

PdfRadioButtonListItem radioButtonItem1 = new PdfRadioButtonListItem("1-9");

radioButtonItem1.Bounds = new RectangleF(100, 140, 20, 20);

PdfRadioButtonListItem radioButtonItem2 = new PdfRadioButtonListItem("10-49");

radioButtonItem2.Bounds = new RectangleF(100, 170, 20, 20);

//Add the items to radio button group.

employeesRadioList.Items.Add(radioButtonItem1);

employeesRadioList.Items.Add(radioButtonItem2);

//Save the document.

document.Save("Form.pdf");

//Close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
   

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create a Radio button.

Dim employeesRadioList As New PdfRadioButtonListField(page, "employeesRadioList")

'Add the radio button into form

document.Form.Fields.Add(employeesRadioList)

'Create radio button items.

Dim radioItem1 As New PdfRadioButtonListItem("1-9")

radioItem1.Bounds = New RectangleF(100, 140, 20, 20)

Dim radioItem2 As New PdfRadioButtonListItem("10-49")

radioItem2.Bounds = New RectangleF(100, 170, 20, 20)

'Add the items to radio button group.

employeesRadioList.Items.Add(radioItem1)

employeesRadioList.Items.Add(radioItem2)

'Save the PDF document.

document.Save("Form.pdf")

'close the document

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Radio button.

PdfRadioButtonListField employeesRadioList = new PdfRadioButtonListField(page, "employeesRadioList");

//Add the radio button into form

document.Form.Fields.Add(employeesRadioList);

//Create radio button items.

PdfRadioButtonListItem radioButtonItem1 = new PdfRadioButtonListItem("1-9");

radioButtonItem1.Bounds = new RectangleF(100, 140, 20, 20);

PdfRadioButtonListItem radioButtonItem2 = new PdfRadioButtonListItem("10-49");

radioButtonItem2.Bounds = new RectangleF(100, 170, 20, 20);

//Add the items to radio button group.

employeesRadioList.Items.Add(radioButtonItem1);

employeesRadioList.Items.Add(radioButtonItem2);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Radio button.

PdfRadioButtonListField employeesRadioList = new PdfRadioButtonListField(page, "employeesRadioList");

//Add the radio button into form

document.Form.Fields.Add(employeesRadioList);

//Create radio button items.

PdfRadioButtonListItem radioButtonItem1 = new PdfRadioButtonListItem("1-9");

radioButtonItem1.Bounds = new Syncfusion.Drawing.RectangleF(100, 140, 20, 20);

PdfRadioButtonListItem radioButtonItem2 = new PdfRadioButtonListItem("10-49");

radioButtonItem2.Bounds = new Syncfusion.Drawing.RectangleF(100, 170, 20, 20);

//Add the items to radio button group.

employeesRadioList.Items.Add(radioButtonItem1);

employeesRadioList.Items.Add(radioButtonItem2);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Radio button.

PdfRadioButtonListField employeesRadioList = new PdfRadioButtonListField(page, "employeesRadioList");

//Add the radio button into form

document.Form.Fields.Add(employeesRadioList);

//Create radio button items.

PdfRadioButtonListItem radioButtonItem1 = new PdfRadioButtonListItem("1-9");

radioButtonItem1.Bounds = new Syncfusion.Drawing.RectangleF(100, 140, 20, 20);

PdfRadioButtonListItem radioButtonItem2 = new PdfRadioButtonListItem("10-49");

radioButtonItem2.Bounds = new Syncfusion.Drawing.RectangleF(100, 170, 20, 20);

//Add the items to radio button group.

employeesRadioList.Items.Add(radioButtonItem1);

employeesRadioList.Items.Add(radioButtonItem2);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

The below code snippet illustrates how to add the radio button in existing PDF document:

{% tabs %}  

{% highlight c# %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Create the form if the form does not exist in the loaded document

if(loadedDocument.Form==null)

loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a Radio button.

PdfRadioButtonListField employeesRadioList = new PdfRadioButtonListField(loadedPage, "employeesRadioList");

//Add the radio button into loaded document

loadedDocument.Form.Fields.Add(employeesRadioList);

//Create radio button items.

PdfRadioButtonListItem radioButtonItem1 = new PdfRadioButtonListItem("1-9");

radioButtonItem1.Bounds = new RectangleF(100, 140, 20, 20);

PdfRadioButtonListItem radioButtonItem2 = new PdfRadioButtonListItem("10-49");

radioButtonItem2.Bounds = new RectangleF(100, 170, 20, 20);

//Add the items to radio button group.

employeesRadioList.Items.Add(radioButtonItem1);

employeesRadioList.Items.Add(radioButtonItem2);

//Save the document.

loadedDocument.Save("Form.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Create the form if the form does not exist in the loaded document

If loadedDocument.Form Is Nothing Then

loadedDocument.CreateForm()

End If

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create a Radio button.

Dim employeesRadioList As New PdfRadioButtonListField(loadedPage, "employeesRadioList")

'Add the radio button into loaded document

loadedDocument.Form.Fields.Add(employeesRadioList)

'Create radio button items.

Dim radioButtonItem1 As New PdfRadioButtonListItem("1-9")

radioButtonItem1.Bounds = New RectangleF(100, 140, 20, 20)

Dim radioButtonItem2 As New PdfRadioButtonListItem("10-49")

radioButtonItem2.Bounds = New RectangleF(100, 170, 20, 20)

'Add the items to radio button group.

employeesRadioList.Items.Add(radioButtonItem1)

employeesRadioList.Items.Add(radioButtonItem2)

'Save the document.

loadedDocument.Save("Form.pdf")

'Close the document

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

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a Radio button.

PdfRadioButtonListField employeesRadioList = new PdfRadioButtonListField(loadedPage, "employeesRadioList");

//Add the radio button into loaded document

loadedDocument.Form.Fields.Add(employeesRadioList);

//Create radio button items.

PdfRadioButtonListItem radioButtonItem1 = new PdfRadioButtonListItem("1-9");

radioButtonItem1.Bounds = new RectangleF(100, 140, 20, 20);

PdfRadioButtonListItem radioButtonItem2 = new PdfRadioButtonListItem("10-49");

radioButtonItem2.Bounds = new RectangleF(100, 170, 20, 20);

//Add the items to radio button group.

employeesRadioList.Items.Add(radioButtonItem1);

employeesRadioList.Items.Add(radioButtonItem2);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a Radio button.

PdfRadioButtonListField employeesRadioList = new PdfRadioButtonListField(loadedPage, "employeesRadioList");

//Add the radio button into loaded document

loadedDocument.Form.Fields.Add(employeesRadioList);

//Create radio button items.

PdfRadioButtonListItem radioButtonItem1 = new PdfRadioButtonListItem("1-9");

radioButtonItem1.Bounds = new Syncfusion.Drawing.RectangleF(100, 140, 20, 20);

PdfRadioButtonListItem radioButtonItem2 = new PdfRadioButtonListItem("10-49");

radioButtonItem2.Bounds = new Syncfusion.Drawing.RectangleF(100, 170, 20, 20);

//Add the items to radio button group.

employeesRadioList.Items.Add(radioButtonItem1);

employeesRadioList.Items.Add(radioButtonItem2);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a Radio button.

PdfRadioButtonListField employeesRadioList = new PdfRadioButtonListField(loadedPage, "employeesRadioList");

//Add the radio button into loaded document

loadedDocument.Form.Fields.Add(employeesRadioList);

//Create radio button items.

PdfRadioButtonListItem radioButtonItem1 = new PdfRadioButtonListItem("1-9");

radioButtonItem1.Bounds = new Syncfusion.Drawing.RectangleF(100, 140, 20, 20);

PdfRadioButtonListItem radioButtonItem2 = new PdfRadioButtonListItem("10-49");

radioButtonItem2.Bounds = new Syncfusion.Drawing.RectangleF(100, 170, 20, 20);

//Add the items to radio button group.

employeesRadioList.Items.Add(radioButtonItem1);

employeesRadioList.Items.Add(radioButtonItem2);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

### Adding the list box field

You can create the list box field in PDF forms using PdfListBoxField class.

Please refer the below code snippet for adding the list box field in new PDF document:

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create list box.

PdfListBoxField listBoxField = new PdfListBoxField(page, "list1");

//Set the properties.

listBoxField.Bounds = new RectangleF(100, 60, 100, 50);

//Add the items to the list box.

listBoxField.Items.Add(new PdfListFieldItem("English", "English"));

listBoxField.Items.Add(new PdfListFieldItem("French", "French"));

listBoxField.Items.Add(new PdfListFieldItem("German", "German"));

//Select the item.

listBoxField.SelectedIndex = 2;

//Set the multi select option.

listBoxField.MultiSelect = true;

//Add the list box into PDF document

document.Form.Fields.Add(listBoxField);

//Save the document.

document.Save("Form.pdf");

//close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
 

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create list box.

Dim listBoxField As New PdfListBoxField(page, "list1")

'Set the properties.

listBoxField.Bounds = New RectangleF(100, 60, 100, 50)

'Add the items to the list box.

listBoxField.Items.Add(New PdfListFieldItem("English", "English"))

listBoxField.Items.Add(New PdfListFieldItem("French", "French"))

listBoxField.Items.Add(New PdfListFieldItem("German", "German"))

'Select the item.

listBoxField.SelectedIndex = 2

'Set the multi select option.

listBoxField.MultiSelect = True

'Add the list box into PDF document

document.Form.Fields.Add(listBoxField)

'Save the document.

document.Save("Form.pdf")

'close the document

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create list box.

PdfListBoxField listBoxField = new PdfListBoxField(page, "list1");

//Set the properties.

listBoxField.Bounds = new RectangleF(100, 60, 100, 50);

//Add the items to the list box.

listBoxField.Items.Add(new PdfListFieldItem("English", "English"));

listBoxField.Items.Add(new PdfListFieldItem("French", "French"));

listBoxField.Items.Add(new PdfListFieldItem("German", "German"));

//Select the item.

listBoxField.SelectedIndex = 2;

//Set the multi select option.

listBoxField.MultiSelect = true;

//Add the list box into PDF document

document.Form.Fields.Add(listBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create list box.

PdfListBoxField listBoxField = new PdfListBoxField(page, "list1");

//Set the properties.

listBoxField.Bounds = new Syncfusion.Drawing.RectangleF(100, 60, 100, 50);

//Add the items to the list box.

listBoxField.Items.Add(new PdfListFieldItem("English", "English"));

listBoxField.Items.Add(new PdfListFieldItem("French", "French"));

listBoxField.Items.Add(new PdfListFieldItem("German", "German"));

//Select the item.

listBoxField.SelectedIndex = 0;

//Set the multi select option.

listBoxField.MultiSelect = true;

//Add the list box into PDF document

document.Form.Fields.Add(listBoxField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create list box.

PdfListBoxField listBoxField = new PdfListBoxField(page, "list1");

//Set the properties.

listBoxField.Bounds = new Syncfusion.Drawing.RectangleF(100, 60, 100, 50);

//Add the items to the list box.

listBoxField.Items.Add(new PdfListFieldItem("English", "English"));

listBoxField.Items.Add(new PdfListFieldItem("French", "French"));

listBoxField.Items.Add(new PdfListFieldItem("German", "German"));

//Select the item.

listBoxField.SelectedIndex = 2;

//Set the multi select option.

listBoxField.MultiSelect = true;

//Add the list box into PDF document

document.Form.Fields.Add(listBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

Please refer the below code snippet for adding the list box field in existing PDF document:

{% tabs %} 

{% highlight c# %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Create the form if the form does not exist in the loaded document

if(loadedDocument.Form==null)

loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create list box.

PdfListBoxField listBoxField = new PdfListBoxField(loadedPage, "list1");

//Set the properties.

listBoxField.Bounds = new RectangleF(100, 60, 100, 50);

//Add the items to the list box.

listBoxField.Items.Add(new PdfListFieldItem("English", "English"));

listBoxField.Items.Add(new PdfListFieldItem("French", "French"));

listBoxField.Items.Add(new PdfListFieldItem("German", "German"));

//Select the item.

listBoxField.SelectedIndex = 2;

//Set the multi select option.

listBoxField.MultiSelect = true;

//Add the list box into PDF document

loadedDocument.Form.Fields.Add(listBoxField);

//Save the document.

loadedDocument.Save("Form.pdf");

//close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Create the form if the form does not exist in the loaded document

If loadedDocument.Form Is Nothing Then

loadedDocument.CreateForm()

End If

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create list box.

Dim listBoxField As New PdfListBoxField(loadedPage, "list1")

'Set the properties.

listBoxField.Bounds = New RectangleF(100, 60, 100, 50)

'Add the items to the list box.

listBoxField.Items.Add(New PdfListFieldItem("English", "English"))

listBoxField.Items.Add(New PdfListFieldItem("French", "French"))

listBoxField.Items.Add(New PdfListFieldItem("German", "German"))

'Select the item.

listBoxField.SelectedIndex = 2

'Set the multi select option.

listBoxField.MultiSelect = True

'Add the list box into PDF document

loadedDocument.Form.Fields.Add(listBoxField)

'Save the document.

loadedDocument.Save("Form.pdf")

'close the document

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

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create list box.

PdfListBoxField listBoxField = new PdfListBoxField(loadedPage, "list1");

//Set the properties.

listBoxField.Bounds = new RectangleF(100, 60, 100, 50);

//Add the items to the list box.

listBoxField.Items.Add(new PdfListFieldItem("English", "English"));

listBoxField.Items.Add(new PdfListFieldItem("French", "French"));

listBoxField.Items.Add(new PdfListFieldItem("German", "German"));

//Select the item.

listBoxField.SelectedIndex = 2;

//Set the multi select option.

listBoxField.MultiSelect = true;

//Add the list box into PDF document

loadedDocument.Form.Fields.Add(listBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create list box.

PdfListBoxField listBoxField = new PdfListBoxField(loadedPage, "list1");

//Set the properties.

listBoxField.Bounds = new Syncfusion.Drawing.RectangleF(100, 60, 100, 50);

//Add the items to the list box.

listBoxField.Items.Add(new PdfListFieldItem("English", "English"));

listBoxField.Items.Add(new PdfListFieldItem("French", "French"));

listBoxField.Items.Add(new PdfListFieldItem("German", "German"));

//Select the item.

listBoxField.SelectedIndex = 2;

//Set the multi select option.

listBoxField.MultiSelect = true;

//Add the list box into PDF document

loadedDocument.Form.Fields.Add(listBoxField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create list box.

PdfListBoxField listBoxField = new PdfListBoxField(loadedPage, "list1");

//Set the properties.

listBoxField.Bounds = new Syncfusion.Drawing.RectangleF(100, 60, 100, 50);

//Add the items to the list box.

listBoxField.Items.Add(new PdfListFieldItem("English", "English"));

listBoxField.Items.Add(new PdfListFieldItem("French", "French"));

listBoxField.Items.Add(new PdfListFieldItem("German", "German"));

//Select the item.

listBoxField.SelectedIndex = 2;

//Set the multi select option.

listBoxField.MultiSelect = true;

//Add the list box into PDF document

loadedDocument.Form.Fields.Add(listBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}


{% endhighlight %}

{% endtabs %}  
 

### Adding the check Box field

You can create the check box field in PDF forms using PdfCheckBoxField class. 

Please refer the below code snippet for adding the check box field in new PDF document:

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create Check Box field.

PdfCheckBoxField checkBoxField = new PdfCheckBoxField(page, "CheckBox");

//Set check box properties.

checkBoxField.ToolTip = "Check Box";

checkBoxField.Bounds = new RectangleF(0, 20, 10, 10);

//Add the form field to the document.

document.Form.Fields.Add(checkBoxField);

//Save the document.

document.Save("Form.pdf");

//close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
  

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create Check Box field.

Dim checkBoxField As New PdfCheckBoxField(page, "CheckBox")

'Set check box properties.

checkBoxField.ToolTip = "Check Box"

checkBoxField.Bounds = New RectangleF(0, 20, 10, 10)

'Add the form field to the document.

document.Form.Fields.Add(checkBoxField)

'Save the document.

document.Save("Form.pdf")

'close the document

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create Check Box field.

PdfCheckBoxField checkBoxField = new PdfCheckBoxField(page, "CheckBox");

//Set check box properties.

checkBoxField.ToolTip = "Check Box";

checkBoxField.Bounds = new RectangleF(0, 20, 10, 10);

//Add the form field to the document.

document.Form.Fields.Add(checkBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create Check Box field.

PdfCheckBoxField checkBoxField = new PdfCheckBoxField(page, "CheckBox");

//Set check box properties.

checkBoxField.ToolTip = "Check Box";

checkBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 20, 10, 10);

//Add the form field to the document.

document.Form.Fields.Add(checkBoxField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create Check Box field.

PdfCheckBoxField checkBoxField = new PdfCheckBoxField(page, "CheckBox");

//Set check box properties.

checkBoxField.ToolTip = "Check Box";

checkBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 20, 10, 10);

//Add the form field to the document.

document.Form.Fields.Add(checkBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}


{% endhighlight %}

{% endtabs %}  

Please refer the below code snippet for adding the check box field in existing PDF document:

{% tabs %}

{% highlight c# %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Create the form if the form does not exist in the loaded document

if(loadedDocument.Form==null)

loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create Check Box field.

PdfCheckBoxField checkBoxField = new PdfCheckBoxField(loadedPage, "CheckBox");

//Set check box properties.

checkBoxField.ToolTip = "Check Box";

checkBoxField.Bounds = new RectangleF(0, 20, 10, 10);

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(checkBoxField);

//Save the document.

loadedDocument.Save("Form.pdf");

//close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Create the form if the form does not exist in the loaded document

If loadedDocument.Form Is Nothing Then

loadedDocument.CreateForm()

End If

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create Check Box field.

Dim checkBoxField As New PdfCheckBoxField(loadedPage, "CheckBox")

'Set check box properties.

checkBoxField.ToolTip = "Check Box"

checkBoxField.Bounds = New RectangleF(0, 20, 10, 10)

'Add the form field to the existing document.

loadedDocument.Form.Fields.Add(checkBoxField)

'Save the document.

loadedDocument.Save("Form.pdf")

'close the document

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

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create Check Box field.

PdfCheckBoxField checkBoxField = new PdfCheckBoxField(loadedPage, "CheckBox");

//Set check box properties.

checkBoxField.ToolTip = "Check Box";

checkBoxField.Bounds = new RectangleF(0, 20, 10, 10);

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(checkBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create Check Box field.

PdfCheckBoxField checkBoxField = new PdfCheckBoxField(loadedPage, "CheckBox");

//Set check box properties.

checkBoxField.ToolTip = "Check Box";

checkBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 20, 10, 10);

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(checkBoxField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

  loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create Check Box field.

PdfCheckBoxField checkBoxField = new PdfCheckBoxField(loadedPage, "CheckBox");

//Set check box properties.

checkBoxField.ToolTip = "Check Box";

checkBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 20, 10, 10);

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(checkBoxField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  
  

### Adding the signature field

You can add the signature field in PDF forms using PdfSignatureField class.

Please refer the below code snippet for adding the signature field in new PDF document:

{% tabs %} 

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create PDF Signature field.

PdfSignatureField signatureField = new PdfSignatureField(page, "Signature");

//Set properties to the signature field.

signatureField.Bounds = new RectangleF(0, 400, 90, 20);

signatureField.ToolTip = "Signature";

//Add the form field to the document.

document.Form.Fields.Add(signatureField);

//Save the document.

document.Save("Form.pdf");

//Close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF Signature field.

Dim signatureField As New PdfSignatureField(page, "Signature")

'Set properties to the signature field.

signatureField.Bounds = New RectangleF(0, 400, 90, 20)

signatureField.ToolTip = "Signature"

'Add the form field to the document.

document.Form.Fields.Add(signatureField)

'Save the document.

document.Save("Form.pdf")

'Close the document

document.Close(True)





{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create PDF Signature field.

PdfSignatureField signatureField = new PdfSignatureField(page, "Signature");

//Set properties to the signature field.

signatureField.Bounds = new RectangleF(0, 400, 90, 20);

signatureField.ToolTip = "Signature";

//Add the form field to the document.

document.Form.Fields.Add(signatureField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create PDF Signature field.

PdfSignatureField signatureField = new PdfSignatureField(page, "Signature");

//Set properties to the signature field.

signatureField.Bounds = new Syncfusion.Drawing.RectangleF(0, 400, 90, 20);

signatureField.ToolTip = "Signature";

//Add the form field to the document.

document.Form.Fields.Add(signatureField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create PDF Signature field.

PdfSignatureField signatureField = new PdfSignatureField(page, "Signature");

//Set properties to the signature field.

signatureField.Bounds = new Syncfusion.Drawing.RectangleF(0, 400, 90, 20);

signatureField.ToolTip = "Signature";

//Add the form field to the document.

document.Form.Fields.Add(signatureField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}


{% endhighlight %}

{% endtabs %}  

Please refer the below code snippet for adding the signature field in existing PDF document:

{% tabs %} 

{% highlight c# %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Create the form if the form does not exist in the loaded document

if(loadedDocument.Form==null)

loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create PDF Signature field.

PdfSignatureField signatureField = new PdfSignatureField(loadedPage, "Signature");

//Set properties to the signature field.

signatureField.Bounds = new RectangleF(0, 400, 90, 20);

signatureField.ToolTip = "Signature";

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(signatureField);

//Save the document.

loadedDocument.Save("Form.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Create the form if the form does not exist in the loaded document

If loadedDocument.Form Is Nothing Then

loadedDocument.CreateForm()

End If

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create PDF Signature field.

Dim signatureField As New PdfSignatureField(loadedPage, "Signature")

'Set properties to the signature field.

signatureField.Bounds = New RectangleF(0, 400, 90, 20)

signatureField.ToolTip = "Signature"

'Add the form field to the existing document.

loadedDocument.Form.Fields.Add(signatureField)

'Save the document.

loadedDocument.Save("Form.pdf")

'Close the document

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

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create PDF Signature field.

PdfSignatureField signatureField = new PdfSignatureField(loadedPage, "Signature");

//Set properties to the signature field.

signatureField.Bounds = new RectangleF(0, 400, 90, 20);

signatureField.ToolTip = "Signature";

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(signatureField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create PDF Signature field.

PdfSignatureField signatureField = new PdfSignatureField(loadedPage, "Signature");

//Set properties to the signature field.

signatureField.Bounds = new Syncfusion.Drawing.RectangleF(0, 400, 90, 20);

signatureField.ToolTip = "Signature";

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(signatureField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create PDF Signature field.

PdfSignatureField signatureField = new PdfSignatureField(loadedPage, "Signature");

//Set properties to the signature field.

signatureField.Bounds = new Syncfusion.Drawing.RectangleF(0, 400, 90, 20);

signatureField.ToolTip = "Signature";

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(signatureField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

### Adding the button field 

To create Button fields in PDF forms, you can use PdfButtonField class.

The below code illustrates how to add the button field in new PDF document:

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Button.

PdfButtonField buttonField = new PdfButtonField(page, "Click");

//Set properties to the Button field.

buttonField.Bounds = new RectangleF(0, 150, 90, 20);

buttonField.Text = "Click";

//Add the form field to the document.

document.Form.Fields.Add(buttonField);

//Save the document.

document.Save("Form.pdf");

//close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
    

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create a Button.

Dim buttonField As New PdfButtonField(page, "Click")

'Set properties to the Button field.

buttonField.Bounds = New RectangleF(0, 150, 90, 20)

buttonField.Text = "Click"

'Add the form field to the document.

document.Form.Fields.Add(buttonField)

'Save the document.

document.Save("Form.pdf")

'close the document

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Button.

PdfButtonField buttonField = new PdfButtonField(page, "Click");

//Set properties to the Button field.

buttonField.Bounds = new RectangleF(0, 150, 90, 20);

buttonField.Text = "Click";

//Add the form field to the document.

document.Form.Fields.Add(buttonField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Button.

PdfButtonField buttonField = new PdfButtonField(page, "Click");

//Set properties to the Button field.

buttonField.Bounds = new Syncfusion.Drawing.RectangleF(0, 150, 90, 20);

buttonField.Text = "Click";

//Add the form field to the document.

document.Form.Fields.Add(buttonField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Button.

PdfButtonField buttonField = new PdfButtonField(page, "Click");

//Set properties to the Button field.

buttonField.Bounds = new Syncfusion.Drawing.RectangleF(0, 150, 90, 20);

buttonField.Text = "Click";

//Add the form field to the document.

document.Form.Fields.Add(buttonField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

Please refer the below code snippet for adding the button field in existing PDF document:

{% tabs %}  

{% highlight c# %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a Button and set properties to the Button field.

PdfButtonField buttonField = new PdfButtonField(loadedPage, "Click");

buttonField.Bounds = new RectangleF(0, 150, 90, 20);

buttonField.Text = "Click";

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(buttonField);

//Save the document.

loadedDocument.Save("Form.pdf");

//close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Create the form if the form does not exist in the loaded document

If loadedDocument.Form Is Nothing Then

loadedDocument.CreateForm()

End If

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create a Button and set properties to the Button field.

Dim buttonField As New PdfButtonField(loadedPage, "Click")

buttonField.Bounds = New RectangleF(0, 150, 90, 20)

buttonField.Text = "Click"

'Add the form field to the existing document.

loadedDocument.Form.Fields.Add(buttonField)

'Save the document.

loadedDocument.Save("Form.pdf")

'close the document

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

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a Button and set properties to the Button field.

PdfButtonField buttonField = new PdfButtonField(loadedPage, "Click");

buttonField.Bounds = new RectangleF(0, 150, 90, 20);

buttonField.Text = "Click";

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(buttonField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a Button and set properties to the Button field.

PdfButtonField buttonField = new PdfButtonField(loadedPage, "Click");

buttonField.Bounds = new Syncfusion.Drawing.RectangleF(0, 150, 90, 20);

buttonField.Text = "Click";

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(buttonField);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

 //Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create the form if the form does not exist in the loaded document

if (loadedDocument.Form == null)

    loadedDocument.CreateForm();

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a Button and set properties to the Button field.

PdfButtonField buttonField = new PdfButtonField(loadedPage, "Click");

buttonField.Bounds = new Syncfusion.Drawing.RectangleF(0, 150, 90, 20);

buttonField.Text = "Click";

//Add the form field to the existing document.

loadedDocument.Form.Fields.Add(buttonField);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
      Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  


## Modifying the existing form field in PDF document 

You can modify an existing form field by getting the field from the form field collection. You can retrieve a field from the field collection by index or by field name. 

The following code snippet explains how to modify an existing form field in a PDF document.

{% tabs %}  

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded form field and modify the properties.

PdfLoadedTextBoxField loadedTextBoxField= loadedForm.Fields[0] as PdfLoadedTextBoxField;

RectangleF newBounds = new RectangleF(100, 100, 150, 50);

loadedTextBoxField.Bounds = newBounds;

loadedTextBoxField.SpellCheck = true;

loadedTextBoxField.Text = "New text of the field.";

loadedTextBoxField.Password = false;

//Save the document.

loadedDocument.Save("sample.pdf");

//close the document

loadedDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Get the loaded form field and Modify the properties.

Dim loadedTextBoxField As PdfLoadedTextBoxField = TryCast(loadedForm.Fields(0), PdfLoadedTextBoxField)

Dim newBounds As New RectangleF(100, 100, 150, 50)

loadedTextBoxField.Bounds = newBounds

loadedTextBoxField.SpellCheck = True

loadedTextBoxField.Text = "New text of the field."

loadedTextBoxField.Password = False

'Save the document.

loadedDocument.Save("sample.pdf")

'close the document

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

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded form field and modify the properties.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

RectangleF newBounds = new RectangleF(100, 100, 150, 50);

loadedTextBoxField.Bounds = newBounds;

loadedTextBoxField.SpellCheck = true;

loadedTextBoxField.Text = "New text of the field.";

loadedTextBoxField.Password = false;

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded form field and modify the properties.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

RectangleF newBounds = new RectangleF(100, 100, 150, 50);

loadedTextBoxField.Bounds = newBounds;

loadedTextBoxField.SpellCheck = true;

loadedTextBoxField.Text = "New text of the field.";

loadedTextBoxField.Password = false;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded form field and modify the properties.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

Syncfusion.Drawing.RectangleF newBounds = new Syncfusion.Drawing.RectangleF(100, 100, 150, 50);

loadedTextBoxField.Bounds = newBounds;

loadedTextBoxField.SpellCheck = true;

loadedTextBoxField.Text = "New text of the field.";

loadedTextBoxField.Password = false;

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

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


## Filling form fields in an existing PDF Document

Essential PDF allows you to fill the form fields using PdfLoadedField class. 

### Filling the text box field

Please refer the below sample for filling a textbox field.

{% tabs %}  

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded text box field and fill it.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "First Name";

//Save the modified document.

loadedDocument.Save("sample.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Get the loaded text box field and fill it.

Dim loadedTextBoxField As PdfLoadedTextBoxField = TryCast(loadedForm.Fields(0), PdfLoadedTextBoxField)

loadedTextBoxField.Text = "First Name"

'Save the modified document.

loadedDocument.Save("sample.pdf")

'Close the document

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

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded text box field and fill it.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "First Name";

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded text box field and fill it.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "First Name";

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded text box field and fill it.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "First Name";

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

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

### Filling the combo box field

The below code snippet illustrates how to fill the combo box field in an existing PDF document.

{% tabs %} 

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded combo box field  and modify the properties

PdfLoadedComboBoxField loadedComboboxField = loadedForm.Fields[1] as PdfLoadedComboBoxField;

loadedComboboxField.SelectedIndex = 1;

//Save the modified document.

loadedDocument.Save("sample.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Get the loaded combo box field and modify the properties

Dim loadedComboboxField As PdfLoadedComboBoxField = TryCast(loadedForm.Fields(1), PdfLoadedComboBoxField)

loadedComboboxField.SelectedIndex = 1

'Save the modified document.

loadedDocument.Save("sample.pdf")

'Close the document

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

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded combo box field  and modify the properties

PdfLoadedComboBoxField loadedComboboxField = loadedForm.Fields[1] as PdfLoadedComboBoxField;

loadedComboboxField.SelectedIndex = 1;

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "sample.pdf"); 


{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded combo box field  and modify the properties

PdfLoadedComboBoxField loadedComboboxField = loadedForm.Fields[1] as PdfLoadedComboBoxField;

loadedComboboxField.SelectedIndex = 1;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded combo box field  and modify the properties

PdfLoadedComboBoxField loadedComboboxField = loadedForm.Fields[1] as PdfLoadedComboBoxField;

loadedComboboxField.SelectedIndex = 1;

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

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

### Filling the radio button field

Please refer the below code snippet to fill the radio button field in an existing PDF document.

{% tabs %}  

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded radio button field.

PdfLoadedRadioButtonListField loadedRadioButtonField = loadedForm.Fields[3] as PdfLoadedRadioButtonListField;

loadedRadioButtonField.SelectedIndex = 1;

//Save the modified document.

loadedDocument.Save("sample.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Get the loaded radio button field.

Dim loadedRadioButtonField As PdfLoadedRadioButtonListField = TryCast(loadedForm.Fields(3), PdfLoadedRadioButtonListField)

loadedRadioButtonField.SelectedIndex = 1

'Save the modified document.

loadedDocument.Save("sample.pdf")

'Close the document

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

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded radio button field.

PdfLoadedRadioButtonListField loadedRadioButtonField = loadedForm.Fields[3] as PdfLoadedRadioButtonListField;

loadedRadioButtonField.SelectedIndex = 1;

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded radio button field.

PdfLoadedRadioButtonListField loadedRadioButtonField = loadedForm.Fields[3] as PdfLoadedRadioButtonListField;

loadedRadioButtonField.SelectedIndex = 1;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded radio button field.

PdfLoadedRadioButtonListField loadedRadioButtonField = loadedForm.Fields[0] as PdfLoadedRadioButtonListField;

loadedRadioButtonField.SelectedIndex = 1;

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

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


### Filling the list box field

The below code snippet illustrates how to fill the list box field in an existing PDF document.

{% tabs %} 

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Fill list box.

PdfLoadedListBoxField loadedListBox = loadedForm.Fields[2] as PdfLoadedListBoxField;

// Fill list box and Modify the list box select index

loadedListBox.SelectedIndex = new int[2] { 1, 2 };

//Save the modified document.

loadedDocument.Save("sample.pdf");

//Close the document

loadedDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Fill list box and Modify the list box select index

Dim loadedListBox As PdfLoadedListBoxField = TryCast(loadedForm.Fields(0), PdfLoadedListBoxField)

loadedListBox.SelectedIndex = New Integer(1) {1, 2}

'Save the modified document.

loadedDocument.Save("sample.pdf")

'close the document

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

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Fill list box.

PdfLoadedListBoxField loadedListBox = loadedForm.Fields[2] as PdfLoadedListBoxField;

// Fill list box and Modify the list box select index

loadedListBox.SelectedIndex = new int[2] { 1, 2 };

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Fill list box.

PdfLoadedListBoxField loadedListBox = loadedForm.Fields[2] as PdfLoadedListBoxField;

// Fill list box and Modify the list box select index

loadedListBox.SelectedIndex = new int[2] { 1, 2 };

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Fill list box.

PdfLoadedListBoxField loadedListBox = loadedForm.Fields[2] as PdfLoadedListBoxField;

// Fill list box and Modify the list box select index

loadedListBox.SelectedIndex = new int[2] { 1, 2 };

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

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

### Filling the check Box field

Please refer the below code snippet to fill the check box field.

{% tabs %} 

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//load the check box from field collection

PdfLoadedCheckBoxField loadedCheckBoxField = loadedForm.Fields[0] as PdfLoadedCheckBoxField;

// fill the checkbox .

loadedCheckBoxField.Items[0].Checked = true;

//Check the checkbox if it is not grouped.

loadedCheckBoxField.Checked = true;

//Save the modified document.

loadedDocument.Save("sample.pdf");

//close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'load the check box from field collection

Dim loadedCheckBoxField As PdfLoadedCheckBoxField = TryCast(loadedForm.Fields(0), PdfLoadedCheckBoxField)

'Fill the checkbox.

loadedCheckBoxField.Items(0).Checked = True

'Check the checkbox if it is not grouped.

loadedCheckBoxField.Checked = True

'Save the modified document.

loadedDocument.Save("sample.pdf")

'Close the document

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

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//load the check box from field collection

PdfLoadedCheckBoxField loadedCheckBoxField = loadedForm.Fields[0] as PdfLoadedCheckBoxField;

// fill the checkbox .

loadedCheckBoxField.Items[0].Checked = true;

//Check the checkbox if it is not grouped.

loadedCheckBoxField.Checked = true;

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//load the check box from field collection

PdfLoadedCheckBoxField loadedCheckBoxField = loadedForm.Fields[0] as PdfLoadedCheckBoxField;

// fill the checkbox .

loadedCheckBoxField.Items[0].Checked = true;

//Check the checkbox if it is not grouped.

loadedCheckBoxField.Checked = true;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//load the check box from field collection

PdfLoadedCheckBoxField loadedCheckBoxField = loadedForm.Fields[0] as PdfLoadedCheckBoxField;

// fill the checkbox .

loadedCheckBoxField.Items[0].Checked = true;

//Check the checkbox if it is not grouped.

loadedCheckBoxField.Checked = true;

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

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

### Filling the signature field

The below code snippet illustrates how to fill the signature field with certificate:

{% tabs %} 

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Create PDF Certificate.

PdfCertificate certificate = new PdfCertificate("Pdf.pfx", "password");

//Load the signature field from field collection and fill this with certificate

PdfLoadedSignatureField loadedSignatureField = loadedForm.Fields[0] as PdfLoadedSignatureField;

loadedSignatureField.Signature = new PdfSignature(loadedPage);

loadedSignatureField.Signature.Certificate = certificate;

loadedSignatureField.Signature.Reason = "Reason";

//Save the modified document.

loadedDocument.Save("output.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Create PDF Certificate.

Dim certificate As New PdfCertificate("Pdf.pfx", "password")

'Load the signature field from field collection and fill with certificate

Dim loadedSignatureField As PdfLoadedSignatureField = TryCast(loadedForm.Fields(0), PdfLoadedSignatureField)

loadedSignatureField.Signature = New PdfSignature(loadedPage)

loadedSignatureField.Signature.Certificate = certificate

loadedSignatureField.Signature.Reason = "Reason"

'Save the modified document.

loadedDocument.Save("output.pdf")

'Close the document

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

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the loaded form

PdfLoadedForm loadedForm = loadedDocument.Form;

//Create PDF Certificate

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");

PdfCertificate certificate = new PdfCertificate(certificateStream, "syncfusion");

//Load the signature field from field collection and fill this with certificate

PdfLoadedSignatureField loadedSignatureField = loadedForm.Fields[9] as PdfLoadedSignatureField;

loadedSignatureField.Signature = new PdfSignature();

loadedSignatureField.Signature.Certificate = certificate;

loadedSignatureField.Signature.Reason = "Reason";

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the loaded form

PdfLoadedForm loadedForm = loadedDocument.Form;

//Create PDF Certificate

FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);

PdfCertificate certificate = new PdfCertificate(certificateStream, "syncfusion");

//Load the signature field from field collection and fill this with certificate

PdfLoadedSignatureField loadedSignatureField = loadedForm.Fields[9] as PdfLoadedSignatureField

loadedSignatureField.Signature = new PdfSignature();

loadedSignatureField.Signature.Certificate = certificate;

loadedSignatureField.Signature.Reason = "Reason";

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the loaded form

PdfLoadedForm loadedForm = loadedDocument.Form;

//Create PDF Certificate

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");

PdfCertificate certificate = new PdfCertificate(certificateStream, "syncfusion");

//Load the signature field from field collection and fill this with certificate

PdfLoadedSignatureField loadedSignatureField = loadedForm.Fields[9] as PdfLoadedSignatureField;

loadedSignatureField.Signature = new PdfSignature();

loadedSignatureField.Signature.Certificate = certificate;

loadedSignatureField.Signature.Reason = "Reason";

//Save the PDF document to stream.

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

### Enumerate the form fields

You can enumerate the fields from form field collection and fill them. 

The following code example illustrates how to enumerate the form fields.

{% tabs %} 

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument document = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm form = document.Form;

PdfLoadedFormFieldCollection fields = form.Fields;

//Enumerates the form fields.

for (int i = 0; i < fields.Count; i++)

{

if (fields[i] is PdfLoadedTextBoxField)

{

PdfLoadedTextBoxField loadedTextBoxField = fields[i] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "Text";

}

}

//Save and close the modified document.

document.Save(OutputFileName);

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim document As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim form As PdfLoadedForm = document.Form

Dim fields As PdfLoadedFormFieldCollection = form.Fields

'Enumerate the form fields.

For i As Integer = 0 To fields.Count - 1

If TypeOf fields(i) Is PdfLoadedTextBoxField Then

Dim loadedTextBoxField As PdfLoadedTextBoxField = TryCast(fields(i), PdfLoadedTextBoxField)

loadedTextBoxField.Text = "Text"

End If

Next i

'Save and close the modified document.

document.Save(OutputFileName)

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

//Get the loaded form.

PdfLoadedForm form = document.Form;

PdfLoadedFormFieldCollection fields = form.Fields;

//Enumerates the form fields.

for (int i = 0; i < fields.Count; i++)

{

    if (fields[i] is PdfLoadedTextBoxField)

    {

        PdfLoadedTextBoxField loadedTextBoxField = fields[i] as PdfLoadedTextBoxField;

        loadedTextBoxField.Text = "Text";

    }

}

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm form = document.Form;

PdfLoadedFormFieldCollection fields = form.Fields;

//Enumerates the form fields.

for (int i = 0; i < fields.Count; i++)

{

    if (fields[i] is PdfLoadedTextBoxField)

    {

        PdfLoadedTextBoxField loadedTextBoxField = fields[i] as PdfLoadedTextBoxField;

        loadedTextBoxField.Text = "Text";

    }

}

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm form = document.Form;

PdfLoadedFormFieldCollection fields = form.Fields;

//Enumerates the form fields.

for (int i = 0; i < fields.Count; i++)

{

    if (fields[i] is PdfLoadedTextBoxField)

    {

        PdfLoadedTextBoxField loadedTextBoxField = fields[i] as PdfLoadedTextBoxField;

        loadedTextBoxField.Text = "Text";

    }

}

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

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
 

### TryGetField

To get a form field from an existing document using the field name, you can use the TryGetField method in the PdfFormFieldCollection class. It specifies whether the particular field is available in the form or not by returning a Boolean value.

The below code snippet explains how to get the field from collection using TryGetField method.

{% tabs %} 

{% highlight c# %}


// Load the document.

PdfLoadedDocument doc = new PdfLoadedDocument(fileName);

// Load the form from the loaded document.

PdfLoadedForm form = doc.Form;

// Load the form field collections from the form.

PdfLoadedFormFieldCollection fieldCollection = form.Fields as PdfLoadedFormFieldCollection;

PdfLoadedField loadedField = null;

// Get the field using TryGetField Method.

if (fieldCollection.TryGetField("f1-1", out loadedField))

{

(loadedField as PdfLoadedTextBoxField).Text = "1";

}

//Save and close the modified document.

doc.Save("output.pdf");

doc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


' Load the document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

' Load the form from the loaded document.

Dim form As PdfLoadedForm = loadedDocument.Form

' Load the form field collections from the form.

Dim fieldCollection As PdfLoadedFormFieldCollection = TryCast(form.Fields, PdfLoadedFormFieldCollection)

Dim loadedField As PdfLoadedField = Nothing

' Get the field using TryGetField Method.

If fieldCollection.TryGetField("f1-1", loadedField) Then

TryCast(loadedField, PdfLoadedTextBoxField).Text = "1"

End If

'Save and close the modified document.

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

PdfLoadedDocument doc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await doc.OpenAsync(file);

// Load the form from the loaded document.

PdfLoadedForm form = doc.Form;

// Load the form field collections from the form.

PdfLoadedFormFieldCollection fieldCollection = form.Fields as PdfLoadedFormFieldCollection;

PdfLoadedField loadedField = null;

// Get the field using TryGetField Method.

if (fieldCollection.TryGetField("f1-1", out loadedField))

{

    (loadedField as PdfLoadedTextBoxField).Text = "1";

}

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

// Load the form from the loaded document.

PdfLoadedForm form = doc.Form;

// Load the form field collections from the form.

PdfLoadedFormFieldCollection fieldCollection = form.Fields as PdfLoadedFormFieldCollection;

PdfLoadedField loadedField = null;

// Get the field using TryGetField Method.

if (fieldCollection.TryGetField("f1-1", out loadedField))

{

    (loadedField as PdfLoadedTextBoxField).Text = "1";

}

//Save the document into stream.

MemoryStream stream = new MemoryStream();

doc.Save(stream);

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

// Load the form from the loaded document.

PdfLoadedForm form = doc.Form;

// Load the form field collections from the form.

PdfLoadedFormFieldCollection fieldCollection = form.Fields as PdfLoadedFormFieldCollection;

PdfLoadedField loadedField = null;

// Get the field using TryGetField Method.

if (fieldCollection.TryGetField("f1-1", out loadedField))

{

    (loadedField as PdfLoadedTextBoxField).Text = "1";

}

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

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

### TryGetValue

To get the field value from the given field name, you can use TryGetValue method in PdfFormFieldCollection class. It specifies whether the particular field is available in the form or not by returning a boolean value.

Please refer the below code snippet to get the field value from collection using TryGetValue method.

{% tabs %} 

{% highlight c# %}


// Load the document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(filename);

// Load the form from the loaded document.

PdfLoadedForm form = loadedDocument.Form;

// Load the form field collections from the form.

PdfLoadedFormFieldCollection fieldCollection = form.Fields as PdfLoadedFormFieldCollection;

string fieldValue = string.Empty;

// Get the field value using TryGetValue Method

fieldCollection.TryGetValue("f1-2", out fieldValue);

//Save and close the modified document.

loadedDocument.Save("output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


' Load the document.

Dim loadedDocument As New PdfLoadedDocument(filename)

' Load the form from the loaded document.

Dim form As PdfLoadedForm = loadedDocument.Form

' Load the form field collections from the form.

Dim fieldCollection As PdfLoadedFormFieldCollection = TryCast(form.Fields, PdfLoadedFormFieldCollection)

Dim fieldValue As String = String.Empty

' Get the field value using TryGetValue Method

fieldCollection.TryGetValue("f1-2", fieldValue)

'Save and close the modified document.

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

// Load the form from the loaded document

PdfLoadedForm form = loadedDocument.Form;

// Load the form field collections from the form

PdfLoadedFormFieldCollection fieldCollection = form.Fields as PdfLoadedFormFieldCollection;

string fieldValue = string.Empty;

// Get the field value using TryGetValue Method

fieldCollection.TryGetValue("f1-2", out fieldValue);

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

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

// Load the form from the loaded document.

PdfLoadedForm form = loadedDocument.Form;

// Load the form field collections from the form.

PdfLoadedFormFieldCollection fieldCollection = form.Fields as PdfLoadedFormFieldCollection;

string fieldValue = string.Empty;

// Get the field value using TryGetValue Method

fieldCollection.TryGetValue("FirstName", out fieldValue);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

// Load the form from the loaded document.

PdfLoadedForm form = loadedDocument.Form;

// Load the form field collections from the form.

PdfLoadedFormFieldCollection fieldCollection = form.Fields as PdfLoadedFormFieldCollection;

string fieldValue = string.Empty;

// Get the field value using TryGetValue Method

fieldCollection.TryGetValue("FirstName", out fieldValue);

//Save the PDF document to stream.

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

## Removing editing capability of form fields

The form field editing or filling capabilities can be removed by either flattening the PDF document or by marking the form or field as read only.

Essential PDF provides support to flatten a form field by removing the existing form field and replacing it with graphical objects that would resemble the form field and cannot be edited.

Please refer the sample for flattening the form fields in new PDF document.

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Text box field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Flatten the whole form field 

document.Form.Flatten = true;

//Flattens the first field //form.Fields[0].Flatten = true;

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Save the document.

document.Save("Form.pdf");

//close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create a Text box field and add the properties.

Dim textBoxField As New PdfTextBoxField(page, "FirstName")

textBoxField.Bounds = New RectangleF(0, 0, 100, 20)

textBoxField.ToolTip = "First Name"

'Flatten the whole form field

document.Form.Flatten = True

'Add the form field to the document.

document.Form.Fields.Add(textBoxField)

'Save the PDF document.

document.Save("Form.pdf")

'close the document

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a new page to PDF document

PdfPage page = document.Pages.Add();

//Create a Text box field and add the properties

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Flatten the whole form field 

document.Form.Flatten = true;

//Flattens the first field //form.Fields[0].Flatten = true;

//Add the form field to the document

document.Form.Fields.Add(textBoxField);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a new page to PDF document

PdfPage page = document.Pages.Add();

//Create a Text box field and add the properties

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Flatten the whole form field 

document.Form.Flatten = true;

//Flattens the first field //form.Fields[0].Flatten = true;

//Add the form field to the document

document.Form.Fields.Add(textBoxField);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name.

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a new page to PDF document

PdfPage page = document.Pages.Add();

//Create a Text box field and add the properties

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Flatten the whole form field 

document.Form.Flatten = true;

//Flattens the first field //form.Fields[0].Flatten = true;

//Add the form field to the document

document.Form.Fields.Add(textBoxField);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code sample

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

Please refer the sample for flattening the form fields in existing PDF document:

{% tabs %}  

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

PdfLoadedFormFieldCollection fields = loadedForm.Fields;

//Get the loaded text box field

PdfLoadedTextBoxField loadedTextBoxField = fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "Text";

//Flatten the whole form.

loadedForm.Flatten = true;

//Save and close the modified document.

loadedDocument.Save("output.pdf");

loadedDocument.Close(true);



{% endhighlight %}



{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

Dim fields As PdfLoadedFormFieldCollection = loadedForm.Fields

'Get the loaded text box field

Dim loadedTextBoxField As PdfLoadedTextBoxField = TryCast(fields(0), PdfLoadedTextBoxField)

loadedTextBoxField.Text = "Text"

'Flatten the whole form.

loadedForm.Flatten = True

'Save and close the modified document.

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

//Get the loaded form

PdfLoadedForm loadedForm = loadedDocument.Form;

PdfLoadedFormFieldCollection fields = loadedForm.Fields;

//Get the loaded text box field

PdfLoadedTextBoxField loadedTextBoxField = fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "Text";

//Flatten the whole form

loadedForm.Flatten = true;

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

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

PdfLoadedFormFieldCollection fields = loadedForm.Fields;

//Get the loaded text box field

PdfLoadedTextBoxField loadedTextBoxField = fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "Text";

//Flatten the whole form.

loadedForm.Flatten = true;

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

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

PdfLoadedFormFieldCollection fields = loadedForm.Fields;

//Get the loaded text box field

PdfLoadedTextBoxField loadedTextBoxField = fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "Text";

//Flatten the whole form.

loadedForm.Flatten = true;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

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


To prevent the user from changing the form field content, you can also use Read-only property.

The below code snippet illustrates how to set the read only property to a new PDF document.

{% tabs %} 

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create the form

PdfForm form = document.Form;

//Set the form as read only

form.ReadOnly = true;

//Create a text box field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

textBoxField.Text = "john";

//set read only property for a particular field

//textBoxField.ReadOnly = true;

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Save the document.

document.Save("Form.pdf");

//close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create the form

Dim form As PdfForm = document.Form

'Set the form as read only

form.ReadOnly = True

'Create a Text box field and add the properties.

Dim textBoxField As New PdfTextBoxField(page, "FirstName")

textBoxField.Bounds = New RectangleF(0, 0, 100, 20)

textBoxField.ToolTip = "First Name"

textBoxField.Text = "john"

'set read only property for a particular field

'textBoxField.ReadOnly = True;

'Add the form field to the document.

document.Form.Fields.Add(textBoxField)

'Save the document.

document.Save("Form.pdf")

'close the document

document.Close(True)





{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create the form

PdfForm form = document.Form;

//Set the form as read only

form.ReadOnly = true;

//Create a text box field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

textBoxField.Text = "john";

//set read only property for a particular field

//textBoxField.ReadOnly = true;

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create the form

PdfForm form = document.Form;

//Set the form as read only

form.ReadOnly = true;

//Create a text box field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

textBoxField.Text = "john";

//set read only property for a particular field

//textBoxField.ReadOnly = true;

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create the form

PdfForm form = document.Form;

//Set the form as read only

form.ReadOnly = true;

//Create a text box field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

textBoxField.Text = "john";

//set read only property for a particular field

//textBoxField.ReadOnly = true;

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}


{% endhighlight %}

{% endtabs %}  

The below code snippet illustrates how to set the read only property to an existing PDF document.

{% tabs %}  

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Set the form as read only

loadedForm.ReadOnly = true;

//Save the document.

loadedDocument.Save("sample.pdf");

//close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Set the form as read only

loadedForm.ReadOnly = True

'Save the document.

loadedDocument.Save("Form1.pdf")

'close the document

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

//Get the loaded form

PdfLoadedForm loadedForm = loadedDocument.Form;

//Set the form as read only

loadedForm.ReadOnly = true;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form

PdfLoadedForm loadedForm = loadedDocument.Form;

//Set the form as read only

loadedForm.ReadOnly = true;

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Set the form as read only

loadedForm.ReadOnly = true;

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

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

N> Flattening and adding Read-only properties can be done to the entire form or an individual form field.

## Removing the form fields from existing PDF document:

You can remove the form fields from an existing PDF document using PdfLoadedFormFieldCollection class.

The below code illustrates how to remove the form fields from the existing PDF document:

{% tabs %}  

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Load the textbox field

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

//Remove the field

loadedForm.Fields.Remove(loadedTextBoxField);

//Remove the field at index 0

loadedForm.Fields.RemoveAt(0);

//Save the modified document.

loadedDocument.Save("form.pdf");

//Close the document

loadedDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Load the textbox field

Dim loadedTextBoxField As PdfLoadedTextBoxField = TryCast(loadedForm.Fields(0), PdfLoadedTextBoxField)

'Remove the field

loadedForm.Fields.Remove(loadedTextBoxField)

'Remove the field at index 0 

loadedForm.Fields.RemoveAt(0);

'Save the modified document.

loadedDocument.Save("form.pdf")

'Close the document

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

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Load the textbox field

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

//Remove the field

loadedForm.Fields.Remove(loadedTextBoxField);

//Remove the field at index 0

loadedForm.Fields.RemoveAt(0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code sample

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Load the textbox field

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

//Remove the field

loadedForm.Fields.Remove(loadedTextBoxField);

//Remove the field at index 0

loadedForm.Fields.RemoveAt(0);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Load the textbox field

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

//Remove the field

loadedForm.Fields.Remove(loadedTextBoxField);

//Remove the field at index 0

loadedForm.Fields.RemoveAt(0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

## Importing FDF file to PDF

FDF stands for Forms Data Format. FDF is a file format for representing form data and annotations that are contained in a PDF form. You can import the FDF file to PDF using ImportDataFDF method in PdfLoadedForm class.

The below code illustrates how to import FDF file to PDF.

{% tabs %} 

{% highlight c# %}


//Load an existing document.  

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

// Load the existing form

PdfLoadedForm loadedForm = loadedDocument.Form;

// Load the FDF file

FileStream stream = new FileStream("ImportFDF.fdf", FileMode.Open);

// Import the FDF stream

loadedForm.ImportDataFDF(stream, true);

//Close the document.

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load an existing document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

' Load the existing form

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

' Load the FDF file

Dim stream As New FileStream("ImportFDF.fdf", FileMode.Open)

' Import the FDF stream

loadedForm.ImportDataFDF(stream, True)

' Close the document

loadedDocument.Close(True)



{% endhighlight %}

{% endtabs %}  
 

## Export PDF file to FDF

To export the FDF file from PDF document, you can use ExportData method in PdfLoadedForm class.

The below code illustrates how to export FDF file from PDF document.

{% tabs %} 

{% highlight c# %}


// Load an existing document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

// Load an existing form

PdfLoadedForm loadedForm = loadedDocument.Form;

//Export the existing PDF document to FDF file

loadedForm.ExportData("Export.fdf", DataFormat.Fdf, "SourceForm.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

' Load an existing document

Dim loadedDocument As New PdfLoadedDocument(fileName)

' Load an existing form

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Export the existing PDF document to FDF file

loadedForm.ExportData("Export.fdf", DataFormat.Fdf, "SourceForm.pdf")

'Close the document

loadedDocument.Close(True)



{% endhighlight %}

{% endtabs %}  

 
## Adding actions to form fields 

Please refer to the [actions](/file-formats/pdf/working-with-action#adding-an-action-to-the-form-field "Working with action") section for more details

N> Essential PDF allows users to preserve the extended rights for form filling alone.

## Troubleshooting



Form fields may appear empty in adobe reader some time due to the absence of the appearance dictionary. To resolve this, you have to enable the Adobe Reader default appearance by using the SetDefaultAppearance method in PdfForm class.

The below code illustrates how to enable the default appearance in new PDF document:

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Text box field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Enable the default Appearance

document.Form.SetDefaultAppearance(true);

//Save the document.

document.Save("Form.pdf");

//close the document

document.Close(true);



{% endhighlight %}



{% highlight vb.net %}


'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Create a Text box field and add the properties.

Dim textBoxField As New PdfTextBoxField(page, "FirstName")

textBoxField.Bounds = New RectangleF(0, 0, 100, 20)

textBoxField.ToolTip = "First Name"

'Add the form field to the document.

document.Form.Fields.Add(textBoxField)

'Enable the default Appearance

document.Form.SetDefaultAppearance(True)

'Save the document.

document.Save("Form.pdf")

'close the document

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a new page to PDF document

PdfPage page = document.Pages.Add();

//Create a Text box field and add the properties

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the document

document.Form.Fields.Add(textBoxField);

//Enable the default Appearance

document.Form.SetDefaultAppearance(true);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Form.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Text box field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Enable the default Appearance

document.Form.SetDefaultAppearance(true);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Form.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page to PDF document.

PdfPage page = document.Pages.Add();

//Create a Text box field and add the properties.

PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");

textBoxField.Bounds = new Syncfusion.Drawing.RectangleF(0, 0, 100, 20);

textBoxField.ToolTip = "First Name";

//Add the form field to the document.

document.Form.Fields.Add(textBoxField);

//Enable the default Appearance

document.Form.SetDefaultAppearance(true);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Form.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Form.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

The below code illustrates how to enable the default appearance in existing PDF document:

{% tabs %}  

{% highlight c# %}


//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded text box field and fill it.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "First Name";

//Enable the default Appearance

loadedDocument.Form.SetDefaultAppearance(true);

//Save the modified document.

loadedDocument.Save("sample.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}



{% highlight vb.net %}


'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Get the loaded form.

Dim loadedForm As PdfLoadedForm = loadedDocument.Form

'Get the loaded text box field and fill it.

Dim loadedTextBoxField As PdfLoadedTextBoxField = TryCast(loadedForm.Fields(0), PdfLoadedTextBoxField)

loadedTextBoxField.Text = "First Name"

'Enable the default Appearance

loadedDocument.Form.SetDefaultAppearance(True)

'Save the modified document.

loadedDocument.Save("sample.pdf")

'Close the document

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

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded text box field and fill it.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "First Name";

//Enable the default Appearance

loadedDocument.Form.SetDefaultAppearance(true);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded text box field and fill it.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "First Name";

//Enable the default Appearance

loadedDocument.Form.SetDefaultAppearance(true);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the loaded form.

PdfLoadedForm loadedForm = loadedDocument.Form;

//Get the loaded text box field and fill it.

PdfLoadedTextBoxField loadedTextBoxField = loadedForm.Fields[0] as PdfLoadedTextBoxField;

loadedTextBoxField.Text = "First Name";

//Enable the default Appearance

loadedDocument.Form.SetDefaultAppearance(true);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

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