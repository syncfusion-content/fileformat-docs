---
title: Security
description: This section illustrate how to encrypt and protect the Word document
platform: FileFormat
control: DocIO
documentation: UG
---
# Security

You can encrypt a Word document with password to restrict unauthorized access. You can also control the types of changes you make to this document.

## Encrypting with password

The following code example shows how to encrypt the Word document with password.

{% highlight c# %}
C#

//Opens an input Word document

WordDocument document = new WordDocument(”Template.docx”);

//Encrypts the Word document with a password

document.EncryptDocument("password");

//Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Opens an input Word document

Dim document As New WordDocument("Template.docx")

'Encrypts the Word document with a password

document.EncryptDocument("password")

‘Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}



## Opening the encrypted Word document

The following code example shows how to open the encrypted Word document. 

{% highlight c# %}
C#

//Opens an encrypted Word document

WordDocument document = new WordDocument (”Template.docx”, "password");

//Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Opens an encrypted Word document

Dim document As New WordDocument("Template.docx", "password")

‘Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Protecting Word document from editing

You can restrict a Word document from editing either by providing a password or without password. 

The following are the types of protection:

1. AllowOnlyComments: You can add/modify only the comments in the Word document.

2. AllowOnlyFormFields: You can modify the form field values in the Word document.

3. AllowOnlyRevisions: You can accept or reject the revisions in the Word document.

4. AllowOnlyReading: You can only view the content in the Word document.

5. NoProtection: You can access/edit the Word document contents as normally.

The following code example shows how to restrict editing to modify only form fields in a Word document.



{% highlight c# %}
C#

//Opens a Word document

WordDocument document = new WordDocument(@"Template.docx");

//Sets the protection with password and it allows only to modify the form fields type

document.Protect(ProtectionType.AllowOnlyFormFields, "password"); 

//Saves the Word document

document.Save("Protection.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Opens a Word document

Dim document As New WordDocument("Template.docx")

'Sets the protection with password and it allows only to modify the form fields type

document.Protect(ProtectionType.AllowOnlyFormFields, "password")

'Saves the Word document

document.Save("Protection.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

