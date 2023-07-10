---
title: Convert Excel to Image in Azure Functions v4 | Syncfusion
description: Convert Excel to Image in Azure Functions v4 using .NET Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel document to Image in Azure Functions v4

Syncfusion XlsIO is a [.NET Excel library](https://www.syncfusion.com/document-processing/excel-framework/net) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to Image in Azure Functions v4**.

## Steps to convert an Excel document to Image in Azure Functions v4

Step 1: Create a new Azure Functions project.
<img src="Azure_Images/Functions_v4/Create_Application.png" alt="Create an Azure Functions project" width="100%" Height="Auto"/>

Step 2: Name the project.
<img src="Azure_Images/Functions_v4/Name_the_Application_Image.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Select functions worker as **.NET (6.0) Long Term Support**. 
<img src="Azure_Images/Functions_v4/Functions_Worker.png" alt="Select functions worker" width="100%" Height="Auto"/>

Step 4: Install the [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
<img src="Azure_Images/Functions_v4/Install_NuGet_Image.png" alt="Install Syncfusion.XlsIORenderer.Net.Core NuGet package" width="100%" Height="Auto"/>

Step 5: Include the following namespaces in the **Function1.cs** file.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.XlsIORenderer;
{% endhighlight %}
{% endtabs %}

Step 6: Add the following code snippet in **Run** method of **Function1** class to perform **Excel to Image conversion** in Azure Functions and return the resultant **image** to client end.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize XlsIO renderer.
  application.XlsIORenderer = new XlsIORenderer();

  //Create the MemoryStream to save the image.      
  MemoryStream imageStream = new MemoryStream();

  //Save the converted image to MemoryStream.
  worksheet.ConvertToImage(worksheet.UsedRange, imageStream);
  imageStream.Position = 0;
  
  //Create the response to return.
  HttpResponseMessage response = new HttpResponseMessage(HttpStatusCode.OK);

  //Set the image saved stream as content of response.
  response.Content = new ByteArrayContent(imageStream.ToArray());

  //Set the contentDisposition as attachment.
  response.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment")
  {
    FileName = "Sample.jpeg"
  };

  //Set the content type as image mime type.
  response.Content.Headers.ContentType = new MediaTypeHeaderValue("application/jpeg");

  //Return the response with output image stream.
  return response;
}
{% endhighlight %}
{% endtabs %}

Step 7: Right-click the project and select **Publish** option.
<img src="Azure_Images/Functions_v4/Publish_Image.png" alt="Publish" width="100%" Height="Auto"/>

Step 8: Select the publish target as **Azure**.
<img src="Azure_Images/Functions_v4/Publish_Profile.png" alt="Add a Publish Profile" width="100%" Height="Auto"/>

Step 9: Select the Specific target as **Azure Function App (Windows)**.
<img src="Azure_Images/Functions_v4/Windows_Function_App.png" alt="Select the publish target" width="100%" Height="Auto"/>

Step 10: Select the **Create new** button.
<img src="Azure_Images/Functions_v4/Create_New.png" alt="Click create new option" width="100%" Height="Auto"/>

Step 11: Click the **Create** button to proceed with creation. 
<img src="Azure_Images/Functions_v4/Hosting_Image.png" alt="Hosting" width="100%" Height="Auto"/>

Step 12: Click the **Finish** button to finalize the **Azure Function** creation. 
<img src="Azure_Images/Functions_v4/Azure_Function_Image.png" alt="Creating app service" width="100%" Height="Auto"/>

Step 13: Click **Close** button.
<img src="Azure_Images/Functions_v4/Profile_Created_Image.png" alt="Profile created" width="100%" Height="Auto"/>

Step 14: Click the **Publish** button.
<img src="Azure_Images/Functions_v4/Start_Publish_Image.png" alt="Click Publish Button" width="100%" Height="Auto"/>

Step 15: Publish has been succeeded.
<img src="Azure_Images/Functions_v4/Publish_Success_Image.png" alt="Publish succeeded" width="100%" Height="Auto"/>

Step 16: Now, go to Azure portal and select the App Services. After running the service, click **Get function URL by copying it**. Then, paste it in the below client sample (which will request the Azure Functions, to perform **Excel to Image conversion** using the template Excel document). You will get the output image as follows.
<img src="Azure_Images/Functions_v4/ExcelToImage_Function_v4.png" alt="Excel to Image in Azure Functions v4" width="100%" Height="Auto"/>

## Steps to post the request to Azure Functions

Step 1: Create a console application to request the Azure Functions API.

Step 2: Add the following code snippet into **Main** method to post the request to Azure Functions with template Excel document and get the resultant image.
{% tabs %}
{% highlight c# tabtitle="C#" %}
//Reads the template Excel document.
FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
fileStream.Position = 0;

//Saves the Excel document in memory stream.
MemoryStream inputStream = new MemoryStream();
fileStream.CopyTo(inputStream);
inputStream.Position = 0;

try
{
  Console.WriteLine("Please enter your Azure Functions URL :");
  string functionURL = Console.ReadLine();

  //Create HttpWebRequest with hosted azure functions URL.                
  HttpWebRequest req = (HttpWebRequest)WebRequest.Create(functionURL);

  //Set request method as POST
  req.Method = "POST";

  //Get the request stream to save the Excel document stream
  Stream stream = req.GetRequestStream();

  //Write the Excel document stream into request stream
  stream.Write(inputStream.ToArray(), 0, inputStream.ToArray().Length);

  //Gets the responce from the Azure Functions.
  HttpWebResponse res = (HttpWebResponse)req.GetResponse();

  //Saves the image stream.
  FileStream fileStream = File.Create("Sample.jpeg");
  res.GetResponseStream().CopyTo(fileStream);

  //Dispose the streams
  inputStream.Dispose();
  fileStream.Dispose();
}
catch (Exception ex)
{
    throw;
}
{% endhighlight %}
{% endtabs %}
