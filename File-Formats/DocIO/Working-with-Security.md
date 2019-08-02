---
title: Working with Security | DocIO | Syncfusion
description: This section illustrate how to encrypt and protect the Word document
platform: file-formats
control: DocIO
documentation: UG
---
# Security

You can encrypt a Word document with password to restrict unauthorized access. You can also control the types of changes you make to this document.

## Encrypting with password

The following code example shows how to encrypt the Word document with password.

{% tabs %}  

{% highlight c# %}


//Opens an input Word document

WordDocument document = new WordDocument("Template.docx");

//Encrypts the Word document with a password

document.EncryptDocument("password");

//Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vb.net %}


'Opens an input Word document

Dim document As New WordDocument("Template.docx")

'Encrypts the Word document with a password

document.EncryptDocument("password")

‘Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

{% endtabs %}  

## Opening the encrypted Word document

The following code example shows how to open the encrypted Word document. 

{% tabs %}  

{% highlight c# %}

//Opens an encrypted Word document

WordDocument document = new WordDocument ("Template.docx", "password");

//Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vb.net %}

'Opens an encrypted Word document

Dim document As New WordDocument("Template.docx", "password")

‘Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %} 

{% highlight UWP %}

//"App" is the class of Portable project.

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

using (WordDocument document = new WordDocument())

{

/Loads or opens an existing Word document from stream

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

// Saves the Word document
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

// Write compressed data from memory to file

using (Stream outstream = zipStream.AsStreamForWrite())

{

byte[] buffer = streams.ToArray();

outstream.Write(buffer, 0, buffer.Length);

outstream.Flush();

}

}

}

// Launch the saved Word file

await Windows.System.Launcher.LaunchFileAsync(stFile);

}

{% endhighlight %}

{% endtabs %}  

  
  
## Protecting Word document from editing

You can restrict a Word document from editing either by providing a password or without password. 

The following are the types of protection:

1. `AllowOnlyComments`: You can add/modify only the comments in the Word document.

2. `AllowOnlyFormFields`: You can modify the form field values in the Word document.

3. `AllowOnlyRevisions`: You can accept or reject the revisions in the Word document.

4. `AllowOnlyReading`: You can only view the content in the Word document.

5. `NoProtection`: You can access/edit the Word document contents as normally.

The following code example shows how to restrict editing to modify only form fields in a Word document.

{% tabs %}  

{% highlight c# %}


//Opens a Word document

WordDocument document = new WordDocument(@"Template.docx");

//Sets the protection with password and it allows only to modify the form fields type

document.Protect(ProtectionType.AllowOnlyFormFields, "password"); 

//Saves the Word document

document.Save("Protection.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vb.net %}


'Opens a Word document

Dim document As New WordDocument("Template.docx")

'Sets the protection with password and it allows only to modify the form fields type

document.Protect(ProtectionType.AllowOnlyFormFields, "password")

'Saves the Word document

document.Save("Protection.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

{% highlight ASP.NET CORE %}

FileStream fileStreamPath = new FileStream(@"Data/Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))

{

//Sets the protection with password and it allows only to modify the form fields type

document.Protect(ProtectionType.AllowOnlyFormFields, "password"); 

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.docx);

//Closes the Word document

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "Protection.docx");

}



{% endhighlight %}

{% highlight UWP %}

//"App" is the class of Portable project.

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx")),
              FormatType.Docx))
{

//Sets the protection with password and it allows only to modify the form fields type

document.Protect(ProtectionType.AllowOnlyFormFields, "password"); 

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream, FormatType.Docx);

//Saves the stream as Word file in local machine

Save(stream, "Protection.docx");
                
//Closes the Word document

document.Close();

}

// Saves the Word document

async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".docx;

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".docx"});

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

// Write compressed data from memory to file

using (Stream outstream = zipStream.AsStreamForWrite())

{

byte[] buffer = streams.ToArray();

outstream.Write(buffer, 0, buffer.Length);

outstream.Flush();

}

}

}

// Launch the saved Word file

await Windows.System.Launcher.LaunchFileAsync(stFile);

}

}

}

{% endhighlight %}

{% highlight Xamarin %}

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx")),
              FormatType.Docx))
{

//Sets the protection with password and it allows only to modify the form fields type

document.Protect(ProtectionType.AllowOnlyFormFields, "password"); 

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Docx);

//Save the stream as a file in the device and invoke it for viewing

Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("Protection.docx", "application/msword", stream);

//Closes the Word document

document.Close();

}

{% endhighlight %}

{% endtabs %}  