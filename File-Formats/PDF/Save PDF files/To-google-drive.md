---
title: Save PDF file to Google Drive | Syncfusion
description: This page describes how to save PDF file to file google drive in C#  using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Save PDF file to Google Drive

To save a PDF file to Google Drive, you can follow the steps below

Step 1: Set up Google Drive API

You must set up a project in the Google Developers Console and enable the Google Drive API. Obtain the necessary credentials to access the API. For more information, view the official [link](https://developers.google.com/drive/api/guides/enable-sdk).

Step 2: Create a simple console application

![Project configuration window](Save-PDF-Images/Console-Application.png)

Step 3: Install the [Syncfusion.Pdf.Net.Core ](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core) and [Google.Apis.Drive.v3](https://www.nuget.org/packages/Google.Apis.Drive.v3) NuGet packages as a reference to your project from the [NuGet.org](https://www.nuget.org/).
![NuGet package installation](Save-PDF-Images/Syncfusion.Pdf.Net.Core-nuget.png)
<br><br>
![NuGet package installation](Save-PDF-Images/Google.Apis.Drive.V3-nuget.png)


Step 4: Include the following namespaces in the Program.cs file.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

using Syncfusion.Pdf;
using Syncfusion.Pdf.Graphics;
using Google.Apis.Auth.OAuth2;
using Google.Apis.Drive.v3;
using Google.Apis.Services;
using Google.Apis.Util.Store;
using File = Google.Apis.Drive.v3.Data.File;
using Syncfusion.Drawing;

{% endhighlight %}

{% endtabs %}


Step 5: Add the below code example to create a simple PDF and save in google drive.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

// Step 1: Create a new PDF document and add a page
PdfDocument document = new PdfDocument();
PdfPage page = document.Pages.Add();
PdfGraphics graphics = page.Graphics;
// Draw "Hello, World!" text on the page
graphics.DrawString("Hello, World!", new PdfStandardFont(PdfFontFamily.Helvetica, 12), PdfBrushes.Black, new PointF(10, 10));

// Step 2: Save the PDF to a MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);
document.Close(true);

// Step 3: Authenticate with Google Drive
UserCredential credential;
string[] Scopes = { DriveService.Scope.Drive };
string ApplicationName = "YourAppName";
using (var stream1 = new FileStream("credentials.json", FileMode.Open, FileAccess.Read))// Replace with your actual credentials.json

{
    string credPath = "token.json";
    // Authorize using Google Web Authorization Broker
    credential = GoogleWebAuthorizationBroker.AuthorizeAsync(
        GoogleClientSecrets.Load(stream1).Secrets,
        Scopes,
        "user",
        CancellationToken.None,
        new FileDataStore(credPath, true)).Result;
}

// Step 4: Create Drive API service
var service = new DriveService(new BaseClientService.Initializer()
{
    HttpClientInitializer = credential,
    ApplicationName = ApplicationName,
});

// Step 5: Upload the PDF to Google Drive
var fileMetadata = new File()
{
    Name = "Sample.pdf", // Name of the file in Google Drive
    MimeType = "application/pdf",
};

FilesResource.CreateMediaUpload request;
using (var fs = new MemoryStream(stream.ToArray()))
{
    // Create an upload request
    request = service.Files.Create(fileMetadata, fs, "application/pdf");
    request.Upload();
}

File file = request.ResponseBody;

Console.WriteLine("File ID: " + file.Id);


{% endhighlight %}

{% endtabs %}

You can download a complete working sample from GitHub.
