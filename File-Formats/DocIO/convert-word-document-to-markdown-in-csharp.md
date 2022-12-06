---
title: Word Document to Markdown conversion | DocIO | Syncfusion
description: This section illustrates how to convert Word document to Markdown using Syncfusion Word library (Essential DocIO)
platform: file-formats
control: DocIO
documentation: UG
---

# Word to Markdown Conversion

Markdown is a lightweight markup language that adds formatting elements to plaintext text documents. The .NET Word (DocIO) library supports the conversion of a Word document to a Markdown file, which mostly follows the CommonMark specification and GitHub-flavored syntax.

## Convert Word to Markdown

Convert an existing Word document or document that is created from scratch into a Markdown file using the .NET Word (DocIO) library.

The following code example shows how to convert a Word document to a Markdown.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Open an existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    //Save the document as a Markdown file.
    document.Save("WordtoMd.md", FormatType.Markdown);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
    'Save the document as a Markdown file.
    document.Save("WordtoMd.md", FormatType.Markdown)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Save as a Markdown file into the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Markdown);
        //Save the stream as a Markdown file in the local machine.
        Save(stream, "WordtoMd.md");
    }
}
//Saves a Word document.
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".md";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".md" });
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
            //Write the compressed data from the memory to a file.
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file.
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as a Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Save as a Markdown file into the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Markdown);
        outputStream.Position = 0;
        //Download the Markdown file in the browser.
        return File(outputStream, "application/msword", "WordToMd.md");
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Save as a Markdown file into the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Markdown);
        //Save the stream as a file in the device and invoke it for viewing. 
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WordtoMd.md", "application/msword", outputStream);
    }
//Please download the helper files from the following link to save the stream as a file and open the file for viewing in the Xamarin platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}
{% endtabs %}

## Supported Markdown elements

The following table illustrates the supported Markdown elements in Word to Markdown conversion and how to set that Markdown elements in input Word document.

<table style="width: 760px;">
<thead>
<tr>
<td style="width: 182.986px;"><strong>Markdown elements</strong></td>
<td style="width: 557.014px;"><strong>How to set in Word document</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td style="width: 182.986px;">Thematic breaks</td>
<td style="width: 557.014px;">Add an horizontal rule.&nbsp;</td>
</tr>
<tr>
<td style="width: 182.986px;">Headings</td>
<td style="width: 557.014px;">
<p>Apply heading style for paragraphs. DocIO supports converting 6 levels of headings from a Word document to their equivalent headings' syntax in Markdown.</p>
<p>Heading style paragraph. &nbsp;</p>
6 level headings only supported in Markdown.</td>
</tr>
<tr>
<td style="width: 182.986px;">Indented code block</td>
<td style="width: 557.014px;">Paragraph with &ldquo;IndentedCode&rdquo; style name.</td>
</tr>
<tr>
<td style="width: 182.986px;">Fenced code block</td>
<td style="width: 557.014px;">Paragraph with &ldquo;FencedCode&rdquo; style name.</td>
</tr>
<tr>
<td style="width: 182.986px;">Block quotes</td>
<td style="width: 557.014px;">Paragraph with &ldquo;Quote&rdquo; style name</td>
</tr>
<tr>
<td style="width: 182.986px;">List items</td>
<td style="width: 557.014px;">Apply numbered or bulleted list format to paragraphs.&nbsp;</td>
</tr>
<tr>
<td style="width: 182.986px;">Codespan</td>
<td style="width: 557.014px;">Set &ldquo;InlineCode&rdquo; character style for text.</td>
</tr>
<tr>
<td style="width: 182.986px;">Emphasis and strong emphasis</td>
<td style="width: 557.014px;">Bold and Italic formats for text.</td>
</tr>
<tr>
<td style="width: 182.986px;">Links</td>
<td style="width: 557.014px;">Set hyperlinks in Word document.</td>
</tr>
<tr>
<td style="width: 182.986px;">Task items</td>
<td style="width: 557.014px;">Set checkbox content control as the first item of the paragraph.</td>
</tr>
</tbody>
</table>

## Create Markdown elements

Create all the supported Markdown elements in a Word document using the .NET Word (DocIO) library, then save a Word document as a Markdown file.

### Code blocks

The Essential DocIO supports two types of code blocks in Word to Markdown conversion. 

