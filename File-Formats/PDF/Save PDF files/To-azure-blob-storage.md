---
title: Save PDF file to Azure blob storage | Syncfusion
description: This page describes how to save PDF file to file azure blob storage in C#  using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Save PDF file to Azure Blob storage

To save a PDF file to Azure blob storage, you can follow the steps below


Step 1: Create a simple console application

![Project configuration window](Save-PDF-Images/Console-Application.png)

Step 3: Install the [Syncfusion.Pdf.Net.Core ](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core) and [Microsoft.Azure.Storage.Blob](https://www.nuget.org/packages/Microsoft.Azure.Storage.Blob) NuGet packages as a reference to your project from the [NuGet.org](https://www.nuget.org/).
![NuGet package installation](Save-PDF-Images/Syncfusion.Pdf.Net.Core-nuget.png)
<br><br>
![NuGet package installation](Save-PDF-Images/Microsoft.Azure.Storage.Blob-nuget.png)


Step 4: Include the following namespaces in the Program.cs file.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

using Syncfusion.Pdf;
using Syncfusion.Pdf.Graphics;
using Syncfusion.Drawing;
using Microsoft.Azure.Storage;
using Microsoft.Azure.Storage.Blob;

{% endhighlight %}

{% endtabs %}


Step 5: Add the below code example to create a simple PDF and save in google drive.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

using (PdfDocument doc = new PdfDocument())
{
    PdfPage page = doc.Pages.Add();
    PdfGraphics graphics = page.Graphics;
    PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12);
    graphics.DrawString("Hello, World!", font, PdfBrushes.Black, new PointF(10, 10));
    MemoryStream stream = new MemoryStream();
    doc.Save(stream);
    File.WriteAllBytes("output.pdf", stream.ToArray());
}
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
container.CreateIfNotExists();

CloudBlockBlob blockBlob = container.GetBlockBlobReference(blobName);
using (var fileStream = System.IO.File.OpenRead("sample.pdf"))
{
    blockBlob.UploadFromStream(fileStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from GitHub.
