---
title: Working with XFA Forms
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

Essential PDF allows you to create and manipulate the XFA form in PDF document by using PdfXfaDocument and PdfXfaForm classes. The PdfXfaFieldCollection class represents the entire field collection of the XFA form.

### Adding a new page to the XFA document

The following code sample explains you on how to add a new page in a PDF XFA document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a text element and add the properties.
PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");           
//Add the field to the XFA form.
mainForm.Fields.Add(textElement);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//Close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a text element and add the properties.
Dim textElement As New PdfXfaTextElement("Hello World!")
'Add the field to the XFA form.
mainForm.Fields.Add(textElement)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'Close the document
document.Close()

{% endhighlight %}

{% endtabs %}

N> XFA documents are created based on the flow layout, so the pages are sequentially added if the doesn’t have space to fit the field it will automatically move on the next page, so we can’t specify the page and page numbers.

### Adding the XFA document settings

Essential PDF supports various XFA page setting options to control the page display.

The below sample illustrates how to create a new PDF document with XFA page size.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Set the page size.
document.PageSettings.Size = PdfPageSize.A4;
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a text element and add the properties.
PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");
//Set font
textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form.
mainForm.Fields.Add(textElement);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Set the page size.
document.PageSettings.Size = PdfPageSize.A4
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a text element and add the properties.
Dim textElement As New PdfXfaTextElement("Hello World!!!")
'Set font
textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)
'Add the text element to the XFA form.
mainForm.Fields.Add(textElement)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

You can create a custom page size to the PDF document by using following code snippet.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Set the page size.
document.PageSettings.Size = new SizeF(500,700);
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a text element and add the properties.
PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");
//Set font
textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form.
mainForm.Fields.Add(textElement);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Set the page size.
document.PageSettings.Size = New SizeF(500,700)
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a text element and add the properties.
Dim textElement As New PdfXfaTextElement("Hello World!!!")
'Set font
textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)
'Add the text element to the XFA form.
mainForm.Fields.Add(textElement)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

You can change page orientation from portrait to landscape by using the following code snippet.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Set the page size.
document.PageSettings.Size = new SizeF(500,700);
//Change the page orientation to landscape.
document.PageSettings. PageOrientation = PdfXfaPageOrientation.Landscape;
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a text element and add the properties.
PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");
//Set font
textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form.
mainForm.Fields.Add(textElement);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Set the page size.
document.PageSettings.Size = New SizeF(500,700)
'Change the page orientation to landscape.
document.PageSettings.PageOrientation = PdfXfaPageOrientation.Landscape
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a text element and add the properties.
Dim textElement As New PdfXfaTextElement("Hello World!!!")
'Set font
textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)
'Add the text element to the XFA form.
mainForm.Fields.Add(textElement)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

## Creating dynamic XFA forms

The below sample illustrates how to create a dynamic XFA forms.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Set the page size.
document.PageSettings.Size = PdfPageSize.A4;
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a text element and add the properties.
PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");
//Set font
textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form.
mainForm.Fields.Add(textElement);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document dynamic form.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Set the page size.
document.PageSettings.Size = PdfPageSize.A4
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1", xfaPage,xfaPage.GetClientSize().Width)
'Create a text element and add the properties.
Dim textElement As New PdfXfaTextElement("Hello World!!!")
'Set font
textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)
'Add the text element to the XFA form.
mainForm.Fields.Add(textElement)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document dynamic form.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

## Creating static XFA forms

The below sample illustrates how to create a static XFA forms.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Set the page size.
document.PageSettings.Size = PdfPageSize.A4;
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a text element and add the properties.
PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!!!");
//Set font
textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form.
mainForm.Fields.Add(textElement);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document with static form.
document.Save("XfaForm.pdf",PdfXfaType.Static);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Set the page size.
document.PageSettings.Size = PdfPageSize.A4
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a text element and add the properties.
Dim textElement As New PdfXfaTextElement("Hello World!!!")
'Set font
textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)
'Add the text element to the XFA form.
mainForm.Fields.Add(textElement)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document with static form.
document.Save("XfaForm.pdf",PdfXfaType.Static)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

## Creating XFA form fields

### Adding the XFA text box field.