* Indented code block: Set the paragraph style as “IndentedCode.”
* Fenced code block: Set the paragraph style as “FencedCode.”

The following code example shows how to create code blocks in a Word document using DocIO.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Add a new section to the document.
    IWSection section = document.AddSection();
    //Add a new paragraph to the section.
    IWParagraph paragraph = section.AddParagraph();
    //Append text to the paragraph.
    IWTextRange textRange = paragraph.AppendText("Fenced Code");
    //Add a new paragraph to the section.
    paragraph = section.AddParagraph();
    //Create a user-defined style as FencedCode.
    IWParagraphStyle style = document.AddParagraphStyle("FencedCode");
    //Apply FencedCode style for the paragraph.
    paragraph.ApplyStyle("FencedCode");
    //Append text.
    textRange = paragraph.AppendText("class Hello\n{\n\tStatic void Main()\n\t{\n\t\tConsole.WriteLine(\"Fenced Code\")\n\t}\n}");
    //Add a new paragraph and append text to the paragraph.
    section.AddParagraph().AppendText("Indented Code");
    //Add a new paragraph to the section.
    paragraph = section.AddParagraph();
    //Create a user-defined style as IndentedCode.
    style = document.AddParagraphStyle("IndentedCode");
    //Apply IndentedCode style for the paragraph.
    paragraph.ApplyStyle("IndentedCode");
    //Append text.
    textRange = paragraph.AppendText("class Hello\n\t{\n\t\tStatic void Main()\n\t\t{\n\t\t\tConsole.WriteLine(\"Indented Code\")\n\t\t}\n\t}");
    //Save the document as a Markdown file.
    document.Save("WordtoMd.md", FormatType.Markdown);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a new Word document.
