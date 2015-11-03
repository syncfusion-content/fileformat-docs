---
title: Encrypting and Decrypting the PowerPoint Presentation
description: Encrypting and Decrypting the PowerPoint Presentation; security in using presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Security

## Encrypting with password 

You can protect a PowerPoint presentation by encrypting the document by using a password. This prevents unauthorized users to access or make changes in the presentation. 

The following code example demonstrates how to encrypt a PowerPoint presentation with password.

{% tabs %}

{% highlight c# %}

//Creates an instance for presentation

IPresentation presentation = Presentation.Create();

//Adds slide to presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds textbox to slide

IShape shape = slide.Shapes.AddTextBox(100, 30, 200, 300);

//Adds a paragraph with text content.

IParagraph paragraph = shape.TextBody.AddParagraph("Password Protected.");

//Protects the file with password

presentation.Encrypt("PASSWORD!@1#$");

//Saves the presentation

presentation.Save("Sample.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates an instance for presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds slide to presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds textbox to slide

Dim shape As IShape = slide.Shapes.AddTextBox(100, 30, 200, 300)

'Adds a paragraph with text content.

Dim paragraph As IParagraph = shape.TextBody.AddParagraph("Password Protected.")

'Protects the file with password

presentationDocument.Encrypt("PASSWORD!@1#$")

'Saves the presentation

presentationDocument.Save("Sample.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Decrypting the PowerPoint presentation

Essential Presentation provides ability to remove the encryption from the PowerPoint presentation. You can decrypt a PowerPoint presentation by opening it with the password.

**Opening** **the** **Encrypted** **PowerPoint** **presentation**

The following code example demonstrates opening the encrypted PowerPoint presentation. 

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from file system and it can be decrypted by using the provided password.

IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$");

//Saves the presentation

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation from file system and it can be decrypted by using the provided password.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")

'Saves the presentation

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

**Removing** **the** **encryption** **from** **presentation**

The following code example demonstrates removing the encryption from a PowerPoint presentation. 

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from file system and it can be decrypted by using the provided password.

IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$");

//Decrypts the document

presentation.RemoveEncryption();

//Saves the presentation

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation from file system and it can be decrypted by using the provided password.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")

'Decrypts the document

presentationDocument.RemoveEncryption()

'Saves the presentation

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

