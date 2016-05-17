---
title: Encrypting and Decrypting the PowerPoint Presentation
description: Encrypting and Decrypting the PowerPoint Presentation; security in using Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Security

## Encrypting with password 

You can protect a PowerPoint Presentation by encrypting the document by using a password. This prevents unauthorized users to access or make changes in the Presentation. 

The following code example demonstrates how to encrypt a PowerPoint Presentation with password.

{% tabs %}

{% highlight c# %}

//Creates an instance for Presentation

IPresentation presentation = Presentation.Create();

//Adds slide to Presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds textbox to slide

IShape shape = slide.Shapes.AddTextBox(100, 30, 200, 300);

//Adds a paragraph with text content.

IParagraph paragraph = shape.TextBody.AddParagraph("Password Protected.");

//Protects the file with password

presentation.Encrypt("PASSWORD!@1#$");

//Saves the Presentation

presentation.Save("Sample.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates an instance for Presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds slide to Presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds textbox to slide

Dim shape As IShape = slide.Shapes.AddTextBox(100, 30, 200, 300)

'Adds a paragraph with text content.

Dim paragraph As IParagraph = shape.TextBody.AddParagraph("Password Protected.")

'Protects the file with password

presentationDocument.Encrypt("PASSWORD!@1#$")

'Saves the Presentation

presentationDocument.Save("Sample.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Decrypting the PowerPoint Presentation

Essential Presentation provides ability to remove the encryption from the PowerPoint Presentation. You can decrypt a PowerPoint Presentation by opening it with the password.

**Opening** **the** **Encrypted** **PowerPoint** **Presentation**

The following code example demonstrates opening the encrypted PowerPoint Presentation. 

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from file system and it can be decrypted by using the provided password.

IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$");

//Saves the Presentation

presentation.Save("Output.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system and it can be decrypted by using the provided password.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")

'Saves the Presentation

presentationDocument.Save("Output.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

**Removing** **the** **encryption** **from** **Presentation**

The following code example demonstrates removing the encryption from a PowerPoint Presentation. 

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from file system and it can be decrypted by using the provided password.

IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$");

//Decrypts the document

presentation.RemoveEncryption();

//Saves the presentation

presentation.Save("Output.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system and it can be decrypted by using the provided password.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")

'Decrypts the document

presentationDocument.RemoveEncryption()

'Saves the Presentation

presentationDocument.Save("Output.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

