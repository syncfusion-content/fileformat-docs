---
title: Protect the zip files with password | Syncfusion
description: This page demonstrates how to protect the zip files with password using Syncfusion.Compression.Base.
platform: File-formats
control: XlsIO
documentation: UG
---

# How to protect the zip files using Syncfusion.Compression.Base?

Password is used for protecting files which needs more security. This can be achieved by using various encryption algorithms. The compressed zip files can be protected using encryption algorithms with password as a key for that algorithm. 

Syncfusion.Compression.Base supports AES-128 bits, AES-192 bits, AES-256 bits and ZipCrypto encryption algorithms. These encryption algorithms are available under the enumeration **EncryptionAlgorithm**.

The following complete code snippet explains how to protect a zip file with password using AES-256 bits encryption algorithm.

{% tabs %}
{% highlight c# %}
using Syncfusion.Compression.Zip;

class Program
{
  static void Main(string[] args)
  {
    //Initialize ZipArchive
    ZipArchive zipArchive = new ZipArchive();

    //Add files into ZipArchive
    zipArchive.AddFile("../../Data/Template1.txt");
    zipArchive.AddFile("../../Data/Template2.txt");
    zipArchive.AddFile("../../Data/Template3.txt");

    //Protect the ZipArchive with password
    zipArchive.Protect("password", EncryptionAlgorithm.AES256);

    //Save the ZipArchive
    zipArchive.Save("WithPassword256Bit.zip");
  }
}
{% endhighlight %}

{% highlight vb %}
Imports Syncfusion.Compression.Zip

Module Module1
  Sub Main()
    'Initialize ZipArchive
    Dim zipArchive As ZipArchive = New ZipArchive

    'Add files into ZipArchive
    zipArchive.AddFile("../../Data/Template1.txt")
    zipArchive.AddFile("../../Data/Template2.txt")
    zipArchive.AddFile("../../Data/Template3.txt")

    'Protect the ZipArchive with password
    zipArchive.Protect("password", EncryptionAlgorithm.AES256)

    'Save the ZipArchive
    zipArchive.Save("WithPassword256Bit.zip")
  End Sub
End Module
{% endhighlight %}
{% endtabs %}

## See Also

* [How to un-protect the zip files using Syncfusion.Compression.Base?](how-to-un-protect-the-zip-files-using-syncfusion-compression-base)
* [How to zip files using the Syncfusion.Compression.Zip namespace?](how-to-zip-files-using-the-syncfusion-compression-zip-namespace)
* [How to zip all the files in subfolders using Syncfusion Compression?](how-to-zip-all-the-files-in-subfolders-using-syncfusion-compression)
* [How to protect certain cells in a worksheet?](how-to-protect-certain-cells-in-a-worksheet)
* [How to protect Excel workbook?](https://help.syncfusion.com/file-formats/xlsio/migrate-from-office-automation-to-syncfusion-xlsio/protect-excel-workbook)
* [How to protect worksheet?](https://help.syncfusion.com/file-formats/xlsio/security#protect-worksheet)
