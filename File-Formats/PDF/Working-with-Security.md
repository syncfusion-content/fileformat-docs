---
title: Working with Security | Syncfusion
description: This sections explains how to protect the PDF document using encryption and set permission to the PDF document operations like printing, editing, copy content
platform: file-formats
control: PDF
documentation: UG
---
# Working with Security

Essential PDF allows you to [protect the PDF document](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library/protect-pdf) using encryption and set permission to the PDF document operations like printing, editing, copy content etc. using user password and owner password. Two types of encryption algorithms are available
1. Rivest Cipher 4 (RC4)
2. Advanced Encryption Standard (AES)

## Working with RC4 Encryption

You can encrypt PDF document by specifying the [Algorithm](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_Algorithm) property as **RC4** through [PdfEncryptionAlgorithm](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfEncryptionAlgorithm.html) Enum and [KeySize](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_KeySize) property as **40bit or 128bit** through [PdfEncryptionKeySize](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfEncryptionKeySize.html) Enum in [PdfSecurity](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html) class. The following code snippet illustrates how to encrypt the PDF document with the [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword).

User password: Prevents people from opening or viewing a PDF document. Once the User Password is set, to open the PDF document, Adobe Acrobat/Reader will prompt a user to enter this password. If it is not correct, the document will not open. By setting a PDF User password, you can secure the PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key128Bit;
security.Algorithm = PdfEncryptionAlgorithm.RC4;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with RC4 128bit", font, brush, new PointF(0, 40));

//Save and close the document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics
'Set the font.
Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)
'Set the brush.
Dim brush As PdfBrush = PdfBrushes.Black

'Document security.
Dim security As PdfSecurity = document.Security
'Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key128Bit
security.Algorithm = PdfEncryptionAlgorithm.RC4
security.UserPassword = "password"
'Draw the text.
graphics.DrawString("Encrypted with RC4 128bit", font, brush, New PointF(0, 40))

'Save and close the document.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key128Bit;
security.Algorithm = PdfEncryptionAlgorithm.RC4;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with RC4 128bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document.
document.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key128Bit;
security.Algorithm = PdfEncryptionAlgorithm.RC4;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with RC4 128bit", font, brush, new PointF(0, 40));

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key128Bit;
security.Algorithm = PdfEncryptionAlgorithm.RC4;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with RC4 128bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
//Save the stream into pdf file.
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Encrypt-PDF-with-RC4-using-user-password/).

N> While using both user and owner passwords, please specify different user and owner password while encrypting the PDF document for better security.

You can protect the PDF document from printing, editing, copying with the [OwnerPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_OwnerPassword) by using the following code snippet.

Owner password: Sets PDF document restrictions, which can include printing, content copying, editing, page extracting, commenting, and more. Once the owner password is set, Acrobat will require this password to make any changes to the PDF document. It further secures the PDF document to set a PDF Owner Password.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key128Bit;
security.Algorithm = PdfEncryptionAlgorithm.RC4;
security.OwnerPassword = "syncfusion";
//It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save and close the document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics
'Set the font.
Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)
'Set the brush.
Dim brush As PdfBrush = PdfBrushes.Black

'Document security.
Dim security As PdfSecurity = document.Security
'Specifies key size and encryption algorithm using 128 bit key in RC4 mode.
security.KeySize = PdfEncryptionKeySize.Key128Bit
security.Algorithm = PdfEncryptionAlgorithm.RC4
security.OwnerPassword = "syncfusion"
'It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print Or PdfPermissionsFlags.AccessibilityCopyContent
security.UserPassword = "password"
'Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, New PointF(0, 40))

'Save and close the document.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key128Bit;
security.Algorithm = PdfEncryptionAlgorithm.RC4;
security.OwnerPassword = "syncfusion";
//It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document.
document.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key128Bit;
security.Algorithm = PdfEncryptionAlgorithm.RC4;
security.OwnerPassword = "syncfusion";
//It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key128Bit;
security.Algorithm = PdfEncryptionAlgorithm.RC4;
security.OwnerPassword = "syncfusion";
//It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
//Save the stream into pdf file.
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Encrypt-PDF-with-RC4-using-owner-password/).

