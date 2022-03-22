---
title: Working with Form Fields | DocIO | Syncfusion
description: This section illustrated how to work with FormFields in the Syncfusion Word (DocIO) Library and more.
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Form Fields in Word Library

You can create template document with form fields such as Text, Checkbox and Drop-Down. You can also open an existing template document and fill the form fields with the specified data. 

The following are the types of form field in the Word document

* Checkbox – represented by an instance of WCheckBox
* Drop-down – represented by an instance of WDropDownFormField
* Text input – represented by an instance of WTextFormField


## Check Box

You can add new Checkbox form field to a Word document by using `AppendCheckBox` method of `WParagraph` class.

The following code illustrates how to add new checkbox form field.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("Gender\t");
//Appends new Checkbox
WCheckBox checkbox = paragraph.AppendCheckBox();
checkbox.Checked = false;
//Sets Checkbox size
checkbox.CheckBoxSize = 10; 
checkbox.CalculateOnExit = true;
//Sets help text
checkbox.Help = "Help text";
paragraph.AppendText("Male\t");
checkbox = paragraph.AppendCheckBox();
checkbox.Checked = false;
checkbox.CheckBoxSize = 10;
checkbox.CalculateOnExit = true;
paragraph.AppendText("Female");
//Saves the Word document
document.Save("Checkbox.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As WParagraph = TryCast(section.AddParagraph(), WParagraph)
paragraph.AppendText("Gender" & vbTab)
'Appends new Checkbox
Dim checkbox As WCheckBox = paragraph.AppendCheckBox()
checkbox.Checked = False
'Sets Checkbox size
checkbox.CheckBoxSize = 10
checkbox.CalculateOnExit = True
'Sets help text
checkbox.Help = "Help text"
paragraph.AppendText("Male" & vbTab)
checkbox = paragraph.AppendCheckBox()
checkbox.Checked = False
checkbox.CheckBoxSize = 10
checkbox.CalculateOnExit = True
paragraph.AppendText("Female")
'Saves the Word document
document.Save("Checkbox.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("Gender\t");
//Appends new Checkbox
WCheckBox checkbox = paragraph.AppendCheckBox();
checkbox.Checked = false;
//Sets Checkbox size
checkbox.CheckBoxSize = 10; 
checkbox.CalculateOnExit = true;
//Sets help text
checkbox.Help = "Help text";
paragraph.AppendText("Male\t");
checkbox = paragraph.AppendCheckBox();
checkbox.Checked = false;
checkbox.CheckBoxSize = 10;
checkbox.CalculateOnExit = true;
paragraph.AppendText("Female");
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Checkbox.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("Gender\t");
//Appends new Checkbox
WCheckBox checkbox = paragraph.AppendCheckBox();
checkbox.Checked = false;
//Sets Checkbox size
checkbox.CheckBoxSize = 10; 
checkbox.CalculateOnExit = true;
//Sets help text
checkbox.Help = "Help text";
paragraph.AppendText("Male\t");
checkbox = paragraph.AppendCheckBox();
checkbox.Checked = false;
checkbox.CheckBoxSize = 10;
checkbox.CalculateOnExit = true;
paragraph.AppendText("Female");
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Checkbox.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("Gender\t");
//Appends new Checkbox
WCheckBox checkbox = paragraph.AppendCheckBox();
checkbox.Checked = false;
//Sets Checkbox size
checkbox.CheckBoxSize = 10; 
checkbox.CalculateOnExit = true;
//Sets help text
checkbox.Help = "Help text";
paragraph.AppendText("Male\t");
checkbox = paragraph.AppendCheckBox();
checkbox.Checked = false;
checkbox.CheckBoxSize = 10;
checkbox.CalculateOnExit = true;
paragraph.AppendText("Female");
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Checkbox.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Form-Fields/Add-checkbox-form-field).

You can modify the checkbox properties such as checked state, size, help text in a Word document. The following code illustrates how to modify the checkbox form field properties.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Loads the template document 
WordDocument document = new WordDocument("Checkbox.docx");
//Iterates through paragraph items
foreach (ParagraphItem item in document.LastParagraph.ChildEntities)
{
    if (item is WCheckBox)
    {
        WCheckBox checkbox = item as WCheckBox;
        //Modifies check box properties
        if (checkbox.Checked)
            checkbox.Checked = false;
        checkbox.SizeType = CheckBoxSizeType.Exactly;
    }
}
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document 
Dim document As New WordDocument("Checkbox.docx")
'Iterates through paragraph items
For Each item As ParagraphItem In document.LastParagraph.ChildEntities
	If TypeOf item Is WCheckBox Then
		Dim checkbox As WCheckBox = TryCast(item, WCheckBox)
		'Modifies check box properties
		If checkbox.Checked Then
			checkbox.Checked = False
		End If
		checkbox.SizeType = CheckBoxSizeType.Exactly
	End If
Next
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}  

