---
title: Working with PowerPoint presentation
description: Working with PowerPoint presentation; Cloning the presentation; printing the presentation
platform: FileFormats
control: Presentation
documentation: UG
---
# Work with PowerPoint presentation

## Cloning a PowerPoint presentation

Cloning a PowerPoint presentation creates a new copy of the PowerPoint presentation. The cloned copy is an independent object that indicates changes made in the cloned copy of the presentation do not affect the source PowerPoint presentation.

{% highlight c# %}
[C#]

//Opens a PowerPoint presentation file

IPresentation sourcePresentation = Presentation.Open(fileName);

//Clones the presentation

IPresentation clonedPresentation = sourcePresentation.Clone();

//Gets the first slide from the cloned PowerPoint presentation

ISlide firstSlide = clonedPresentation.Slides[0];

//Adds a textbox in a slide by specifying its position and size

IShape textShape = firstSlide.AddTextBox(100, 75, 756, 200);

//Adds a paragraph in the body of the textShape

IParagraph paragraph = textShape.TextBody.AddParagraph();

//Adds a textPart in the paragraph

ITextPart textPart = paragraph.AddTextPart("Essential Presentation");

//Saves the modified cloned PowerPoint presentation

clonedPresentation.Save("ClonedPresentation.pptx");



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Opens a PowerPoint presentation file

Dim sourcePresentation_1 As IPresentation = Presentation.Open(fileName)

'Clones the presentation

Dim clonedPresentation_1 As IPresentation = sourcePresentation_1.Clone()

'Gets the first slide from the cloned PowerPoint presentation

Dim firstSlide As ISlide = clonedPresentation_1.Slides(0)

'Adds a textbox in a slide by specifying its position and size

Dim textShape As IShape = firstSlide.AddTextBox(100, 75, 756, 200)

'Adds a paragraph in the body of the textShape

Dim paragraph As IParagraph = textShape.TextBody.AddParagraph()

'Adds a textPart in the paragraph

Dim textPart As ITextPart = paragraph.AddTextPart("Essential Presentation")

'Saves the modified cloned PowerPoint presentation

clonedPresentation_1.Save("ClonedPresentation.pptx")



{% endhighlight %}

## Print a PowerPoint presentation

You can print the presentation document by converting the PowerPoint Presentation slides to images. For more information about converting the PowerPoint presentation slides to images, see [Conversion](http://www.google.com/# ""). You can use the System.Drawing.Printing.[PrintDocument](https://msdn.microsoft.com/en-us/library/system.drawing.printing.printdocument(v=vs.110).aspx# "") class to print the converted images by the default printer or to any of the available printer with customized settings.

The following code example demonstrates how to convert the slides of a PowerPoint presentationto images.

{% highlight c# %}
[C#]

//Opens a PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Converts the slides to images

Image[] images = presentation.RenderAsImages(Syncfusion.Drawing.ImageType.Bitmap);

//Closes the PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Opens a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Converts the slides to images

Dim images As Image() = presentation_1.RenderAsImages(Syncfusion.Drawing. ImageType.Bitmap)

'Closes the PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

The following code example demonstrates how to print the converted images.

{% highlight c# %}
[C#]

//Initializes the start and page for printing

int startPageIndex = 1;

int endPageIndex = images.Length;

//Creates new PrintDialog instance.

System.Windows.Forms.PrintDialog printDialog = new System.Windows.Forms.PrintDialog();

//Sets new PrintDocument instance to print dialog.

printDialog.Document = new PrintDocument();

//Enables the print current page option.

printDialog.AllowCurrentPage = true;

//Enables the print selected pages option.

printDialog.AllowSomePages = true;

//Sets the start and end page index

printDialog.PrinterSettings.FromPage = 1;

printDialog.PrinterSettings.ToPage = images.Length;

//Opens the print dialog box.

if (printDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)

{

//Checks whether the selected page range is valid or not

if (printDialog.PrinterSettings.FromPage > 0 && printDialog.PrinterSettings.ToPage <= images.Length)

{

//Updates the start page of the document to print.

startPageIndex = printDialog.PrinterSettings.FromPage - 1;

//Updates the end page of the document to print.

endPageIndex = printDialog.PrinterSettings.ToPage;

//Hooks the PrintPage event to handle be drawing pages for printing.

printDialog.Document.PrintPage += new PrintPageEventHandler(PrintPageMethod);

//Prints the document.

printDialog.Document.Print();

}

}

private void PrintPageMethod (object sender, PrintPageEventArgs e)

{

//Gets the print start page width.

int currentPageWidth = images[startPageIndex].Width;

//Gets the print start page height.

int currentPageHeight = images[startPageIndex].Height;

//Gets the visible bounds width for print.

int visibleClipBoundsWidth = (int)e.Graphics.VisibleClipBounds.Width;

//Gets the visible bounds height for print.

int visibleClipBoundsHeight = (int)e.Graphics.VisibleClipBounds.Height;

//Checks whether the page layout is landscape or portrait.

if (currentPageWidth > currentPageHeight)

{

//Translates the position.

e.Graphics.TranslateTransform(0, visibleClipBoundsHeight);

//Rotates the object at 270 degrees

e.Graphics.RotateTransform(270.0f);

//Draws the current page image.

e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, currentPageWidth, currentPageHeight));

}

else

{

//Draws the current page image.

e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight));

}

//Disposes the current page image after drawing.

images[startPageIndex].Dispose();

//Increments the start page index.

startPageIndex++;

//Updates whether the document contains more pages to print or not.

if (startPageIndex < endPageIndex)

e.HasMorePages = true;

else

startPageIndex = 0;

}



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

Dim endPageIndex As Integer = images.Length

'Creates new PrintDialog instance.

Dim printDialog As New System.Windows.Forms. PrintDialog()

'Sets new PrintDocument instance to print dialog.

printDialog.Document = New PrintDocument()

'Enables the print current page option.

printDialog.AllowCurrentPage = True

'Enables the print selected pages option.

printDialog.AllowSomePages = True

'Sets the start and end page index

printDialog.PrinterSettings.FromPage = 1

printDialog.PrinterSettings.ToPage = images.Length

'Opens the print dialog box.

If printDialog.ShowDialog() = System.Windows.Forms.DialogResult.OK Then

'Checks whether the selected page range is valid or not.

If printDialog.PrinterSettings.FromPage > 0 AndAlso printDialog.PrinterSettings.ToPage <= images.Length Then

'Updates the start page of the document to print.

startPageIndex = printDialog.PrinterSettings.FromPage - 1

'Updates the end page of the document to print.

endPageIndex = printDialog.PrinterSettings.ToPage

'Hooks the PrintPage event to handle the drawing pages for printing.

printDialog.Document.PrintPage += New PrintPageEventHandler(PrintPageMethod)

'Prints the document.

printDialog.Document.Print()

End If

End If

Private Sub PrintPageMethod(sender As Object, e As PrintPageEventArgs)

'Gets the print start page width.

Dim currentPageWidth As Integer = images(startPageIndex).Width

'Gets the print start page height.

Dim currentPageHeight As Integer = images(startPageIndex).Height

'Gets the visible bounds width for print.

Dim visibleClipBoundsWidth As Integer = CInt(e.Graphics.VisibleClipBounds.Width)

'Gets the visible bounds height for print.

Dim visibleClipBoundsHeight As Integer = CInt(e.Graphics.VisibleClipBounds.Height)

'Checks whether the page layout is landscape or portrait.

If currentPageWidth > currentPageHeight Then

'Translates the position.

e.Graphics.TranslateTransform(0, visibleClipBoundsHeight)

'Rotates the object at 270 degrees

e.Graphics.RotateTransform(270.0F)

'Draws the current page image.

e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle (0, 0, currentPageWidth, currentPageHeight))

Else

'Draws the current page image.

e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle (0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight))

End If

'Disposes the current page image after drawing.

images(startPageIndex).Dispose()

'Increments the start page index.

startPageIndex += 1

'Updates whether the document contains more pages to print or not.

If startPageIndex < endPageIndex Then

e.HasMorePages = True

Else

startPageIndex = 0

End If

End Sub



{% endhighlight %}

## Work with PowerPoint presentation properties

Document properties, also known as metadata, are details about a file that describe or identify it. Document properties are classified into two categories. 

* **Built****-****in** **Document** **Properties** - that include details such as title, author name, subject, and keywords that identify the document's topic or contents.
* **Custom** **Document** **properties** - define the user-defined document properties.

**Built****-****in** **Document** **Properties**

You can access and modify the built in document properties of a PowerPoint presentation with Essential Presentation library. The Built-in document properties of a PowerPoint presentation is represented by **IBuiltInDocumentProperties** type.

**Accessing** **and** **Modifying** **Built****-****in** **Document** **Properties**

The following code example demonstrates how to access the existing built in document property.

{% highlight c# %}
[C#]

//Opens a PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Accessess the built-in document properties

Console.WriteLine("Title - {0}", presentation.BuiltInDocumentProperties.Title);

Console.WriteLine("Author - {0}", presentation.BuiltInDocumentProperties.Author);

//Closes the PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Opens a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Accessess the built-in document properties

Console.WriteLine("Title - {0}", presentation_1.BuiltInDocumentProperties.Title)

Console.WriteLine("Author - {0}", presentation_1.BuiltInDocumentProperties.Author)

'Closes the PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

The following code example demonstrates how to modify the existing built in document property

{% highlight c# %}
[C#]

//Opens a PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Modifies the Built-in document properties

presentation.BuiltInDocumentProperties.Category = "Sales reports";

presentation.BuiltInDocumentProperties.Company = "Northwind traders";

//Saves the modified PowerPoint presentation

presentation.Save("Output.pptx");

//Closes the modified PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Opens a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Modifies the Built-in document properties

presentation_1.BuiltInDocumentProperties.Category = "Sales reports"

presentation_1.BuiltInDocumentProperties.Company = "Northwind traders"

'Saves the modified PowerPoint presentation

presentation_1.Save("Output.pptx")

'Closes the modified PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

**Custom** **Document** **properties**

You can create and modify the custom document properties of a PowerPoint presentation with Essential Presentation library. The collection of custom document properties in a PowerPoint presentation is represented by **ICustomDocumentProperties** object. 

**Adding** **Custom** **Document** **properties**

The following code example demonstrates how to add new custom document property.

{% highlight c# %}
[C#]

//Creates a PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Adds custom document properties of various data type

presentation.CustomDocumentProperties.Add("PropertyA");

presentation.CustomDocumentProperties.Add("PropertyB");

//Saves the PowerPoint presentation            

presentation.Save("Output.pptx");

//Closes the PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Creates a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Create()

'Adds custom document properties of various data type

presentation_1.CustomDocumentProperties.Add("PropertyA")

presentation_1.CustomDocumentProperties.Add("PropertyB")

'Saves the PowerPoint presentation            

presentation_1.Save("Output.pptx")

'Closes the PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

**Accessing** **and** **Modifying** **Custom** **Document** **Properties**

The following code example demonstrates how to access and modify an existing custom document property:

{% highlight c# %}
[C#]

//Opens a PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Accessess an existing custom document property

IDocumentProperty property = presentation.CustomDocumentProperties["PropertyA"];

//Modifies the value of DocumentProperty

property.Value = "Hello world";

//Saves the PowerPoint presentation

presentation.Save("Output.pptx");

//Closes the PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Opens a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Accessess an existing custom document property

Dim [property] As IDocumentProperty = presentation_1.CustomDocumentProperties("PropertyA")

'Modifies the value of DocumentProperty

[property].Value = "Hello world"

'Saves the PowerPoint presentation

presentation_1.Save("Output.pptx")

'Closes the PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

