---
title: Upload a file to Azure blob and download as stream | Syncfusion
description: This page shows how to upload an Excel file to Azure blob and download it as stream.
platform: file-formats
control: XlsIO
documentation: UG
---

# How to upload a file to Azure blob and download as stream?

The following code snippet shows how to upload an Excel file to Azure blob and download it as stream.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
public static class Function1
{
  [FunctionName("Function1")]
  public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req, ILogger log)
  {
    using FileStream uploadFileStream = File.OpenRead("Sample.xlsx");

    var accountName = "Account Name";
    var accountKey = "Account Key";

    StorageSharedKeyCredential sharedKeyCredential = new StorageSharedKeyCredential(accountName, accountKey);

    string blobUri = "https://" + accountName + ".blob.core.windows.net";

    BlobServiceClient blobServiceClient = new BlobServiceClient(new Uri(blobUri), sharedKeyCredential);

    BlobContainerClient containerClient = blobServiceClient.GetBlobContainerClient("Container Name");

    var filename = "AzureFile_Upload.xlsx";

    BlobClient blobClientUpload = containerClient.GetBlobClient(filename);
    await blobClientUpload.UploadAsync(uploadFileStream, true);

    MemoryStream readStream = new MemoryStream();
    BlobClient blobClientRead = containerClient.GetBlobClient(filename);
    await blobClientRead.DownloadToAsync(readStream);

    readStream.Position = 0;

    FileStream outputStream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.Write);
    readStream.CopyTo(outputStream);

    return new OkObjectResult("done");
  }
}
{% endhighlight %}
{% endtabs %}