---
title: Converting Word document to ODT format | DocIO | Syncfusion
description: This section explains on what is ODT & Converting Word document to ODT format using Syncfusion Word library (Essential DocIO)
platform: file-formats
control: DocIO
documentation: UG
---

# Converting Word to ODT format

The [OpenDocument format (ODF)](http://en.wikipedia.org/wiki/OpenDocument#) is an open file format for office documents originally developed for Open Office suite by Sun Microsystems. OpenDocument Text (ODT) is the file format for Word processing documents and currently for an OASIS and ISO standard.

The Essential DocIO supports converting the Word document into ODT file. The following code example shows how to convert the Word document into ODT file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Loads the existing Word document
WordDocument document = new WordDocument("Template.docx");
//Saves the document as ODT file
document.Save("WordToODT.odt", FormatType.Odt);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the existing Word document 
Dim document As New WordDocument("Template.docx")
'Saves the document as ODT file
document.Save("WordToODT.odt", FormatType.Odt)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    MemoryStream stream = new MemoryStream();
    await document.SaveAsync(stream, FormatType.Odt);
    //Saves the stream as Word file in local machine
    Save(stream, "WordToODT.odt");
    //Closes the Word document
    document.Close();
}

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".odt";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".odt" });
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

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Odt);
    //Closes the Word document
    document.Close();
    stream.Position = 0;
    //Download Word document in the browser
    return File(stream, "application/msword", "WordToODT.odt");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")), FormatType.Docx))
{
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Odt);
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>()
                        .SaveAndView("WordToODT.odt", "application/msword", stream);
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% endtabs %}

## Supported Document elements
<table>
<thead> 
<tr>
<th>Document Element</th>
<th>Attribute</th>
<th>Support Status</th>
<th>Notes</th>
</tr>
</thead>
<tr>
<td>
Bookmark<br/><br/></td>
<td>
Id<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td colspan="1" rowspan="4">
<br/><br/><br/><br/><br/><br/><br/>Border<br/><br/><br/></td>
<td>
Color<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Distance from text<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Line style<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Line width<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Document Properties<br/><br/></td>
<td>
<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Field<br/><br/></td>
<td>
<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
For some of the fields, the field results have been preserved as span text.
</td>
</tr>
<tr>
<td>
Footnotes and Endnotes<br/><br/></td>
<td>
<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Form Field<br/><br/></td>
<td>
<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Header / Footer<br/><br/></td>
<td>
Different per section<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td colspan="1" rowspan="2">
<br/><br/>Hyperlink<br/><br/><br/></td>
<td>
External URL<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Local<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td colspan="1" rowspan="2">
<br/><br/>Image<br/><br/><br/></td>
<td>
Inline<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Scale<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td colspan="1" rowspan="5">
<br/><br/><br/><br/><br/><br/><br/><br/><br/>List<br/><br/><br/><br/><br/><br/></td>
<td>
Custom bullets<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Multi-level<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Numbered<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Restart numbering<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Standard bullets<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Comment<br/><br/></td>
<td>
<br/><br/></td>
<td>
No<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
Symbols<br/><br/></td>
<td>
<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
Paragraph<br/><br/></td>
<td>
Alignment<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Borders<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
See Borders, for more details.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Keep lines and paragraphs together<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Paragraph Indents<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Line spacing<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Page break before<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Shading<br/><br/></td>
<td>
No<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Spacing before and after<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Shading<br/><br/></td>
<td>
Background color<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>

</td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Foreground color<br/><br/></td>
<td>
No<br/><br/></td>
<td>

</td>
</tr>
<tr>
<td>
Styles<br/><br/></td>
<td>
Paragraph styles<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Character styles<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
List styles<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Table<br/><br/></td>
<td>
Alignment<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Cell margins<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Column widths<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Indent from left<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Preferred width<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Spacing between cells<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Borders<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
See Borders, for more details.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Shading<br/><br/></td>
<td>
No<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
Nested Table<br/><br/></td>
<td>
<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
Table Cell<br/><br/></td>
<td>
Borders<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
See Borders, for more details.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Cell margins<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Horizontal merge<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Shading<br/><br/></td>
<td>
No<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Vertical alignment<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Vertical merge<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Table Row<br/><br/></td>
<td>
Height<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Padding<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Text<br/><br/></td>
<td>
All caps<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Bold<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Character spacing<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Color<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Emboss<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
Rendered as bold.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Engrave<br/><br/></td>
<td>
No<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Font<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Hidden<br/><br/></td>
<td>
No<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Highlighting<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Italic<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Line breaks<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Outline<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
Rendered as bold.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Page breaks<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Shading<br/><br/></td>
<td>
No<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Small caps<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Special symbols<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Strike out<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Subscript / Superscript<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Underline<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>

</td>
</tr>
</table>
