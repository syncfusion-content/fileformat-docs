---
title: Working with UWP
description: Working with Presentation library in UWP Platform
platform: file-formats
control: Presentation
documentation: UG
keywords: Working with Presentation library in UWP Platform
---

# Working with UWP

In your UWP application, please add the required assemblies in order to use Presentation. [Refer here for assemblies required](/File-Formats/Presentation/Assemblies-Required)

## Loading the Presentation

You can load and save PowerPoint Presentation asynchronously using Presentation. 

The following code example illustrates how to load PowerPoint Presentation by using stream in UWP.
{% tabs %}
{% highlight c# %}
//Loads the PowerPoint Presentation as stream.

Assembly assembly = typeof(GettingStartedPresentation).GetTypeInfo().Assembly;

string resourcePath = "SampleBrowser.Presentation.Assets.HelloWorld.pptx";

Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Loads or opens existing Presentation using open method of Presentation class.

IPresentation presentation = await Presentation.OpenAsync(fileStream);

//Saves Presentation with PPTX format.

SavePPTX(presentation);

/// <summary>
/// Saves as PPTX Format
/// </summary>
/// <param name="presentation"></param>
private async void SavePPTX(IPresentation presentation)
{

StorageFile stgFile;

if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
{
  FileSavePicker savePicker = new FileSavePicker();

  savePicker.SuggestedStartLocation = PickerLocationId.DocumentsLibrary;

  // Dropdown of file types the user can save the file as 

  savePicker.FileTypeChoices.Add("Presentation", new List<string>() { ".pptx" });

  // Default file name if the user does not type one in or select a file to replace
 
  savePicker.SuggestedFileName = "GettingStartedSample";

  stgFile = await savePicker.PickSaveFileAsync();
}
else
{
  StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

  stgFile = await local.CreateFileAsync("PowerPointPresentation.pptx", CreationCollisionOption.ReplaceExisting);

}
if (stgFile != null)
  {
   //Saves as PPTX Format

   await presentation.SaveAsync(stgFile);
  }
{% endhighlight %}
{% endtabs %}

## Save the Presentation

The following code example illustrates how to save the PowerPoint Presentation in UWP using save file picker.
{% tabs %}
{% highlight c# %}
//Creates new Presentation without slides.

IPresentation presentation = Presentation.Create();

//Adds new Blank type of slide.

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds Rectangle auto shape with specified size and positions.

IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 1.92 * 72, 1.51 * 72, 10.85 * 72, 4.12 * 72);

//Adds text into the shape.

shape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Creates new memory stream to save Presentation.

MemoryStream stream = new MemoryStream();

//Saves Presentation with PPTX format.
SavePPTX(presentation);

/// <summary>
/// Saves as PPTX Format
/// </summary>
/// <param name="presentation"></param>
private async void SavePPTX(IPresentation presentation)
{

StorageFile stgFile;

if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
{
  FileSavePicker savePicker = new FileSavePicker();

  savePicker.SuggestedStartLocation = PickerLocationId.DocumentsLibrary;

  // Dropdown of file types the user can save the file as 

  savePicker.FileTypeChoices.Add("Presentation", new List<string>() { ".pptx" });

  // Default file name if the user does not type one in or select a file to replace 

  savePicker.SuggestedFileName = "GettingStartedSample";

  stgFile = await savePicker.PickSaveFileAsync();
}
else
{
  StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

  stgFile = await local.CreateFileAsync("PowerPointPresentation.pptx", CreationCollisionOption.ReplaceExisting);

}
if (stgFile != null)
  {
   //Saves as PPTX Format
   await presentation.SaveAsync(stgFile);
  }
{% endhighlight %}
{% endtabs %}

N> The image and PDF conversions are not supported in UWP,Xamarin.Forms,Xamarin.Android,Xamarin.IOS,Xamarin.WindowsPhone platforms.