## Working with AES Encryption

You can encrypt PDF document by specifying the [Algorithm](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_Algorithm) property as **AES** through [PdfEncryptionAlgorithm](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfEncryptionAlgorithm.html) Enum and [KeySize](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_KeySize) property as **40bit or 128bit or 256bit** through [PdfEncryptionKeySize](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfEncryptionKeySize.html) Enum in [PdfSecurity](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html) class. The following code snippet illustrates how to encrypt the PDF document with the [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword).

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save and close the document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics
'Set the font.
Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)
'Set the brush.
Dim brush As PdfBrush = PdfBrushes.Black

'Document security.
Dim security As PdfSecurity = document.Security
'Specifies key size and encryption algorithm using 256 bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit
security.Algorithm = PdfEncryptionAlgorithm.AES
security.UserPassword = "password"
'Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, New PointF(0, 40))

'Save and close the document.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document.
document.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
//Save the stream into pdf file.
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Encrypt-PDF-with-AES-using-user-password/).

You can protect the PDF document from printing, editing, copying with the [OwnerPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_OwnerPassword) by using the following code snippet.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm using 256 bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
security.OwnerPassword = "syncfusion";
//It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save and close the document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics
'Set the font.
Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)
'Set the brush.
Dim brush As PdfBrush = PdfBrushes.Black

'Document security.
Dim security As PdfSecurity = document.Security
'Specifies key size and encryption algorithm using 256 bit key in RC4 mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit
security.Algorithm = PdfEncryptionAlgorithm.AES
security.OwnerPassword = "syncfusion"
'It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print Or PdfPermissionsFlags.AccessibilityCopyContent
security.UserPassword = "password"
'Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, New PointF(0, 40))

'Save and close the document.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm using 256 bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
security.OwnerPassword = "syncfusion";
//It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document.
document.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm using 256 bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
security.OwnerPassword = "syncfusion";
//It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm using 256 bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
security.OwnerPassword = "syncfusion";
//It allows printing and accessibility copy content.
security.Permissions = PdfPermissionsFlags.Print | PdfPermissionsFlags.AccessibilityCopyContent;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("This document is protected with owner password", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
//Save the stream into pdf file.
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Encrypt-PDF-with-AES-using-owner-password/).

## Encryption Options

Now, the Syncfusion PDF library has provided options to encrypt the PDF document as follows: 

* **Encrypt all contents** – All contents of the document will be encrypted.

*	**Encrypt all contents except Metadata** – All contents of the document will be encrypted except metadata.

*	**Encrypt only attachments**  – Encrypts only the file attachments, rest of the document will be left unencrypted.

The default value of EncryptionOptions is EncryptAllContents. You can choose any one of these options using the property [EncryptionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_EncryptionOptions) available in the class [PdfSecurity](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html).

### Encrypt all contents

You can encrypt all the PDF content by specifying the [EncryptionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_EncryptionOptions) property as **EncryptAllContents** option through [PdfEncryptionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfEncryptionOptions.html) Enum in [PdfSecurity](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html) class. The following code snippet explains how to encrypt all contents of the PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContents;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save and close the document
document.Save("Output.pdf");
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics
'Set the font.
Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)
'Set the brush.
Dim brush As PdfBrush = PdfBrushes.Black

'Document security.
Dim security As PdfSecurity = document.Security
'Specifies key size and encryption algorithm using 256 bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit
security.Algorithm = PdfEncryptionAlgorithm.AES
'Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContents;
security.UserPassword = "password"
'Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, New PointF(0, 40))        

'Save and close the document
document.Save("Output.pdf")
document.Close()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContents;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream. 
MemoryStream stream = new MemoryStream(); 
await document.SaveAsync(stream); 
//Close the document.
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContents;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));                        

//Save the document into stream.
MemoryStream stream = new MemoryStream(); 
document.Save(stream); 
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file. 
string contentType = "application/pdf"; 
//Define the file name. 
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContents;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with AES 256bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream(); 
document.Save(stream); 
//Closes the document. 
document.Close(true);
//Save the stream into pdf file. 
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Encrypt-all-contents-of-the-PDF-document/).

