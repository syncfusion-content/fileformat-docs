---
title: Open PDF file from Azure blob storage | Syncfusion
description: This page describes how to Open PDF file from file azure blob storage in C#  using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Open PDF file from Azure Blob storage

To load a PDF file from Azure blob storage, you can follow the steps below


Step 1: Create a simple console application

![Project configuration window](Open-PDF-Images/Console-Application.png)

Step 3: Install the [Microsoft.Azure.Storage.Blob](https://www.nuget.org/packages/Microsoft.Azure.Storage.Blob) NuGet package as a reference to your project from the [NuGet.org](https://www.nuget.org/).

![NuGet package installation](Open-PDF-Images/Microsoft.Azure.Storage.Blob-nuget.png)


Step 4: Include the following namespaces in the Program.cs file.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

    using Microsoft.Azure.Storage;
    using Microsoft.Azure.Storage.Blob;

{% endhighlight %}

{% endtabs %}


Step 5: Add the below code example to load a PDF from Azure blob storage.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

    // Parse the connection string to your Azure Storage Account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

    // Create a client to interact with Blob storage.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to the container name.
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    // Get a reference to the block blob name.
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(blobName);
    
    // Open a file stream to save the downloaded blob content.
    using (var fileStream = File.OpenWrite("sample.pdf"))
    {
        // Download the blob's content to the file stream.
        blockBlob.DownloadToStream(fileStream);
    }

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Open-PDF-file/To%20Azure%20Blob%20Storage).