Using document As WordDocument = New WordDocument()
    'Add a new section to the document.
    Dim section As IWSection = document.AddSection()
    'Add a new paragraph to the section.
    Dim paragraph As IWParagraph = section.AddParagraph()
    'Append text to the paragraph.
    Dim textRange As IWTextRange = paragraph.AppendText("Fenced Code")
    'Add a new paragraph to the section.
    paragraph = section.AddParagraph()
    'Create a user-defined style as FencedCode.
    Dim style As IWParagraphStyle = document.AddParagraphStyle("FencedCode")
    'Apply FencedCode style for the paragraph.
    paragraph.ApplyStyle("FencedCode")
    'Append text.
    textRange = paragraph.AppendText("class Hello" & vbLf & "{" & vbLf & vbTab & "Static void Main()" & vbLf & vbTab & "{" & vbLf & vbTab & vbTab & "Console.WriteLine(""Fenced Code"")" & vbLf & vbTab & "}" & vbLf & "}")
    'Add a new paragraph and append text to the paragraph.
    section.AddParagraph().AppendText("Indented Code")
    'Add a new paragraph to the section.
    paragraph = section.AddParagraph()
    'Create a user-defined style as IndentedCode.
    style = document.AddParagraphStyle("IndentedCode")
    'Apply IndentedCode style for the paragraph.
    paragraph.ApplyStyle("IndentedCode")
    'Append text.
    textRange = paragraph.AppendText("class Hello" & vbLf & vbTab & "{" & vbLf & vbTab & vbTab & "Static void Main()" & vbLf & vbTab & vbTab & "{" & vbLf & vbTab & vbTab & vbTab & "Console.WriteLine(""Indented Code"")" & vbLf & vbTab & vbTab & "}" & vbLf & vbTab & "}")
    'Save the document as a Markdown file.
    document.Save("WordtoMd.md", FormatType.Markdown)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Add a new section to the document.
    IWSection section = document.AddSection();
    //Add a new paragraph to the section.
    IWParagraph paragraph = section.AddParagraph();
    //Append text to the paragraph.
    IWTextRange textRange = paragraph.AppendText("Fenced Code");
    //Add a new paragraph to the section.
    paragraph = section.AddParagraph();
    //Create a user-defined style as FencedCode..
    IWParagraphStyle style = document.AddParagraphStyle("FencedCode");
    //Apply FencedCode style for the paragraph.
    paragraph.ApplyStyle("FencedCode");
    //Append text.
    textRange = paragraph.AppendText("class Hello\n{\n\tStatic void Main()\n\t{\n\t\tConsole.WriteLine(\"Fenced Code\")\n\t}\n}");
    //Add a new paragraph and append text to the paragraph.
    section.AddParagraph().AppendText("Indented Code");
    //Add a new paragraph to the section.
    paragraph = section.AddParagraph();
    //Create a user-defined style as IndentedCode.
    style = document.AddParagraphStyle("IndentedCode");
    //Apply IndentedCode style for the paragraph.
    paragraph.ApplyStyle("IndentedCode");
    //Append text.
    textRange = paragraph.AppendText("class Hello\n\t{\n\t\tStatic void Main()\n\t\t{\n\t\t\tConsole.WriteLine(\"Indented Code\")\n\t\t}\n\t}");
    //Save the document as a Markdown file.
    Save(stream, "WordtoMd.md");
}
//Please refer to the following link to save a Word document in the UWP platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Add a new section to the document.
    IWSection section = document.AddSection();
    //Add a new paragraph to the section.
    IWParagraph paragraph = section.AddParagraph();
    //Append text to the paragraph.
    IWTextRange textRange = paragraph.AppendText("Fenced Code");
    /Add a new paragraph to the section.
    paragraph = section.AddParagraph();
    //Create a user-defined style as FencedCode.
    IWParagraphStyle style = document.AddParagraphStyle("FencedCode");
    /Apply FencedCode style for the paragraph.
    paragraph.ApplyStyle("FencedCode");
    //Append text.
    textRange = paragraph.AppendText("class Hello\n{\n\tStatic void Main()\n\t{\n\t\tConsole.WriteLine(\"Fenced Code\")\n\t}\n}");
    //Add a new paragraph and append text to the paragraph.
    section.AddParagraph().AppendText("Indented Code");
    //Add a new paragraph to the section.
    paragraph = section.AddParagraph();
    //Create a user-defined style as IndentedCode.
    style = document.AddParagraphStyle("IndentedCode");
    //Apply IndentedCode style for the paragraph.
    paragraph.ApplyStyle("IndentedCode");
    //Append text.
    textRange = paragraph.AppendText("class Hello\n\t{\n\t\tStatic void Main()\n\t\t{\n\t\t\tConsole.WriteLine(\"Indented Code\")\n\t\t}\n\t}");
    //Save as a Markdown file into the MemoryStream.
    MemoryStream outputStream = new MemoryStream();
    document.Save(outputStream, FormatType.Markdown);
    outputStream.Position = 0;
    return File(outputStream, "application/msword", "WordToMd.md");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Add a new section to the document.
    IWSection section = document.AddSection();
    //Add a new paragraph to the section.
    IWParagraph paragraph = section.AddParagraph();
    //Append text to the paragraph.
    IWTextRange textRange = paragraph.AppendText("Fenced Code");
    //Add a new paragraph to the section.
    paragraph = section.AddParagraph();
    //Create a user-defined style as FencedCode.
    IWParagraphStyle style = document.AddParagraphStyle("FencedCode");
    //Apply FencedCode style for the paragraph.
    paragraph.ApplyStyle("FencedCode");
    //Append text.
    textRange = paragraph.AppendText("class Hello\n{\n\tStatic void Main()\n\t{\n\t\tConsole.WriteLine(\"Fenced Code\")\n\t}\n}");
    //Add a new paragraph and append text to the paragraph.
    section.AddParagraph().AppendText("Indented Code");
    //Add a new paragraph to the section.
    paragraph = section.AddParagraph();
    //Create a user-defined style as IndentedCode.
    style = document.AddParagraphStyle("IndentedCode");
    //Apply IndentedCode style for the paragraph.
    paragraph.ApplyStyle("IndentedCode");
    //Append text.
    textRange = paragraph.AppendText("class Hello\n\t{\n\t\tStatic void Main()\n\t\t{\n\t\t\tConsole.WriteLine(\"Indented Code\")\n\t\t}\n\t}");
    //Save the document as a Markdown file.
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WordToMd.md", "application/msword", stream);
}
//Please download the helper files from the following link to save the stream as a file and open the file for viewing in the Xamarin platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}
{% endtabs %}

### Block quotes

Create block quotes in a Word document by applying the “Quote” paragraph style to the paragraphs.