### Encrypt all contents except metadata

The Syncfusion Essential PDF library now supports encrypting the PDF document except the document information (metadata) by using the EncryptAllContentsExceptMetadata option. The document information will not be encrypted when using this EncryptionOption.

You can encrypt all contents except metadata by specifying the [EncryptionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_EncryptionOptions) property as **EncryptAllContentsExceptMetadata** option through [PdfEncryptionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfEncryptionOptions.html) Enum in [PdfSecurity](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html) class. The following code snippet explains how to encrypt all contents except metadata of the PDF document.

N> Encrypt all contents except metadata  is only supported in AES algorithms with 128bit, 256bit, and 256bit revision6 key size.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContentsExceptMetadata;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted all contents except metadata with AES 256bit", font, brush, new PointF(0, 40));

//Save and close the document.
document.Save("Output.pdf");
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics
'Set the font.
Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)
'Set the brush.
Dim brush As PdfBrush = PdfBrushes.Black

'Document security.
Dim security As PdfSecurity = document.Security
'Specifies key size and encryption algorithm using 256 bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit
security.Algorithm = PdfEncryptionAlgorithm.AES
'Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContentsExceptMetadata
security.UserPassword = "password"
'Draw the text.
graphics.DrawString("Encrypted all contents except metadata with AES 256bit", font, brush, New PointF(0, 40))        

'Save and close the document.
document.Save("Output.pdf"
document.Close()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContentsExceptMetadata;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted with all contents except metadata AES 256bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream(); 
await document.SaveAsync(stream); 
//Close the document.
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContentsExceptMetadata;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted all contents except metadata with AES 256bit", font, brush, new PointF(0, 40));                        

//Save the document into stream.
MemoryStream stream = new MemoryStream(); 
document.Save(stream);
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptAllContentsExceptMetadata;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted all contents except metadata with AES 256bit", font, brush, new PointF(0, 40));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream(); 
document.Save(stream); 
//Closes the document. 
document.Close(true);
//Save the stream into pdf file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Encrypt-all-contents-except-metadata-of-the-PDF/).

### Encrypt only attachments

You can encrypt only attachments present in the PDF document by specifying the [EncryptionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_EncryptionOptions) property as **EncryptOnlyAttachments** option through [PdfEncryptionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfEncryptionOptions.html) Enum in [PdfSecurity](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html) class.

The following code example explains how to create an encrypt only attachment document using the Syncfusion PDF Library. 

N> [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword) is mandatory for encrypt only attachments and it is only supported in AES algorithms with 128bit, 256bit, and 256bit revision6 key size.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted only attachments with AES 256bit", font, brush, new PointF(0, 40));

//Creates an attachment.
PdfAttachment attachment = new PdfAttachment("Input.txt");
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Add the attachment to the document.
document.Attachments.Add(attachment);

//Save and close the document.
document.Save("Output.pdf");
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.      
Dim document As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics
'Set the font.
Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 20.0F, PdfFontStyle.Bold)
'Set the brush.
Dim brush As PdfBrush = PdfBrushes.Black

'Document security.
Dim security As PdfSecurity = document.Security
'Specifies key size and encryption algorithm using 256 bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit
security.Algorithm = PdfEncryptionAlgorithm.AES
'Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments;
security.UserPassword = "password"
'Draw the text.
graphics.DrawString("Encrypted only attachments with AES 256bit", font, brush, New PointF(0, 40))

'Creates an attachment.
Dim attachment As New PdfAttachment("Input.txt")
attachment.ModificationDate = DateTime.Now
attachment.Description = "Input.txt" 
attachment.MimeType = "application/txt" 
'Add the attachment to the document.
document.Attachments.Add(attachment)

'Save and close the document.
document.Save("Output.pdf")
document.Close()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.           
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted only attachments with AES 256bit", font, brush, new PointF(0, 40));

