---
title: Print Word documents | DocIO | Syncfusion
description: This section illustrates how to print a Word document using the Syncfusion Word library and the .NET Framework Class.
platform: file-formats
control: DocIO
documentation: UG
---
# Print Word documents

You can print a Word document by utilizing DocIO’s capability to convert the document into images and .NET framework’s [PrintDocument](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.printing.printdocument?view=dotnet-plat-ext-7.0&viewFallbackFrom=net-5.0) class

Initially you have to render the pages as images as shown below

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens the Word document
WordDocument document = new WordDocument((string)this.textBox.Tag);
//Renders the Word document as image
Image[] images = document.RenderAsImages(ImageType.Metafile);
//Closes the Word Document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens the Word document
Dim document As New WordDocument(DirectCast(Me.textBox.Tag, String))
'Renders the Word document as image
Dim images As Image() = document.RenderAsImages(ImageType.Metafile)
'Closes the Word Document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO supports Word to Image conversion in Windows forms, WPF, ASP.NET and ASP.NET MVC platforms only.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//DocIO supports Word to Image conversion in Windows forms, WPF, ASP.NET and ASP.NET MVC platforms only.
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//DocIO supports Word to Image conversion in Windows forms, WPF, ASP.NET and ASP.NET MVC platforms only.
{% endhighlight %}

{% endtabs %}  

You can specify the printer settings and page settings through the [PrintDocument](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.printing.printdocument?view=dotnet-plat-ext-7.0&viewFallbackFrom=net-5.0) class. The [PrintDocument.PrintPage](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.printing.printdocument.printpage?view=dotnet-plat-ext-7.0&viewFallbackFrom=net-5.0) event should be handled to layout the document for printing. 

The following code example demonstrates how to print the Word document pages that have been rendered as an image:

{% tabs %}

