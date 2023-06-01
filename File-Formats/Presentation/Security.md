---
title: Encrypting & Decrypting the PowerPoint Presentation | Syncfusion
description: This section explains on Encrypting, Decrypting and providing protection for the PowerPoint Presentation.
platform: file-formats
control: Presentation
documentation: UG
---
# Security in Presentation

## Encrypting with password 

You can protect a PowerPoint Presentation by encrypting the document by using a password. This prevents unauthorized users to access or make changes in the Presentation. 

The following code example demonstrates how to encrypt a PowerPoint Presentation with password.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
using (IPresentation presentation = Presentation.Create())
{
    //Adds slide to Presentation.
    ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);
    //Adds textbox to slide.
    IShape shape = slide.Shapes.AddTextBox(100, 30, 200, 300);
    //Adds a paragraph with text content.
    IParagraph paragraph = shape.TextBody.AddParagraph("Password Protected.");
    //Protects the file with password.
    presentation.Encrypt("PASSWORD!@1#$");
    //Save the PowerPoint Presentation as stream.
    using (FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create))
    {
        presentation.Save(outputStream);
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates an instance for Presentation.
using (IPresentation presentation = Presentation.Create())
{
    //Adds slide to Presentation.
    ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);
    //Adds textbox to slide.
    IShape shape = slide.Shapes.AddTextBox(100, 30, 200, 300);
    //Adds a paragraph with text content.
    IParagraph paragraph = shape.TextBody.AddParagraph("Password Protected.");
    //Protects the file with password.
    presentation.Encrypt("PASSWORD!@1#$");
    //Saves the Presentation.
    presentation.Save("Sample.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates an instance for Presentation.
Using presentationDocument As IPresentation = Presentation.Create()
    'Adds slide to Presentation.
    Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)
    'Adds textbox to slide.
    Dim shape As IShape = slide.Shapes.AddTextBox(100, 30, 200, 300)
    'Adds a paragraph with text content.
    Dim paragraph As IParagraph = shape.TextBody.AddParagraph("Password Protected.")
    'Protects the file with password.
    presentationDocument.Encrypt("PASSWORD!@1#$")
    'Saves the Presentation.
    presentationDocument.Save("Sample.pptx")
End Using
{% endhighlight %}

{% endtabs %}

## Decrypting the PowerPoint Presentation

Essential Presentation provides ability to remove the encryption from the PowerPoint Presentation. You can decrypt a PowerPoint Presentation by opening it with the password.

**Opening** **the** **Encrypted** **PowerPoint** **Presentation**

The following code example demonstrates opening the encrypted PowerPoint Presentation. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens an existing Presentation from file system and it can be decrypted by using the provided password.
using (FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open))
{
    using (IPresentation presentation = Presentation.Open(inputStream, "PASSWORD!@1#$"))
    {
        //Save the PowerPoint Presentation as stream.
        using (FileStream outputStream = new FileStream("Output.pptx", FileMode.Create))
        {
            presentation.Save(outputStream);
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens an existing Presentation from file system and it can be decrypted by using the provided password.
using (IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$"))
{
    //Saves the Presentation.
    presentation.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens an existing Presentation from file system and it can be decrypted by using the provided password.
Using presentationDocument As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")
    'Saves the Presentation
    presentationDocument.Save("Output.pptx")
End Using
{% endhighlight %}

{% endtabs %}

**Removing the encryption from Presentation**

The following code example demonstrates removing the encryption from a PowerPoint Presentation. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
 //Opens an existing Presentation from file system and it can be decrypted by using the provided password.
using (FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open))
{
    //Opens an existing Presentation from file system and it can be decrypted by using the provided password.
    using (IPresentation presentation = Presentation.Open(inputStream, "PASSWORD!@1#$"))
    {
        //Decrypts the document.
        presentation.RemoveEncryption();
        //Save the PowerPoint Presentation as stream.
        using (FileStream outputStream = new FileStream("Output.pptx", FileMode.Create))
        {
            presentation.Save(outputStream);
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens an existing Presentation from file system and it can be decrypted by using the provided password.
using (IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$"))
{
    //Decrypts the document.
    presentation.RemoveEncryption();
    //Saves the presentation.
    presentation.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens an existing Presentation from file system and it can be decrypted by using the provided password.
Using presentationDocument As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")
    'Decrypts the document.
    presentationDocument.RemoveEncryption()
    'Saves the Presentation.
    presentationDocument.Save("Output.pptx")
End Using
{% endhighlight %}

{% endtabs %}

## Write Protection

You can set write protection for a PowerPoint Presentation and remove protection from the write protected PowerPoint presentation.

### Protect PowerPoint Presentation

You can protect a PowerPoint Presentation with password to restrict unauthorized editing.

The following code example shows how to set write protection for a PowerPoint Presentation. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create a new instance for PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add the blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add the shape to the slide
IShape shape = slide.Shapes.AddShape(AutoShapeType.BlockArc, 0, 0, 200, 200);
//Add the paragraph to the shape.
IParagraph paragraph = shape.TextBody.AddParagraph("welcome");
//Sets the author name
pptxDoc.BuiltInDocumentProperties.Author = "Syncfusion";
//Set the write protection for presentation instance
pptxDoc.SetWriteProtection("MYPASSWORD");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create a new instance for PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add the blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add the shape to the slide
IShape shape = slide.Shapes.AddShape(AutoShapeType.BlockArc, 0, 0, 200, 200);
//Add the paragraph to the shape.
IParagraph paragraph = shape.TextBody.AddParagraph("welcome");
//Sets the author name
pptxDoc.BuiltInDocumentProperties.Author = "Syncfusion";
//Set the write protection for presentation instance
pptxDoc.SetWriteProtection("MYPASSWORD");
//Saves the modified cloned PowerPoint presentation
pptxDoc.Save("Sample.pptx");
//Close the presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create a new instance for PowerPoint presentation
IPresentation pptxDoc = Presentation.Create()
'Add the blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add the shape to the slide
IShape shape = slide.Shapes.AddShape(AutoShapeType.BlockArc, 0, 0, 200, 200)
'Add the paragraph to the shape.
IParagraph paragraph = shape.TextBody.AddParagraph("welcome")
'Sets the author name
pptxDoc.BuiltInDocumentProperties.Author = "Syncfusion"
'Set the write protection for presentation instance
pptxDoc.SetWriteProtection("MYPASSWORD")
'Saves the modified cloned PowerPoint presentation
pptxDoc.Save("Sample.pptx")
'Close the presentation instance
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

### Remove Protection

You can check whether a PowerPoint Presentation is write protected and remove protection from the write protected PowerPoint Presentation.

The following code example shows how to remove restriction protection from the write protected PowerPoint Presentation 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets whether the presentation is write Protected. Read - only.
bool writeProtected = pptxDoc.IsWriteProtected;
//Checks whether the presentation is write protected
if (writeProtected)
{
     //Removes the write protection for presentation instance.
     pptxDoc.RemoveWriteProtection();
}
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Open the PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Gets whether the presentation is write Protected. Read - only.
bool writeProtected = pptxDoc.IsWriteProtected;
//Checks whether the presentation is write protected
if (writeProtected)
{
     //Removes the write protection for presentation instance.
     pptxDoc.RemoveWriteProtection();
}
//Saves the modified cloned PowerPoint presentation
pptxDoc.Save("Output.pptx");
//Close the presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Open the PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
'Gets whether the presentation is write Protected. Read - only.
bool writeProtected = pptxDoc.IsWriteProtected;
'Checks whether the presentation is write protected
if (writeProtected)
{
     'Removes the write protection for presentation instance.
     pptxDoc.RemoveWriteProtection();
}
'Saves the modified cloned PowerPoint presentation
pptxDoc.Save("Output.pptx")
'Close the presentation instance
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

N> 1. In Xamarin applications, Encryption, Decryption and Write Protection features are supported from the target framework .NET Standard 2.0 version onwards.
N> 2. For ASP.NET Core, Encryption, Decryption and Write Protection features are supported from the .NET Core 2.0 version onwards.

