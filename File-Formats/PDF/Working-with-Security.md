---
title: Working with Security | Syncfusion
description: This sections explains how to protect the PDF document using encryption and set permission to the PDF document operations like printing, editing, copy content
platform: file-formats
control: PDF
documentation: UG
---
# Working with Security

Essential PDF allows you to protect the PDF document using encryption and set permission to the PDF document operations like printing, editing, copy content etc. using user password and owner password.  Two types of encryption algorithms are available

1. Rivest Cipher 4 (RC4)
2. Advanced Encryption Standard (AES)

## Working with RC4 Encryption


You can encrypt PDF document using RC4 algorithm with 40bit or 128bit key size. The following code snippet illustrates how to encrypt the PDF document with the user password.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm

security.KeySize = PdfEncryptionKeySize.Key128Bit;

security.Algorithm = PdfEncryptionAlgorithm.RC4;

security.UserPassword = "password";

graphics.DrawString("Encrypted with RC4 128bit", font, brush, new PointF(0, 40));

//Save and close the document.

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)

Dim brush As PdfBrush = PdfBrushes.Black

'Document security.

Dim security As PdfSecurity = document.Security

'Specifies key size and encryption algorithm

security.KeySize = PdfEncryptionKeySize.Key128Bit

security.Algorithm = PdfEncryptionAlgorithm.RC4

security.UserPassword = "password"

graphics.DrawString("Encrypted with RC4 128bit", font, brush, New PointF(0, 40))

'Save and close the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm

security.KeySize = PdfEncryptionKeySize.Key128Bit;

security.Algorithm = PdfEncryptionAlgorithm.RC4;

security.UserPassword = "password";

graphics.DrawString("Encrypted with RC4 128bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm

security.KeySize = PdfEncryptionKeySize.Key128Bit;

security.Algorithm = PdfEncryptionAlgorithm.RC4;

security.UserPassword = "password";

graphics.DrawString("Encrypted with RC4 128bit", font, brush, new PointF(0, 40));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm

security.KeySize = PdfEncryptionKeySize.Key128Bit;

security.Algorithm = PdfEncryptionAlgorithm.RC4;

security.UserPassword = "password";

graphics.DrawString("Encrypted with RC4 128bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}


{% endtabs %}

N> While using both user and owner passwords, please specify different user and owner password while encrypting the PDF document for better security.

You can protect the PDF document from printing, editing, copying with the owner password by using the following code snippet.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm.

security.KeySize = PdfEncryptionKeySize.Key128Bit;

security.Algorithm = PdfEncryptionAlgorithm.RC4;

security.OwnerPassword = "syncfusion";

//It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;

security.UserPassword = "password";

graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save and close the document.

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)

Dim brush As PdfBrush = PdfBrushes.Black

'Document security.

Dim security As PdfSecurity = document.Security

'Specifies key size and encryption algorithm using 128 bit key in RC4 mode.

security.KeySize = PdfEncryptionKeySize.Key128Bit

security.Algorithm = PdfEncryptionAlgorithm.RC4

security.OwnerPassword = "syncfusion"

'It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print Or PdfPermissionsFlags.AccessibilityCopyContent

security.UserPassword = "password"

graphics.DrawString("This document is protected with owner password", font, brush, New PointF(0, 40))

'Save and close the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm.

security.KeySize = PdfEncryptionKeySize.Key128Bit;

security.Algorithm = PdfEncryptionAlgorithm.RC4;

security.OwnerPassword = "syncfusion";

//It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;

security.UserPassword = "password";

graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm.

security.KeySize = PdfEncryptionKeySize.Key128Bit;

security.Algorithm = PdfEncryptionAlgorithm.RC4;

security.OwnerPassword = "syncfusion";

//It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;

security.UserPassword = "password";

graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));


//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm.

security.KeySize = PdfEncryptionKeySize.Key128Bit;

security.Algorithm = PdfEncryptionAlgorithm.RC4;

security.OwnerPassword = "syncfusion";

//It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;

security.UserPassword = "password";

graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Working with AES Encryption

You can encrypt PDF document using AES algorithm with 40bit or 128bit or 256bit key size. The following code snippet illustrates how to encrypt the PDF document with the user password.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm.

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

security.UserPassword = "password";

graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save and close the document.

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)

Dim brush As PdfBrush = PdfBrushes.Black

'Document security.

Dim security As PdfSecurity = document.Security

'Specifies key size and encryption algorithm using 256 bit key in AES mode.

security.KeySize = PdfEncryptionKeySize.Key256Bit

security.Algorithm = PdfEncryptionAlgorithm.AES

security.UserPassword = "password"

graphics.DrawString("Encrypted with AES 256bit", font, brush, New PointF(0, 40))