{% highlight c# tabtitle="C#" %}
int endPageIndex = images.Length;
//Creates new PrintDialog instance
System.Windows.Forms.PrintDialog printDialog = new System.Windows.Forms.PrintDialog();
//Sets new PrintDocument instance to print dialog
printDialog.Document = new PrintDocument();
//Enables the print current page option
printDialog.AllowCurrentPage = true;
//Enables the print selected pages option
printDialog.AllowSomePages = true;
//Sets the start and end page index
printDialog.PrinterSettings.FromPage = 1;
printDialog.PrinterSettings.ToPage = images.Length;
//Opens the print dialog box
if (printDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)
{
    //Checks whether the selected page range is valid
    if (printDialog.PrinterSettings.FromPage > 0 && printDialog.PrinterSettings.ToPage <= images.Length)
    {
        //Updates the start page of the document to print
        startPageIndex = printDialog.PrinterSettings.FromPage - 1;
        //Updates the end page of the document to print
        endPageIndex = printDialog.PrinterSettings.ToPage;
        //Hooks the PrintPage event to handle the drawing pages for printing
        printDialog.Document.PrintPage += new PrintPageEventHandler(PrintPageMethod);
        //Print the document
        printDialog.Document.Print();
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim endPageIndex As Integer = images.Length
'Creates new PrintDialog instance
Dim printDialog As New System.Windows.Forms.PrintDialog()
'Sets new PrintDocument instance to print dialog
printDialog.Document = New PrintDocument()
'Enables the print current page option
printDialog.AllowCurrentPage = True
'Enables the print selected pages option
printDialog.AllowSomePages = True
'Sets the start and end page index
printDialog.PrinterSettings.FromPage = 1
printDialog.PrinterSettings.ToPage = images.Length
'Opens the print dialog box
If printDialog.ShowDialog() = System.Windows.Forms.DialogResult.OK Then
    'Checks whether the selected page range is valid or not
    If printDialog.PrinterSettings.FromPage > 0 AndAlso printDialog.PrinterSettings.ToPage <= images.Length Then
        'Updates the start page of the document to print
        startPageIndex = printDialog.PrinterSettings.FromPage - 1
        'Updates the end page of the document to print
        endPageIndex = printDialog.PrinterSettings.ToPage
        'Hooks the PrintPage event to handle the drawing pages for printing
        printDialog.Document.PrintPage += New PrintPageEventHandler(PrintPageMethod)
        'Prints the document
        printDialog.Document.Print()
    End If
End If
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO supports Word to Image conversion in Windows forms, WPF, ASP.NET and ASP.NET MVC platforms only.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//DocIO supports Word to Image conversion in Windows forms, WPF, ASP.NET and ASP.NET MVC platforms only.
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//DocIO supports Word to Image conversion in Windows forms, WPF, ASP.NET and ASP.NET MVC platforms only.
{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods for the above code.

{% tabs %} 
{% highlight c# tabtitle="C#" %}
private void PrintPageMethod(object sender, PrintPageEventArgs e)
{
    //Gets the print start page width
    int currentPageWidth = images[startPageIndex].Width;
    //Gets the print start page height
    int currentPageHeight = images[startPageIndex].Height;
    //Gets the visible bounds width for print
    int visibleClipBoundsWidth = (int)e.Graphics.VisibleClipBounds.Width;
    //Gets the visible bounds height for print
    int visibleClipBoundsHeight = (int)e.Graphics.VisibleClipBounds.Height;
    //Checks whether the page layout is landscape or portrait
    if (currentPageWidth > currentPageHeight)
    {
        //Translates the position
        e.Graphics.TranslateTransform(0, visibleClipBoundsHeight);
        //Rotates the object at 270 degrees
        e.Graphics.RotateTransform(270.0f);
        //Draws the current page image
        e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, currentPageWidth, currentPageHeight));
    }
    else
    {
        //Draws the current page image
        e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight));
    }
    //Disposes the current page image after drawing
    images[startPageIndex].Dispose();
    //Increments the start page index
    startPageIndex++;
    //Updates whether the document contains some more pages to print
    if (startPageIndex < endPageIndex)
        e.HasMorePages = true;
    else
        startPageIndex = 0;
}
{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET" %}
Private Sub PrintPageMethod(sender As Object, e As PrintPageEventArgs)
'Gets the print start page width
Dim currentPageWidth As Integer = images(startPageIndex).Width
'Gets the print start page height
Dim currentPageHeight As Integer = images(startPageIndex).Height
'Gets the visible bounds width for print
Dim visibleClipBoundsWidth As Integer = CInt(e.Graphics.VisibleClipBounds.Width)
'Gets the visible bounds height for print
Dim visibleClipBoundsHeight As Integer = CInt(e.Graphics.VisibleClipBounds.Height)
'Checks whether the page layout is landscape or portrait
If currentPageWidth > currentPageHeight Then
    'Translates the position
    e.Graphics.TranslateTransform(0, visibleClipBoundsHeight)
    'Rotates the object at 270 degrees
    e.Graphics.RotateTransform(270.0F)
    'Draws the current page image
    e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle(0, 0, currentPageWidth, currentPageHeight))
Else
    'Draws the current page image
    e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle(0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight))
End If
'Disposes the current page image after drawing
images(startPageIndex).Dispose()
'Increments the start page index
startPageIndex += 1
'Updates whether the document contains some more pages to print
If startPageIndex<endPageIndex Then
    e.HasMorePages = True
Else
    startPageIndex = 0
End If
End Sub
{% endhighlight %}
{% highlight c# tabtitle="UWP" %}
//DocIO supports Word to Image conversion in Windows forms, WPF, ASP.NET and ASP.NET MVC platforms only.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//DocIO supports Word to Image conversion in Windows forms, WPF, ASP.NET and ASP.NET MVC platforms only.
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//DocIO supports Word to Image conversion in Windows forms, WPF, ASP.NET and ASP.NET MVC platforms only.
{% endhighlight %}
{% endtabs %}   

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Print-Word-document).

## See Also

* [How to do silent printing to print the Word document by rendering document pages as Image using Essential DocIO](https://www.syncfusion.com/kb/4887/how-to-do-silent-printing-to-print-the-word-document-by-rendering-document-pages-as-image)