{% highlight c# tabtitle="UWP" %}
//Loads the template document 
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Checkbox.docx"), FormatType.Docx);
//Iterates through paragraph items
foreach (ParagraphItem item in document.LastParagraph.ChildEntities)
{
    if (item is WCheckBox)
    {
        WCheckBox checkbox = item as WCheckBox;
        //Modifies check box properties
        if (checkbox.Checked)
            checkbox.Checked = false;
        checkbox.SizeType = CheckBoxSizeType.Exactly;
    }
}
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document 
FileStream fileStreamPath = new FileStream("Checkbox.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Iterates through paragraph items
foreach (ParagraphItem item in document.LastParagraph.ChildEntities)
{
    if (item is WCheckBox)
    {
        WCheckBox checkbox = item as WCheckBox;
        //Modifies check box properties
        if (checkbox.Checked)
            checkbox.Checked = false;
        checkbox.SizeType = CheckBoxSizeType.Exactly;
    }
}
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Loads the template document 
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Checkbox.docx"), FormatType.Docx);
//Iterates through paragraph items
foreach (ParagraphItem item in document.LastParagraph.ChildEntities)
{
    if (item is WCheckBox)
    {
        WCheckBox checkbox = item as WCheckBox;
        //Modifies check box properties
        if (checkbox.Checked)
            checkbox.Checked = false;
        checkbox.SizeType = CheckBoxSizeType.Exactly;
    }
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Form-Fields/Modify-checkbox-form-field).

## Drop-Down

You can add new Dropdown form field to a Word document by using `AppendDropDownFormField` method of `WParagraph` class.

The following code illustrates how to add a new dropdown field.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("Educational Qualification\t");
//Appends Dropdown field
WDropDownFormField dropDownField = paragraph.AppendDropDownFormField();
//Adds items to the Dropdown items collection
dropDownField.DropDownItems.Add("Higher");
dropDownField.DropDownItems.Add("Vocational");
dropDownField.DropDownItems.Add("Universal");
dropDownField.Enabled = true;
//Sets the item index for default value
dropDownField.DropDownSelectedIndex = 1;
dropDownField.CalculateOnExit = true;
//Saves the Word document
document.Save("Dropdown.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As WParagraph = TryCast(section.AddParagraph(), WParagraph)
paragraph.AppendText("Educational Qualification" & vbTab)
'Appends Dropdown field
Dim dropDownField As WDropDownFormField = paragraph.AppendDropDownFormField()
'Adds items to the Dropdown items collection
dropDownField.DropDownItems.Add("Higher")
dropDownField.DropDownItems.Add("Vocational")
dropDownField.DropDownItems.Add("Universal")
dropDownField.Enabled = True
'Sets the item index for default value
dropDownField.DropDownSelectedIndex = 1
dropDownField.CalculateOnExit = True
'Saves the Word document
document.Save("Dropdown.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("Educational Qualification\t");
//Appends Dropdown field
WDropDownFormField dropDownField = paragraph.AppendDropDownFormField();
//Adds items to the Dropdown items collection
dropDownField.DropDownItems.Add("Higher");
dropDownField.DropDownItems.Add("Vocational");
dropDownField.DropDownItems.Add("Universal");
dropDownField.Enabled = true;
//Sets the item index for default value
dropDownField.DropDownSelectedIndex = 1;
dropDownField.CalculateOnExit = true;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Dropdown.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("Educational Qualification\t");
//Appends Dropdown field
WDropDownFormField dropDownField = paragraph.AppendDropDownFormField();
//Adds items to the Dropdown items collection
dropDownField.DropDownItems.Add("Higher");
dropDownField.DropDownItems.Add("Vocational");
dropDownField.DropDownItems.Add("Universal");
dropDownField.Enabled = true;
//Sets the item index for default value
dropDownField.DropDownSelectedIndex = 1;
dropDownField.CalculateOnExit = true;
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Dropdown.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("Educational Qualification\t");
//Appends Dropdown field
WDropDownFormField dropDownField = paragraph.AppendDropDownFormField();
//Adds items to the Dropdown items collection
dropDownField.DropDownItems.Add("Higher");
dropDownField.DropDownItems.Add("Vocational");
dropDownField.DropDownItems.Add("Universal");
dropDownField.Enabled = true;
//Sets the item index for default value
dropDownField.DropDownSelectedIndex = 1;
dropDownField.CalculateOnExit = true;
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Dropdown.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}  

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Form-Fields/Add-dropdown-form-field).

You can add or modify list of items of a Dropdown form field in a Word document. The following code illustrates how to modify the dropdown list of a Dropdown form field.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Loads the template document 
WordDocument document = new WordDocument("Dropdown.docx");
//Iterates through paragraph items
foreach (ParagraphItem item in document.LastParagraph.ChildEntities)
{
    if (item is WDropDownFormField)
    {
        WDropDownFormField dropdown = item as WDropDownFormField;
        //Modifies the dropdown items
        dropdown.DropDownItems.Remove(1);
        dropdown.DropDownSelectedIndex = 0;
        dropdown.CharacterFormat.FontName = "Arial";
    }
}
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document 
Dim document As New WordDocument("Dropdown.docx")
'Iterates through paragraph items
For Each item As ParagraphItem In document.LastParagraph.ChildEntities
	If TypeOf item Is WDropDownFormField Then
		Dim dropdown As WDropDownFormField = TryCast(item, WDropDownFormField)
		'Modifies the dropdown items
		dropdown.DropDownItems.Remove(1)
		dropdown.DropDownSelectedIndex = 0
		dropdown.CharacterFormat.FontName = "Arial"
	End If
Next
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Loads the template document 
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Dropdown.docx"), FormatType.Docx);
//Iterates through paragraph items
foreach (ParagraphItem item in document.LastParagraph.ChildEntities)
{
    if (item is WDropDownFormField)
    {
        WDropDownFormField dropdown = item as WDropDownFormField;
        //Modifies the dropdown items
        dropdown.DropDownItems.Remove(1);
        dropdown.DropDownSelectedIndex = 0;
        dropdown.CharacterFormat.FontName = "Arial";
    }
}
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document 
FileStream fileStreamPath = new FileStream("Dropdown.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Iterates through paragraph items
foreach (ParagraphItem item in document.LastParagraph.ChildEntities)
{
    if (item is WDropDownFormField)
    {
        WDropDownFormField dropdown = item as WDropDownFormField;
        //Modifies the dropdown items
        dropdown.DropDownItems.Remove(1);
        dropdown.DropDownSelectedIndex = 0;
        dropdown.CharacterFormat.FontName = "Arial";
    }
}
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Loads the template document 
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Dropdown.docx"), FormatType.Docx);
//Iterates through paragraph items
foreach (ParagraphItem item in document.LastParagraph.ChildEntities)
{
    if (item is WDropDownFormField)
    {
        WDropDownFormField dropdown = item as WDropDownFormField;
        //Modifies the dropdown items
        dropdown.DropDownItems.Remove(1);
        dropdown.DropDownSelectedIndex = 0;
        dropdown.CharacterFormat.FontName = "Arial";
    }
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Form-Fields/Modify-dropdown-form-field).

## Text Form field

You can add new text form field to a Word document by using `AppendTextFormField` method of `WParagraph` class.

The following code illustrates how to add new text form field.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("General Information");
section.AddParagraph();
paragraph = section.AddParagraph() as WParagraph;
IWTextRange text = paragraph.AppendText("Name\t");
text.CharacterFormat.Bold = true;
//Appends Text form field 
WTextFormField textField = paragraph.AppendTextFormField(null);
//Sets type of Text form field
textField.Type = TextFormFieldType.RegularText;
textField.CharacterFormat.FontName = "Calibri";
textField.CalculateOnExit = true;
section.AddParagraph();
paragraph = section.AddParagraph() as WParagraph;
text = paragraph.AppendText("Date of Birth\t");
text.CharacterFormat.Bold = true;
//Appends Text form field
textField = paragraph.AppendTextFormField("Date field", DateTime.Now.ToString("MM/DD/YY"));
textField.StringFormat = "MM/DD/YY";
//Sets Text form field type
textField.Type = TextFormFieldType.DateText;
textField.CalculateOnExit = true;
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As WParagraph = TryCast(section.AddParagraph(), WParagraph)
paragraph.AppendText("General Information")
section.AddParagraph()
paragraph = TryCast(section.AddParagraph(), WParagraph)
Dim text As IWTextRange = paragraph.AppendText("Name" & vbTab)
text.CharacterFormat.Bold = True
'Appends Text form field 
Dim textField As WTextFormField = paragraph.AppendTextFormField(Nothing)
'Sets type of Text form field
textField.Type = TextFormFieldType.RegularText
textField.CharacterFormat.FontName = "Calibri"
textField.CalculateOnExit = True
section.AddParagraph()
paragraph = TryCast(section.AddParagraph(), WParagraph)
text = paragraph.AppendText("Date of Birth" & vbTab)
text.CharacterFormat.Bold = True
'Appends Text form field
textField = paragraph.AppendTextFormField("Date field", DateTime.Now.ToString("MM/DD/YY"))
textField.StringFormat = "MM/DD/YY"
'Sets Text form field type
textField.Type = TextFormFieldType.DateText
textField.CalculateOnExit = True
'Saves the Word document
document.Save("textField.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}  

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("General Information");
section.AddParagraph();
paragraph = section.AddParagraph() as WParagraph;
IWTextRange text = paragraph.AppendText("Name\t");
text.CharacterFormat.Bold = true;
//Appends Text form field 
WTextFormField textField = paragraph.AppendTextFormField(null);
//Sets type of Text form field
textField.Type = TextFormFieldType.RegularText;
textField.CharacterFormat.FontName = "Calibri";
textField.CalculateOnExit = true;
section.AddParagraph();
paragraph = section.AddParagraph() as WParagraph;
text = paragraph.AppendText("Date of Birth\t");
text.CharacterFormat.Bold = true;
//Appends Text form field
textField = paragraph.AppendTextFormField("Date field", DateTime.Now.ToString("MM/DD/YY"));
textField.StringFormat = "MM/DD/YY";
//Sets Text form field type
textField.Type = TextFormFieldType.DateText;
textField.CalculateOnExit = true;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("General Information");
section.AddParagraph();
paragraph = section.AddParagraph() as WParagraph;
IWTextRange text = paragraph.AppendText("Name\t");
text.CharacterFormat.Bold = true;
//Appends Text form field 
WTextFormField textField = paragraph.AppendTextFormField(null);
//Sets type of Text form field
textField.Type = TextFormFieldType.RegularText;
textField.CharacterFormat.FontName = "Calibri";
textField.CalculateOnExit = true;
section.AddParagraph();
paragraph = section.AddParagraph() as WParagraph;
text = paragraph.AppendText("Date of Birth\t");
text.CharacterFormat.Bold = true;
//Appends Text form field
textField = paragraph.AppendTextFormField("Date field", DateTime.Now.ToString("MM/DD/YY"));
textField.StringFormat = "MM/DD/YY";
//Sets Text form field type
textField.Type = TextFormFieldType.DateText;
textField.CalculateOnExit = true;
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
paragraph.AppendText("General Information");
section.AddParagraph();
paragraph = section.AddParagraph() as WParagraph;
IWTextRange text = paragraph.AppendText("Name\t");
text.CharacterFormat.Bold = true;
//Appends Text form field 
WTextFormField textField = paragraph.AppendTextFormField(null);
//Sets type of Text form field
textField.Type = TextFormFieldType.RegularText;
textField.CharacterFormat.FontName = "Calibri";
textField.CalculateOnExit = true;
section.AddParagraph();
paragraph = section.AddParagraph() as WParagraph;
text = paragraph.AppendText("Date of Birth\t");
text.CharacterFormat.Bold = true;
//Appends Text form field
textField = paragraph.AppendTextFormField("Date field", DateTime.Now.ToString("MM/DD/YY"));
textField.StringFormat = "MM/DD/YY";
//Sets Text form field type
textField.Type = TextFormFieldType.DateText;
textField.CalculateOnExit = true;
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Form-Fields/Add-text-form-field).

You can add or modify text form field properties such as default text, type in a Word document. The following code illustrates how to modify the text form field

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Loads the template document 
WordDocument document = new WordDocument("Template.docx");
//Iterates through section
foreach (WSection section in document.Sections)
    //Iterates through section child elements
    foreach (WTextBody textBody in section.ChildEntities)
    {
        //Iterates through form fields
        foreach (WFormField formField in textBody.FormFields)
        {
            switch (formField.FormFieldType)
            {
                case FormFieldType.TextInput:
                    WTextFormField textField = formField as WTextFormField;
                    if (textField.Type == TextFormFieldType.DateText)
                    {
                        //Modifies the text form field
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
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document 
Dim document As New WordDocument("Template.docx")
'Iterates through section
For Each section As WSection In document.Sections
	'Iterates through section child elements
	For Each textBody As WTextBody In section.ChildEntities
		'Iterates through form fields
		For Each formField As WFormField In textBody.FormFields
			Select Case formField.FormFieldType
				Case FormFieldType.TextInput
					Dim textField As WTextFormField = TryCast(formField, WTextFormField)
					If textField.Type = TextFormFieldType.DateText Then
						'Modifies the text form field
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
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Loads the template document 
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Iterates through section
foreach (WSection section in document.Sections)
    //Iterates through section child elements
    foreach (WTextBody textBody in section.ChildEntities)
    {
        //Iterates through form fields
        foreach (WFormField formField in textBody.FormFields)
        {
            switch (formField.FormFieldType)
            {
                case FormFieldType.TextInput:
                    WTextFormField textField = formField as WTextFormField;
                    if (textField.Type == TextFormFieldType.DateText)
                    {
                        //Modifies the text form field
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
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Iterates through section
foreach (WSection section in document.Sections)
    //Iterates through section child elements
    foreach (WTextBody textBody in section.ChildEntities)
    {
        //Iterates through form fields
        foreach (WFormField formField in textBody.FormFields)
        {
            switch (formField.FormFieldType)
            {
                case FormFieldType.TextInput:
                    WTextFormField textField = formField as WTextFormField;
                    if (textField.Type == TextFormFieldType.DateText)
                    {
                        //Modifies the text form field
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
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Loads the template document 
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Template.docx"), FormatType.Docx);
//Iterates through section
foreach (WSection section in document.Sections)
    //Iterates through section child elements
    foreach (WTextBody textBody in section.ChildEntities)
    {
        //Iterates through form fields
        foreach (WFormField formField in textBody.FormFields)
        {
            switch (formField.FormFieldType)
            {
                case FormFieldType.TextInput:
                    WTextFormField textField = formField as WTextFormField;
                    if (textField.Type == TextFormFieldType.DateText)
                    {
                        //Modifies the text form field
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
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Form-Fields/Modify-text-form-field).