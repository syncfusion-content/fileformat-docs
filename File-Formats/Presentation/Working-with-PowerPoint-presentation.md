---
title: Working with PowerPoint presentation | Syncfusion
description: Working with PowerPoint presentation. Cloning the Presentation. Printing the Presentation. Essential Presentation use Points to add slide elements.
platform: file-formats
control: Presentation
documentation: UG
---
# Working with PowerPoint presentation

## Cloning a PowerPoint presentation

Cloning a PowerPoint presentation creates a new copy of the PowerPoint presentation and the changes made in the cloned copy of the presentation do not affect the source PowerPoint presentation.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Clones the Presentation
IPresentation clonedPresentation = pptxDoc.Clone();
String ContentType=null;
//Gets the first slide from the cloned PowerPoint presentation
ISlide firstSlide = clonedPresentation.Slides[0];
//Adds a textbox in a slide by specifying its position and size
IShape textShape = firstSlide.AddTextBox(100, 75, 756, 200);
//Adds a paragraph in the body of the textShape
IParagraph paragraph = textShape.TextBody.AddParagraph();
//Adds a textPart in the paragraph
ITextPart textPart = paragraph.AddTextPart("Essential Presentation");
//Save the PowerPoint Presentation to stream
FileStream outputStream = new FileStream(outputFileName, FileMode.Create);
clonedPresentation.SaveAs(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens a PowerPoint presentation
IPresentation sourcePresentation = Presentation.Open(fileName);
//Clones the Presentation
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a PowerPoint presentation
Dim sourcePresentation_1 As IPresentation = Presentation.Open(fileName)
'Clones the Presentation
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PowerPoint-Presentation/Clone-PowerPoint-presentation).

## Printing a PowerPoint presentation

You can print the Presentation document by converting the PowerPoint presentation slides to images. For more information about converting the PowerPoint presentation slides to images, see [Conversion](/file-formats/presentation/getting-started). You can use the System.Drawing.Printing.[PrintDocument](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.printing.printdocument?redirectedfrom=MSDN&view=dotnet-plat-ext-7.0) class to print the converted images by the default printer or to any of the available printer with customized settings.

The following code example demonstrates how to convert the slides of a PowerPoint presentation to images.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Converts the slides to images
Image[] images = pptxDoc.RenderAsImages(Syncfusion.Drawing.ImageType.Bitmap);
//Closes the PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Converts the slides to images
Dim images As Image() = pptxDoc.RenderAsImages(Syncfusion.Drawing. ImageType.Bitmap)
'Closes the PowerPoint presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

The following code example demonstrates how to print the converted images.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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
        //Draws the current page image.
        e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight));
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
        'Rotates the object at 270 degrees.
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PowerPoint-Presentation/Print-PowerPoint-presentation).

## Working with PowerPoint presentation properties

Document properties, also known as meta data, are details about a file that describe or identify it. Document properties are classified into two categories. 

* **Built****-****in** **Document** **Properties** - that include details such as title, author name, subject, and keywords that identify the document's topic or contents.
* **Custom** **Document** **properties** - define the user-defined document properties.

**Built****-****in** **Document** **Properties**

You can access and modify the built in document properties of a PowerPoint presentation with Essential Presentation library. The Built-in document properties of a PowerPoint presentation is represented by [IBuiltInDocumentProperties](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IBuiltInDocumentProperties.html) type.

**Accessing** **and** **Modifying** **Built****-****in** **Document** **Properties**

The following code example demonstrates how to access the existing built in document property.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Accesses the built-in document properties
Console.WriteLine("Title - {0}", pptxDoc.BuiltInDocumentProperties.Title);
Console.WriteLine("Author - {0}", pptxDoc.BuiltInDocumentProperties.Author);
//Closes the PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Accesses the built-in document properties
Console.WriteLine("Title - {0}", presentationDocument.BuiltInDocumentProperties.Title)
Console.WriteLine("Author - {0}", presentationDocument.BuiltInDocumentProperties.Author)
'Closes the PowerPoint presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PowerPoint-Presentation/Access-built-in-document-properties).

The following code example demonstrates how to modify the existing built in document property

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Modifies the Built-in document properties
pptxDoc.BuiltInDocumentProperties.Category = "Sales reports";
pptxDoc.BuiltInDocumentProperties.Company = "Northwind traders";
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Close the instance of PowerPoint Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Modifies the Built-in document properties
pptxDoc.BuiltInDocumentProperties.Category = "Sales reports";
pptxDoc.BuiltInDocumentProperties.Company = "Northwind traders";
//Saves the modified PowerPoint presentation
pptxDoc.Save("Output.pptx");
//Closes the modified PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Modifies the Built-in document properties
pptxDoc.BuiltInDocumentProperties.Category = "Sales reports"
pptxDoc.BuiltInDocumentProperties.Company = "Northwind traders"
'Saves the modified PowerPoint presentation
pptxDoc.Save("Output.pptx")
'Closes the modified PowerPoint presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PowerPoint-Presentation/Modify-built-in-document-properties).

## Custom Document properties

You can create and modify the custom document properties of a PowerPoint presentation with Essential Presentation library. The collection of custom document properties in a PowerPoint presentation is represented by [ICustomDocumentProperties](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ICustomDocumentProperties.html) object. 

