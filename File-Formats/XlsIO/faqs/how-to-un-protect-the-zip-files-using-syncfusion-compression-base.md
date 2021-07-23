---
title: FAQ Section| XlsIO | Syncfusion
description: This page demonstrates with an example to un-protect the zip files using Syncfusion.Compression.Base.
platform: File-formats
control: XlsIO
documentation: UG
---

# How to un-protect the zip files using Syncfusion.Compression.Base?

The following complete code snippet explains how to unprotect the zip file.

{% tabs %}
{% highlight c# %}
using Syncfusion.Compression.Zip;
using System.IO;

class Program
{
  static void Main(string[] args)
  {
    //Initailize ZipArchive
    ZipArchive zipArchive = new ZipArchive();

    //Load the zip file into ZipArchive
    zipArchive.Open(new FileStream("../../Data/Protected.zip", FileMode.Open), false, "password");

    //Unprotect the ZipArchive
    zipArchive.UnProtect();

    //Save the ZipArchive
    zipArchive.Save("WithOutPassword.zip");
  }
}
{% endhighlight %}

{% highlight vb %}
Imports Syncfusion.Compression.Zip
Imports System.IO

Module Module1
  Sub Main()
    'Initailize ZipArchive
    Dim zipArchive As ZipArchive = New ZipArchive

    'Load the zip file into ZipArchive
    zipArchive.Open(New FileStream("../../Data/Protected.zip", FileMode.Open), False, "password")

    'Unprotect the ZipArchive
    zipArchive.UnProtect()

    'Save the ZipArchive
    zipArchive.Save("WithOutPassword.zip")
  End Sub
End Module
{% endhighlight %}
{% endtabs %}

## See Also

* [How to protect the zip files using Syncfusion.Compression.Base?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-protect-the-zip-files-using-syncfusion-compression-base)
* [How to zip files using the Syncfusion.Compression.Zip namespace?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-zip-files-using-the-syncfusion-compression-zip-namespace)
* [How to zip all the files in subfolders using Syncfusion Compression?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-zip-all-the-files-in-subfolders-using-syncfusion-compression)
* [How to protect certain cells in a worksheet?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-protect-certain-cells-in-a-worksheet)
* [How to unprotect Excel workbook?](https://help.syncfusion.com/file-formats/xlsio/migrate-from-office-automation-to-syncfusion-xlsio/unprotect-excel-workbook)
* [How to protect worksheet?](https://help.syncfusion.com/file-formats/xlsio/security#protect-worksheet)