The following code example shows how to create block quotes in a Word document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Add a new section to the document.
    IWSection section = document.AddSection();
    //Create a user-defined style.
    IWParagraphStyle style = document.AddParagraphStyle("Quote");
    //Add a new paragraph to the section.
    IWParagraph paragraph = section.AddParagraph();
    //Apply Quote style to simple hello world text.
    paragraph.ApplyStyle("Quote");
    //Append text.
    IWTextRange textRange = paragraph.AppendText("Hello World");
    document.Save("WordToMd.md", FormatType.Markdown);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a new Word document.
Using document As WordDocument = New WordDocument()
    'Add a new section to the document.
    Dim section As IWSection = document.AddSection()
    'Create a user-defined style.
    Dim style As IWParagraphStyle = document.AddParagraphStyle("Quote")
    'Add a new paragraph to the section.
    Dim paragraph As IWParagraph = section.AddParagraph()
    'Apply Quote style to simple hello world text.
    paragraph.ApplyStyle("Quote")
    'Append text.
    Dim textRange As IWTextRange = paragraph.AppendText("Hello World")
    document.Save("WordToMd.md", FormatType.Markdown)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Add a new section to the document.
    IWSection section = document.AddSection();
    //Create a user-defined style.
    IWParagraphStyle style = document.AddParagraphStyle("Quote");
    //Add a new paragraph to the section.
    IWParagraph paragraph = section.AddParagraph();
    //Apply Quote style to simple hello world text.
    paragraph.ApplyStyle("Quote");
    //Append text.
    IWTextRange textRange = paragraph.AppendText("Hello World");
    //Save the document as a Markdown file.
    Save(stream, "WordtoMd.md");
}
//Please refer to the following link to save a Word document in the UWP platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Add a new section to the document.
    IWSection section = document.AddSection();
    //Create a user-defined style.
    IWParagraphStyle style = document.AddParagraphStyle("Quote");
    //Add a new paragraph to the section.
    IWParagraph paragraph = section.AddParagraph();
    //Apply Quote style to simple hello world text.
    paragraph.ApplyStyle("Quote");
    //Append text.
    IWTextRange textRange = paragraph.AppendText("Hello World");
    //Save the document as a Markdown file.
    return File(outputStream, "application/msword", "WordToMd.md");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Add a new section to the document.
    IWSection section = document.AddSection();
    //Create a user-defined style.
    IWParagraphStyle style = document.AddParagraphStyle("Quote");
    //Add a new paragraph to the section.
    IWParagraph paragraph = section.AddParagraph();
    //Apply Quote style to a simple hello world text.
    paragraph.ApplyStyle("Quote");
    //Append text.
    IWTextRange textRange = paragraph.AppendText("Hello World");
    //Save a Word document to the MemoryStream.
    MemoryStream outputStream = new MemoryStream();
    document.Save(outputStream, FormatType.Markdown);
    //Save the stream as a file in the device and invoke it for viewing.
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WordToMd.md", "application/msword", outputStream);
}
//Please download the helper files from the following link to save the stream as a file and open the file for viewing in the Xamarin platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}
{% endtabs %}

N> Nested block quotes are not supported in a Word to the Markdown conversion. To preserve nested block quotes, add the number of “>” characters at the beginning of the paragraph in a Word document as equivalent to the nth nested level of the block quote. For example, to insert the 2nd nested level block quote, add two “>” characters at the start of the sentence, and no need to apply the “Quote” style to the paragraph.

## Customize image saving

When converting a Word document to a Markdown using the Save(fileName) overloads, DocIO creates a new folder parallel to the output file name and exports all the images into it as default.

When converting a Word document to a Markdown using the Save(Stream, FormatType) overloads, DocIO preserves the images as base64 format in the output Markdown file as default.

Also, customize the above default behaviors using the following options in DocIO.

### Export images to folder

Specify the folder location to export the images using the MarkdownExportImagesFolder API.

The following code example illustrates how set the images folder to export the images while converting a Word document to a Markdown file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Open an existing Word document. 
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    //Set images folder to export images. 
    document.SaveOptions.MarkdownExportImagesFolder = "D:\\WordToMdConversion ";
    //Save a Word document as a Markdown file.
    document.Save("WordtoMd.md", FormatType.Markdown);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