The below code snippet illustrates how to add a textbox field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a textbox field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName",new SizeF(200,20));
//Set the caption text.
textBoxField.Caption.Text = "First Name";
//Set the tool tip.
textBoxField.ToolTip = "First Name";
//Add the field to the XFA form.
mainForm.Fields.Add(textBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a textbox field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("FirstName",New SizeF(200,20))
'Set the caption text.
textBoxField.Caption.Text = "First Name"
'Set the tool tip.
textBoxField.ToolTip = "First Name"
'Add the field to the XFA form.
mainForm.Fields.Add(textBoxField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add a textbox field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a textbox field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "First Name";
//Set the tool tip.
textBoxField.ToolTip = "First Name";
//Add the field to the existing XFA form.
lform.Fields.Add(textBoxField);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a textbox field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("FirstName", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "First Name"
'Set the tool tip.
textBoxField.ToolTip = "First Name"
'Add the field to the existing XFA form.
lform.Fields.Add(textBoxField)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA numeric field

The below code snippet illustrates how to add a numeric field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a numeric field and add the properties.
PdfXfaNumericField numericField = new PdfXfaNumericField("nfield",new SizeF(200,20));
//Set the caption text.
numericField.Caption.Text = "Numeric Field";
//Add the field to the XFA form.
mainForm.Fields.Add(numericField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a numeric field and add the properties.
Dim numericField As New PdfXfaNumericField("nfield",New SizeF(200,20))
'Set the caption text.
numericField.Caption.Text = "Numeric Field"
'Add the field to the XFA form.
mainForm.Fields.Add(numericField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add the numeric field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a numeric field and add the properties.
PdfXfaNumericField numericField = new PdfXfaNumericField("nfield",new SizeF(200,20));
//Set the caption text.
numericField.Caption.Text = "Numeric Field";
//Add the field to the existing XFA form.
lform.Fields.Add(numericField);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a numeric field and add the properties.
Dim numericField As New PdfXfaNumericField("nfield",New SizeF(200,20))
'Set the caption text.
numericField.Caption.Text = "Numeric Field"
'Add the field to the existing XFA form.
lform.Fields.Add(numericField)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA combo box field.

The below code snippet illustrates how to add a combo box field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a combo box field and add the properties.
PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("cfield", new SizeF(200, 20));
//Set the caption text.
comboBoxField.Caption.Text = "Job Title";
//Add the combo box items
comboBoxField.Items.Add("Development.");
comboBoxField.Items.Add("Support.");
comboBoxField.Items.Add("Documentation.");
//Add the field to the XFA form.
mainForm.Fields.Add(comboBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a combo box field and add the properties.
PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("cfield", new SizeF(200, 20));
//Set the caption text.
comboBoxField.Caption.Text = "Job Title";
//Add the combo box items
comboBoxField.Items.Add("Development.");
comboBoxField.Items.Add("Support.");
comboBoxField.Items.Add("Documentation.");
//Add the field to the XFA form.
mainForm.Fields.Add(comboBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add the combo box field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a combo box field and add the properties.
PdfXfaComboBoxField comboBoxField = new PdfXfaComboBoxField("comboField", new SizeF(200, 20));
//Set the caption text.
comboBoxField.Caption.Text = "Job Title";
//Add the combo box items
comboBoxField.Items.Add("Development.");
comboBoxField.Items.Add("Support.");
comboBoxField.Items.Add("Documentation.");
//Add the field to the existing XFA form.
lform.Fields.Add(comboBoxField);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a combo box field and add the properties.
Dim comboBoxField As New PdfXfaComboBoxField("comboField", New SizeF(200, 20))
'Set the caption text.
comboBoxField.Caption.Text = "Job Title"
'Add the combo box items
comboBoxField.Items.Add("Development.")
comboBoxField.Items.Add("Support.")
comboBoxField.Items.Add("Documentation.")
'Add the field to the existing XFA form.
lform.Fields.Add(comboBoxField)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA list box field

The below code snippet illustrates how to add a list box field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);

//Create a list box field and add the properties.
PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("lfield", new SizeF(150, 50));
//Set the caption text.
listBoxField.Caption.Text = "Known Languages";
listBoxField.Caption.Position = PdfXfaPosition.Top;
listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;
//Add the list box items
listBoxField.Items.Add("English");
listBoxField.Items.Add("French");
listBoxField.Items.Add("German");
//Add the field to the XFA form.
mainForm.Fields.Add(comboBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a list box field and add the properties.
Dim listBoxField As New PdfXfaListBoxField("lfield", New SizeF(150, 50))
'Set the caption text.
listBoxField.Caption.Text = "Known Languages"
listBoxField.Caption.Position = PdfXfaPosition.Top
listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center
'Add the list box items
listBoxField.Items.Add("English")
listBoxField.Items.Add("French")
listBoxField.Items.Add("German")
'Add the field to the XFA form.
mainForm.Fields.Add(comboBoxField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add the list box field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a list box field and add the properties.
PdfXfaListBoxField listBoxField = new PdfXfaListBoxField("lfield", new SizeF(150, 50));
//Set the caption text.
listBoxField.Caption.Text = "Known Languages";
listBoxField.Caption.Position = PdfXfaPosition.Top;
listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center;
//Add the list box items
listBoxField.Items.Add("English");
listBoxField.Items.Add("French");
listBoxField.Items.Add("German");
//Add the field to the existing XFA form.
lform.Fields.Add(comboBoxField);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a list box field and add the properties.
Dim listBoxField As New PdfXfaListBoxField("lfield", New SizeF(150, 50))
'Set the caption text.
listBoxField.Caption.Text = "Known Languages"
listBoxField.Caption.Position = PdfXfaPosition.Top
listBoxField.Caption.HorizontalAlignment = PdfXfaHorizontalAlignment.Center
'Add the list box items
listBoxField.Items.Add("English")
listBoxField.Items.Add("French")
listBoxField.Items.Add("German")
'Add the field to the existing XFA form.
lform.Fields.Add(comboBoxField)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding XFA check box field

The below code snippet illustrates how to add a check box field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a check box field and add the properties.
PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkfld", new SizeF(100, 20));
//Set the caption text.
checkBoxField.Caption.Text = "Check box Field";
checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;
//Add the field to the XFA form.
mainForm.Fields.Add(checkBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a check box field and add the properties.
Dim checkBoxField As New PdfXfaCheckBoxField("checkfld", New SizeF(100, 20))
'Set the caption text.
checkBoxField.Caption.Text = "Check box Field"
checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross
'Add the field to the XFA form.
mainForm.Fields.Add(checkBoxField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add the check box field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a check box field and add the properties.
PdfXfaCheckBoxField checkBoxField = new PdfXfaCheckBoxField("checkfld", new SizeF(100, 20));
//Set the caption text.
checkBoxField.Caption.Text = "Check box Field";
checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross;
//Add the field to the existing XFA form.
lform.Fields.Add(checkBoxField);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a check box field and add the properties.
Dim checkBoxField As New PdfXfaCheckBoxField("checkfld", New SizeF(100, 20))
'Set the caption text.
checkBoxField.Caption.Text = "Check box Field"
checkBoxField.CheckedStyle = PdfXfaCheckedStyle.Cross
'Add the field to the existing XFA form.
lform.Fields.Add(checkBoxField)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}
 
### Adding the XFA radio button field

The below code snippet illustrates how to add a radio button field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a radio button group
PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");
group.FlowDirection = PdfXfaFlowDirection.Vertical;
//Create a radio button field and add the properties.
PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));
//Set the caption text.
radioButtonField1.Caption.Text = "Male";
PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));
radioButtonField2.Caption.Text = "Female";
//Add the radio button fields to the radio button group
group.Items.Add(radioButtonField1);
group.Items.Add(radioButtonField2);
//Add the field to the XFA form.
mainForm.Fields.Add(group);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a radio button group 
Dim group As New PdfXfaRadioButtonGroup("radioGroup")
group.FlowDirection = PdfXfaFlowDirection.Vertical
'Create a radio button field and add the properties.
Dim radioButtonField1 As New PdfXfaRadioButtonField("r1", New SizeF(80, 20))
'Set the caption text.
radioButtonField1.Caption.Text = "Male"
Dim radioButtonField2 As New PdfXfaRadioButtonField("r2", New SizeF(80, 20))
radioButtonField2.Caption.Text = "Female"
'Add the radio button fields to the radio button group
group.Items.Add(radioButtonField1)
group.Items.Add(radioButtonField2)
'Add the field to the XFA form.
mainForm.Fields.Add(group)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add the radio button field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a radio button group
PdfXfaRadioButtonGroup group = new PdfXfaRadioButtonGroup("radioGroup");
group.FlowDirection = PdfXfaFlowDirection.Vertical;
//Create a radio button field and add the properties.
PdfXfaRadioButtonField radioButtonField1 = new PdfXfaRadioButtonField("r1", new SizeF(80, 20));
//Set the caption text.
radioButtonField1.Caption.Text = "Male";
PdfXfaRadioButtonField radioButtonField2 = new PdfXfaRadioButtonField("r2", new SizeF(80, 20));
radioButtonField2.Caption.Text = "Female";
//Add the radio button fields to the radio button group
group.Items.Add(radioButtonField1);
group.Items.Add(radioButtonField2);
//Add the field to the existing XFA form.
lform.Fields.Add(group);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a radio button group 
Dim group As New PdfXfaRadioButtonGroup("radioGroup")
group.FlowDirection = PdfXfaFlowDirection.Vertical
'Create a radio button field and add the properties.
Dim radioButtonField1 As New PdfXfaRadioButtonField("r1", New SizeF(80, 20))
'Set the caption text.
radioButtonField1.Caption.Text = "Male"
Dim radioButtonField2 As New PdfXfaRadioButtonField("r2", New SizeF(80, 20))
radioButtonField2.Caption.Text = "Female"
'Add the radio button fields to the radio button group
group.Items.Add(radioButtonField1)
group.Items.Add(radioButtonField2)
'Add the field to the existing XFA form.
lform.Fields.Add(group)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA date time field

The below code snippet illustrates how to add a date time field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a date time field and add the properties.
PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));
//Set the caption text.
dateTimeField.Caption.Text = "Date Time Field";
//Set the tool tip.
dateTimeField.ToolTip = "Date Time";
//Add the field to the XFA form.
mainForm.Fields.Add(dateTimeField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a date time field and add the properties.
Dim dateTimeField As New PdfXfaDateTimeField("date", New SizeF(200, 20))
'Set the caption text.
dateTimeField.Caption.Text = "Date Time Field"
'Set the tool tip.
dateTimeField.ToolTip = "Date Time"
'Add the field to the XFA form.
mainForm.Fields.Add(dateTimeField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add the date time field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a date time field and add the properties.
PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("date", new SizeF(200, 20));
//Set the caption text.
dateTimeField.Caption.Text = "Date Time Field";
//Set the tool tip.
dateTimeField.ToolTip = "Date Time";
//Add the field to the existing XFA form.
lform.Fields.Add(dateTimeField);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a date time field and add the properties.
Dim dateTimeField As New PdfXfaDateTimeField("date", New SizeF(200, 20))
'Set the caption text.
dateTimeField.Caption.Text = "Date Time Field"
'Set the tool tip.
dateTimeField.ToolTip = "Date Time"
'Add the field to the existing XFA form.
lform.Fields.Add(dateTimeField)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA button field

The below code snippet illustrates how to add a button field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a button field and add the properties.
PdfXfaButtonField buttonField = new PdfXfaButtonField("btn", new SizeF(70, 20));
//Set the caption text.
buttonField.Content = "Click";
//Add the field to the XFA form.
mainForm.Fields.Add(buttonField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a button field and add the properties.
Dim buttonField As New PdfXfaButtonField("btn", New SizeF(70, 20))
'Set the caption text.
buttonField.Content = "Click"
'Add the field to the XFA form.
mainForm.Fields.Add(buttonField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add the button field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a button field and add the properties.
PdfXfaButtonField buttonField = new PdfXfaButtonField("btn", new SizeF(70, 20));
//Set the caption text.
buttonField.Content = "Click";
//Add the field to the existing XFA form.
lform.Fields.Add(buttonField);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a button field and add the properties.
Dim buttonField As New PdfXfaButtonField("btn", New SizeF(70, 20))
'Set the caption text.
buttonField.Content = "Click"
'Add the field to the existing XFA form.
lform.Fields.Add(buttonField)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA text element

The below code snippet illustrates how to add a text element to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a text element and add the properties.
PdfXfaTextElement textElement = new PdfXfaTextElement("Hello World!");
//Set font
textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);

//Add the text element to the XFA form.
mainForm.Fields.Add(textElement);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a text element and add the properties.
Dim textElement As New PdfXfaTextElement("Hello World!")
'Set font
textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)
'Add the text element to the XFA form.
mainForm.Fields.Add(textElement)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add a text element to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a text element and add the properties.
PdfXfaTextElement textElement  = new PdfXfaTextElement("Hello World!");
//Set font
textElement.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold);
//Add the text element to the existing XFA form.
lform.Fields.Add(textElement);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a text element and add the properties.
Dim textElement As New PdfXfaTextElement("Hello World!")
'Set font
textElement.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 14, PdfFontStyle.Bold)
'Add the text element to the existing XFA form.
lform.Fields.Add(textElement)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA rectangle field

The below code snippet illustrates how to add the rectangle field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a rectangle field and add the properties.
PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1",new SizeF (100,50));
//Set the fill color
rectangle.Border.FillColor = new PdfXfaSolidBrush(Color.Red);

//Add the rectangle field to the XFA form.
mainForm.Fields.Add(rectangle);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a rectangle field and add the properties.
Dim rectangle As New PdfXfaRectangleField("rect1",New SizeF(100,50))
'Set the fill color
rectangle.Border.FillColor = New PdfXfaSolidBrush(Color.Red)
'Add the rectangle field to the XFA form.
mainForm.Fields.Add(rectangle)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add the rectangle field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a rectangle field and add the properties.
PdfXfaRectangleField rectangle = new PdfXfaRectangleField("rect1", new SizeF(100, 50));
//Set the fill color
rectangle.Border.FillColor = new PdfXfaSolidBrush(Color.Red);
//Add the rectangle to the existing XFA form.
lform.Fields.Add(rectangle);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a rectangle field and add the properties.
Dim rectangle As New PdfXfaRectangleField("rect1", New SizeF(100, 50))
'Set the fill color
rectangle.Border.FillColor = New PdfXfaSolidBrush(Color.Red)
'Add the rectangle to the existing XFA form.
lform.Fields.Add(rectangle)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA circle field

The below code snippet illustrates how to add the circle field to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a circle field and add the properties.
PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));
//Set the fill color
circle.Border.FillColor = new PdfXfaSolidBrush(Color.Red);
//Add the text element to the XFA form.
mainForm.Fields.Add(circle);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a circle field and add the properties.
Dim circle As New PdfXfaCircleField("circle", New SizeF(100, 100))
'Set the fill color
circle.Border.FillColor = New PdfXfaSolidBrush(Color.Red)
'Add the text element to the XFA form.
mainForm.Fields.Add(circle)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add the circle field to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a circle field and add the properties.
PdfXfaCircleField circle = new PdfXfaCircleField("circle", new SizeF(100, 100));
//Set the fill color
circle.Border.FillColor = new PdfXfaSolidBrush(Color.Red);
//Add the circle to the existing XFA form.
lform.Fields.Add(circle);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a circle field and add the properties.
Dim circle As New PdfXfaCircleField("circle", New SizeF(100, 100))
'Set the fill color
circle.Border.FillColor = New PdfXfaSolidBrush(Color.Red)
'Add the circle to the existing XFA form.
lform.Fields.Add(circle)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA line

The below code snippet illustrates how to add a line to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a line and add the properties.
PdfXfaLine line = new PdfXfaLine(new PointF(0,0),new PointF (200,0),3);
//Set the line color
line.Color = new PdfColor(Color.Red);
//Add the text line to the XFA form.
mainForm.Fields.Add(line);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a line and add the properties.
Dim line As New PdfXfaLine(New PointF(0,0),New PointF(200,0),3)
'Set the line color
line.Color = New PdfColor(Color.Red)
'Add the text line to the XFA form.
mainForm.Fields.Add(line)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add a line to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a line and add the properties.
PdfXfaLine line = new PdfXfaLine(new PointF(0, 0), new PointF(200, 0), 3);
//Set the line color
line.Color = new PdfColor(Color.Red);
//Add the line to the existing XFA form.
lform.Fields.Add(line);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a line and add the properties.
Dim line As New PdfXfaLine(New PointF(0, 0), New PointF(200, 0), 3)
'Set the line color
line.Color = New PdfColor(Color.Red)
'Add the line to the existing XFA form.
lform.Fields.Add(line)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

### Adding the XFA image

The below code snippet illustrates how to add an image to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();   
//Add a new XFA page.
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form
PdfXfaForm mainForm = new PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize ().Width);
//Create a image and add the properties.
PdfXfaImage image = new PdfXfaImage("image1", "image.jpg");

