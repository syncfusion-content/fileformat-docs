---
title: Open PDF file from AWS S3 | Syncfusion
description: This page describes how to Open PDF file from file AWS S3 in C#  using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Open PDF file from AWS S3

To load a PDF file from AWS S3, you can follow the steps below


Step 1: Create a simple console application

![Project configuration window](Open-PDF-Images/Console-Application.png)

Step 3: Install the [AWSSDK.S3](https://www.nuget.org/packages/AWSSDK.S3) NuGet package as a reference to your project from the [NuGet.org](https://www.nuget.org/).

![NuGet package installation](Open-PDF-Images/AWSSDK.S3-nuget.png)


Step 4: Include the following namespaces in the Program.cs file.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

    using Amazon;
    using Amazon.S3;
    using Amazon.S3.Transfer;

{% endhighlight %}

{% endtabs %}


Step 5: Add the below code example to load a PDF from AWS S3.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

    // Set your AWS credentials and region
    string accessKey = "YOUR_ACCESS_KEY";
    string secretKey = "YOUR_SECRET_KEY";
    RegionEndpoint region = RegionEndpoint.YOUR_REGION; // Change to your desired region

    // Specify the bucket name and object key
    string bucketName = "YOUR_BUCKET_NAME";
    string objectKey = "YOUR_OBJECT_KEY"; 

    string localFilePath = "Output.pdf";
    // Download the PDF from S3
    //MemoryStream pdfStream = DownloadFromS3(accessKey, secretKey, region, bucketName, objectKey);
    using (var s3Client = new AmazonS3Client(accessKey, secretKey, region))
    {
        using (var transferUtility = new TransferUtility(s3Client))
        {   
            transferUtility.Download(localFilePath, bucketName, objectKey);
        }
    }

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from GitHub.
