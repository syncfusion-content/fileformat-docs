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

![Create an Azure Functions project in visual studio](Azure_Images/Functions_v4/Create_Application.png)

Step 2: Name the project.

![Name the project](Azure_Images/Functions_v4/Name_the_Application_Image.png)

Step 3: Select functions worker as **.NET (6.0) Long Term Support**. 

![Select functions worker](Azure_Images/Functions_v4/Functions_Worker.png)

Step 4: Install the [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.XlsIORenderer.Net.Core NuGet package](Azure_Images/Functions_v4/Install_NuGet_Image.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components. 

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

  //Initialize XlsIO renderer.
  application.XlsIORenderer = new XlsIORenderer();

  //Gets the input Excel document as stream from request.
  Stream excelStream = req.Content.ReadAsStreamAsync().Result;

  //Load the stream into IWorkbook.
  IWorkbook workbook = application.Workbooks.Open(excelStream);
  IWorksheet worksheet = workbook.Worksheets[0];

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

![Publish](Azure_Images/Functions_v4/Publish_Image.png)

Step 8: Select the publish target as **Azure**.

![Add a Publish Profile](Azure_Images/Functions_v4/Publish_Profile.png)

Step 9: Select the Specific target as **Azure Function App (Windows)**.

![Select the publish target](Azure_Images/Functions_v4/Windows_Function_App.png)

Step 10: Select the **Create new** button.

![Click create new option](Azure_Images/Functions_v4/Create_New.png)

Step 11: Click the **Create** button to proceed with creation. 

![Hosting](Azure_Images/Functions_v4/Hosting_Image.png)

Step 12: Click the **Finish** button to finalize the **Azure Function** creation. 

![Creating app service](Azure_Images/Functions_v4/Azure_Function_Image.png)

Step 13: Click **Close** button.

![Profile created](Azure_Images/Functions_v4/Profile_Created_Image.png)

Step 14: Click the **Publish** button.

![Click Publish Button](Azure_Images/Functions_v4/Start_Publish_Image.png)

Step 15: Publish has been succeeded.

![Publish succeeded](Azure_Images/Functions_v4/Publish_Success_Image.png)

Step 16: Now, go to Azure portal and select the App Services. After running the service, click **Get function URL by copying it**. Then, paste it in the below client sample (which will request the Azure Functions, to perform **Excel to Image conversion** using the template Excel document). You will get the output image as follows.

![Output File](Azure_Images/Functions_v4/ExcelToImage_Function_v4.png)

## Steps to post the request to Azure Functions

Step 1: Create a console application to request the Azure Functions API.

Step 2: Add the following code snippet into **Main** method to post the request to Azure Functions with template Excel document and get the resultant image.
{% tabs %}
{% highlight c# tabtitle="C#" %}
//Reads the template Excel document.
FileStream excelStream = new FileStream("../../Sample.xlsx", FileMode.Open, FileAccess.Read);
excelStream.Position = 0;

//Saves the Excel document in memory stream.
MemoryStream inputStream = new MemoryStream();
excelStream.CopyTo(inputStream);
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
  FileStream outStream = File.Create("Sample.jpeg");
  res.GetResponseStream().CopyTo(outStream);

  //Dispose the streams
  inputStream.Dispose();
  outStream.Dispose();
}
catch (Exception ex)
{
    throw;
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Azure%20V4%20Function/Convert%20Excel%20to%20Image). 

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net-core) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to Image](https://ej2.syncfusion.com/aspnetcore/Excel/WorksheetToImage#/material3) in ASP.NET Core.