//Creates an attachment.
PdfAttachment attachment = new PdfAttachment("Input.txt");
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Add the attachment to the document.
document.Attachments.Add(attachment);

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream(); 
await document.SaveAsync(stream); 
//Close the document.
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted only attachments with AES 256bit", font, brush, new PointF(0, 40));

//Creates an attachment.
PdfAttachment attachment = new PdfAttachment("Input.txt");
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Add the attachment to the document.
document.Attachments.Add(attachment);

//Save the document into stream.
MemoryStream stream = new MemoryStream(); 
document.Save(stream); 
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Set the font.
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 20f, PdfFontStyle.Bold);
//Set the brush.
PdfBrush brush = PdfBrushes.Black;

//Document security.
PdfSecurity security = document.Security;
//Specifies key size and encryption algorithm.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments;
security.UserPassword = "password";
//Draw the text.
graphics.DrawString("Encrypted only attachments with AES 256bit", font, brush, new PointF(0, 40));

//Creates an attachment.
PdfAttachment attachment = new PdfAttachment("Input.txt");
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Add the attachment to the document.
document.Attachments.Add(attachment);

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream(); 
document.Save(stream); 
//Closes the document.
document.Close(true);
//Save the stream into pdf file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Encrypt-only-attachment-in-the-PDF-document).

## Opening an encrypt-only-attachment document

The Syncfusion Essential PDF library now provides support for loading the encrypt-only-attachment PDF documents. To access the attachments in the existing PDF document, the [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword) is mandatory. 

You can provide the [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword) in following ways:
*	Load the PDF document with password. 
*	Provide password using the OnPdfPassword Event when accessing the attachments. 

It is possible to access all the contents except attachment when loading the PDF document without [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword). 

The following code example explains how to load an encrypt-only-attachment document with password in [PdfAttachment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachment.html) class using Syncfusion PDF Library. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document.
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf","password");
            
//Accessing the attachments.
foreach(PdfAttachment attachment in document.Attachments)
{
  FileStream stream = new FileStream(attachment.FileName, FileMode.Create);
  stream.Write(attachment.Data, 0, attachment.Data.Length);
  stream.Dispose();
}         

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the PDF document.
Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf", "password")
             
'Accessing the attachments.
For Each attachment As PdfAttachment In document.Attachments
  Dim stream = New FileStream(attachment.FileName, FileMode.Create)
  stream.Write(attachment.Data, 0, attachment.Data.Length)
  stream.Dispose
Next

'Close the document.
document.Close(true)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load the PDF document as stream.
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance.
PdfLoadedDocument document = new PdfLoadedDocument(pdfStream, "password");                       
             
//Accessing the attachments.
foreach(PdfAttachment  attachment in document.Attachments)
{
  FileStream stream= new FileStream(attachment.FileName, FileMode.Create);
  stream.Write(attachment.Data, 0, attachment.Data.Length);
  stream.Dispose();
}                                

//Close the document.
document.Close(true);             

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document.            
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read); 
PdfLoadedDocument document = new PdfLoadedDocument(docStream,"password");

//Accessing the attachments.
foreach(PdfAttachment  attachment in document.Attachments)
{
  FileStream  stream = new FileStream(attachment.FileName, FileMode.Create);
  stream.Write(attachment.Data, 0, attachment.Data.Length);
  stream.Dispose();
}                      

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the PDF document as stream.
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Creates an empty PDF loaded document instance.
PdfLoadedDocument document = new PdfLoadedDocument(docStream,"password");                 

//Accessing the attachments.
foreach(PdfAttachment  attachment in document.Attachments)
{
  FileStream  stream= new FileStream(attachment.FileName, FileMode.Create);
  stream.Write(attachment.Data, 0, attachment.Data.Length);
  stream.Dispose();
}                                 

//Close the document.
document.Close(true);	

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Load-an-encrypt-only-attachment-document).

## Set user password using event when accessing the attachment

The following code example illustrates how to provide the password when accessing attachments from encrypt-only-attachment document using the OnPdfPassword event.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document.
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");
document.OnPdfPassword += LDoc_OnPdfPassword;

