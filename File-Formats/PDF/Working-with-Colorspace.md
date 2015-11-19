---
title: Working with Color Spaces
description: This section explains how to create a PDF document with the specified color space
platform: file-formats
control: PDF
documentation: UG
---
# Working with Color Spaces

Essential PDF allows you to set the color spaces in the following different ways.

* Document Color Space
* Graphics Color Space

## Working with color space in document 


You can set the color space by using Color Space property in PDF document.

It supports the following types

* Device color Spaces
* CIE-based Color Spaces
* ICC-based Color Spaces

## Device Color Space


Device color space simply describes the range of colors that a camera can see, a printer can print, or a monitor can display. These color spaces depend upon the device where it is displayed. It contains the following types.

* DeviceGray
* DeviceRGB
* DeviceCMYK

##  CIE-based Color Spaces

CIE-based color space in the PDF document is classified as, 

* CalGray
* CalRGB
* Lab

The following code example illustrates how to draw a rectangle with **CalGray** brush in new PDF document.
{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

//Saves the document.

pdfDocument.Save("Output.pdf");

//closes the document

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim pdfDocument As New PdfDocument()

'Adds a page to the PDF document

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Acquires graphics of the page.

Dim graphics As PdfGraphics = pdfPage.Graphics

'Creates CalGray color space.

Dim calGrayColorSpace As New PdfCalGrayColorSpace()

'Updates color values.

calGrayColorSpace.Gamma = 0.7

calGrayColorSpace.WhitePoint = New Double() {0.2, 1, 0.8}

Dim calGrayColorSpace1 As New PdfCalGrayColor(calGrayColorSpace)

calGrayColorSpace1.Gray = 0.1

Dim brush As PdfBrush = New PdfSolidBrush(calGrayColorSpace1)

Dim bounds As New RectangleF(0, 0, 300, 300)

'Draws rectangle using the PdfBrush

graphics.DrawRectangle(brush, bounds)

'Saves the document.

pdfDocument.Save("Output.pdf")

'closes the document

pdfDocument.Close(True)



{% endhighlight %}
{% endtabs %}

The following code example illustrates how to draw a rectangle with **CalGray** brush in existing PDF document.
{% tabs %}
{% highlight c# %}


//Loads the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

//Saves the modified document.

loadedDocument.Save("Output.pdf");

//Closes the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Loads the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Loads the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Acquires graphics of the page.

Dim graphics As PdfGraphics = loadedPage.Graphics

'Creates CalGray color space.

Dim calGrayColorSpace As New PdfCalGrayColorSpace()

'Updates color values.

calGrayColorSpace.Gamma = 0.7

calGrayColorSpace.WhitePoint = New Double() {0.2, 1, 0.8}

Dim calGrayColorSpace1 As New PdfCalGrayColor(calGrayColorSpace)

calGrayColorSpace1.Gray = 0.1

Dim brush As PdfBrush = New PdfSolidBrush(calGrayColorSpace1)

Dim bounds As New RectangleF(0, 0, 300, 300)

'Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds)

'Saves the modified document.

loadedDocument.Save("Output.pdf")

'closes the document

loadedDocument.Close(True)





{% endhighlight %}
{% endtabs %}

## ICC-based Color Spaces

To create color for brush/pen to render shape or text in the PDF document, you can use ICC based color spaces.

It contains the following types:

* Special color spaces –Pantone colors
* Indexed
* Separation

The following code example illustrates how to set the indexed ICC color space in new PDF document.

{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

FileStream fs = new FileStream(@"input.icc", FileMode.Open, FileAccess.Read);

byte[] profileData = new byte[fs.Length];

fs.Read(profileData, 0, profileData.Length);

fs.Close();

//Instantiates ICC color space.

PdfICCColorSpace IccBasedCS = new PdfICCColorSpace();

IccBasedCS.ProfileData = profileData;

IccBasedCS.AlternateColorSpace = calRgbCS;

IccBasedCS.ColorComponents = 3;

IccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(IccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

//Saves the document.

pdfDocument.Save("Output.pdf");

//Closes the document

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim pdfDocument As New PdfDocument()

'Adds a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Acquires graphics of the page.

Dim graphics As PdfGraphics = pdfPage.Graphics

'Creates ICCBased color space.

Dim calRgbCS As New PdfCalRGBColorSpace()

calRgbCS.Gamma = New Double() {7.6, 5.1, 8.5}

calRgbCS.Matrix = New Double() {1, 0, 0, 0, 1, 0, 0, 0, 1}

calRgbCS.WhitePoint = New Double() {0.7, 1, 0.8}

'Reads the ICC profile.

Dim fs As New FileStream("input.icc", FileMode.Open, FileAccess.Read)

Dim profileData(fs.Length - 1) As Byte

fs.Read(profileData, 0, profileData.Length)

fs.Close()

'Instantiates ICC color space.

Dim IccBasedCS As New PdfICCColorSpace()

IccBasedCS.ProfileData = profileData

IccBasedCS.AlternateColorSpace = calRgbCS

IccBasedCS.ColorComponents = 3

IccBasedCS.Range = New Double() {0.0, 1.0, 0.0, 1.0, 0.0, 1.0}

Dim red As New PdfICCColor(IccBasedCS)

red.ColorComponents = New Double() {1, 0, 1}

Dim brush As PdfBrush = New PdfSolidBrush(red)

Dim bounds As New RectangleF(0, 0, 300, 300)

'Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds)

'Saves the document.

pdfDocument.Save("Output.pdf")

'Closes the document

pdfDocument.Close(True)



{% endhighlight %}
{% endtabs %}

The following code example illustrates how to set the indexed ICC color space in existing PDF document.

{% tabs %}
{% highlight c# %}


//Loads the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

FileStream fs = new FileStream(@"input.icc", FileMode.Open, FileAccess.Read);

byte[] profileData = new byte[fs.Length];

fs.Read(profileData, 0, profileData.Length);

fs.Close();

//Instantiates ICC color space.

PdfICCColorSpace IccBasedCS = new PdfICCColorSpace();

IccBasedCS.ProfileData = profileData;

IccBasedCS.AlternateColorSpace = calRgbCS;

IccBasedCS.ColorComponents = 3;

IccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(IccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

//Saves the document.

loadedDocument.Save("Output.pdf");

//Closes the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Loads the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Loads the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Acquires graphics of the page.

Dim graphics As PdfGraphics = loadedPage.Graphics

'Creates CalGray color space.

Dim calGrayColorSpace As New PdfCalGrayColorSpace()

'Updates color values.

calGrayColorSpace.Gamma = 0.7

calGrayColorSpace.WhitePoint = New Double() {0.2, 1, 0.8}

Dim calGrayColorSpace1 As New PdfCalGrayColor(calGrayColorSpace)

calGrayColorSpace1.Gray = 0.1

Dim brush As PdfBrush = New PdfSolidBrush(calGrayColorSpace1)

Dim bounds As New RectangleF(0, 0, 300, 300)

'Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds)

'Saves the document.

loadedDocument.Save("Output.pdf")

'Closes the document

loadedDocument.Close(True)





{% endhighlight %}
{% endtabs %}

## Pantone colors

The following code example illustrates how to draw the graphics elements by using pantone colors in new PDF document.

{% tabs %}
{% highlight c# %}
          

// Creates a new document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

// Creates exponential interpolation function

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numArray = new float[4];

numArray[0] = 0.38f;

numArray[1] = 0.88f;

function.C1 = numArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorspace = new PdfSeparationColorSpace();

colorspace.TintTransform = function;

colorspace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorspace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

page.Graphics.DrawRectangle(pen, bounds);

//Saves the document

document.Save("SeparationColor.pdf");

//Closes the document

document.Close(true);





{% endhighlight %}

{% highlight vb.net %}

' Creates a new document

Dim docuemnt As PdfDocument = New PdfDocument()

' Creates a page

Dim page As PdfPage = docuemnt.Pages.Add()

' Creates exponential interpolation function 

Dim [function] As PdfExponentialInterpolationFunction = New PdfExponentialInterpolationFunction(True)

Dim numArray() As Single = New Single(4) {}

numArray(0) = 0.38F

numArray(1) = 0.88F

[function].C1 = numArray

' Creates SeparationColorSpace

Dim colorspace As PdfSeparationColorSpace = New PdfSeparationColorSpace()

colorspace.TintTransform = [function]

colorspace.Colorant = "PANTONE Orange 021 C"

Dim color As PdfSeparationColor = New PdfSeparationColor(colorspace)

color.Tint = 0.7

Dim bounds As RectangleF = New RectangleF(20, 70, 200, 100)

Dim pen As PdfPen = New PdfPen(color)

'Draws the rectangle

page.Graphics.DrawRectangle(pen, bounds)

'Saves the document

docuemnt.Save("SeparationColor.pdf")

'Closes the document

docuemnt.Close(True)



{% endhighlight %}
{% endtabs %}

The following code example illustrates how to draw the graphics elements by using pantone colors in existing PDF document.

{% tabs %}
{% highlight c# %}


//Loads the document.

PdfLoadedDocument loadeddocument = new PdfLoadedDocument(fileName);

PdfLoadedPage loadedPage = loadeddocument.Pages[0] as PdfLoadedPage;

// Creates exponential interpolation function 

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numArray = new float[4];

numArray[0] = 0.38f;

numArray[1] = 0.88f;

function.C1 = numArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorspace = new PdfSeparationColorSpace();

colorspace.TintTransform = function;

colorspace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorspace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

loadedPage.Graphics.DrawRectangle(pen, bounds);

//Saves the document

loadeddocument.Save("SeparationColor.pdf");

//Closes the document

loadeddocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Loads the document.

Dim loadeddocument As New PdfLoadedDocument(fileName)

Dim loadedPage As PdfLoadedPage = TryCast(loadeddocument.Pages(0), PdfLoadedPage)

' Creates exponential interpolation function

Dim [function] As PdfExponentialInterpolationFunction = New PdfExponentialInterpolationFunction(True)

Dim numArray() As Single = New Single(3) {}

numArray(0) = 0.38F

numArray(1) = 0.88F

[function].C1 = numArray

' Creates SeparationColorSpace

Dim colorspace As PdfSeparationColorSpace = New PdfSeparationColorSpace()

colorspace.TintTransform = [function]

colorspace.Colorant = "PANTONE Orange 021 C"

Dim color As PdfSeparationColor = New PdfSeparationColor(colorspace)

color.Tint = 0.7

Dim bounds As RectangleF = New RectangleF(20, 70, 200, 100)

Dim pen As PdfPen = New PdfPen(color)

'Draws the rectangle

loadedPage.Graphics.DrawRectangle(pen, bounds)

'Saves the document

loadeddocument.Save("SeparationColor.pdf")

'Closes the document

loadeddocument.Close(True)



{% endhighlight %}
{% endtabs %}

## Working with color space in graphics

You can set the color spaces to the particular object in the PDF document by using the ColorSpace property in PdfGraphics class.

The following code illustrates how to use the color spaces in particular objects in new PDF document.
{% tabs %}
{% highlight c# %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

PdfPen pen = new PdfPen(Color.Red);

PdfBrush brush = new PdfSolidBrush(Color.Blue);

RectangleF rectangle = new RectangleF(0, 0, 100, 100);

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Save();

//GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale;

graphics.DrawRectangle(pen, brush, rectangle);

//CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK;

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Restore();

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

//Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle);

//Saves the document.

pdfDocument.Save("Output.pdf");

//Closes the document

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim pdfDocument As New PdfDocument()

'Adds a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Acquires graphics of the page.

Dim graphics As PdfGraphics = pdfPage.Graphics

Dim pen As New PdfPen(Color.Red)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Blue)

Dim rectangle As New RectangleF(0, 0, 100, 100)

'Default color space.

graphics.DrawRectangle(pen, brush, rectangle)

graphics.Save()

'GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale

graphics.DrawRectangle(pen, brush, rectangle)

'CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK

graphics.DrawRectangle(pen, brush, rectangle)

graphics.Restore()

'Default color space.

graphics.DrawRectangle(pen, brush, rectangle)

'Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle)

'Saves the document.

pdfDocument.Save("Output.pdf")

'Closes the document

pdfDocument.Close(True)



{% endhighlight %}
{% endtabs %}

The following code illustrates how to use the color spaces in particular objects in existing PDF document.
{% tabs %}
{% highlight c# %}


//Loads the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

PdfPen pen = new PdfPen(Color.Red);

PdfBrush brush = new PdfSolidBrush(Color.Blue);

RectangleF rectangle = new RectangleF(0, 0, 100, 100);

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Save();

//GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale;

graphics.DrawRectangle(pen, brush, rectangle);

//CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK;

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Restore();

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

//Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle);

//Saves the document.

loadedDocument.Save("Output.pdf");

//Closes the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Loads the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Loads the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Acquires graphics of the page.

Dim graphics As PdfGraphics = loadedPage.Graphics

Dim pen As New PdfPen(Color.Red)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Blue)

Dim rectangle As New RectangleF(0, 0, 100, 100)

'Default color space.

graphics.DrawRectangle(pen, brush, rectangle)

graphics.Save()

'GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale

graphics.DrawRectangle(pen, brush, rectangle)

'CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK

graphics.DrawRectangle(pen, brush, rectangle)

graphics.Restore()

'Default color space.

graphics.DrawRectangle(pen, brush, rectangle)

'Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle)

'Saves the document.

loadedDocument.Save("Output.pdf")

'Closes the document

loadedDocument.Close(True)



{% endhighlight %}
{% endtabs %}