'Save and close the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm.

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

security.UserPassword = "password";

graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm.

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

security.UserPassword = "password";

graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm.

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

security.UserPassword = "password";

graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

You can protect the PDF document from printing, editing, copying with the owner password by using the following code snippet.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm using 256 bit key in AES mode.

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

security.OwnerPassword = "syncfusion";

//It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;

security.UserPassword = "password";

graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save and close the document.

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)

Dim brush As PdfBrush = PdfBrushes.Black

'Document security.

Dim security As PdfSecurity = document.Security

'Specifies key size and encryption algorithm using 256 bit key in RC4 mode.

security.KeySize = PdfEncryptionKeySize.Key256Bit

security.Algorithm = PdfEncryptionAlgorithm.AES

security.OwnerPassword = "syncfusion"

'It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print Or PdfPermissionsFlags.AccessibilityCopyContent

security.UserPassword = "password"

graphics.DrawString("This document is protected with owner password", font, brush, New PointF(0, 40))

'Save and close the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm using 256 bit key in AES mode.

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

security.OwnerPassword = "syncfusion";

//It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;

security.UserPassword = "password";

graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm using 256 bit key in AES mode.

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

security.OwnerPassword = "syncfusion";

//It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;

security.UserPassword = "password";

graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);

PdfBrush brush = PdfBrushes.Black;

//Document security.

PdfSecurity security = document.Security;

//Specifies key size and encryption algorithm using 256 bit key in AES mode.

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

security.OwnerPassword = "syncfusion";

//It allows printing and accessibility copy content

security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;

security.UserPassword = "password";

graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Protect an existing document

You can protect an existing PDF document with both owner and user password by using the following code snippet.

{% tabs %}

{% highlight c# %}

//Load the PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//PDF document security 

PdfSecurity security = document.Security;

//Specifies encryption key size, algorithm and permission. 

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

 //Provide owner and user password.

 security.OwnerPassword = "ownerPassword256";

 security.UserPassword = "userPassword256";

 //Save the document.

 document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load an existing document.

 Dim document As New PdfLoadedDocument("Input.pdf")

'Document Security

Dim security As PdfSecurity = document.Security

'Specifies key size and encryption algorithm

 security.KeySize = PdfEncryptionKeySize.Key128Bit

security.Algorithm = PdfEncryptionAlgorithm.RC4

'Provide owner and user password.

security.OwnerPassword = "ownerPassword256"

security.UserPassword = "userPassword256"

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Load the PDF document as stream

Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");

//Creates an empty PDF loaded document instance

PdfLoadedDocument document = new PdfLoadedDocument(pdfStream);

//PDF document security 

PdfSecurity security = document.Security;

//Specifies encryption key size, algorithm and permission. 

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

//Provide owner and user password.

security.OwnerPassword = "ownerPassword256";

security.UserPassword = "userPassword256";

MemoryStream memoryStream = new MemoryStream();

//Save the document.

document.Save(memoryStream);

//Close the documents.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples.

Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//PDF document security 

PdfSecurity security = document.Security;

//Specifies encryption key size, algorithm and permission. 

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

//Provide owner and user password.

security.OwnerPassword = "ownerPassword256";

security.UserPassword = "userPassword256";

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//PDF document security 

PdfSecurity security = document.Security;

//Specifies encryption key size, algorithm and permission. 

security.KeySize = PdfEncryptionKeySize.Key256Bit;

security.Algorithm = PdfEncryptionAlgorithm.AES;

//Provide owner and user password.

security.OwnerPassword = "ownerPassword256";

security.UserPassword = "userPassword256";

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Changing the password of the PDF document

You can change the user password of the existing PDF document by using following code snippet.

{% tabs %}

{% highlight c# %}

//Load the password protected PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf","password");

//Change the user password 

loadedDocument.Security.UserPassword = "NewPassword";

//Save the password changed PDF document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load the password protected PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf", "password")

'Change the user password 

loadedDocument.Security.UserPassword = "NewPassword"

'Save the password changed PDF document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Load the PDF document as stream

Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(pdfStream,"password");

//Change the user password 

loadedDocument.Security.UserPassword = "NewPassword";

MemoryStream memoryStream = new MemoryStream();

//Save the document.

loadedDocument.Save(memoryStream);

//Close the documents.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples.

Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream, "password");

//Change the user password 

loadedDocument.Security.UserPassword = "NewPassword";

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the documents.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream, "password");

//Change the user password 

loadedDocument.Security.UserPassword = "NewPassword";

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Closes the document

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Change the permission of the PDF document

You can change the permission of the PDF document using the owner password. The following code snippet illustrates the same.

{% tabs %}

