---
title: FAQ Section| XlsIO | Syncfusion
description: This page demonstrates with an example on how to zip files using the Syncfusion.Compression.Zip namespace.
platform: File-formats
control: XlsIO
documentation: UG
---

# How to zip files using the Syncfusion.Compression.Zip namespace?

You can compress the file using Syncfusion.Compression.Zip namespace. The following code illustrate this.

{% tabs %}  

{% highlight c# %}
using Syncfusion.Compression.Zip;

ZipArchive zipArchive = new Syncfusion.Compression.Zip.ZipArchive();

zipArchive.DefaultCompressionLevel = Syncfusion.Compression.CompressionLevel.Best;

//Add the file you want to zip.

zipArchive.AddFile("SampleFile.cs");

//Zip file name and location.

zipArchive.Save("SyncfusionCompressFileSample.zip");

zipArchive.Close();



{% endhighlight %}

{% highlight vb %}
Imports Syncfusion.Compression.Zip

Dim zipArchive As ZipArchive = New Syncfusion.Compression.Zip.ZipArchive()

zipArchive.DefaultCompressionLevel = Syncfusion.Compression.CompressionLevel.Best

'Add the file you want to zip.

zipArchive.AddFile("SampleFile.cs")

'Zip file name and location.

zipArchive.Save("SyncfusionCompressFileSample.zip")

zipArchive.Close()



{% endhighlight %}

  {% endtabs %}  

T>You can use CompressionLevel to reduce the size of the file.  

For compressing directories, you can make use of the **AddDirectory** method which adds an empty directory file to a ZipArchive. If you want to add all the files inside the directory, then you should manually add these files by using the **AddItem** method.

The following code snippet illustrate how to add the file from the local drive.

{% tabs %}  

{% highlight c# %}
string fileName = @"SampleFile.cs";

ZipArchive zipArchive = new Syncfusion.Compression.Zip.ZipArchive();

zipArchive.DefaultCompressionLevel =CompressionLevel.Best;

Stream stream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

FileAttributes attributes = File.GetAttributes(fileName);

ZipArchiveItem item = new ZipArchiveItem(zipArchive, "SampleFile.cs", stream, true, attributes);

zipArchive.AddItem(item);

zipArchive.Save(@"SyncfusionCompressFileSample.zip");

zipArchive.Close();



{% endhighlight %}

{% highlight vb %}
Dim fileName As String = "SampleFile.cs"

Dim zipArchive As ZipArchive = New Syncfusion.Compression.Zip.ZipArchive()

zipArchive.DefaultCompressionLevel = CompressionLevel.Best

Dim stream As Stream = New FileStream(fileName, FileMode.Open, FileAccess.Read)

Dim attributes As FileAttributes = File.GetAttributes(fileName)

Dim item As New ZipArchiveItem(zipArchive, "SampleFile.cs", stream, True, attributes)

zipArchive.AddItem(item)

zipArchive.Save("SyncfusionCompressFileSample.zip")

zipArchive.Close()



{% endhighlight %}

  {% endtabs %}  

 
## See Also

How to zip all the files in subfolders using Syncfusion's Compression?
How to protect the zip files using Syncfusion.Compression.Base?
How to un-protect the zip files using Syncfusion.Compression.Base?
How to merge Excel files from more than one workbook to a single file?

