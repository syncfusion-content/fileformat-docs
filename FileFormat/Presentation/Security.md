---
layout: Post
title: Encrypting and Decrypting the PowerPoint Presentation
description: Encrypting and Decrypting the PowerPoint Presentation; security in using presentation
platform: FileFormats
control: Presentation
documentation: UG
---
# Security

## Encrypting with password 

You can protect a PowerPoint presentation by encrypting the document using a password. This prevents unauthorized users to access or make changes in the presentation. 

The following code snippet demonstrates how to encrypt a PowerPoint presentation with password.

{% highlight c# %}
[C#]

//Create an instance for presentation

IPresentation presentation = Presentation.Create();

//Add slide to presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Add textbox to slide

IShape shape = slide.Shapes.AddTextBox(100, 30, 200, 300);

//Add a paragraph with text content.

IParagraph paragraph = shape.TextBody.AddParagraph("Password Protected.");

//Protect the file with password

presentation.Encrypt("PASSWORD!@1#$");

//Save the presentation

presentation.Save("Sample.pptx");

//close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create an instance for presentation

Dim presentation_1 As IPresentation = Presentation.Create()

'Add slide to presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

'Add textbox to slide

Dim shape As IShape = slide.Shapes.AddTextBox(100, 30, 200, 300)

'Add a paragraph with text content.

Dim paragraph As IParagraph = shape.TextBody.AddParagraph("Password Protected.")

'Protect the file with password

presentation_1.Encrypt("PASSWORD!@1#$")

'Save the presentation

presentation_1.Save("Sample.pptx")

'close the presentation

presentation_1.Close()



{% endhighlight %}

## Decrypting the PowerPoint presentation

Essential Presentation provides ability to remove the encryption from the PowerPoint presentation. You can decrypt a PowerPoint presentation by opening it with the password~~.~~

**Opening** **the** **Encrypted** **PowerPoint** **presentation**

The below code snippet demonstrates opening the encrypted PowerPoint presentation. 

{% highlight c# %}
[C#]

//Open an existing presentation from file system, will be decrypted using the provided password.

IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$");

//Save the presentation

presentation.Save("Output.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation from file system, will be decrypted using the provided password.

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")

'Save the presentation

presentation_1.Save("Output.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

**Removing** **the** **encryption** **form** **presentation**

The below code snippet demonstrates removing the encryption from a PowerPoint presentation. 

{% highlight c# %}
[C#]

//Open an existing presentation from file system, will be decrypted using the provided password.

IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$");

//Decrypt the document

presentation.RemoveEncryption();

//Save the presentation

presentation.Save("Output.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation from file system, will be decrypted using the provided password.

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")

'Decrypt the document

presentation_1.RemoveEncryption()

'Save the presentation

presentation_1.Save("Output.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

