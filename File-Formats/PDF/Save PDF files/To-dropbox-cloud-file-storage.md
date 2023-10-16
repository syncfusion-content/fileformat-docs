---
title: Save PDF file to Dropbox cloud file storage| Syncfusion
description: This page describes how to save PDF file to  Dropbox cloud file storage in C#  using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Save PDF file to Dropbox cloud file storage

To save a PDF file to Dropbox cloud file storage, you can follow the steps below

Step 1: Create a Dropbox API


To create a Dropbox API App, you should follow the official documentation provided by Dropbox [link](https://www.dropbox.com/developers/documentation/dotnet#tutorial). The process involves visiting the Dropbox Developer website and using their App Console to set up your API app. This app will allow you to interact with Dropbox programmatically, enabling secure access to files and data.



Step 2: Create a simple console application
![Project configuration window](Save-PDF-Images/Console-Application.png)

Step 3: Install the [Syncfusion.Pdf.Net.Core ](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core) and [Dropbox.Api](https://www.nuget.org/packages/Dropbox.Api) NuGet packages as a reference to your project from the [NuGet.org](https://www.nuget.org/).

![NuGet package installation](Save-PDF-Images/Syncfusion.Pdf.Net.Core-nuget.png)<br><br>
![NuGet package installation](Save-PDF-Images/Dropbox.Api-nuget.png)

Step 4: Include the following namespaces in the Program.cs file.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

using Syncfusion.Pdf.Graphics;
using Syncfusion.Pdf;
using Dropbox.Api;
using Dropbox.Api.Files;
using Syncfusion.Drawing;

{% endhighlight %}

{% endtabs %}


Step 5: Add the below code example to create a simple PDF and save in Dropbox cloud file storage.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

PdfDocument doc = new PdfDocument();
PdfPage page = doc.Pages.Add();

PdfGraphics graphics = page.Graphics;
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12);

graphics.DrawString("Hello, World!", font, PdfBrushes.Black, new PointF(10, 10));

// Add more content if needed...

// Save the PDF to a memory stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);
doc.Close(true);

var accessToken = "YOUR_ACCESS_TOKEN";// Replace with your actual access token

using (var dbx = new DropboxClient(accessToken))
{
    var uploadResult = await dbx.Files.UploadAsync(
        "/path/to/save/yourfile.pdf",
        WriteMode.Overwrite.Instance,
        body: new MemoryStream(stream.ToArray()));
    Console.WriteLine("Saved to Dropbox as " + uploadResult.PathDisplay);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from GitHub.
