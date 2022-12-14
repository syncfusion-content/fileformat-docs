---
title: Create Word document in UWP | Syncfusion
description: Create Word document without Microsoft Word or interop dependencies in UWP application using Syncfusion UWP Word (Essential DocIO) library
platform: file-formats
control: DocIO
documentation: UG
---

# Create Word document in UWP

Syncfusion Essential DocIO is a [UWP Word library](https://www.syncfusion.com/word-framework/uwp/word-library) used to create, read, and edit **Word** documents programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **create a Word document in UWP**.

## Steps to create Word document programmatically in UWP:

Step 1: Create a new C# Blank App (Universal Windows) project.

![Create UWP application in Visual Studio](UWP_images/CreateProject.png)

Step 2: Install the [Syncfusion.DocIO.UWP](https://www.nuget.org/packages/Syncfusion.DocIO.UWP/) NuGet package as a reference to your UWP application from [NuGet.org](https://www.nuget.org/).

![Install DocIO UWP NuGet package](UWP_images/Install_NuGet.jpg)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.

Step 3: Add a new button in the MainPage.xaml as shown below.

{% capture codesnippet1 %}
{% tabs %}

{% highlight c# tabtitle="C#" %}

<Page
   x:Class="CreateWordSample.MainPage"
   xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
   xmlns:local="using:CreateWordSample"
   xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
   xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
   mc:Ignorable="d">
  
   <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
         <Button x:Name="button" Content="Create Document" Click="OnButtonClicked" HorizontalAlignment="Center" VerticalAlignment="Center"/>
   </Grid>
</Page>

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet1 | OrderList_Indent_Level_1 }}

Step 4: Include the following namespaces in the MainPage.xaml.cs file.

{% capture codesnippet2 %}
{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Windows.Storage.Pickers;
using Windows.Storage;
using Windows.Storage.Streams;
using System.Reflection;

{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet2 | OrderList_Indent_Level_1 }}

Step 5: Include the below code snippet in the click event of the button in MainPage.xaml.cs, to **create a Word document** and save the **Word** document as a physical file and open the file for viewing.

{% capture codesnippet3 %}
{% tabs %}

{% highlight c# tabtitle="C#" %}

private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
	//Creating a new document
	WordDocument document = new WordDocument();
	//Adding a new section to the document
	WSection section = document.AddSection() as WSection;
	//Set Margin of the section
	section.PageSetup.Margins.All = 72;
	//Set page size of the section
	section.PageSetup.PageSize = new SizeF(612, 792);

	//Create Paragraph styles
	WParagraphStyle style = document.AddParagraphStyle("Normal") as WParagraphStyle;
	style.CharacterFormat.FontName = "Calibri";
	style.CharacterFormat.FontSize = 11f;
	style.ParagraphFormat.BeforeSpacing = 0;
	style.ParagraphFormat.AfterSpacing = 8;
	style.ParagraphFormat.LineSpacing = 13.8f;

	style = document.AddParagraphStyle("Heading 1") as WParagraphStyle;
	style.ApplyBaseStyle("Normal");
	style.CharacterFormat.FontName = "Calibri Light";
	style.CharacterFormat.FontSize = 16f;
	style.CharacterFormat.TextColor = Color.FromArgb(46, 116, 181);
	style.ParagraphFormat.BeforeSpacing = 12;
	style.ParagraphFormat.AfterSpacing = 0;
	style.ParagraphFormat.Keep = true;
	style.ParagraphFormat.KeepFollow = true;
	style.ParagraphFormat.OutlineLevel = OutlineLevel.Level1;
	IWParagraph paragraph = section.HeadersFooters.Header.AddParagraph();

	//Gets the image stream
	Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("CreateWordSample.Assets.AdventureCycle.jpg");
	IWPicture picture = paragraph.AppendPicture(imageStream);
	picture.TextWrappingStyle = TextWrappingStyle.InFrontOfText;
	picture.VerticalOrigin = VerticalOrigin.Margin;
	picture.VerticalPosition = -45;
	picture.HorizontalOrigin = HorizontalOrigin.Column;
	picture.HorizontalPosition = 263.5f;
	picture.WidthScale = 20;
	picture.HeightScale = 15;

	paragraph.ApplyStyle("Normal");
	paragraph.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Left;
	WTextRange textRange = paragraph.AppendText("Adventure Works Cycles") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Calibri";
	textRange.CharacterFormat.TextColor = Color.Red;

	//Appends paragraph
	paragraph = section.AddParagraph();
	paragraph.ApplyStyle("Heading 1");
	paragraph.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
	textRange = paragraph.AppendText("Adventure Works Cycles") as WTextRange;
	textRange.CharacterFormat.FontSize = 18f;
	textRange.CharacterFormat.FontName = "Calibri";

	//Appends paragraph
	paragraph = section.AddParagraph();
	paragraph.ParagraphFormat.FirstLineIndent = 36;
	paragraph.BreakCharacterFormat.FontSize = 12f;
	textRange = paragraph.AppendText("Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base.") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;

	//Appends paragraph
	paragraph = section.AddParagraph();
	paragraph.ParagraphFormat.FirstLineIndent = 36;
	paragraph.BreakCharacterFormat.FontSize = 12f;
	textRange = paragraph.AppendText("In 2000, AdventureWorks Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;

	paragraph = section.AddParagraph();
	paragraph.ApplyStyle("Heading 1");
	paragraph.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Left;
	textRange = paragraph.AppendText("Product Overview") as WTextRange;
	textRange.CharacterFormat.FontSize = 16f;
	textRange.CharacterFormat.FontName = "Calibri";
	//Appends table
	IWTable table = section.AddTable();
	table.ResetCells(3, 2);
	table.TableFormat.Borders.BorderType = BorderStyle.None;
	table.TableFormat.IsAutoResized = true;

	//Appends paragraph
	paragraph = table[0, 0].AddParagraph();
	paragraph.ParagraphFormat.AfterSpacing = 0;
	paragraph.BreakCharacterFormat.FontSize = 12f;
	//Appends picture to the paragraph
	imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("CreateWordSample.Assets.Mountain-200.jpg");
	picture = paragraph.AppendPicture(imageStream);
	picture.TextWrappingStyle = TextWrappingStyle.TopAndBottom;
	picture.VerticalOrigin = VerticalOrigin.Paragraph;
	picture.VerticalPosition = 4.5f;
	picture.HorizontalOrigin = HorizontalOrigin.Column;
	picture.HorizontalPosition = -2.15f;
	picture.WidthScale = 79;
	picture.HeightScale = 79;

	//Appends paragraph
	paragraph = table[0, 1].AddParagraph();
	paragraph.ApplyStyle("Heading 1");
	paragraph.ParagraphFormat.AfterSpacing = 0;
	paragraph.ParagraphFormat.LineSpacing = 12f;
	paragraph.AppendText("Mountain-200");
	//Appends paragraph
	paragraph = table[0, 1].AddParagraph();
	paragraph.ParagraphFormat.AfterSpacing = 0;
	paragraph.ParagraphFormat.LineSpacing = 12f;
	paragraph.BreakCharacterFormat.FontSize = 12f;
	paragraph.BreakCharacterFormat.FontName = "Times New Roman";

	textRange = paragraph.AppendText("Product No: BK-M68B-38\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Size: 38\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Weight: 25\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Price: $2,294.99\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	//Appends paragraph
	paragraph = table[0, 1].AddParagraph();
	paragraph.ParagraphFormat.AfterSpacing = 0;
	paragraph.ParagraphFormat.LineSpacing = 12f;
	paragraph.BreakCharacterFormat.FontSize = 12f;

	//Appends paragraph
	paragraph = table[1, 0].AddParagraph();
	paragraph.ApplyStyle("Heading 1");
	paragraph.ParagraphFormat.AfterSpacing = 0;
	paragraph.ParagraphFormat.LineSpacing = 12f;
	paragraph.AppendText("Mountain-300 ");
	//Appends paragraph
	paragraph = table[1, 0].AddParagraph();
	paragraph.ParagraphFormat.AfterSpacing = 0;
	paragraph.ParagraphFormat.LineSpacing = 12f;
	paragraph.BreakCharacterFormat.FontSize = 12f;
	paragraph.BreakCharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Product No: BK-M47B-38\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Size: 35\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Weight: 22\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Price: $1,079.99\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	//Appends paragraph
	paragraph = table[1, 0].AddParagraph();
	paragraph.ParagraphFormat.AfterSpacing = 0;
	paragraph.ParagraphFormat.LineSpacing = 12f;
	paragraph.BreakCharacterFormat.FontSize = 12f;

	//Appends paragraph
	paragraph = table[1, 1].AddParagraph();
	paragraph.ApplyStyle("Heading 1");
	paragraph.ParagraphFormat.LineSpacing = 12f;
	//Appends picture to the paragraph
	imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("CreateWordSample.Assets.Mountain-300.jpg");
	picture = paragraph.AppendPicture(imageStream);
	picture.TextWrappingStyle = TextWrappingStyle.TopAndBottom;
	picture.VerticalOrigin = VerticalOrigin.Paragraph;
	picture.VerticalPosition = 8.2f;
	picture.HorizontalOrigin = HorizontalOrigin.Column;
	picture.HorizontalPosition = -14.95f;
	picture.WidthScale = 75;
	picture.HeightScale = 75;

	//Appends paragraph
	paragraph = table[2, 0].AddParagraph();
	paragraph.ApplyStyle("Heading 1");
	paragraph.ParagraphFormat.LineSpacing = 12f;
	//Appends picture to the paragraph
	imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("CreateWordSample.Assets.Road-550-W.jpg");
	picture = paragraph.AppendPicture(imageStream);
	picture.TextWrappingStyle = TextWrappingStyle.TopAndBottom;
	picture.VerticalOrigin = VerticalOrigin.Paragraph;
	picture.VerticalPosition = 3.75f;
	picture.HorizontalOrigin = HorizontalOrigin.Column;
	picture.HorizontalPosition = -5f;
	picture.WidthScale = 92;
	picture.HeightScale = 92;
	
	//Appends paragraph
	paragraph = table[2, 1].AddParagraph();
	paragraph.ApplyStyle("Heading 1");
	paragraph.ParagraphFormat.AfterSpacing = 0;
	paragraph.ParagraphFormat.LineSpacing = 12f;
	paragraph.AppendText("Road-150 ");
	//Appends paragraph
	paragraph = table[2, 1].AddParagraph();
	paragraph.ParagraphFormat.AfterSpacing = 0;
	paragraph.ParagraphFormat.LineSpacing = 12f;
	paragraph.BreakCharacterFormat.FontSize = 12f;
	paragraph.BreakCharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Product No: BK-R93R-44\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Size: 44\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Weight: 14\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	textRange = paragraph.AppendText("Price: $3,578.27\r") as WTextRange;
	textRange.CharacterFormat.FontSize = 12f;
	textRange.CharacterFormat.FontName = "Times New Roman";
	//Appends paragraph
	section.AddParagraph();
	
	MemoryStream stream = new MemoryStream();

	//Saves the Word document to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);

	//Saves the stream as Word document file in local machine
	Save(stream, "Sample.docx");
}
{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet3 | OrderList_Indent_Level_1 }}

## Save Word document in UWP

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Getting-Started/UWP).

By executing the program, you will get the Word document as follows.

![UWP output Word document](UWP_images/GettingStartedOutput.jpg)