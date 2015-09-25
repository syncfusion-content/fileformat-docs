---
layout: Post
title: Working with PowerPoint presentation
description: Working with PowerPoint presentation; Cloning the presentation; printing the presentation
platform: FileFormats
control: Presentation
documentation: UG
---
# Working with PowerPoint presentation

## Cloning a PowerPoint presentation

Cloning a PowerPoint presentation creates a new copy of the PowerPoint presentation. The cloned copy will be an independent object, this means changes made in the cloned copy of the presentation will not affect the source PowerPoint presentation.

{% highlight c# %}
[C#]

//Open a PowerPoint presentation file

IPresentation sourcePresentation = Presentation.Open(fileName);

//Clone the presentation

IPresentation clonedPresentation = sourcePresentation.Clone();

//Get the first slide from the cloned PowerPoint presentation

ISlide firstSlide = clonedPresentation.Slides[0];

//Add a textbox in a slide by specifying its position & size

IShape textShape = firstSlide.AddTextBox(100, 75, 756, 200);

//Add a paragraph in the body of the textShape

IParagraph paragraph = textShape.TextBody.AddParagraph();

//Add a textPart in the paragraph

ITextPart textPart = paragraph.AddTextPart("Essential Presentation");

//Save the modified cloned PowerPoint presentation

clonedPresentation.Save("ClonedPresentation.pptx");



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open a PowerPoint presentation file

Dim sourcePresentation_1 As IPresentation = Presentation.Open(fileName)

'Clone the presentation

Dim clonedPresentation_1 As IPresentation = sourcePresentation_1.Clone()

'Get the first slide from the cloned PowerPoint presentation

Dim firstSlide As ISlide = clonedPresentation_1.Slides(0)

'Add a textbox in a slide by specifying its position & size

Dim textShape As IShape = firstSlide.AddTextBox(100, 75, 756, 200)

'Add a paragraph in the body of the textShape

Dim paragraph As IParagraph = textShape.TextBody.AddParagraph()

'Add a textPart in the paragraph

Dim textPart As ITextPart = paragraph.AddTextPart("Essential Presentation")

'Save the modified cloned PowerPoint presentation

clonedPresentation_1.Save("ClonedPresentation.pptx")



{% endhighlight %}

## Printing a PowerPoint presentation

You can print the presentation document by converting the PowerPoint Presentation slides to images. For more information about converting the PowerPoint presentation slides to images, see [Conversion](http://www.google.com/# ""). You can use the System.Drawing.Printing.[PrintDocument](https://msdn.microsoft.com/en-us/library/system.drawing.printing.printdocument(v=vs.110).aspx# "") class to print the converted images by the default printer or to any of the available printer with customized settings.

The below code snippet demonstrates converting the slides of a PowerPoint presentationto images.

{% highlight c# %}
[C#]

//Open a PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Convert the slides to images

Image[] images = presentation.RenderAsImages(Syncfusion.Drawing.ImageType.Bitmap);

//Close the PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Convert the slides to images

Dim images As Image() = presentation_1.RenderAsImages(Syncfusion.Drawing. ImageType.Bitmap)

'Close the PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

The below code snippet demonstrates printing the converted images.

{% highlight c# %}
[C#]

//Initialize the start and page for printing

int startPageIndex = 1;

int endPageIndex = images.Length;

//Create new PrintDialog instance.

System.Windows.Forms.PrintDialog printDialog = new System.Windows.Forms.PrintDialog();

//Set new PrintDocument instance to print dialog.

printDialog.Document = new PrintDocument();

//Enable the print current page option.

printDialog.AllowCurrentPage = true;

//Enable the print selected pages option.

printDialog.AllowSomePages = true;

//Set the start and end page index

printDialog.PrinterSettings.FromPage = 1;

printDialog.PrinterSettings.ToPage = images.Length;

//Open the print dialog box.

if (printDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)

{

//Checks if the selected page range is valid.

if (printDialog.PrinterSettings.FromPage > 0 && printDialog.PrinterSettings.ToPage <= images.Length)

{

//Update the start page of the document to print.

startPageIndex = printDialog.PrinterSettings.FromPage - 1;

//Update the end page of the document to print.

endPageIndex = printDialog.PrinterSettings.ToPage;

//Hook the PrintPage event to handle be drawing pages for printing.

printDialog.Document.PrintPage += new PrintPageEventHandler(PrintPageMethod);

//Print the document.

printDialog.Document.Print();

}

}

private void PrintPageMethod (object sender, PrintPageEventArgs e)

{

//Get the print start page width.

int currentPageWidth = images[startPageIndex].Width;

//Get the print start page height.

int currentPageHeight = images[startPageIndex].Height;

//Get the visible bounds width for print.

int visibleClipBoundsWidth = (int)e.Graphics.VisibleClipBounds.Width;

//Get the visible bounds height for print.

int visibleClipBoundsHeight = (int)e.Graphics.VisibleClipBounds.Height;

//Check if the page layout is landscape or portrait.

if (currentPageWidth > currentPageHeight)

{

//Translate the position.

e.Graphics.TranslateTransform(0, visibleClipBoundsHeight);

//Rotate the object at 270 degrees

e.Graphics.RotateTransform(270.0f);

//Draw the current page image.

e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, currentPageWidth, currentPageHeight));

}

else

{

//Draws the current page image.

e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight));

}

//Dispose the current page image after drawing.

images[startPageIndex].Dispose();

//Increment the start page index.

startPageIndex++;

//Update if the document contains some more pages to print.

if (startPageIndex < endPageIndex)

e.HasMorePages = true;

else

startPageIndex = 0;

}



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

Dim endPageIndex As Integer = images.Length

'Create new PrintDialog instance.

Dim printDialog As New System.Windows.Forms. PrintDialog()

'Set new PrintDocument instance to print dialog.

printDialog.Document = New PrintDocument()

'Enable the print current page option.

printDialog.AllowCurrentPage = True

'Enable the print selected pages option.

printDialog.AllowSomePages = True

'Set the start and end page index

printDialog.PrinterSettings.FromPage = 1

printDialog.PrinterSettings.ToPage = images.Length

'Open the print dialog box.

If printDialog.ShowDialog() = System.Windows.Forms.DialogResult.OK Then

'Checks if the selected page range is valid.

If printDialog.PrinterSettings.FromPage > 0 AndAlso printDialog.PrinterSettings.ToPage <= images.Length Then

'Update the start page of the document to print.

startPageIndex = printDialog.PrinterSettings.FromPage - 1

'Update the end page of the document to print.

endPageIndex = printDialog.PrinterSettings.ToPage

'Hook the PrintPage event to handle be drawing pages for printing.

printDialog.Document.PrintPage += New PrintPageEventHandler(PrintPageMethod)

'Print the document.

printDialog.Document.Print()

End If

End If

Private Sub PrintPageMethod(sender As Object, e As PrintPageEventArgs)

'Get the print start page width.

Dim currentPageWidth As Integer = images(startPageIndex).Width

'Get the print start page height.

Dim currentPageHeight As Integer = images(startPageIndex).Height

'Get the visible bounds width for print.

Dim visibleClipBoundsWidth As Integer = CInt(e.Graphics.VisibleClipBounds.Width)

'Get the visible bounds height for print.

Dim visibleClipBoundsHeight As Integer = CInt(e.Graphics.VisibleClipBounds.Height)

'Check if the page layout is landscape or portrait.

If currentPageWidth > currentPageHeight Then

'Translate the position.

e.Graphics.TranslateTransform(0, visibleClipBoundsHeight)

'Rotate the object at 270 degrees

e.Graphics.RotateTransform(270.0F)

'Draw the current page image.

e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle (0, 0, currentPageWidth, currentPageHeight))

Else

'Draws the current page image.

e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle (0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight))

End If

'Dispose the current page image after drawing.

images(startPageIndex).Dispose()

'Increment the start page index.

startPageIndex += 1

'Update if the document contains some more pages to print.

If startPageIndex < endPageIndex Then

e.HasMorePages = True

Else

startPageIndex = 0

End If

End Sub



{% endhighlight %}

## Working with PowerPoint presentation properties

Document properties, also known as metadata, are details about a file that describe or identify it. Document properties are classified into two categories. 

* **Built****-****in** **Document** **Properties** - which include details such as title, author name, subject, and keywords that identify the document's topic or contents.
* **Custom** **Document** **properties** - defines the user-defined document properties

**Built****-****in** **Document** **Properties**

You can access and modify the built in document properties of a PowerPoint presentation with Essential Presentation library. The Built-in document properties of a PowerPoint presentation is represented by **IBuiltInDocumentProperties** type.

**Accessing** **&** **Modifying** **Built****-****in** **Document** **Properties**

The below code snippet demonstrates accessing the existing built in document property.

{% highlight c# %}
[C#]

//Open a PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Access the built-in document properties

Console.WriteLine("Title - {0}", presentation.BuiltInDocumentProperties.Title);

Console.WriteLine("Author - {0}", presentation.BuiltInDocumentProperties.Author);

//Close the PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Access the built-in document properties

Console.WriteLine("Title - {0}", presentation_1.BuiltInDocumentProperties.Title)

Console.WriteLine("Author - {0}", presentation_1.BuiltInDocumentProperties.Author)

'Close the PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

The below code snippet demonstrates modifying the existing built in document property

{% highlight c# %}
[C#]

//Open a PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Modify the Built-in document properties

presentation.BuiltInDocumentProperties.Category = "Sales reports";

presentation.BuiltInDocumentProperties.Company = "Northwind traders";

//Save the modified PowerPoint presentation

presentation.Save("Output.pptx");

//Close the modified PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Modify the Built-in document properties

presentation_1.BuiltInDocumentProperties.Category = "Sales reports"

presentation_1.BuiltInDocumentProperties.Company = "Northwind traders"

'Save the modified PowerPoint presentation

presentation_1.Save("Output.pptx")

'Close the modified PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

**Custom** **Document** **properties**

You can create and modify the custom document properties of a PowerPoint presentation with Essential Presentation library. The collection of custom document properties in a PowerPoint presentation is represented by **ICustomDocumentProperties** object. 

**Adding** **Custom** **Document** **properties**

The below code snippet demonstrates adding a new custom document property

{% highlight c# %}
[C#]

//Create a PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Adding custom document properties of various data type

presentation.CustomDocumentProperties.Add("PropertyA");

presentation.CustomDocumentProperties.Add("PropertyB");

//Save the PowerPoint presentation            

presentation.Save("Output.pptx");

//Close the PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Create()

'Adding custom document properties of various data type

presentation_1.CustomDocumentProperties.Add("PropertyA")

presentation_1.CustomDocumentProperties.Add("PropertyB")

'Save the PowerPoint presentation            

presentation_1.Save("Output.pptx")

'Close the PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

**Accessing** **&** **Modifying** **Custom** **Document** **Properties**

The below code snippet demonstrates accessing and modifying an existing custom document property:

{% highlight c# %}
[C#]

//Open a PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Access an existing custom document property

IDocumentProperty property = presentation.CustomDocumentProperties["PropertyA"];

//Modify the value of DocumentProperty

property.Value = "Hello world";

//Save the PowerPoint presentation

presentation.Save("Output.pptx");

//Close the PowerPoint presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open a PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Access an existing custom document property

Dim [property] As IDocumentProperty = presentation_1.CustomDocumentProperties("PropertyA")

'Modify the value of DocumentProperty

[property].Value = "Hello world"

'Save the PowerPoint presentation

presentation_1.Save("Output.pptx")

'Close the PowerPoint presentation

presentation_1.Close()



{% endhighlight %}