'Set images folder to export images. 
document.SaveOptions.MarkdownExportImagesFolder = "D:\\WordToMdConversion ";
'Save a document as a Markdown file.
document.Save("WordtoMd.md", FormatType.Markdown)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO doesn’t support the MarkdownExportImagesFolder API in UWP and Xamarin platforms.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as a Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Set images folder to export images. 
        document.SaveOptions.MarkdownExportImagesFolder = "D:\\WordToMdConversion ";

        //Save a Markdown file to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Markdown);
        outputStream.Position = 0;
        //Download as a Markdown file in the browser.
        return File(outputStream, "application/msword", "WordtoMd.md");
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//DocIO doesn’t support the MarkdownExportImagesFolder API in UWP and Xamarin platforms.
{% endhighlight %}
{% endtabs %}

### Customize the image path

DocIO provides an ImageNodeVisited event, which is used to customize the image path to set in the output Markdown file and save images externally while converting a Word document to a Markdown.

The following code example illustrates how to save Image files during a Word to Markdown Conversion.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Open an existing Word document. 
using (WordDocument document = new WordDocument(@"Input.docx"))
{
    //Hook the event to customize the image. 
    document.SaveOptions.ImageNodeVisited += SaveImage;
    //Save a Word document as a Markdown file.
    document.Save("WordtoMd.md", FormatType.Markdown);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing Word document. 
Using document As WordDocument = New WordDocument("Input.docx")
 'Hook the event to customize the image. 
document.SaveOptions.ImageNodeVisited += SaveImage
 'Save a Word document as a Markdown file.
document.Save("WordtoMd.md", FormatType.Markdown)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO doesn’t support the ImageNodeVisitedEventArgs in UWP platform.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as a Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Hook the event to customize the image. 
        document.SaveOptions.ImageNodeVisited += SaveImage;
        //Save a Markdown file to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Markdown);
        outputStream.Position = 0;
        //Download as a Markdown file in the browser.
        FileStream outStream = File.Create("WordToMd.md");
        outputStream.CopyTo(outStream);
        outputStream.Dispose();
        outStream.Dispose();
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Hook the event to customize the image. 
        document.SaveOptions.ImageNodeVisited += SaveImage;
        //Save a Markdown file to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Markdown);
        //Save the stream as a file in the device and invoke it for viewing. 
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WordtoMd.md", "application/msword", outputStream);
    }
//Please download the helper files from the following link to save the stream as a file and open the file for viewing in the Xamarin platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}
{% endtabs %}

The following code examples show the event handler to customize the image path and save the image in an external folder.