//Add the image to the XFA form.
mainForm.Fields.Add(image);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add a new XFA page.
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form
Dim mainForm As New PdfXfaForm("subform1",xfaPage,xfaPage.GetClientSize().Width)
'Create a image and add the properties.
Dim image As New PdfXfaImage("image1", "image.jpg")
'Add the image to the XFA form.
mainForm.Fields.Add(image)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf",PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to add an image to an existing PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing XFA document
PdfLoadedXfaDocument ldoc = new PdfLoadedXfaDocument("XfaForm1.pdf");
//Load the existing XFA form.
PdfLoadedXfaForm lform = ldoc.XfaForm;
//Create a image and add the properties.
PdfXfaImage image = new PdfXfaImage("imgage1", "image.jpg");            
//Add the image to the existing XFA form.
lform.Fields.Add(image);
//Save the document
ldoc.Save("XfaForm.pdf");
//Close the document
ldoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing XFA document
Dim ldoc As New PdfLoadedXfaDocument("XfaForm1.pdf")
'Load the existing XFA form.
Dim lform As PdfLoadedXfaForm = ldoc.XfaForm
'Create a image and add the properties.
Dim image As New PdfXfaImage("imgage1", "image.jpg")
'Add the image to the existing XFA form.
lform.Fields.Add(image)
'Save the document
ldoc.Save("XfaForm.pdf")
'Close the document
ldoc.Close()