{% highlight c# %}

//Load the password protected PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf", "syncfusion");

//Change the permission

loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.AssembleDocument;

//Save the PDF document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load the password protected PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf", "syncfusion")

'Change the permission

loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent Or PdfPermissionsFlags.AssembleDocument

'Save the PDF document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Load the PDF document as stream

Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(pdfStream,"syncfusion");

//Change the permission

loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.AssembleDocument;

MemoryStream memoryStream = new MemoryStream();

//Save the document.

loadedDocument.Save(memoryStream);

//Close the documents.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples.

Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream, "syncfusion");

//Change the permission

loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.AssembleDocument;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the documents.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream,"syncfusion");

//Change the permission

loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.AssembleDocument;

//document.Attachments.RemoveAt(1);

//Save the document into stream.

MemoryStream memoryStream = new MemoryStream();

loadedDocument.Save(memoryStream);

//Close the documents.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer pdf/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

## Remove password from the user password PDF document

You can remove the user password from the encrypted PDF document by using the following code snippet.

{% tabs %}

{% highlight c# %}

//Load the password protected PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf","password");

//Change the user password 

loadedDocument.Security.UserPassword = string.Empty;

//Save the password removed PDF document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load the password protected PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf", "password")

'Change the user password 

loadedDocument.Security.UserPassword = String.Empty

'Save the password removed PDF document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Load the PDF document as stream

Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(pdfStream,"password");

//Change the user password 

loadedDocument.Security.UserPassword = string.Empty;

MemoryStream memoryStream = new MemoryStream();

//Save the document.

loadedDocument.Save(memoryStream);

//Close the documents.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples.

Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream, "password");

//Change the user password 

loadedDocument.Security.UserPassword = string.Empty;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the documents.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream,"password");

//Change the user password 

loadedDocument.Security.UserPassword = string.Empty;

//Save the document into stream.

MemoryStream memoryStream = new MemoryStream();

loadedDocument.Save(memoryStream);

//Close the documents.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer pdf/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

## How to determine whether the PDF document is password protected or not?

You can determine whether the existing PDF document is password protected or not by catching the PdfDocumentException as shown below.

{% tabs %}

{% highlight c# %}

try
{
	//Load the password protected PDF document without user password
	PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Output.pdf");
}
catch (PdfDocumentException exception)
{
	if (exception.Message == "Can't open an encrypted document. The password is invalid.")
	{
		MessageBox.Show("Cannot open an encrypted document without password");
	}
}

{% endhighlight %}

{% highlight vb.net %}

Try
	'Load the password protected PDF document without user password
	Dim loadedDocument As New PdfLoadedDocument("Output.pdf")
Catch exception As PdfDocumentException
	If exception.Message = "Can't open an encrypted document. The password is invalid." Then
		MessageBox.Show("Cannot open an encrypted document without password")
	End If
End Try

{% endhighlight %}

{% highlight UWP %}

try
{
    //Load the PDF document as stream

    Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Output.pdf");

    //Creates an empty PDF loaded document instance

    PdfLoadedDocument loadedDocument = new PdfLoadedDocument(pdfStream);

}

catch (PdfDocumentException exception)
{
    
}

{% endhighlight %}

{% highlight ASP.NET Core %}

try

{
    //Load the PDF document

    FileStream docStream = new FileStream("Output.pdf", FileMode.Open, FileAccess.Read);

    PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

}

catch (PdfDocumentException exception)
{
    
}

{% endhighlight %}

{% highlight Xamarin %}

try
{
    //Load the file as stream

    Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Output.pdf");

    PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
}

catch (PdfDocumentException exception)
{
   
}


{% endhighlight %}

{% endtabs %}

## How to determine whether the PDF document is signed by user or owner password?

Essential PDF supports identifying the secured document signed by user or owner.

The following table shows the various combination for loading the signed document with user or owner password:

<table>
<thead>
<tr>
<th>
Document type</th><th>
Open with</th><th>
User password</th><th>
Owner password</th><th>
</thead>
<tbody>
<tr>
<td>
PDF document secured with both the owner and user passwords.</td><td>
User password</td><td>
Returns user password</td><td>
Returns null</td><td>

<tr>
<td>
PDF document secured with both the owner and user passwords.</td><td>
Owner password</td><td>
Returns user password <br/><br/><b>Note:<b/> Returns null for AES 256 and AES 256 Revision 6 encryptions.</td><td>
Returns owner password</td><td>

<tr>
<td>
PDF document secured with owner password alone.</td><td>
Owner password</td><td>
Returns null</td><td>
Returns owner password</td><td>

<tr>
<td>
PDF document secured with user password alone.</td><td>
User Password</td><td>
Returns user password</td><td>
Returns owner Password (owner password is same as the user password; it allows full permission to users).</td><td>

</tbody>
</table>
