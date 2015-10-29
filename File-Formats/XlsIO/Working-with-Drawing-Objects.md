---
title: Working with Drawing Objects
description: Briefs about Drawing Objects in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Working with Drawing Objects 

## Form Controls 

You can add and manipulate the text Box, option button, check box and combo box controls into the worksheet. These controls enables to create forms which are very user friendly.

I> Support for Active X Form controls is not yet available.

This section explains the usage of the following [Form controls](https://support.office.com/en-us/article/Overview-of-forms-Form-controls-and-ActiveX-controls-on-a-worksheet-15BA7E28-8D7F-42AB-9470-FFB9AB94E7C2#bmcontrols_on_the_forms_toolbar "").

* Text Box
* Check Box
* Combo Box
* Option Button

### Text Box

The **ITextBoxShape** interface represents a text box in a worksheet. Various properties like Horizontal and Vertical Alignment, Alternative Text, Text Rotation, and so on, are also supported.

The following code example illustrates how to add and manipulate a text box control.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

// Creates a new Text Box.

ITextBoxShape textbox = sheet.TextBoxes.AddTextBox(2, 2, 30, 200);

textbox.Text = "Text Box 1";

textbox = sheet.TextBoxes.AddTextBox(6, 2, 30, 200);

textbox.Text = "Text Box 2";

// Reads a Text Box.

ITextBoxShape shape1 = sheet.TextBoxes[0];

shape1.Text = "TextBox";

// Format the control.

shape1.Fill.ForeColor = Color.Gold;

shape1.Fill.BackColor = Color.Black;

shape1.Fill.Pattern = ExcelGradientPattern.Pat_90_Percent;



// Remove a Text Box

ITextBoxShape shape2 = sheet.TextBoxes[1];

shape2.Remove();

workbook.SaveAs("Textbox.xlsx");

workbook.Close();

excelEngine.Dispose(); 



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Creates a new Text Box.

Dim textbox As ITextBoxShape = sheet.TextBoxes.AddTextBox(2, 2, 30, 200)

textbox.Text = "Text Box 1"

textbox = sheet.TextBoxes.AddTextBox(6, 2, 30, 200)

textbox.Text = "Text Box 2"

' Reads a Text Box.

Dim shape1 As ITextBoxShape = sheet.TextBoxes(0)

shape1.Text = "TextBox"

' Format the control.

shape1.Fill.ForeColor = Color.Gold

shape1.Fill.BackColor = Color.Black

shape1.Fill.Pattern = ExcelGradientPattern.Pat_90_Percent

' Remove a Text Box

Dim shape2 As ITextBoxShape = sheet.TextBoxes(1)

shape2.Remove()

workbook.SaveAs("Textbox.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

### Check Box

**ICheckBoxShape** object represents a check box in a worksheet. The following code example illustrates how to insert and manipulate a check box control.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Create a check box with cell link.

ICheckBoxShape chkBoxRed = sheet.CheckBoxes.AddCheckBox(2, 4, 20, 75);

chkBoxRed.Text = "Red";

chkBoxRed.CheckState = ExcelCheckState.Unchecked;

chkBoxRed.LinkedCell = sheet["B2"];

ICheckBoxShape chkBoxBlue = sheet.CheckBoxes.AddCheckBox(4, 4, 20, 75);

chkBoxBlue.Text = "Blue";

chkBoxBlue.CheckState = ExcelCheckState.Checked;

chkBoxBlue.LinkedCell = sheet["B4"];

//Read a check box.

chkBoxRed = sheet.CheckBoxes[0];

chkBoxRed.CheckState = ExcelCheckState.Checked;

//Remove a check box

chkBoxBlue = sheet.CheckBoxes[1];

chkBoxBlue.Remove();

workbook.SaveAs("Checkbox.xlsx");

workbook.Close();

excelEngine.Dispose(); 



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Create a check box with cell link.

Dim chkBoxRed As ICheckBoxShape = sheet.CheckBoxes.AddCheckBox(2, 4, 20, 75)

chkBoxRed.Text = "Red"

chkBoxRed.CheckState = ExcelCheckState.Unchecked

chkBoxRed.LinkedCell = sheet("B2")

Dim chkBoxBlue As ICheckBoxShape = sheet.CheckBoxes.AddCheckBox(4, 4, 20, 75)

chkBoxBlue.Text = "Blue"

chkBoxBlue.CheckState = ExcelCheckState.Checked

chkBoxBlue.LinkedCell = sheet("B4")

'Read a check box.

chkBoxRed = sheet.CheckBoxes(0)

chkBoxRed.CheckState = ExcelCheckState.Checked

'Remove a check box

chkBoxBlue = sheet.CheckBoxes(1)

chkBoxBlue.Remove()

workbook.SaveAs("Checkbox.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

### Combo Box

**IComboBoxShape** object represents a combo box in a worksheet. The following code example illustrates how to insert and manipulate a combo box control.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Filling Values

sheet["A2"].Text = "RGB colors";

sheet["A3"].Text = "Red";

sheet["A4"].Text = "Green";

sheet["A5"].Text = "Blue";

sheet["B5"].Text = "Selected Index";

// Create a Combo Box.

IComboBoxShape comboBox1 = sheet.ComboBoxes.AddComboBox(2, 3, 20, 100);

// Assign a value to the Combo Box.

comboBox1.ListFillRange = sheet["A3:A5"];

comboBox1.LinkedCell = sheet["C5"];

comboBox1.SelectedIndex = 2;

// Create a Combo Box.

IComboBoxShape comboBox2 = sheet.ComboBoxes.AddComboBox(5, 3, 20, 100);

// Assign a value to the Combo Box.

comboBox2.ListFillRange = sheet["A3:A5"];

comboBox2.LinkedCell = sheet["C5"];

comboBox2.SelectedIndex = 1;

// Read a Combo Box

comboBox1 = sheet.ComboBoxes[0];

comboBox1.SelectedIndex = 1;

// Remove a Combo Box

comboBox2 = sheet.ComboBoxes[1];

comboBox2.Remove();

workbook.SaveAs("Combobox.xlsx");

workbook.Close();

excelEngine.Dispose(); 



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Filling Values

sheet("A2").Text = "RGB colors"

sheet("A3").Text = "Red"

sheet("A4").Text = "Green"

sheet("A5").Text = "Blue"

sheet("B5").Text = "Selected Index"

' Create a Combo Box.

Dim comboBox1 As IComboBoxShape = sheet.ComboBoxes.AddComboBox(2, 3, 20, 100)

' Assign a value to the Combo Box.

comboBox1.ListFillRange = sheet("A3:A5")

comboBox1.LinkedCell = sheet("C5")

comboBox1.SelectedIndex = 2

' Create a Combo Box.

Dim comboBox2 As IComboBoxShape = sheet.ComboBoxes.AddComboBox(5, 3, 20, 100)

' Assign a value to the Combo Box.

comboBox2.ListFillRange = sheet("A3:A5")

comboBox2.LinkedCell = sheet("C5")

comboBox2.SelectedIndex = 1

' Read a Combo Box

comboBox1 = sheet.ComboBoxes(0)

comboBox1.SelectedIndex = 1

' Remove a Combo Box

comboBox2 = sheet.ComboBoxes(1)

comboBox2.Remove()

workbook.SaveAs("Combobox.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

### Option Button

**IOptionButtonShape** object represents a combo box in a worksheet. The following code example illustrates how to insert and manipulate an option button control.

I> XlsIO provides Option button support for only XLSX format.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

// Create an Option Button.

IOptionButtonShape optionButton1 = sheet.OptionButtons.AddOptionButton(2, 3);

// Assign a value to the Option Button.

optionButton1.Text = "Fed Ex";

// Format the control.

optionButton1.Fill.FillType = ExcelFillType.SolidColor;

optionButton1.Fill.ForeColor = Color.Yellow;

// Change the check state.

optionButton1.CheckState = ExcelCheckState.Checked;

// Create an Option Button.

IOptionButtonShape optionButton2 = sheet.OptionButtons.AddOptionButton(5, 3);

// Assign a value to the Option Button.

optionButton2.Text = "DHL";

// Read an Option Button.

optionButton1 = sheet.OptionButtons[0];

optionButton1.CheckState = ExcelCheckState.Unchecked;

// Remove an Option Button

optionButton2 = sheet.OptionButtons[1];

optionButton2.Remove();

workbook.SaveAs("OptionButton.xlsx");

workbook.Close();

excelEngine.Dispose();          



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Create an Option Button.

Dim optionButton1 As IOptionButtonShape = sheet.OptionButtons.AddOptionButton(2, 3)

' Assign a value to the Option Button.

optionButton1.Text = "Fed Ex"

' Format the control.

optionButton1.Fill.FillType = ExcelFillType.SolidColor

optionButton1.Fill.ForeColor = Color.Yellow

' Change the check state.

optionButton1.CheckState = ExcelCheckState.Checked

' Create an Option Button.

Dim optionButton2 As IOptionButtonShape = sheet.OptionButtons.AddOptionButton(5, 3)

' Assign a value to the Option Button.

optionButton2.Text = "DHL"

' Read an Option Button.

optionButton1 = sheet.OptionButtons(0)

optionButton1.CheckState = ExcelCheckState.Unchecked

' Remove an Option Button

optionButton2 = sheet.OptionButtons(1)

optionButton2.Remove()

workbook.SaveAs("OptionButton.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## Comments

**ICommentShape** object represents a [comments](https://support.office.com/en-au/article/Annotate-a-worksheet-by-using-comments-3b7065dd-531a-4ffe-8f18-8d047a6ccae7# "") in a worksheet. You can insert both **Regular** and **Rich** **Text** comments. The following code example illustrates how to insert and manipulate comments.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

// Adding comments to a cell.

sheet.Range["A1"].AddComment().Text = "Comments";

// Add Rich Text Comments.

IRange range = sheet.Range["A6"];

range.AddComment().RichText.Text = "RichText";

IRichTextString rtf = range.Comment.RichText;

// Formatting first 4 characters.

IFont redFont = workbook.CreateFont();

redFont.Bold = true;

redFont.Color = ExcelKnownColors.Red;

rtf.SetFont(0, 3, redFont);

workbook.SaveAs("Comments.xlsx");

workbook.Close();

excelEngine.Dispose();    



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Adding comments to a cell.

sheet.Range("A1").AddComment().Text = "Comments"

' Add Rich Text Comments.

Dim range As IRange = sheet.Range("A6")

range.AddComment().RichText.Text = "RichText"

Dim rtf As IRichTextString = range.Comment.RichText

' Formatting first 4 characters.

Dim redFont As IFont = workbook.CreateFont()

redFont.Bold = True

redFont.Color = ExcelKnownColors.Red

rtf.SetFont(0, 3, redFont)

workbook.SaveAs("Comments.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

You can also fill the comments with various types of fills by using the **IFill** interface. Following code example illustrates how to fill the comment shape with a TwoColor gradient.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

// Adding comments to a cell.

sheet.Range["A1"].AddComment().Text = "Comments";

// Accessing existing comment

ICommentShape shape = sheet.Range["A1"].Comment;

// Format the comment

shape.Fill.TwoColorGradient();

shape.Fill.GradientStyle = ExcelGradientStyle.Horizontal;

shape.Fill.GradientColorType = ExcelGradientColor.TwoColor;

shape.Fill.ForeColorIndex = ExcelKnownColors.Red;

shape.Fill.BackColorIndex = ExcelKnownColors.White;  

workbook.SaveAs("FormatComments.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Adding comments to a cell.

sheet.Range("A1").AddComment().Text = "Comments"

' Accessing existing comment

Dim shape As ICommentShape = sheet.Range("A1").Comment

' Format the comment

shape.Fill.TwoColorGradient()

shape.Fill.GradientStyle = ExcelGradientStyle.Horizontal

shape.Fill.GradientColorType = ExcelGradientColor.TwoColor

shape.Fill.ForeColorIndex = ExcelKnownColors.Red

shape.Fill.BackColorIndex = ExcelKnownColors.White

workbook.SaveAs("FormatComments.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

Following code snippets illustrates how to remove all the comments in existing worksheet.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Comments.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Remove all the comments in worksheet

sheet.Comments.Clear();

workbook.SaveAs("RemoveComments.xlsx");

workbook.Version = ExcelVersion.Excel2013; 

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Comments.xlsx")

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Remove all the comments in worksheet

sheet.Comments.Clear()

workbook.SaveAs("RemoveComments.xlsx")

workbook.Version = ExcelVersion.Excel2013

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## AutoShapes

The **IShape** interface represents the [AutoShapes](https://support.office.com/en-ca/article/Add-change-or-delete-shapes-4f7931c3-7794-440e-820e-9469ad756f05# "") in an Excel workbook. 

LINK- API reference for AutoShapeType enum.

The following code example illustrates how to insert and format autoshapes.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

// Adding an autoshape.

IShape shape1 = worksheet.Shapes.AddAutoShapes(AutoShapeType.RoundedRectangle, 2, 7, 60, 192);

IShape shape2 = worksheet.Shapes.AddAutoShapes(AutoShapeType.CircularArrow, 8, 7, 60, 192);

// Set the value inside the shape.

shape1.TextFrame.TextRange.Text = "AutoShape";

// Format the shape.

shape1.Fill.ForeColorIndex = ExcelKnownColors.Light_blue;

shape1.TextFrame.VerticalAlignment = ExcelVerticalAlignment.MiddleCentered;

// Read an AutoShape

shape1 = worksheet.Shapes[0];

shape1.TextFrame.TextRange.Text = "RoundedRectangle";

// Remove an AutoShape

shape2 = worksheet.Shapes[1];

shape2.Remove();

workbook.SaveAs("Autoshapes.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

' Adding an autoshape.

Dim shape1 As IShape = worksheet.Shapes.AddAutoShapes(AutoShapeType.RoundedRectangle, 2, 7, 60, 192)

Dim shape2 As IShape = worksheet.Shapes.AddAutoShapes(AutoShapeType.CircularArrow, 8, 7, 60, 192)

' Set the value inside the shape.

shape1.TextFrame.TextRange.Text = "AutoShape"

' Format the shape.

shape1.Fill.ForeColorIndex = ExcelKnownColors.Light_blue

shape1.TextFrame.VerticalAlignment = ExcelVerticalAlignment.MiddleCentered

' Read an AutoShape

shape1 = worksheet.Shapes(0)

shape1.TextFrame.TextRange.Text = "RoundedRectangle"

' Remove an AutoShape

shape2 = worksheet.Shapes(1)

shape2.Remove()

workbook.SaveAs("Autoshapes.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## OLE Objects 

**IOleObject** object represents an [OLE Objects](https://support.office.com/en-US/article/Create-change-or-delete-an-OLE-object-F767F0F1-4170-4850-9B96-0B6C07EC6EA4# "") in a worksheet. 

I> XlsIO provides OLE Objects support for XLSX format in Windows, ASP.NET and WPF platforms only.

**OLE** **Objects** **and** **Linking** **Types**

XlsIO supports two types of association of objects:

* Linked objects.
* Embedded objects. 

**1****.** **Linked** **Objects** 

Linked objects remain as a separate files. When the file is opened in another machine, then linked object should be in the same location as created.

The following sample code illustrates how to linking an OLE Object to an Excel document.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

Image image = Image.FromFile("image.png");

// Select the object, image for the display icon and the type of the OLEObject to insert.

IOleObject ole2 = sheet.OleObjects.Add("Document.docx", image, OleLinkType.Link);

workbook.SaveAs("LinkedObjects.xlsx");

workbook.Close();

excelEngine.Dispose();        



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim image As Image = image.FromFile("image.png")

' Select the object, image for the display icon and the type of the OLEObject to insert.

Dim ole2 As IOleObject = sheet.OleObjects.Add("Document.docx", image, OleLinkType.Link)

workbook.SaveAs("LinkedObjects.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

**2****.** **Embedded** **Objects**  

Embedded objects are stored in the document. When the file is opened in another machine, the embedded object can be viewed without having access to the original data.

The following sample code illustrates how to embed an OLE Object to an Excel document.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

Image image = Image.FromFile("image.png");

// Select the object, image for the display icon and the type of the OLEObject to insert.

IOleObject ole1 = sheet.OleObjects.Add("Test.pptx", image, OleLinkType.Embed);

workbook.SaveAs("EmbeddedObjects.xlsx");

workbook.Close();

excelEngine.Dispose();        



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

Dim image As Image = Image.FromFile("image.png")

' Select the object, image for the display icon and the type of the OLEObject to insert.

Dim ole1 As IOleObject = sheet.OleObjects.Add("Test.pptx", image, OleLinkType.Embed)

workbook.SaveAs("EmbeddedObjects.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

The following code example illustrates how to insert and manipulate OLEObjects with their properties. 

LINK- API reference to IOleObjects

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

// Icon image

Image image = Image.FromFile("Images.png");

// Select the object, image for the display icon and the type of the OLEObject to insert

IOleObject oleObject1 = sheet.OleObjects.Add("Employee.docx", image, OleLinkType.Embed);

// Select the object, image for the display icon and the type of the OLEObject to insert

IOleObject oleObject2 = sheet.OleObjects.Add("Customer.docx", image, OleLinkType.Embed);

// Displays image as icon

oleObject1.DisplayAsIcon = true;

// Set the location of the OleObject

oleObject1.Location = sheet["K8"];

// Reads icon as a image

Image image1 = oleObject1.Picture;

// Reads OleObject as a IPictureShape

IPictureShape oleObjectPicture = oleObject1.Shape;

//Set the size of the OleObject

oleObject1.Size = new Size(30, 30);



// Remove OleObjects

oleObject2 = sheet.OleObjects[1];

oleObject2.Shape.Remove();

workbook.SaveAs("OleObjects.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Icon image

Dim image As Image = image.FromFile("Images.png")

' Select the object, image for the display icon and the type of the OLEObject to insert

Dim oleObject1 As IOleObject = sheet.OleObjects.Add("Employee.docx", image, OleLinkType.Embed)

' Select the object, image for the display icon and the type of the OLEObject to insert

Dim oleObject2 As IOleObject = sheet.OleObjects.Add("Customer.docx", image, OleLinkType.Embed)

' Displays image as icon

oleObject1.DisplayAsIcon = True

' Set the location of the OleObject

oleObject1.Location = sheet("K8")

' Reads icon as a image

Dim image1 As Image = oleObject1.Picture

' Reads OleObject as a IPictureShape

Dim oleObjectPicture As IPictureShape = oleObject1.Shape

'Set the size of the OleObject

oleObject1.Size = New Size(30, 30)

' Remove OleObjects

oleObject2 = sheet.OleObjects(1)

oleObject2.Shape.Remove()

workbook.SaveAs("OleObjects.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

# 

