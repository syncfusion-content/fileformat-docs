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

How to protect the zip files using Syncfusion.Compression.Base?
How to zip files using the Syncfusion.Compression.Zip namespace?
How to zip all the files in subfolders using Syncfusion's Compression?
How to protect certain cells in a worksheet?
[Unprotect Excel Workbook](https://help.syncfusion.com/file-formats/xlsio/migrate-from-office-automation-to-syncfusion-xlsio/unprotect-excel-workbook)
[Protect Worksheet](https://help.syncfusion.com/file-formats/xlsio/security#protect-worksheet)
