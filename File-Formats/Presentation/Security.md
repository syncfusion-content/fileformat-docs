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

{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight ASP.NET CORE %}
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

{% highlight XAMARIN %}
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
	//Save the PowerPoint to stream in pptx format. 
	using (MemoryStream stream = new MemoryStream())
	{
		presentation.Save(stream);
		//Save the stream as a file in the device and invoke it for viewing
		Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
	}
}
{% endhighlight %}

{% endtabs %}

## Decrypting the PowerPoint Presentation

Essential Presentation provides ability to remove the encryption from the PowerPoint Presentation. You can decrypt a PowerPoint Presentation by opening it with the password.

**Opening** **the** **Encrypted** **PowerPoint** **Presentation**

The following code example demonstrates opening the encrypted PowerPoint Presentation. 

{% tabs %}

{% highlight c# %}
//Opens an existing Presentation from file system and it can be decrypted by using the provided password.
using (IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$"))
{
	//Saves the Presentation.
	presentation.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net %}
'Opens an existing Presentation from file system and it can be decrypted by using the provided password.
Using presentationDocument As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")
	'Saves the Presentation
	presentationDocument.Save("Output.pptx")
End Using
{% endhighlight %}

{% highlight ASP.NET CORE %}
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

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads or open an existing PowerPoint Presentation
using (IPresentation presentation = Presentation.Open(assembly.GetManifestResourceStream("Sample.Assets.Sample.pptx"), "PASSWORD!@1#$"))
{
	//Save the PowerPoint to stream in pptx format. 
	using (MemoryStream stream = new MemoryStream())
	{
		presentation.Save(stream);
		//Save the stream as a file in the device and invoke it for viewing
		Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
	}
}
{% endhighlight %}

{% endtabs %}

**Removing** **the** **encryption** **from** **Presentation**

The following code example demonstrates removing the encryption from a PowerPoint Presentation. 

{% tabs %}

{% highlight c# %}
//Opens an existing Presentation from file system and it can be decrypted by using the provided password.
using (IPresentation presentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$"))
{
	//Decrypts the document.
	presentation.RemoveEncryption();
	//Saves the presentation.
	presentation.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net %}
'Opens an existing Presentation from file system and it can be decrypted by using the provided password.
Using presentationDocument As IPresentation = Presentation.Open("Sample.pptx", "PASSWORD!@1#$")
	'Decrypts the document.
	presentationDocument.RemoveEncryption()
	'Saves the Presentation.
	presentationDocument.Save("Output.pptx")
End Using
{% endhighlight %}

{% highlight ASP.NET CORE %}
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

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads or open an existing PowerPoint Presentation
using (IPresentation presentation = Presentation.Open(assembly.GetManifestResourceStream("GettingStarted.Assets.Sample.pptx"), "PASSWORD!@1#$"))
{
	//Decrypts the document.
	presentation.RemoveEncryption();
	//Save the PowerPoint to stream in pptx format. 
	using (MemoryStream stream = new MemoryStream())
	{
		presentation.Save(stream);
		//Save the stream as a file in the device and invoke it for viewing
		Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
	}
}
{% endhighlight %}
{% endtabs %}

## Write Protection

You can set write protection for a PowerPoint Presentation and remove protection from the write protected PowerPoint presentation.

### Protect PowerPoint Presentation

You can protect a PowerPoint Presentation with password to restrict unauthorized editing.

The following code example shows how to set write protection for a PowerPoint Presentation. 

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

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

{% highlight UWP %}

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

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

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

{% highlight XAMARIN %}

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

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

### Remove Protection

You can check whether a PowerPoint Presentation is write protected and remove protection from the write protected PowerPoint Presentation.

The following code example shows how to remove restriction protection from the write protected PowerPoint Presentation 

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

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

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Gets whether the presentation is write Protected. Read - only.
bool writeProtected = pptxDoc.IsWriteProtected;

//Checks whether the presentation is write protected
if (writeProtected)
{
     //Removes the write protection for presentation instance.
     pptxDoc.RemoveWriteProtection();
}

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

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

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Gets whether the presentation is write Protected. Read - only.
bool writeProtected = pptxDoc.IsWriteProtected;

//Checks whether the presentation is write protected
if (writeProtected)
{
     //Removes the write protection for presentation instance.
     pptxDoc.RemoveWriteProtection();
}

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

N> 1. In Xamarin application, Encryption, Decryption and Write Protection features are supported from the target framework .NET Standard 2.0 version onwards. 
N> 2. For ASP.NET Core, Encryption, Decryption and Write Protection features are supported from .NET Core 2.0 version onwards.

