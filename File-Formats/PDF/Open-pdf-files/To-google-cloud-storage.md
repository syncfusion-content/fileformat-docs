---
title: Load PDF file to Google cloud storage | Syncfusion
description: This page describes how to Load PDF file from google cloud storage in C#  using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Open PDF file to Google Cloud storage

To Open a PDF file from Google cloud storage, you can follow the steps below


Step 1: Create a simple console application

![Project configuration window](Open-PDF-Images/Console-Application.png)

Step 3: Install the [Google.Cloud.Storage.V1](https://www.nuget.org/packages/Google.Cloud.Storage.V1) NuGet package as a reference to your project from the [NuGet.org](https://www.nuget.org/).

![NuGet package installation](Open-PDF-Images/Google.Cloud.Storage.V1-nuget.png)


Step 4: Include the following namespaces in the Program.cs file.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

        using Google.Cloud.Storage.V1;
        using Google.Apis.Auth.OAuth2;

{% endhighlight %}

{% endtabs %}


Step 5: Add the below code example to create a simple PDF and save in Google cloud storage.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

        // Create a byte array
        byte[] pdfBytes;
        // Load the credentials file
        GoogleCredential credential = GoogleCredential.FromFile("credentials.json");
        // Create a storage client
        StorageClient storage = StorageClient.Create(credential);
        // Download the PDF from Google Cloud Storage
        using (MemoryStream stream = new MemoryStream())
        {
            storage.DownloadObject("bucket50247", "Sample.pdf", stream);
            pdfBytes = stream.ToArray();
        }

        string filePath = "Sample.pdf";

        // Write the byte array to a PDF file
        File.WriteAllBytes(filePath, pdfBytes);

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from GitHub.
