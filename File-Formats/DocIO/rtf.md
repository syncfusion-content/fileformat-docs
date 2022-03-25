---
title: RTF conversions | DocIO | Syncfusion
description: This section illustrates how to perform RTF to Word conversion and Word to RTF conversions using Syncfusion Word library (Essential DocIO)
platform: file-formats
control: DocIO
documentation: UG
---

# RTF Conversions in Word Library

## RTF
The [Rich Text Format (RTF)](http://en.wikipedia.org/wiki/Rich_Text_Format#) is one of the document formats supported by Microsoft Word and many other Word processing applications. RTF is human readable file format invented for interchanging formatted text between applications. It is an optional format for Word that retains most formatting and all content of the original document.

Most of the Word processors (including Microsoft Word) uses the XML-based file formats, Microsoft has discontinued enhancements to the RTF and still supporting it. The last version was 1.9.1 released in 2008.

The Essential DocIO converts the RTF document into Word document and vice versa. The following code shows how to convert RTF document into Word document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Loads an existing document
WordDocument document = new WordDocument("Input.rtf", FormatType.Rtf);
//Saves the Word document as RTF file
document.Save("RtfToWord.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads an existing document
Dim document As New WordDocument("Input.rtf", FormatType.Rtf)
'Saves the Word document as RTF file
document.Save("RtfToWord.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Input.rtf")),
              FormatType.Rtf))
{
    MemoryStream stream = new MemoryStream();
    await document.SaveAsync(stream, FormatType.Docx);
    //Saves the stream as Word file in local machine
    Save(stream, "RtfToWord.docx");
    //Closes the Word document
    document.Close();
}
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStreamPath = new FileStream("Input.rtf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Rtf))
{
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Closes the Word document
    document.Close();
    stream.Position = 0;
    //Download Word document in the browser
    return File(stream, "application/msword", "RtfToWord.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Input.rtf")),
              FormatType.Rtf))
{
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>()
                        .SaveAndView("RtfToWord.docx", "application/msword", stream);
    //Closes the Word document
    document.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/RTF-conversion/Convert-RTF-to-Word).

The following code example shows how to convert Word document into RTF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Loads an existing document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Saves the Word document as RTF file
document.Save("WordToRtf.rtf", FormatType.Rtf);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads an existing document
Dim document As New WordDocument("Template.docx", FormatType.Docx)
'Saves the Word document as RTF file
document.Save("WordToRtf.rtf", FormatType.Rtf)
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
    await document.SaveAsync(stream, FormatType.Rtf);
    //Saves the stream as Word file in local machine
    Save(stream, "WordToRtf.rtf");
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
        savePicker.DefaultFileExtension = ".rtf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".rtf" });
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
    document.Save(stream, FormatType.Rtf);
    //Closes the Word document
    document.Close();
    stream.Position = 0;
    //Download Word document in the browser
    return File(stream, "application/msword", "WordToRtf.rtf");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")), FormatType.Docx))
{
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Rtf);
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WordToRtf.rtf", "application/msword", stream);
    //Closes the Word document
    document.Close();
	
    //Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/RTF-conversion/Convert-Word-to-RTF).

## Supported and Unsupported features
The supported and unsupported features of DocIO based on file formats can be referred [here](https://help.syncfusion.com/file-formats/docio/supported-and-unsupported-features#)