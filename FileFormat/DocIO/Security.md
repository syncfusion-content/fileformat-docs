---
layout: Post
title: Security
description: This section illustrate how to encrypt and protect the Word document
platform: FileFormat
control: DocIO
documentation: UG
---
# Security

You can encrypt a Word document with password to restrict from unauthorized access. Also you can control what types of changes people can make to this document.

## Encrypting with password

The following code snippet shows how to encrypt the Word document with password.

{% highlight c# %}
C#

//Open an input Word document

WordDocument document = new WordDocument(”Template.docx”);

//Encrypt the Word document with a password

document.EncryptDocument("password");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Open an input Word document

Dim document As New WordDocument("Template.docx")

'Encrypt the Word document with a password

document.EncryptDocument("password")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}



## Opening the encrypted Word document

The following code snippets shows how to open the encrypted Word document. 

{% highlight c# %}
C#

//Open an encrypted Word document

WordDocument document = new WordDocument (”Template.docx”, "password");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Open an encrypted Word document

Dim document As New WordDocument("Template.docx", "password")

‘Save & close the Word document instance

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

The following code snippet shows how to restrict editing to modify only form fields in a Word document.



{% highlight c# %}
C#

//Open a Word document

WordDocument document = new WordDocument(@"Template.docx");

//Set the protection with password and it allow only modify the form fields type

document.Protect(ProtectionType.AllowOnlyFormFields, "password"); 

//Save the Word document

document.Save("Protection.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Open a Word document

Dim document As New WordDocument("Template.docx")

'Set the protection with password and it allow only modify the form fields type

document.Protect(ProtectionType.AllowOnlyFormFields, "password")

'Save the Word document

document.Save("Protection.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