//Accessing the attachments.
foreach(PdfAttachment attachment in document.Attachments)
{
  FileStream stream= new FileStream(attachment.FileName, FileMode.Create);
  stream.Write(attachment.Data, 0, attachment.Data.Length);
  stream.Dispose();
}                      

//Close the document.
document.Close(true);
	
//Provide the user password in event.
private static void LDoc_OnPdfPassword(object sender, OnPdfPasswordEventArgs args)
{
  args.UserPassword = "syncfusion";
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the PDF document.         
Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")
AddHandler document.OnPdfPassword, AddressOf LDoc_OnPdfPassword

'Accessing the attachments.
For Each attachment As PdfAttachment In document.Attachments
  Dim stream As FileStream = New FileStream(attachment.FileName, FileMode.Create)
  stream.Write(attachment.Data, 0, attachment.Data.Length)
  stream.Dispose()
Next

'Close the document.
document.Close(True)

'Provide the user password in event.
Private Sub LDoc_OnPdfPassword(ByVal sender As Object, ByVal args As OnPdfPasswordEventArgs)
  args.UserPassword = "password"
End Sub

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load the PDF document as stream.
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance.
PdfLoadedDocument document = new PdfLoadedDocument(pdfStream);
document.OnPdfPassword += LDoc_OnPdfPassword;

//Accessing the attachments.
foreach(PdfAttachment  attachment in document.Attachments)
{
  FileStream  stream = new FileStream(attachment.FileName, FileMode.Create);
  stream.Write(attachment.Data, 0, attachment.Data.Length);
  stream.Dispose();
}                      

//Close the document.
document.Close(true);
	
//Provide the user password in event.
private static void LDoc_OnPdfPassword(object sender, OnPdfPasswordEventArgs args)
{
  args.UserPassword = "syncfusion";
}

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read); 
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
document.OnPdfPassword += LDoc_OnPdfPassword;

//Accessing the attachments.
foreach(PdfAttachment  attachment in document.Attachments)
{
  FileStream  stream= new FileStream(attachment.FileName, FileMode.Create);
  stream.Write(attachment.Data, 0, attachment.Data.Length);
  stream.Dispose();
}                      

//Close the document.
document.Close(true);
	
//Provide the user password in event.
private static void LDoc_OnPdfPassword(object sender, OnPdfPasswordEventArgs args)
{
  args.UserPassword = "syncfusion";
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the PDF document as stream.
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Creates an empty PDF loaded document instance.
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
document.OnPdfPassword += LDoc_OnPdfPassword;

//Accessing the attachments.
foreach(PdfAttachment  attachment in document.Attachments)
{
  FileStream  stream= new FileStream(attachment.FileName, FileMode.Create);
  stream.Write(attachment.Data, 0, attachment.Data.Length);
  stream.Dispose();
}                      

//Close the document.
document.Close(true);

//Provide the user password in event.
private static void LDoc_OnPdfPassword(object sender, OnPdfPasswordEventArgs args)
{
  args.UserPassword = "syncfusion";
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Set-user-password-when-accessing-the-attachment).

## Protect attachments in existing PDF document

The Syncfusion PDF Library supports encrypting only the attachment files in an existing PDF document using the EncryptOnlyAttachments encryption option. Refer to the following code snippet.

N> [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword) is mandatory for this encryption option.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document.
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//PDF document security.
PdfSecurity security = document.Security; 
//Specifies encryption key size, algorithm and permission.
security.KeySize = PdfEncryptionKeySize.Key256Bit; 
security.Algorithm = PdfEncryptionAlgorithm.AES; 
//Provide user password.
security.UserPassword = "password";
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments;

//Save the document.
document.Save("Output.pdf");
//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the PDF document.        
Dim document As New PdfLoadedDocument("Input.pdf")

'PDF document security.
Dim security As PdfSecurity = document.Security
'Specifies encryption key size, algorithm and permission.
security.KeySize = PdfEncryptionKeySize.Key256Bit
security.Algorithm = PdfEncryptionAlgorithm.AES
'Provide user password.
security.UserPassword = "password"
'Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments

'Save the document.
document.Save("Output.pdf")
'Close the document
document.Close(true)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load the PDF document as stream.
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance.
PdfLoadedDocument document = new PdfLoadedDocument(pdfStream);       

//PDF document security.
PdfSecurity security = document.Security; 
//Specifies encryption key size, algorithm and permission.
security.KeySize = PdfEncryptionKeySize.Key256Bit; 
security.Algorithm = PdfEncryptionAlgorithm.AES; 
//Provide user password.
security.UserPassword = "password";
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments;

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream(); 
await document.SaveAsync(stream); 
//Close the document.
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read); 
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//PDF document security.
PdfSecurity security = document.Security; 
//Specifies encryption key size, algorithm and permission.
security.KeySize = PdfEncryptionKeySize.Key256Bit; 
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Provide user password.
security.UserPassword = "password";
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments;