{% tabs %}
{% highlight c# tabtitle="C#" %}
static void SaveImage(object sender, ImageNodeVisitedEventArgs args)
        {
            string imagepath = @"D:\Temp\Image1.png";
            //Save the image stream as a file. 
            using (FileStream fileStreamOutput = File.Create(imagepath))
                args.ImageStream.CopyTo(fileStreamOutput);
            //Set the image URI to be used in the output markdown.
            args.Uri = imagepath;
        }
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Shared Sub SaveImage(ByVal sender As Object, ByVal args As ImageNodeVisitedEventArgs)
Dim imagepath = "D:\Temp\Image1.png"
 'Save the image stream as a file. 
Using fileStreamOutput = File.Create(imagepath)
   args.ImageStream.CopyTo(fileStreamOutput)
End Using
'Set the URI to be used for the image in the output markdown. 
   args.Uri = imagepath
End Sub
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO doesn’t support the ImageNodeVisitedEventArgs in UWP platform.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
static void SaveImage(object sender, ImageNodeVisitedEventArgs args)
        {
            string imagepath = @"D:\Temp\Image1.png";
            //Save the image stream as a file.
            using (FileStream fileStreamOutput = File.Create(imagepath))
                args.ImageStream.CopyTo(fileStreamOutput);
            //Set the URI to be used for the image in the output Markdown. 
            args.Uri = imagepath;
        }
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
static void SaveImage(object sender, ImageNodeVisitedEventArgs args)
        {
            string imagepath = @"D:\Temp\Image1.png";
            //Save the image stream as a file. 
            using (FileStream fileStreamOutput = File.Create(imagepath))
                args.ImageStream.CopyTo(fileStreamOutput);
            //Set the URI to be used for the image in the output markdown. 
            args.Uri = imagepath;
        }
{% endhighlight %}
{% endtabs %}

## Supported Word document elements

The following table shows the list of Word document elements supported in Word to Markdown conversion.

### Body items

<table style="width: 760px;">
<thead>
<tr style="height: 13px;">
<td style="width: 182.986px; height: 13px;"><strong>Element in Word document</strong></td>
<td style="width: 557.014px; height: 13px;"><strong>Notes</strong></td>
</tr>
</thead>
<tbody>
<tr style="height: 13px;">
<td style="width: 182.986px; height: 13px;">Paragraph</td>
<td style="width: 557.014px; height: 13px;">Preserved as one line.</td>
</tr>
<tr style="height: 13px;">
<td style="width: 182.986px; height: 13px;">Table</td>
<td style="width: 557.014px; height: 13px;">
<ul>
<li>Preserves as per GitHub flavoured Markdown syntax.</li>
<li>Column alignment is based on alignment of first paragraph in cells of row.</li>
<li>Nested tables are not supported in Markdown, and they are merged with contents of parent cell.</li>
</ul>
</td>
</tr>
<tr style="height: 13px;">
<td style="width: 182.986px; height: 13px;">Block Content Control</td>
<td style="width: 557.014px; height: 13px;">Contents inside control controls are preserved as normal text. If the first item of the paragraph is a checkbox content control, then it preserves as a task item.</td>
</tr>
</tbody>
</table>

### Paragraph items

<table style="width: 760px;">
<thead>
<tr style="height: 13px;">
<td style="width: 262.889px; height: 13px;"><strong>Element in Word document</strong></td>
<td style="width: 479.111px; height: 13px;"><strong>Notes</strong></td>
</tr>
</thead>
<tbody>
<tr style="height: 13px;">
<td style="width: 262.889px; height: 13px;">Field</td>
<td style="width: 479.111px; height: 13px;">Field result is preserved.</td>
</tr>
<tr style="height: 13px;">
<td style="width: 262.889px; height: 13px;">Form Field</td>
<td style="width: 479.111px; height: 13px;">Result of text and dropdown form fields are preserved.</td>
</tr>
<tr style="height: 13px;">
<td style="width: 262.889px; height: 13px;">Hyperlink</td>
<td style="width: 479.111px; height: 13px;">-</td>
</tr>
<tr style="height: 13px;">
<td style="width: 262.889px; height: 13px;">Image</td>
<td style="width: 479.111px; height: 13px;">-</td>
</tr>
<tr style="height: 13px;">
<td style="width: 262.889px; height: 13px;">Horizontal rule</td>
<td style="width: 479.111px; height: 13px;">-</td>
</tr>
<tr style="height: 13px;">
<td style="width: 262.889px; height: 13px;">Content Control</td>
<td style="width: 479.111px; height: 13px;">
<p>Contents inside control controls are preserved as normal text.</p>
<p>If the first item of the paragraph is checkbox content control, then it preserves as a task item.</p>
</td>
</tr>
<tr style="height: 13.6667px;">
<td style="width: 262.889px; height: 13.6667px;">Breaks</td>
<td style="width: 479.111px; height: 13.6667px;">Line and text wrapping breaks are supported.</td>
</tr>
</tbody>
</table>

### Formatting

<table style="width: 760px;">
<thead>
<tr>
<td style="width: 318.625px;"><strong>Element in Word document</strong></td>
<td style="width: 424.375px;"><strong>Notes</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td style="width: 318.625px;">Bold</td>
<td style="width: 424.375px;">-</td>
</tr>
<tr>
<td style="width: 318.625px;">Italic</td>
<td style="width: 424.375px;">-</td>
</tr>
<tr>
<td style="width: 318.625px;">StrikeThrough</td>
<td style="width: 424.375px;">-</td>
</tr>
<tr>
<td style="width: 318.625px;">Subscript and Superscript</td>
<td style="width: 424.375px;">-</td>
</tr>
<tr>
<td style="width: 318.625px;">Hidden</td>
<td style="width: 424.375px;">Considered as comments in Markdown syntax</td>
</tr>
<tr>
<td style="width: 318.625px;">List</td>
<td style="width: 424.375px;">
<p>Numbered and bulleted lists are supported.</p>
<p>To restart numbering for the continuous list in the output markdown syntax, you should specify a non-empty paragraph in between the two lists in a Word document.</p>
</td>
</tr>
</tbody>
</table>