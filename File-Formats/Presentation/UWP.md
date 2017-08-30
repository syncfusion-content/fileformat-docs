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

StorageFile storageFile;

if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
{
  FileSavePicker savePicker = new FileSavePicker();

  savePicker.SuggestedStartLocation = PickerLocationId.DocumentsLibrary;

  // Dropdown of file types the user can save the file as 

  savePicker.FileTypeChoices.Add("Presentation", new List<string>() { ".pptx" });

  // Default file name if the user does not type one in or select a file to replace
 
  savePicker.SuggestedFileName = "GettingStartedSample";

  storageFile = await savePicker.PickSaveFileAsync();
}
else
{
  StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

  storageFile = await local.CreateFileAsync("PowerPointPresentation.pptx", CreationCollisionOption.ReplaceExisting);

}
if (storageFile != null)
  {
   //Saves as PPTX Format

   await presentation.SaveAsync(storageFile);
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

//Adds a shape with specified size and positions.

IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 1.92 * 72, 1.51 * 72, 10.85 * 72, 4.12 * 72);

//Adds text into the shape.

shape.TextBody.AddParagraph("In 2000, Adventure Works Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the Adventure Works Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.");

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

StorageFile storageFile;

if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
{
  FileSavePicker savePicker = new FileSavePicker();

  savePicker.SuggestedStartLocation = PickerLocationId.DocumentsLibrary;

  // Dropdown of file types the user can save the file as 

  savePicker.FileTypeChoices.Add("Presentation", new List<string>() { ".pptx" });

  // Default file name if the user does not type one in or select a file to replace 

  savePicker.SuggestedFileName = "GettingStartedSample";

  storageFile = await savePicker.PickSaveFileAsync();
}
else
{
  StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

  storageFile = await local.CreateFileAsync("PowerPointPresentation.pptx", CreationCollisionOption.ReplaceExisting);

}
if (storageFile != null)
  {
   //Saves as PPTX Format
   await presentation.SaveAsync(storageFile);
  }
{% endhighlight %}
{% endtabs %}

N> The PDF conversion is not supported in UWP platform.
