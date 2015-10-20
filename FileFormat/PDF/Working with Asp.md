# Working with Asp.net

# Save the document 

The following code snippet illustrates how to download the PDF document in browser after save the document.

{% highlight c# %}
C#:

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Draw the rectangle.

graphics.DrawRectangle(PdfPens.Black, new RectangleF(0, 0, 100, 100));

//download the document in browser.

document.Save("Output.pdf",HttpContext.Current.Response,HttpReadType.Save);

//Close the document.

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Draw the rectangle.

graphics.DrawRectangle(PdfPens.Black, New RectangleF(0, 0, 100, 100))

'download the document in browser.

document.Save("Output.pdf", HttpContext.Current.Response, HttpReadType.Save)

'Close the document.

document.Close(True)



{% endhighlight %}

The following code snippet illustrates how to open the PDF document in web browser after save the document.

{% highlight c# %}
C#:

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Draw the rectangle.

graphics.DrawRectangle(PdfPens.Black, new RectangleF(0, 0, 100, 100));

// Open the document in browser after save it

document.Save("Output.pdf", HttpContext.Current.Response, HttpReadType.Open);

//Close the document.

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Draw the rectangle.

graphics.DrawRectangle(PdfPens.Black, New RectangleF(0, 0, 100, 100))

' Open the document in browser after save it

document.Save("Output.pdf", HttpContext.Current.Response, HttpReadType.Open);

'Close the document.

document.Close(True)



{% endhighlight %}

