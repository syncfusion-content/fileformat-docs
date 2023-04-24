---
title: Open and save Word document in Xamarin | Syncfusion
description: Open and save Word document in Xamarin application using Syncfusion Xamarin Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Open and Save Word document in Xamarin

Syncfusion DocIO is a [Xamarin Word library](https://www.syncfusion.com/document-processing/word-framework/xamarin/word-library) used to **create, read, and edit Word documents** programmatically without **Microsoft Word** or **interop** dependencies. Using this library, you can **open and save a Word document in Xamarin**.

## Steps to open and save Word document programmatically:

Step 1: Create a new Xamarin.Forms application project.

Step 2: Select a project template and required platforms to deploy the application. In this application the portable assemblies to be shared across multiple platforms, the .NET Standard code sharing strategy has been selected. For more details about code sharing refer [here](https://learn.microsoft.com/en-us/xamarin/cross-platform/app-fundamentals/code-sharing).

N> If .NET Standard is not available in the code sharing strategy, the Portable Class Library (PCL) can be selected.

Step 3: Install [Syncfusion.Xamarin.DocIO](https://www.nuget.org/packages/Syncfusion.Xamarin.DocIO) NuGet package as a reference to the .NET Standard project in your application from [NuGet.org](https://www.nuget.org/).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Add new Forms XAML page in **portable project**. If there is no XAML page defined in the App class. Otherwise proceed to the next step.
<ul>
<li>
To add the new XAML page, right click on the project and select <b>Add > New Item</b> and add a Forms XAML Page from the list. Name it as MainXamlPage.
</li>
<li>
In App class of <b>portable project</b> (App.cs), replace the existing constructor of App class with the code snippet given below which invokes the <b>MainXamlPage</b>.
</li>
</ul>

{% tabs %}

{% highlight c# tabtitle="C#" %}
public App()
{
    // The root page of your application
    MainPage = new MainXamlPage();
}
{% endhighlight %}

{% endtabs %}

Step 5: In the MainXamlPage.xaml add new button as shown below.

{% tabs %}

{% highlight XML %}

<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
        xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
        x:Class="Open_and_save_Word_document.MainXamlPage">

    <StackLayout VerticalOptions="Center">
        <Button Text="open and save Word document" Clicked="OnButtonClicked" HorizontalOptions="Center"/>
    </StackLayout>
</ContentPage>

{% endhighlight %}

{% endtabs %}

Step 6: Include the following namespace in the MainXamlPage.xaml.cs file.

{% tabs %}

{% highlight c# tabtitle="C#" %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% endtabs %}

Step 7: Include the below code snippet in the click event of the button in MainXamlPage.xaml.cs, to **open an existing Word document in Xamarin**.

{% tabs %}

{% highlight c# tabtitle="C#" %}

void OnButtonClicked(object sender, EventArgs args)
{
    //Load an existing Word document.
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Open_and_save_Word_document.Assets.Input.docx"), FormatType.Docx))
    {
    
    }
}
{% endhighlight %}

{% endtabs %}

Step 8: Add below code example to add a paragraph in the Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Access the section in a Word document.
IWSection section = document.Sections[0];
//Add a new paragraph to the section.
IWParagraph paragraph = section.AddParagraph();
paragraph.ParagraphFormat.FirstLineIndent = 36;
paragraph.BreakCharacterFormat.FontSize = 12f;
IWTextRange text = paragraph.AppendText("In 2000, Adventure Works Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the Adventure Works Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.");
text.CharacterFormat.FontSize = 12f;
{% endhighlight %}

{% endtabs %}

Step 9: Add below code example to **save the Word document in Xamarin**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Save a Word document to the MemoryStream.
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing.
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
{% endhighlight %}

{% endtabs %}

## Helper files for Xamarin

Download the helper files from this [link](https://www.syncfusion.com/downloads/support/directtrac/general/HELPER~1-696201504.ZIP) and add them into the mentioned project. These helper files allow you to save the stream as a physical file and open the file for viewing.

<table>
  <tr>
  <td>
    <b>Project</b>
  </td>
  <td>
    <b>File Name</b>
  </td>
  <td>
    <b>Summary</b>
  </td>
  </tr>
  <tr>
  <td>
    Portable project
  </td>
  <td>
    ISave.cs
  </td>
  <td>Represent the base interface for save operation
  </td>
  </tr>
  <tr>
  <td rowspan="2">
    iOS Project
  </td>
  <td>
    SaveIOS.cs
  </td>
  <td>
    Save implementation for iOS device
  </td>
  </tr>
  <tr>
  <td>
    PreviewControllerDS.cs
  </td>
  <td>
    Helper class for viewing the <b>Word document</b> in iOS device
  </td>
  </tr>
  <tr>
  <td>
    Android project
  </td>
  <td>
    SaveAndroid.cs
  </td>
  <td>Save implementation for Android device
  </td>
  </tr>
  <tr>
  <td>
    WinPhone project
  </td>
  <td>
    SaveWinPhone.cs
  </td>
  <td>Save implementation for Windows Phone device
  </td>
  </tr>
  <tr>
  <td>
    UWP project
  </td>
  <td>
    SaveWindows.cs
  </td>
  <td>Save implementation for UWP device.
  </td>
  </tr>
  <tr>
  <td>
    Windows (8.1) project
  </td>
  <td>
    SaveWindows81.cs
  </td>
  <td>Save implementation for WinRT device.
  </td>
  </tr>
</table>

Compile and execute the application. Now this application **opens and saves a Word document**.

By executing the program, you will get the **Word document** as follows.

![Xamarin open and save output Word document](Xamarin_images/OpenAndSaveOutput.png)