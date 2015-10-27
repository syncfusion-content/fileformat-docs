---
title: Working with Security
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

//It allows priting and accessibility copy content

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

{% endtabs %}