//Save the document into stream.
MemoryStream stream = new MemoryStream(); 
document.Save(stream); 
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
 
//Load the PDF document as stream.
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Creates an empty PDF loaded document instance.
PdfLoadedDocument document = new PdfLoadedDocument(docStream);       

//PDF document security.
PdfSecurity security = document.Security; 
//Specifies encryption key size, algorithm and permission.
security.KeySize = PdfEncryptionKeySize.Key256Bit; 
security.Algorithm = PdfEncryptionAlgorithm.AES; 
//Provide user password.
security.UserPassword = "password";
//Specifies encryption option.
security.EncryptionOptions = PdfEncryptionOptions.EncryptOnlyAttachments;

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream(); 
document.Save(stream); 
//Close the document.
document.Close(true);
//Save the stream into pdf file.
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Protect-attachments-in-existing-PDF-document/).

## Protect an existing document

You can protect an existing PDF document with both [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword) and [OwnerPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_OwnerPassword) by using the following code snippet.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PDF document.
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//PDF document security.
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

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing document.
Dim document As New PdfLoadedDocument("Input.pdf")

'PDF Document Security.
Dim security As PdfSecurity = document.Security
'Specifies key size and encryption algorithm.
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

{% highlight c# tabtitle="UWP" %}

//Load the PDF document as stream.
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance.
PdfLoadedDocument document = new PdfLoadedDocument(pdfStream);

//PDF document security.
PdfSecurity security = document.Security;
//Specifies encryption key size, algorithm and permission. 
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Provide owner and user password.
security.OwnerPassword = "ownerPassword256";
security.UserPassword = "userPassword256";

//Save the document into stream.
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Close the document.
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples.
Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//PDF document security.
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
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream.
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//PDF document security.
PdfSecurity security = document.Security;
//Specifies encryption key size, algorithm and permission. 
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = PdfEncryptionAlgorithm.AES;
//Provide owner and user password.
security.OwnerPassword = "ownerPassword256";
security.UserPassword = "userPassword256";

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
//Save the stream into pdf file.
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Protect-an-existing-PDF-document/).

## Changing the password of the PDF document

You can change the [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword) of the existing PDF document by using following code snippet.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the password protected PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf","password");
//Change the user password.
loadedDocument.Security.UserPassword = "NewPassword";

//Save the password changed PDF document.
loadedDocument.Save("Output.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the password protected PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf", "password")
'Change the user password 
loadedDocument.Security.UserPassword = "NewPassword"

'Save the password changed PDF document
loadedDocument.Save("Output.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load the PDF document as stream
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(pdfStream,"password");
//Change the user password 
loadedDocument.Security.UserPassword = "NewPassword";

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
loadedDocument.Save(memoryStream);
//Close the document
loadedDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples
Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream, "password");
//Change the user password 
loadedDocument.Security.UserPassword = "NewPassword";

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream, "password");
//Change the user password 
loadedDocument.Security.UserPassword = "NewPassword";

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Change-password-of-the-PDF-document/).

## Change the permission of the PDF document

