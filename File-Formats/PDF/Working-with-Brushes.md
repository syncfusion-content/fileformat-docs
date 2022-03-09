---
title: Working with Brushes | Syncfusion
description: This section explains how to add shapes using different brushes
platform: file-formats
control: PDF
documentation: UG
---
# Working with Brushes

Brushes are used to draw the content on PDF document with specific color and style. Various brushes available in Syncfusion Essential PDF are,

1. Solid Brush
2. Gradient Brush
	* Linear Gradient Brush
	* Radial Gradient Brush
3. Tiling Brush

## Solid Brush

The solid brush is used to fill an object with solid color. Essential PDF supports drawing shapes on PDF document with solid brush using the [PdfSolidBrush](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfSolidBrush.html) class. The following code snippet illustrates this.

{% tabs %}
{% highlight c# tabtile="C#" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF solid brush
PdfSolidBrush brush = new PdfSolidBrush(Color.Red);

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document
doc.Save("SolidBrush.pdf");

//Close the instance of PdfDocument
doc.Close(true);
{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}
'Create a new PDF document
Dim doc As PdfDocument = New PdfDocument

'Add a page to the document
Dim page As PdfPage = doc.Pages.Add

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Create new PDF solid brush
Dim brush As PdfSolidBrush = New PdfSolidBrush(Color.Red)

'Draw ellipse on the page
graphics.DrawEllipse(brush, New RectangleF(0, 0, 200, 100))

'Save the PDF document
doc.Save("SolidBrush.pdf")

'Close the instance of PdfDocument
doc.Close(True)
{% endhighlight %}

{% highlight c# tabtile="UWP" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF solid brush
PdfSolidBrush brush = new PdfSolidBrush(Color.FromArgb(255, 255, 0, 0));

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the instance of PdfDocument
doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "SolidBrush.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF solid brush
PdfSolidBrush brush = new PdfSolidBrush(Color.Red);

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "SolidBrush.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF solid brush
PdfSolidBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Red);

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the instance of PdfDocument
doc.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SolidBrush.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SolidBrush.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Linear gradient brush

The gradient brush is used to fill an object with blend of two or more colors. Essential PDF supports drawing shapes on PDF document with linear gradient brush using [PdfLinearGradientBrush](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfLinearGradientBrush.html). The following code snippet illustrates this.

{% tabs %}
{% highlight c# tabtile="C#" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF linear gradient brush
PdfLinearGradientBrush brush = new PdfLinearGradientBrush(new PointF(0, 0), new PointF(200, 100), Color.Red, Color.Blue);
            
//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document
doc.Save("LinearGradientBrush.pdf");

//Close the instance of PdfDocument
doc.Close(true);
{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}
'Create a new PDF document
Dim doc As PdfDocument = New PdfDocument

'Add a page to the document
Dim page As PdfPage = doc.Pages.Add

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Create new PDF linear gradient brush
Dim brush As PdfLinearGradientBrush = New PdfLinearGradientBrush(New PointF(0, 0), New PointF(200, 100), Color.Red, Color.Blue)

'Draw ellipse on the page
graphics.DrawEllipse(brush, New RectangleF(0, 0, 200, 100))

'Save the PDF document
doc.Save("LinearGradientBrush.pdf")

'Close the instance of PdfDocument
doc.Close(True)
{% endhighlight %}

{% highlight c# tabtile="UWP" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF linear gradient brush
PdfLinearGradientBrush brush = new PdfLinearGradientBrush(new PointF(0, 0), new PointF(200, 100), Color.FromArgb(255, 255, 0, 0), Color.FromArgb(255, 0, 0, 255));

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the instance of PdfDocument
doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "LinearGradientBrush.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF linear gradient brush
PdfLinearGradientBrush brush = new PdfLinearGradientBrush(new PointF(0, 0), new PointF(200, 100), Color.Red, Color.Blue);

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "LinearGradientBrush.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF linear gradient brush
PdfLinearGradientBrush brush = new PdfLinearGradientBrush(new PointF(0, 0), new PointF(200, 100), Syncfusion.Drawing.Color.Red, Syncfusion.Drawing.Color.Blue);

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the instance of PdfDocument
doc.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
      Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("LinearGradientBrush.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("LinearGradientBrush.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Radial Gradient Brush

The gradient brush is used to fill an object with blend of two or more colors. You can draw any shape on PDF document with radial gradient brush using [PdfRadialGradientBrush](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfRadialGradientBrush.html). The following code snippet explains this.

{% tabs %}
{% highlight c# tabtile="C#" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF radial gradient brush
PdfRadialGradientBrush brush = new PdfRadialGradientBrush(new PointF(50, 50), 0, new PointF(50, 50), 50, Color.Red, Color.Blue);
            
//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 100, 100));

//Save the PDF document
doc.Save("RadialGradientBrush.pdf");

//Close the instance of PdfDocument
doc.Close(true);
{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}
'Create a new PDF document
Dim doc As PdfDocument = New PdfDocument

'Add a page to the document
Dim page As PdfPage = doc.Pages.Add

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Create new PDF radial gradient brush
Dim brush As PdfRadialGradientBrush = New PdfRadialGradientBrush(New PointF(50, 50), 0, New PointF(50, 50), 50, Color.Red, Color.Blue)

'Draw ellipse on the page
graphics.DrawEllipse(brush, New RectangleF(0, 0, 100, 100))

'Save the PDF document
doc.Save("RadialGradientBrush.pdf")

'Close the instance of PdfDocument
doc.Close(True)
{% endhighlight %}

{% highlight c# tabtile="UWP" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF radial gradient brush
PdfRadialGradientBrush brush = new PdfRadialGradientBrush(new PointF(50, 50), 0, new PointF(50, 50), 50, Color.FromArgb(255, 255, 0, 0), Color.FromArgb(255, 0, 0, 255));

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 100, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the instance of PdfDocument
doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "RadialGradientBrush.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF radial gradient brush
PdfRadialGradientBrush brush = new PdfRadialGradientBrush(new PointF(50, 50), 0, new PointF(50, 50), 50, Color.Red, Color.Blue);

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 100, 100));

//Save the PDF document stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "RadialGradientBrush.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF radial gradient brush
PdfRadialGradientBrush brush = new PdfRadialGradientBrush(new PointF(50, 50), 0, new PointF(50, 50), 50, Syncfusion.Drawing.Color.Red, Syncfusion.Drawing.Color.Blue);

//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 100, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the instance of PdfDocument
doc.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("RadialGradientBrush.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("RadialGradientBrush.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Tiling Brush

The tiling brush is used to draw an object repeatedly. You can draw any shape on PDF page with tiling brush using [PdfTilingBrush](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTilingBrush.html). The following code snippet explains this.

{% tabs %}
{% highlight c# tabtile="C#" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF tiling brush
PdfTilingBrush brush = new PdfTilingBrush(new RectangleF(0, 0, 11, 11));

//Draw ellipse inside the tile
brush.Graphics.DrawEllipse(PdfPens.Red, new RectangleF(0, 0, 10, 10));

//Draw ellipse
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document
doc.Save("TilingBrush.pdf");

//Close the instance of PdfDocument
doc.Close(true);
{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}
'Create a new PDF document
Dim doc As PdfDocument = New PdfDocument

'Add a page to the document
Dim page As PdfPage = doc.Pages.Add

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Create new PDF tiling brush
Dim brush As PdfTilingBrush = New PdfTilingBrush(New RectangleF(0, 0, 11, 11))

'Draw ellipse inside the tile
brush.Graphics.DrawEllipse(PdfPens.Red, New RectangleF(0, 0, 10, 10))

'Draw ellipse
graphics.DrawEllipse(brush, New RectangleF(0, 0, 200, 100))

'Save the PDF document
doc.Save("TilingBrush.pdf")

'Close the instance of PdfDocument
doc.Close(True)
{% endhighlight %}

{% highlight c# tabtile="UWP" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF tiling brush
PdfTilingBrush brush = new PdfTilingBrush(new RectangleF(0, 0, 11, 11));

//Draw ellipse inside the tile
brush.Graphics.DrawEllipse(PdfPens.Red, new RectangleF(0, 0, 10, 10));

//Draw ellipse
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document as stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the instance of PdfDocument
doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "TilingBrush.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF tiling brush
PdfTilingBrush brush = new PdfTilingBrush(new RectangleF(0, 0, 11, 11));

//Draw ellipse inside the tile
brush.Graphics.DrawEllipse(PdfPens.Red, new RectangleF(0, 0, 10, 10));

//Draw ellipse
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "TilingBrush.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();

//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create new PDF tiling brush
PdfTilingBrush brush = new PdfTilingBrush(new RectangleF(0, 0, 11, 11));

//Draw ellipse inside the tile
brush.Graphics.DrawEllipse(PdfPens.Red, new RectangleF(0, 0, 10, 10));

//Draw ellipse
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the instance of PdfDocument
doc.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("TilingBrush.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("TilingBrush.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}
