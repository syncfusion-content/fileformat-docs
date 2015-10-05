---
layout: Post
title: Working with Form Fields
description: This section illustrated how to work with FormFields
platform: FileFormat
control: DocIO
documentation: UG
---
# Working with Form Fields

You can create template document with form fields such as Text, Checkbox and Drop-Down. You can also open an existing template document and fill the form fields with specified data. 

The following are the types of form field in Word document

* Checkbox – represented by an instance of WCheckBox
* Drop-down – represented by an instance of WDropDownFormField
* Text input – represented by an instance of WTextFormField
## Check Box


You can add new Checkbox form field to a Word document using **AppendCheckBox** method of **WParagraph** class.

The following code illustrates how to add new checkbox form field.

{% highlight c# %}
[C#]

//Create a new Word document 

WordDocument document = new WordDocument();

//Add new section to the document

IWSection section = document.AddSection();

//Add new paragraph to the section

WParagraph paragraph = section.AddParagraph() as WParagraph;

paragraph.AppendText("Gender\t");

//Append new Checkbox

WCheckBox checkbox = paragraph.AppendCheckBox();

checkbox.Checked = false;

//Set Checkbox size

checkbox.CheckBoxSize = 10; 

checkbox.CalculateOnExit = true;

//Set help text

checkbox.Help = "Help text";

paragraph.AppendText("Male\t");

checkbox = paragraph.AppendCheckBox();

checkbox.Checked = false;

checkbox.CheckBoxSize = 10;

checkbox.CalculateOnExit = true;

paragraph.AppendText("Female");

//Save the Word document

document.Save("Checkbox.docx", FormatType.Docx);

//Close the document

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create a new Word document 

Dim document As New WordDocument()

'Add new section to the document

Dim section As IWSection = document.AddSection()

'Add new paragraph to the section

Dim paragraph As WParagraph = TryCast(section.AddParagraph(), WParagraph)

paragraph.AppendText("Gender" & vbTab)

'Append new Checkbox

Dim checkbox As WCheckBox = paragraph.AppendCheckBox()

checkbox.Checked = False

'Set Checkbox size

checkbox.CheckBoxSize = 10

checkbox.CalculateOnExit = True

'Set help text

checkbox.Help = "Help text"

paragraph.AppendText("Male" & vbTab)

checkbox = paragraph.AppendCheckBox()

checkbox.Checked = False

checkbox.CheckBoxSize = 10

checkbox.CalculateOnExit = True

paragraph.AppendText("Female")

'Save the Word document

document.Save("Checkbox.docx", FormatType.Docx)

'Close the document

document.Close()





{% endhighlight %}

You can modify the checkbox properties such as checked state, size, help text in a Word document. The following code illustrates how to modify the checkbox form field properties.

{% highlight c# %}
[C#]

//Load the template document 

WordDocument document = new WordDocument("Checkbox.docx");

//Iterate through paragraph items

foreach (ParagraphItem item in document.LastParagraph.ChildEntities)

{

if (item is WCheckBox)

{

WCheckBox checkbox = item as WCheckBox;

//Modify check box properties

if (checkbox.Checked)

checkbox.Checked= false;

checkbox.SizeType = CheckBoxSizeType.Exactly;

}

}

//Save the Word document

document.Save("Sample.docx", FormatType.Docx);

//Close the document

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load the template document 

Dim document As New WordDocument("Checkbox.docx")

'Iterate through paragraph items

For Each item As ParagraphItem In document.LastParagraph.ChildEntities

If TypeOf item Is WCheckBox Then

Dim checkbox As WCheckBox = TryCast(item, WCheckBox)

'Modify check box properties

If checkbox.Checked Then

checkbox.Checked = False

End If

checkbox.SizeType = CheckBoxSizeType.Exactly

End If

Next

'Save the Word document

document.Save("Sample.docx", FormatType.Docx)

'Close the document

document.Close()





{% endhighlight %}

## Drop-Down

You can add new Dropdown form field to a Word document using **AppendDropDownFormField** method of **WParagraph** class.

The following code illustrates how to add a new dropdown field.

{% highlight c# %}
[C#]

//Create a new Word document 

WordDocument document = new WordDocument();

//Add new section to the document

IWSection section = document.AddSection();

//Add new paragraph to the section

WParagraph paragraph = section.AddParagraph() as WParagraph;

paragraph.AppendText("Educational Qualification\t");

//Append Dropdown field

WDropDownFormField dropdownfield = paragraph.AppendDropDownFormField();

//Add items to the dropdown items collection

dropdownfield.DropDownItems.Add("Higher");

dropdownfield.DropDownItems.Add("Vocational");

dropdownfield.DropDownItems.Add("Universal");

dropdownfield.Enabled = true;

//Set the item index for default value

dropdownfield.DropDownSelectedIndex = 1;

dropdownfield.CalculateOnExit = true;

//Save the Word document

document.Save("Dropdown.docx", FormatType.Docx);

//Close the document

document.Close();



{% endhighlight %}

You can add or modify list of items of a Dropdown form field in a Word document. The following code illustrates how to modify the dropdown list of a Dropdown form field.

{% highlight c# %}
[C#]

//Load the template document 

WordDocument document = new WordDocument("Dropdown.docx");

//Iterate through paragraph items

foreach (ParagraphItem item in document.LastParagraph.ChildEntities)

{

if (item is WDropDownFormField)

{

WDropDownFormField dropdown = item as WDropDownFormField;

//Modify the dropdown items

dropdown.DropDownItems.Remove(1);

dropdown.DropDownSelectedIndex = 0;

dropdown.CharacterFormat.FontName = "Arial";

}

}

//Save the Word document

document.Save("Sample.docx", FormatType.Docx);

//Close the document

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load the template document 

Dim document As New WordDocument("Dropdown.docx")

'Iterate through paragraph items

For Each item As ParagraphItem In document.LastParagraph.ChildEntities

If TypeOf item Is WDropDownFormField Then

Dim dropdown As WDropDownFormField = TryCast(item, WDropDownFormField)

'Modify the dropdown items

dropdown.DropDownItems.Remove(1)

dropdown.DropDownSelectedIndex = 0

dropdown.CharacterFormat.FontName = "Arial"

End If

Next

'Save the Word document

document.Save("Sample.docx", FormatType.Docx)

'Close the document

document.Close()





{% endhighlight %}

## Text Form field

You can add new text form field to a Word document using **AppendTextFormField** method of **WParagraph** class.

The following code illustrates how to add new text form field.

{% highlight c# %}
[C#]

//Create a new Word document 

WordDocument document = new WordDocument();

//Add new section to the document

IWSection section = document.AddSection();

//Add new paragraph to the section

WParagraph paragraph = section.AddParagraph() as WParagraph;

paragraph.AppendText("General Information");

section.AddParagraph();

paragraph = section.AddParagraph() as WParagraph;

IWTextRange text = paragraph.AppendText("Name\t");

text.CharacterFormat.Bold = true;

//Append Text form field 

WTextFormField textfield = paragraph.AppendTextFormField(null);

//Set type of Text form field

textfield.Type = TextFormFieldType.RegularText;

textfield.CharacterFormat.FontName = "Calibri";

textfield.CalculateOnExit = true;

section.AddParagraph();

paragraph = section.AddParagraph() as WParagraph;

text = paragraph.AppendText("Date of Birth\t");

text.CharacterFormat.Bold = true;

//Append Text form field

textfield = paragraph.AppendTextFormField("Date field", DateTime.Now.ToString("MM/DD/YY"));

textfield.StringFormat = "MM/DD/YY";

//Set Text form field type

textfield.Type = TextFormFieldType.DateText;

textfield.CalculateOnExit = true;

//Save the Word document

document.Save("Textfield.docx", FormatType.Docx);

//Close the document

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create a new Word document 

Dim document As New WordDocument()

'Add new section to the document

section As IWSection = document.AddSection()

'Add new paragraph to the section

Dim paragraph As WParagraph = TryCast(section.AddParagraph(), WParagraph)

paragraph.AppendText("General Information")

section.AddParagraph()

paragraph = TryCast(section.AddParagraph(), WParagraph)

Dim text As IWTextRange = paragraph.AppendText("Name" & vbTab)

text.CharacterFormat.Bold = True

'Append Text form field 

Dim textfield As WTextFormField = paragraph.AppendTextFormField(Nothing)

'Set type of Text form field

textfield.Type = TextFormFieldType.RegularText

textfield.CharacterFormat.FontName = "Calibri"

textfield.CalculateOnExit = True

section.AddParagraph()

paragraph = TryCast(section.AddParagraph(), WParagraph)

text = paragraph.AppendText("Date of Birth" & vbTab)

text.CharacterFormat.Bold = True

'Append Text form field

textfield = paragraph.AppendTextFormField("Date field", DateTime.Now.ToString("MM/DD/YY"))

textfield.StringFormat = "MM/DD/YY"

'Set Text form field type

textfield.Type = TextFormFieldType.DateText

textfield.CalculateOnExit = True

'Save the Word document

document.Save("Textfield.docx", FormatType.Docx)

'Close the document

document.Close()





{% endhighlight %}

You can add or modify text form field properties such as default text, type in a Word document. The following code illustrates how to modify the text form field

{% highlight c# %}
[C#]

//Load the template document 

WordDocument document = new WordDocument("Textfield.docx");

//Iterate through section

foreach (WSection section in document.Sections)

//Iterate through section child elements

foreach (WTextBody textBody in section.ChildEntities)

{

//Iterate through form fields

foreach (WFormField formField in textBody.FormFields)

{

switch (formField.FormFieldType)

{

case FormFieldType.TextInput:

WTextFormField textField = formField as WTextFormField;

if (textField.Type == TextFormFieldType.DateText)

{

//Modify the text form field

textField.Type = TextFormFieldType.RegularText;

textField.StringFormat = "";

textField.DefaultText = "Default text";

textField.Text = "Default text";

textField.CalculateOnExit = false;

}

break;

}

}

}

//Save the Word document

document.Save("Sample.docx", FormatType.Docx);

//Close the document

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load the template document 

Dim document As New WordDocument("Textfield.docx")

'Iterate through section

For Each section As WSection In document.Sections

'Iterate through section child elements

For Each textBody As WTextBody In section.ChildEntities

'Iterate through form fields

For Each formField As WFormField In textBody.FormFields

Select Case formField.FormFieldType

Case FormFieldType.TextInput

Dim textField As WTextFormField = TryCast(formField, WTextFormField)

If textField.Type = TextFormFieldType.DateText Then

'Modify the text form field

textField.Type = TextFormFieldType.RegularText

textField.StringFormat = ""

textField.DefaultText = "Default text"

textField.Text = "Default text"

textField.CalculateOnExit = False

End If

Exit Select

End Select

Next

Next

Next

'Save the Word document

document.Save("Sample.docx", FormatType.Docx)

'Close the document

document.Close()





{% endhighlight %}