{% endhighlight %}

{% endtabs %}

## Working with XFA form flow directions

There are two types of flow directions available in XFA forms.

1. Horizontal
2. Vertical

### Horizontal flow direction

The below samples illustrate how to set the horizontal flow direction in XFA forms

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a textbox field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "First Name";
//Set the tool tip.
textBoxField.ToolTip = "First Name";
//Add the field to the XFA form.
mainForm.Fields.Add(textBoxField);
PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));
//Set the caption text.
textBoxField1.Caption.Text = "Last Name";
mainForm.Fields.Add(textBoxField1);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a textbox field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("FirstName", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "First Name"
'Set the tool tip.
textBoxField.ToolTip = "First Name"
'Add the field to the XFA form.
mainForm.Fields.Add(textBoxField)
Dim textBoxField1 As New PdfXfaTextBoxField("LastName", New SizeF(200, 20))
'Set the caption text.
textBoxField1.Caption.Text = "Last Name"
mainForm.Fields.Add(textBoxField1)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

### Vertical flow direction

The below samples illustrate how to set the vertical flow direction in XFA forms.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with vertical flow direction
PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Vertical, xfaPage.GetClientSize ().Width);
//Create a textbox field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "First Name";
//Set the tool tip.
textBoxField.ToolTip = "First Name";
//Add the field to the XFA form.
mainForm.Fields.Add(textBoxField);
PdfXfaTextBoxField textBoxField1 = new PdfXfaTextBoxField("LastName", new SizeF(200, 20));
//Set the caption text.
textBoxField1.Caption.Text = "Last Name";
mainForm.Fields.Add(textBoxField1);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with vertical flow direction
Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Vertical, xfaPage.GetClientSize().Width)
'Create a textbox field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("FirstName", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "First Name"
'Set the tool tip.
textBoxField.ToolTip = "First Name"
'Add the field to the XFA form.
mainForm.Fields.Add(textBoxField)
Dim textBoxField1 As New PdfXfaTextBoxField("LastName", New SizeF(200, 20))
'Set the caption text.
textBoxField1.Caption.Text = "Last Name"
mainForm.Fields.Add(textBoxField1)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