### Adding Custom Document properties

The following code example demonstrates how to add new custom document property.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Adds custom document properties 
ICustomDocumentProperties documentProperty = pptxDoc.CustomDocumentProperties;
documentProperty.Add("PropertyA");
documentProperty["PropertyA"].Text = "@!123";
documentProperty.Add("PropertyB");
documentProperty["PropertyB"].Text = "B";
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Adds custom document properties 
ICustomDocumentProperties documentProperty = pptxDoc.CustomDocumentProperties;
documentProperty.Add("PropertyA");
documentProperty["PropertyA"].Text = "@!123";
documentProperty.Add("PropertyB");
documentProperty["PropertyB"].Text = "B";
//Saves the PowerPoint presentation
pptxDoc.Save("Output.pptx");
//Closes the PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds custom document properties
Dim documentProperty As ICustomDocumentProperties = pptxDoc.CustomDocumentProperties
documentProperty.Add("PropertyA")
documentProperty("PropertyA").Text = "@!123"
documentProperty.Add("PropertyB")
documentProperty("PropertyB").Text = "B"
'Saves the PowerPoint presentation
pptxDoc.Save("Output.pptx")
'Closes the PowerPoint presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PowerPoint-Presentation/Add-custom-document-properties).

### Accessing and Modifying Custom Document Properties

The following code example demonstrates how to access and modify an existing custom document property:

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Accesses an existing custom document property
IDocumentProperty property = pptxDoc.CustomDocumentProperties["PropertyA"];
//Modifies the value of DocumentProperty
property.Value = "Hello world";
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Accesses an existing custom document property
IDocumentProperty property = pptxDoc.CustomDocumentProperties["PropertyA"];
//Modifies the value of DocumentProperty
property.Value = "Hello world";
//Saves the PowerPoint presentation
pptxDoc.Save("Output.pptx");
//Closes the PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Accesses an existing custom document property
Dim [property] As IDocumentProperty = pptxDoc.CustomDocumentProperties("PropertyA")
'Modifies the value of DocumentProperty
[property].Value = "Hello world"
'Saves the PowerPoint presentation
pptxDoc.Save("Output.pptx")
'Closes the PowerPoint presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PowerPoint-Presentation/Modify-custom-document-properties).

## Marking a PowerPoint presentation as final

PowerPoint presentation can be made read-only to prevent the readers from making inadvertent changes to it. However, making presentation as final is not a security feature. Anyone can disable the final status and edit the presentation.

Below code snippet demonstrates how to create a final non – editable presentation,

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create an instance for PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Mark the presentation as final
pptxDoc.Final = true;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create an instance for PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Mark the presentation as final
pptxDoc.Final = true;
//Save the presentation
pptxDoc.Save("MarkAsFinal.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create an instance for PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Mark the presentation as final
pptxDoc.Final = True
'Save the presentation
pptxDoc.Save("MarkAsFinal.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PowerPoint-Presentation/Mark-as-final).

## First slide number

Change the first slide number of the PowerPoint presentation using the **FirstSlideNumber** API. 

The following code sample illustrates how to modify the first slide number in the PowerPoint presentation.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Open an existing PowerPoint Presentation.
using (FileStream inputStream = new FileStream("Data/Input.pptx", FileMode.Open))
{
    using (IPresentation pptxDoc = Presentation.Open(inputStream))
    {
        //Get the FirstSlideNumber of Presentation.
        int firstSlideNumber = pptxDoc.FirstSlideNumber;

        //Modify the value for the FirstSlideNumber.
        pptxDoc.FirstSlideNumber = 10;

        //Save the PowerPoint Presentation.
        using (FileStream outputStream = new FileStream("Result.pptx", FileMode.Create))
        {
            pptxDoc.Save(outputStream);
        }                       
    }
}

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

using (IPresentation pptxDoc = Presentation.Open("Data/Input.pptx"))
{
    //Get the FirstSlideNumber of Presentation.
    int firstSlideNumber = pptxDoc.FirstSlideNumber;

    //Modify the value for the FirstSlideNumber.
    pptxDoc.FirstSlideNumber = 10;

    //Save the PowerPoint Presentation.
    pptxDoc.Save("Result.pptx");                      
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using pptxDoc As IPresentation = Presentation.Open("Data/Input.pptx")
    'Get the FirstSlideNumber of Presentation.
    Dim firstSlideNumber As Integer = pptxDoc.FirstSlideNumber

    'Modify the value for the FirstSlideNumber.
    pptxDoc.FirstSlideNumber = 10

    'Save the PowerPoint Presentation.
    pptxDoc.Save("Result.pptx")
End Using

{% endhighlight %}
{% endtabs %}

N> The first slide number is the starting slide number of the presentation, and this API allows you to set the first slide number from 0 to 9999.

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PowerPoint-Presentation/First-slide-number/.NET).

## See Also
* [How to merge or combine multiple PowerPoint files](https://support.syncfusion.com/kb/article/7961/how-to-merge-or-combine-multiple-powerpoint-files-in-c-vb-net)
* [How to extract text from a PowerPoint presentation?](https://support.syncfusion.com/kb/article/7711/how-to-extract-text-from-a-powerpoint-presentation)