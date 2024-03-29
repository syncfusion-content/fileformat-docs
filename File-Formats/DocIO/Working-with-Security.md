---
title: Working with Word document Protection | DocIO | Syncfusion
description: Learn how to encrypt, decrypt, and control changes by protecting the Word document using the .NET Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Security

You can encrypt a Word document with password to restrict unauthorized access. You can also control the types of changes you make to this document.

To quickly encrypt and decrypt a Word document with the .NET Word (DOCIO) Library, please check out this video:
{% youtube "https://www.youtube.com/watch?v=7EMtR2zrW80" %}

## Encrypting with password

The following code example shows how to encrypt the Word document with password.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens an existing document from stream through constructor of WordDocument class
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Automatic);
//Encrypts the Word document with a password
document.EncryptDocument("password");
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens an input Word document
WordDocument document = new WordDocument("Template.docx");
//Encrypts the Word document with a password
document.EncryptDocument("password");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens an input Word document
Dim document As New WordDocument("Template.docx")
'Encrypts the Word document with a password
document.EncryptDocument("password")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Security/Encrypt-Word-document-with-password).

## Opening the encrypted Word document

The following code example shows how to open the encrypted Word document. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens an existing document from stream through constructor of WordDocument class
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an encrypted Word document
WordDocument document = new WordDocument(fileStreamPath, "password");
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens an encrypted Word document
WordDocument document = new WordDocument ("Template.docx", "password");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens an encrypted Word document
Dim document As New WordDocument("Template.docx", "password")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument())
{
    //Loads or opens an existing Word document from stream
    Stream inputStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.doc");
    //Loads or opens an existing Word document through Open method of WordDocument class
    document.Open(inputStream, FormatType.Automatic, "password");
    MemoryStream stream = new MemoryStream();
    //Saves the Word file to MemoryStream
    await document.SaveAsync(stream, FormatType.Doc);
    //Saves the stream as Word file in local machine
    Save(stream, "Result.doc");
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
        savePicker.DefaultFileExtension = ".doc";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".doc"});
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Security/Open-encrypted-Word-document).

## Remove encryption

You can open the encrypted Word document and remove the encryption from the document. The following code example shows how to remove the encryption from encrypted Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens an existing document from stream through constructor of WordDocument class
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an encrypted Word document
WordDocument document = new WordDocument(fileStreamPath, "password");
//Removes encryption in Word document
document.RemoveEncryption();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens an encrypted Word document
WordDocument document = new WordDocument("Template.docx", "password");
//Removes encryption in Word document
document.RemoveEncryption();
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens an encrypted Word document
Dim document As New WordDocument("Template.docx", "password")
'Removes encryption in Word document
document.RemoveEncryption()
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Create new Word document instance
using (WordDocument document = new WordDocument())
{
    //Loads or opens an existing Word document from stream
    Stream inputStream = assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
    //Loads or opens an existing Word document using the Open method of WordDocument class
    document.Open(inputStream, FormatType.Docx, "password");
    //Removes encryption in Word document
    document.RemoveEncryption();
    MemoryStream stream = new MemoryStream();
    //Saves the Word file to MemoryStream
    document.Save(stream, FormatType.Docx);
    //Closes the Word document instance
    document.Close();
    //Saves the stream as Word file in local machine
    Save(stream, "Sample.Docx");
}
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Security/Remove-encryption-from-Word-document).

## Protecting Word document from editing

You can restrict a Word document from editing either by providing a password or without password. 

The following are the types of protection:

1. [AllowOnlyComments](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.ProtectionType.html): You can add/modify only the comments in the Word document.

2. [AllowOnlyFormFields](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.ProtectionType.html): You can modify the form field values in the Word document.

3. [AllowOnlyRevisions](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.ProtectionType.html): Allow only revisions to be made to existing content. After enabling this flag, accept and reject changes options in Microsoft Word application are disabled.

4. [AllowOnlyReading](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.ProtectionType.html): You can only view the content in the Word document.

5. [NoProtection](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.ProtectionType.html): You can access/edit the Word document contents as normally.

The following code example shows how to restrict editing to modify only form fields in a Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Sets the protection with password and it allows only to modify the form fields type
    document.Protect(ProtectionType.AllowOnlyFormFields, "password"); 
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.docx);
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens a Word document
WordDocument document = new WordDocument(@"Template.docx");
//Sets the protection with password and it allows only to modify the form fields type
document.Protect(ProtectionType.AllowOnlyFormFields, "password"); 
//Saves the Word document
document.Save("Protection.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a Word document
Dim document As New WordDocument("Template.docx")
'Sets the protection with password and it allows only to modify the form fields type
document.Protect(ProtectionType.AllowOnlyFormFields, "password")
'Saves the Word document
document.Save("Protection.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Security/Allow-editing-form-fields-only).