You can change the permission of the PDF document using the [Permissions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_Permissions). The following code snippet illustrates the same.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the password protected PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf", "syncfusion");
//Change the permission
loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.AssembleDocument;

//Save and Close the PDF document
loadedDocument.Save("Output.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the password protected PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf", "syncfusion")
'Change the permission
loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent Or PdfPermissionsFlags.AssembleDocument

'Save and Close the PDF document
loadedDocument.Save("Output.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load the PDF document as stream
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(pdfStream,"syncfusion");
//Change the permission
loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.AssembleDocument;

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
loadedDocument.Save(memoryStream);
//Close the document
loadedDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples
Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream, "syncfusion");
//Change the permission
loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.AssembleDocument;

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream,"syncfusion");
//Change the permission
loadedDocument.Security.Permissions = PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.AssembleDocument;

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
loadedDocument.Save(memoryStream);
//Close the document
loadedDocument.Close(true);
//Save the stream into pdf file
//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer pdf/xamarin section for respective code samples
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Change-the-permission-of-the-PDF-document/).

## Remove password from the user password PDF document

You can remove the [UserPassword](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSecurity.html#Syncfusion_Pdf_Security_PdfSecurity_UserPassword) from the encrypted PDF document by using the following code snippet.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the password protected PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf","password");
//Change the user password 
loadedDocument.Security.UserPassword = string.Empty;

//Save the password removed PDF document
loadedDocument.Save("Output.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the password protected PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf", "password")
'Change the user password 
loadedDocument.Security.UserPassword = String.Empty

'Save the password removed PDF document
loadedDocument.Save("Output.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load the PDF document as stream
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(pdfStream,"password");
//Change the user password 
loadedDocument.Security.UserPassword = string.Empty;

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
loadedDocument.Save(memoryStream);
//Close the document
loadedDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples
Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream, "password");
//Change the user password
loadedDocument.Security.UserPassword = string.Empty;

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream,"password");
//Change the user password 
loadedDocument.Security.UserPassword = string.Empty;

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
loadedDocument.Save(memoryStream);
//Close the document
loadedDocument.Close(true);
//Save the stream into pdf file
//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer pdf/xamarin section for respective code samples
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Remove-password-from-user-password-PDF-document/).

## How to determine whether the PDF document is password protected or not?

You can determine whether the existing PDF document is password protected or not by catching the [PdfDocumentException](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentException.html) as shown below.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% highlight vb.net tabtitle="VB.NET" %}

Try
	'Load the password protected PDF document without user password
	Dim loadedDocument As New PdfLoadedDocument("Output.pdf")
Catch exception As PdfDocumentException
	If exception.Message = "Can't open an encrypted document. The password is invalid." Then
		MessageBox.Show("Cannot open an encrypted document without password")
	End If
End Try

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% highlight c# tabtitle="ASP.NET Core" %}

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

{% highlight c# tabtitle="Xamarin" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Security/Determine-whether-the-PDF-is-protected-or-not/).

## How to determine whether the PDF document is protected by user or owner password

Essential PDF supports identifying the document whether it is protected by user or owner.

The following table shows the various combination for loading the secured document with user or owner password:

<table>
<thead>
<tr>
<th>
Document type</th><th>
Open with</th><th>
User password</th><th>
Owner password</th></tr>
</thead>
<tbody>
<tr>
<td>
PDF document secured with both the owner and user passwords.</td><td>
User password</td><td>
Returns user password</td><td>
Returns null</td></tr>
<tr>
<td>
PDF document secured with both the owner and user passwords.</td><td>
Owner password</td><td>
Returns user password <br/><br/><b>Note:</b> Returns null for AES 256 and AES 256 Revision 6 encryptions.</td><td>
Returns owner password</td></tr>
<tr>
<td>
PDF document secured with owner password alone.</td><td>
Owner password</td><td>
Returns null</td><td>
Returns owner password</td></tr>
<tr>
<td>
PDF document secured with user password alone.</td><td>
User Password</td><td>
Returns user password</td><td>
Returns owner Password (owner password is same as the user password; it allows full permission to users).</td></tr>
</tbody>
</table>