## Rotating XFA form fields

You can rotate a form fields in XFA document, using the following code snippet.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a textbox field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("FirstName", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "First Name";
//Set the tool tip.
textBoxField.ToolTip = "First Name";
//Set the fields rotation
textBoxField.Rotate = PdfXfaRotateAngle.RotateAngle90;
//Add the field to the XFA form.
mainForm.Fields.Add(textBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a textbox field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("FirstName", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "First Name"
'Set the tool tip.
textBoxField.ToolTip = "First Name"
'Set the fields rotation
textBoxField.Rotate = PdfXfaRotateAngle.RotateAngle90
'Add the field to the XFA form.
mainForm.Fields.Add(textBoxField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

## Validating the date time field

You can validate the date time fields of the input text by using the following code snippet.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a date time field and add the properties.
PdfXfaDateTimeField dateTimeField = new PdfXfaDateTimeField("dob", new SizeF(200, 20));
//Set the caption text.
dateTimeField.Caption.Text = "Date of Birdth";
//Set the date pattern
dateTimeField.DatePattern = PdfXfaDatePattern.DDMMMMYYYY;
//Enable the validation
dateTimeField.RequireValidation = true;
//Add the field to the XFA form.
mainForm.Fields.Add(dateTimeField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a date time field and add the properties.
Dim dateTimeField As New PdfXfaDateTimeField("dob", New SizeF(200, 20))
'Set the caption text.
dateTimeField.Caption.Text = "Date of Birdth"
'Set the date pattern
dateTimeField.DatePattern = PdfXfaDatePattern.DDMMMMYYYY
'Enable the validation
dateTimeField.RequireValidation = True
'Add the field to the XFA form.
mainForm.Fields.Add(dateTimeField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

## Customizing the numeric field value

You can customize the numeric field input value to the specific pattern, using the following code snippet.

Please refer the below link for numeric pattern format in detail,

[http://help.adobe.com/en_US/livecycle/10.0/DesignerHelp/WS92d06802c76abadb-56c02439129b8b00ebc-7ecf.html](http://help.adobe.com/en_US/livecycle/10.0/DesignerHelp/WS92d06802c76abadb-56c02439129b8b00ebc-7ecf.html)

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a numeric field and add the properties.
PdfXfaNumericField numericField = new PdfXfaNumericField("numericField", new SizeF(200, 20));
//Set the caption text.
numericField.Caption.Text = "Numeric Field";
//Set the pattern string
numericField.PatternString = "zzzzzzzzz9";
//Add the field to the XFA form.
mainForm.Fields.Add(numericField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a numeric field and add the properties.
Dim numericField As New PdfXfaNumericField("numericField", New SizeF(200, 20))
'Set the caption text.
numericField.Caption.Text = "Numeric Field"
'Set the pattern string
numericField.PatternString = "zzzzzzzzz9"
'Add the field to the XFA form.
mainForm.Fields.Add(numericField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

## Adding nested sub forms

You can add the nested sub forms by using the following code snippet.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a font
PdfFont font = new PdfStandardFont(xfaPage,PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a text element
PdfXfaTextElement element = new PdfXfaTextElement("Main Form", font, 400, 20);                
//Add the field to the XFA form.
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
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Static);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a font
Dim font As PdfFont = New PdfStandardFont(xfaPage,PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold)
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a text element
Dim element As New PdfXfaTextElement("Main Form", font, 400, 20)
'Add the field to the XFA form.
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
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Static)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

## Formatting XFA form fields

### Working with alignments

XFA support both the horizontal and vertical alignments

### Horizontal alignment

You can add the horizontal alignments in XFA form fields by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a text box field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "Fist Name";
//Set the horizontal alignment
textBoxField.HorizontalAlignment = PdfXfaHorizontalAlignment.Right;
//Add the field to the XFA form.
mainForm.Fields.Add(textBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a text box field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "Fist Name"
'Set the horizontal alignment 
textBoxField.HorizontalAlignment = PdfXfaHorizontalAlignment.Right
'Add the field to the XFA form.
mainForm.Fields.Add(textBoxField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

### Vertical alignment

You can add the vertical alignments in XFA form fields by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(XfaPagePdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a text box field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "Fist Name";
//Set the vertical alignment
textBoxField.VerticalAlignment = PdfXfaVerticalAlignment.Bottom;

//Add the field to the XFA form.
mainForm.Fields.Add(textBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(XfaPagePdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a text box field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "Fist Name"
'Set the vertical alignment 
textBoxField.VerticalAlignment = PdfXfaVerticalAlignment.Bottom
'Add the field to the XFA form.
mainForm.Fields.Add(textBoxField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

### Adding margins to the XFA fields

You can add margin to the XFA form fields by using the below code snippets.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a text box field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "Fist Name";
//Set the margins
textBoxField.Margins.Left = 10;
textBoxField.Margins.Right = 5;
//Add the field to the XFA form.
mainForm.Fields.Add(textBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a text box field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "Fist Name"
'Set the margins 
textBoxField.Margins.Left = 10
textBoxField.Margins.Right = 5
'Add the field to the XFA form.
mainForm.Fields.Add(textBoxField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

### Adding padding to the XFA fields

You can add padding to the XFA form fields by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a text box field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "Fist Name";
//Set the paddings
textBoxField.Padding.All = 2;

//Add the field to the XFA form.
mainForm.Fields.Add(textBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a text box field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "Fist Name"
'Set the paddings 
textBoxField.Padding.All = 2
'Add the field to the XFA form.
mainForm.Fields.Add(textBoxField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

### Adding border to the XFA fields

You can add the fields border by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize ().Width);
//Create a text box field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "Fist Name";
//Set the border color and width
textBoxField.Border.Color = new PdfColor (200,123,0);
textBoxField.Border.Width = 2;
//Add the field to the XFA form.
mainForm.Fields.Add(textBoxField);
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(xfaPage,PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a text box field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "Fist Name"
'Set the border color and width 
textBoxField.Border.Color = New PdfColor(200,123,0)
textBoxField.Border.Width = 2
'Add the field to the XFA form.
mainForm.Fields.Add(textBoxField)
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

## Filling form fields in an existing XFA document

Essential PDF allows you to fill the XFA form fields using PdfLoadedXfaform class.

### Filling the XFA text box field

Please refer the below sample for filling the XFA text box field.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm lform = loadedDocument.XfaForm;
//Get the loaded text box field.
PdfLoadedXfaTextBoxField ltext = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;
//fill the text box
ltext.Text = "First Name";
//Save the document
loadedDocument.Save("output.pdf");
//Close the document
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim lform As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the loaded text box field.
Dim ltext As PdfLoadedXfaTextBoxField = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("text[0]"), PdfLoadedXfaTextBoxField)
'fill the text box
ltext.Text = "First Name"
'Save the document 
loadedDocument.Save("output.pdf")
'Close the document
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}

### Filling the XFA numeric field

You can fill the XFA numeric field by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm lform = loadedDocument.XfaForm;
//Get the loaded numeric field.
PdfLoadedXfaNumericField lnumericField = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["numericField[0]"] as PdfLoadedXfaNumericField;
//fill the numeric field
lnumericField.NumericValue = 945322;
//Save the document
loadedDocument.Save("output.pdf");
//Close the document
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim lform As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the loaded numeric field.
Dim lnumericField As PdfLoadedXfaNumericField = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("numericField[0]"), PdfLoadedXfaNumericField)
'fill the numeric field
lnumericField.NumericValue = 945322
'Save the document 
loadedDocument.Save("output.pdf")
'Close the document
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}

### Filling the XFA combo box field

You can fill the XFA combo box field by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm lform = loadedDocument.XfaForm;
//Get the loaded combo box field.
PdfLoadedXfaComboBoxField lcomboBoxField = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["comboBoxField[0]"] as PdfLoadedXfaComboBoxField;
//Set the combo box selected index
lcomboBoxField.SelectedIndex = 1;
//Save the document
loadedDocument.Save("output.pdf");
//Close the document
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim lform As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the loaded combo box field.
Dim lcomboBoxField As PdfLoadedXfaComboBoxField = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("comboBoxField[0]"), PdfLoadedXfaComboBoxField)
'Set the combo box selected index
lcomboBoxField.SelectedIndex = 1
'Save the document 
loadedDocument.Save("output.pdf")
'Close the document
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}

### Filling the XFA list box field

You can fill the XFA list box field by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm lform = loadedDocument.XfaForm;
//Get the loaded list box field.
PdfLoadedXfaListBoxField llistBoxField = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;
//Set the list box selected index
llistBoxField.SelectedIndex = 1;
//Save the document
loadedDocument.Save("output.pdf");
//Close the document
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim lform As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the loaded list box field.
Dim llistBoxField As PdfLoadedXfaListBoxField = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("listBoxField[0]"), PdfLoadedXfaListBoxField)
'Set the list box selected index
llistBoxField.SelectedIndex = 1
'Save the document 
loadedDocument.Save("output.pdf")
'Close the document
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}

You can also select the multiple values by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm lform = loadedDocument.XfaForm;
//Get the loaded list box field.
PdfLoadedXfaListBoxField llistBoxField = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["listBoxField[0]"] as PdfLoadedXfaListBoxField;
//Set the list box selected items
llistBoxField .SelectedItems =new string[] {"English","Spanish"};
//Save the document
loadedDocument.Save("output.pdf");
//Close the document
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim lform As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the loaded list box field.
Dim llistBoxField As PdfLoadedXfaListBoxField = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("listBoxField[0]"), PdfLoadedXfaListBoxField)
'Set the list box selected items           
llistBoxField.SelectedItems = New String() {"English","Spanish"}
'Save the document 
loadedDocument.Save("output.pdf")
'Close the document
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}

### Filling the XFA date time field

You can fill the XFA date time field by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm lform = loadedDocument.XfaForm;
//Get the loaded date time field.
PdfLoadedXfaDateTimeField ldateTimeField = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["dateTimeField[0]"] as PdfLoadedXfaDateTimeField;
//Set the value
ldateTimeField.Value = DateTime.Now;
//Save the document
loadedDocument.Save("output.pdf");
//Close the document
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim lform As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the loaded date time field.
Dim ldateTimeField As PdfLoadedXfaDateTimeField = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("dateTimeField[0]"), PdfLoadedXfaDateTimeField)
'Set the value           
ldateTimeField.Value = Date.Now
'Save the document 
loadedDocument.Save("output.pdf")
'Close the document
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}

### Filling the XFA check box field

You can fill the XFA check box field by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm lform = loadedDocument.XfaForm;
//Get the loaded check box field.
PdfLoadedXfaCheckBoxField lcheckBox = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["checkBox[0]"] as PdfLoadedXfaCheckBoxField;
 //Check the check box          
lcheckBox.IsChecked = true;
//Save the document
loadedDocument.Save("output.pdf");
//Close the document
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim lform As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the loaded check box field.
Dim lcheckBox As PdfLoadedXfaCheckBoxField = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("checkBox[0]"), PdfLoadedXfaCheckBoxField)
 'Check the check box          
lcheckBox.IsChecked = True
'Save the document 
loadedDocument.Save("output.pdf")
'Close the document
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}

### Filling the XFA radio button field

You can fill the XFA radio button field by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm lform = loadedDocument.XfaForm;
//Get the radio button group
PdfLoadedXfaRadioButtonGroup lgroup = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["radioButtonGroup[0]"] as PdfLoadedXfaRadioButtonGroup;
//Get the radio button field
PdfLoadedXfaRadioButtonField lradio = lgroup.Fields[0] as PdfLoadedXfaRadioButtonField;
//Check the radio button
lradio.IsChecked = true;
//Save the document
loadedDocument.Save("output.pdf");
//Close the document
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim lform As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the radio button group
Dim lgroup As PdfLoadedXfaRadioButtonGroup = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("radioButtonGroup[0]"), PdfLoadedXfaRadioButtonGroup)
'Get the radio button field
Dim lradio As PdfLoadedXfaRadioButtonField = TryCast(lgroup.Fields(0), PdfLoadedXfaRadioButtonField)
'Check the radio button          
lradio.IsChecked = True
'Save the document 
loadedDocument.Save("output.pdf")
'Close the document
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}

### Removing editing capability of form fields

The form field editing or filling capabilities can be removed by marking the form or field as read only. To prevent the user from changing the form field content, you can use Read-only property.

The below code snippet illustrates how to set the read only property to a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF XFA document.
PdfXfaDocument document = new PdfXfaDocument();
//Add new XFA page
PdfXfaPage xfaPage = document.Pages.Add();
//Create a new PDF XFA form with horizontal flow direction
PdfXfaForm mainForm = new PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width);
//Create a text box field and add the properties.
PdfXfaTextBoxField textBoxField = new PdfXfaTextBoxField("textBoxField", new SizeF(200, 20));
//Set the caption text.
textBoxField.Caption.Text = "Fist Name";
//Add the text box to the XFA form.
mainForm.Fields.Add(textBoxField);
//Set the form as read only.
mainForm.ReadOnly = true;
//Add the XFA form to the document.
document.XfaForm = mainForm;
//Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic);
//close the document
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF XFA document.
Dim document As New PdfXfaDocument()
'Add new XFA page
Dim xfaPage As PdfXfaPage = document.Pages.Add()
'Create a new PDF XFA form with horizontal flow direction
Dim mainForm As New PdfXfaForm(PdfXfaFlowDirection.Horizontal, xfaPage.GetClientSize().Width)
'Create a text box field and add the properties.
Dim textBoxField As New PdfXfaTextBoxField("textBoxField", New SizeF(200, 20))
'Set the caption text.
textBoxField.Caption.Text = "Fist Name"
'Add the text box to the XFA form.
mainForm.Fields.Add(textBoxField)
'Set the form as read only.
mainForm.ReadOnly = True
'Add the XFA form to the document.
document.XfaForm = mainForm
'Save the document.
document.Save("XfaForm.pdf", PdfXfaType.Dynamic)
'close the document
document.Close()

{% endhighlight %}

{% endtabs %}

The below code snippet illustrates how to set the read only property to an existing PDF document.

{% tabs %}  

{% highlight c# %}

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

{% highlight vb.net %}

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

{% endtabs %}

## Removing the dynamic form fields from an existing XFA document

You can remove the dynamic XFA form fields by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;
//Get the existing field
PdfLoadedXfaTextBoxField loadedText = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;
//Remove the field
loadedForm.Fields.Remove(loadedText);
//Save the document
loadedDocument.Save("output.pdf");
//Close the document
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Load the existing PDF document 
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the existing field
Dim loadedText As PdfLoadedXfaTextBoxField = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("text[0]"), PdfLoadedXfaTextBoxField)
'Remove the field
loadedForm.Fields.Remove(loadedText)
'Save the document 
loadedDocument.Save("output.pdf")
'Close the document
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}

## Modifying the existing fields in XFA document

You can modify the existing dynamic XFA fields by using the below code snippet.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document
PdfLoadedXfaDocument loadedDocument = new PdfLoadedXfaDocument("input.pdf");
//Load the existing XFA form
PdfLoadedXfaForm loadedForm = loadedDocument.XfaForm;
//Get the existing field
PdfLoadedXfaTextBoxField loadedText = (lform.Fields["subform1[0]"] as PdfLoadedXfaForm).Fields["text[0]"] as PdfLoadedXfaTextBoxField;
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

{% highlight vb.net %}

'Load the existing PDF document 
Dim loadedDocument As New PdfLoadedXfaDocument("input.pdf")
'Load the existing XFA form
Dim loadedForm As PdfLoadedXfaForm = loadedDocument.XfaForm
'Get the existing field
Dim loadedText As PdfLoadedXfaTextBoxField = TryCast((TryCast(lform.Fields("subform1[0]"), PdfLoadedXfaForm)).Fields("text[0]"), PdfLoadedXfaTextBoxField)
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

{% endtabs %}

N> Removing and modifying the XFA form fields will not support in **static** XFA forms.