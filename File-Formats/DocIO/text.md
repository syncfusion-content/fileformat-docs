---
title: Word document to Text Conversion | DocIO | Syncfusion
description: This section illustrates how to perform Word document to Text conversion using Syncfusion Word library (Essential DocIO)
platform: file-formats
control: DocIO
documentation: UG
---

# Text Conversions in Word Library

The Essential DocIO converts the Word document into Text file and vice versa. The following code example shows how to convert the Word document into text file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Loads a template document
WordDocument document = new WordDocument("Template.docx");
//Saves the document as text file
document.Save("WordToText.txt", FormatType.Txt);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a text file
Dim document As New WordDocument("Template.docx")
'Saves the document as text file
document.Save("WordToText.txt", FormatType.Txt)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    MemoryStream stream = new MemoryStream();
    await document.SaveAsync(stream, FormatType.Txt);
    //Saves the stream as Word file in local machine
    Save(stream, "WordToText.txt");
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
        savePicker.DefaultFileExtension = ".txt";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".txt" });
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
    document.Save(stream, FormatType.Txt);
    //Closes the Word document
    document.Close();
    stream.Position = 0;
    //Download Word document in the browser
    return File(stream, "application/msword", "WordToText.txt");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Txt);
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>()
                        .SaveAndView("WordToText.txt", "application/msword", stream);
    //Closes the Word document
    document.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Text-file-conversion/Convert-Word-to-text-file).

The following code example shows how to convert a Text file into Word document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Loads a text file
WordDocument document = new WordDocument("Template.txt");
//Saves the document as text file
document.Save("TextToWord.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a text file
Dim document As New WordDocument("Template.txt")
'Saves the document as text file
document.Save("TextToWord.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.txt")),
              FormatType.Txt))
{
    MemoryStream stream = new MemoryStream();
    await document.SaveAsync(stream, FormatType.Docx);
    //Saves the stream as Word file in local machine
    Save(stream, "TextToWord.docx");
    //Closes the Word document
    document.Close();
}
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStreamPath = new FileStream("Template.txt", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Txt))
{
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Closes the Word document
    document.Close();
    stream.Position = 0;
    //Download Word document in the browser
    return File(stream, "application/msword", "TextToWord.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.txt")), FormatType.Txt))
{
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("TextToWord.docx", "application/msword", stream);
    //Closes the Word document
    document.Close();

    //Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Text-file-conversion/Convert-text-file-to-Word).

The following code example shows how to retrieve the Word document contents as a plain text.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Loads a template document
WordDocument document = new WordDocument("Template.docx");
//Gets the document text
string text = document.GetText();
//Creates new Word document
WordDocument newdocument = new WordDocument();
//Adds new section
IWSection section = newdocument.AddSection();
//Adds new paragraph
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the paragraph
paragraph.AppendText(text);
//Saves and closes the document
newdocument.Save("Sample.docx");
newdocument.Close();
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a template document
Dim document As New WordDocument("Template.docx")
'Gets the document text
Dim text As String = document.GetText()
'Creates new Word document
Dim newdocument As New WordDocument()
'Adds new section
Dim section As IWSection = newdocument.AddSection()
'Adds new paragraph
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends the text to the paragraph
paragraph.AppendText(text)
'Saves and closes the document
newdocument.Save("Sample.docx")
newdocument.Close()
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Gets the document text
    string text = document.GetText();
    //Creates new Word document
    WordDocument newdocument = new WordDocument();
    //Adds new section
    IWSection section = newdocument.AddSection();
    //Adds new paragraph
    IWParagraph paragraph = section.AddParagraph();
    //Appends the text to the paragraph
    paragraph.AppendText(text);
    MemoryStream stream = new MemoryStream();
    await newdocument.SaveAsync(stream, FormatType.Docx);
    //Saves the stream as Word file in local machine
    Save(stream, "Sample.docx");
    //Closes the Word document
    document.Close();
    newdocument.Close();
}
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Gets the document text
    string text = document.GetText();
    //Creates new Word document
    WordDocument newdocument = new WordDocument();
    //Adds new section
    IWSection section = newdocument.AddSection();
    //Adds new paragraph
    IWParagraph paragraph = section.AddParagraph();
    //Appends the text to the paragraph
    paragraph.AppendText(text);
    MemoryStream stream = new MemoryStream();
    newdocument.Save(stream, FormatType.Docx);
    //Closes the Word document
    document.Close();
    newdocument.Close();
    stream.Position = 0;
    //Download Word document in the browser
    return File(stream, "application/msword", "Sample.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")), FormatType.Docx))
{
    //Gets the document text
    string text = document.GetText();
    //Creates new Word document
    WordDocument newdocument = new WordDocument();
    //Adds new section
    IWSection section = newdocument.AddSection();
    //Adds new paragraph
    IWParagraph paragraph = section.AddParagraph();
    //Appends the text to the paragraph
    paragraph.AppendText(text);
    MemoryStream stream = new MemoryStream();
    newdocument.Save(stream, FormatType.Docx);
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
    //Closes the Word document
    newdocument.Close();
    document.Close();

    //Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Text-file-conversion/Retrieve-Word-document-as-plain-text).
