---
title: Working with Silverlight
description: This section explains how to load and save PDF document in Silverlight
platform: file-formats
control: PDF
documentation: UG
---
# Working with Silverlight 

In your Silverlight application, please add the required assemblies in order to use Essential PDF. [Refer here for assemblies required](/File-Formats/PDF/Assemblies-Required).

## Loading the document 

The following code example illustrates how to load the file by using URI in Silverlight.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Load the file as url

Uri uri = new Uri(@"\Resources\data\Sample.pdf", UriKind.Relative);

Stream docStream = ResourceManager.Load(uri);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create booklet with two sides

PdfDocument document = PdfBookletCreator.CreateBooklet(loadedDocument, new SizeF(1000, 700), true);

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

document.Save();

//close the documents

document.Close(true);

loadedDocument.Close(true);

public static class Extensions

{

public static void Save(this PdfDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

DefaultExt = ".pdf",

Filter = "Adobe PDF Files(*.pdf)|*.pdf",

FilterIndex = 1

};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream);

}

}

}

public static void Save(this PdfLoadedDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

DefaultExt = ".pdf",

Filter = "Adobe PDF Files(*.pdf)|*.pdf",

FilterIndex = 1

};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream);

}

}

}

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Load the file as url

Dim uri As New Uri("\Resources\data\Sample.pdf", UriKind.Relative)

Dim docStream As Stream = ResourceManager.Load(uri)

Dim loadedDocument As New PdfLoadedDocument(docStream)

'Create booklet with two sides

Dim document As PdfDocument = PdfBookletCreator.CreateBooklet(loadedDocument, New SizeF(1000, 700), True)

Dim stream As New MemoryStream()

'Save the document into memory stream

document.Save()

'close the documents

document.Close(True)

loadedDocument.Close(True)

Public Module Extensions

<System.Runtime.CompilerServices.Extension> _

Public Sub Save(ByVal document As PdfDocument)

Dim sfd As New SaveFileDialog() With {.DefaultExt = ".pdf", .Filter = "Adobe PDF Files(*.pdf)|*.pdf", .FilterIndex = 1}

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream)

End Using

End If

End Sub

<System.Runtime.CompilerServices.Extension> _

Public Sub Save(ByVal document As PdfLoadedDocument)

Dim sfd As New SaveFileDialog() With {.DefaultExt = ".pdf", .Filter = "Adobe PDF Files(*.pdf)|*.pdf", .FilterIndex = 1}

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream)

End Using

End If

End Sub

End Module

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to load the file by using stream in Silverlight.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Load the file as stream

Stream docStream = Assembly.GetExecutingAssembly().GetManifestResourceStream("sample.Resources.Data.sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create booklet with two sides

PdfDocument document = PdfBookletCreator.CreateBooklet(loadedDocument, new SizeF(1000, 700), true);

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

document.Save();

//close the documents

document.Close(true);

loadedDocument.Close(true);

public static class Extensions

{

public static void Save(this PdfDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

DefaultExt = ".pdf",

Filter = "Adobe PDF Files(*.pdf)|*.pdf",

FilterIndex = 1

};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream);

}

}

}

public static void Save(this PdfLoadedDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

DefaultExt = ".pdf",

Filter = "Adobe PDF Files(*.pdf)|*.pdf",

FilterIndex = 1

};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream);

}

}

}

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Load the file as stream

Dim docStream As Stream = System.Reflection.Assembly.GetExecutingAssembly().GetManifestResourceStream("sample.Resources.Data.sample.pdf")

Dim loadedDocument As New PdfLoadedDocument(docStream)

'Create booklet with two sides

Dim document As PdfDocument = PdfBookletCreator.CreateBooklet(loadedDocument, New SizeF(1000, 700), True)

Dim stream As New MemoryStream()

'Save the document into memory stream

document.Save()

'close the documents

document.Close(True)

loadedDocument.Close(True)

Public Module Extensions

<System.Runtime.CompilerServices.Extension> _

Public Sub Save(ByVal document As PdfDocument)

Dim sfd As New SaveFileDialog() With {.DefaultExt = ".pdf", .Filter = "Adobe PDF Files(*.pdf)|*.pdf", .FilterIndex = 1}

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream)

End Using

End If

End Sub

<System.Runtime.CompilerServices.Extension> _

Public Sub Save(ByVal document As PdfLoadedDocument)

Dim sfd As New SaveFileDialog() With {.DefaultExt = ".pdf", .Filter = "Adobe PDF Files(*.pdf)|*.pdf", .FilterIndex = 1}

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream)

End Using

End If

End Sub

End Module

{% endhighlight %}

{% endtabs %}

## Saving the document 

The following code example illustrates how to save the PDF document in Silverlight.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create Pdf graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a solid brush

PdfBrush brush = new PdfSolidBrush(Color.FromArgb(0, 0, 0, 0));

//Set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//Save the document

document.Save();

//Close the document

document.Close(true);

public static class Extensions

{

public static void Save(this PdfDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

DefaultExt = ".pdf",

Filter = "Adobe PDF Files(*.pdf)|*.pdf",

FilterIndex = 1

};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream);

}

}

}

public static void Save(this PdfLoadedDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

DefaultExt = ".pdf",

Filter = "Adobe PDF Files(*.pdf)|*.pdf",

FilterIndex = 1

};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream);

}

}

}

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}
VB:

'Create a new document.

Dim document As New PdfDocument()

'Add a page

Dim page As PdfPage = document.Pages.Add()

'Create Pdf graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush

Dim brush As PdfBrush = New PdfSolidBrush(Color.FromArgb(0, 0, 0, 0))

'Set the font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'Save the document

document.Save()

'Close the document

document.Close(True)

Public Module Extensions

<System.Runtime.CompilerServices.Extension> _

Public Sub Save(ByVal document As PdfDocument)

Dim sfd As New SaveFileDialog() With {.DefaultExt = ".pdf", .Filter = "Adobe PDF Files(*.pdf)|*.pdf", .FilterIndex = 1}

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream)

End Using

End If

End Sub

<System.Runtime.CompilerServices.Extension> _

Public Sub Save(ByVal document As PdfLoadedDocument)

Dim sfd As New SaveFileDialog() With {.DefaultExt = ".pdf", .Filter = "Adobe PDF Files(*.pdf)|*.pdf", .FilterIndex = 1}

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream)

End Using

End If

End Sub

End Module

{% endhighlight %}

{% endtabs %}