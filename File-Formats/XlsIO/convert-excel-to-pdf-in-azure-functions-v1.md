---
title: Convert Excel to PDF in Azure Functions v1 | Syncfusion
description: Convert Excel to PDF in Azure Functions v1 using .NET Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel document to PDF in Azure Functions v1

Syncfusion XlsIO is a [.NET Excel library](https://www.syncfusion.com/document-processing/excel-framework/net) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in Azure Functions v1**.

## Steps to convert an Excel document to PDF in Azure Functions v1

Step 1: Create a new Azure Functions project.
<img src="Azure_Images/Functions_v1/Create_Application.png" alt="Create an Azure Functions project" width="100%" Height="Auto"/>

Step 2: Name the project.
<img src="Azure_Images/Functions_v1/Name_the_Application.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Select functions worker as **.NET Framework v1**. 
<img src="Azure_Images/Functions_v1/Functions_Worker.png" alt="Select functions worker" width="100%" Height="Auto"/>

Step 4: Install the [Syncfusion.ExcelToPdfConverter.WinForms](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.WinForms) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
<img src="Azure_Images/Functions_v1/Install_NuGet.png" alt="Install Syncfusion.ExcelToPdfConverter.WinForms NuGet package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components. 

Step 5: Include the following namespaces in the **Function1.cs** file.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.ExcelToPdfConverter;
using Syncfusion.Pdf;
{% endhighlight %}
{% endtabs %}

Step 6: Add the following code snippet in **Run** method of **Function1** class to perform **Excel to PDF conversion** in Azure Functions and return the resultant **PDF document** to client end.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Gets the input Excel document as stream from request.
  Stream excelStream = req.Content.ReadAsStreamAsync().Result;

  //Load the stream into IWorkbook.
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize ExcelToPdfConverter
  ExcelToPdfConverter excelToPdfConverter = new ExcelToPdfConverter(workbook);

  //Convert Excel document into PDF document 
  PdfDocument pdfDocument = excelToPdfConverter.Convert();

  //Create the MemoryStream to save the converted PDF.      
  MemoryStream pdfStream = new MemoryStream();

  //Save the converted PDF document to MemoryStream.
  pdfDocument.Save(pdfStream);
  pdfStream.Position = 0;

  //Create the response to return.
  HttpResponseMessage response = new HttpResponseMessage(HttpStatusCode.OK);

  //Set the PDF document saved stream as content of response.
  response.Content = new ByteArrayContent(pdfStream.ToArray());

  //Set the contentDisposition as attachment.
  response.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment")
  {
    FileName = "Sample.pdf"
  };

  //Set the content type as PDF document mime type.
  response.Content.Headers.ContentType = new MediaTypeHeaderValue("application/pdf");

  //Return the response with output PDF document stream.
  return response;
}
{% endhighlight %}
{% endtabs %}

Step 6: Right-click the project and select **Publish** option.
<img src="Azure_Images/Functions_v1/Publish.png" alt="Publish" width="100%" Height="Auto"/>

Step 7: Select the publish target as **Azure**.
<img src="Azure_Images/Functions_v1/Publish_Profile.png" alt="Add a Publish Profile" width="100%" Height="Auto"/>

Step 8: Select the **Create new** button.
<img src="Azure_Images/Functions_v1/Create_New.png" alt="Click create new option" width="100%" Height="Auto"/>

Step 9: Click the **Create** button to proceed with creation. 
<img src="Azure_Images/Functions_v1/Hosting.png" alt="Hosting" width="100%" Height="Auto"/>

Step 10: Click the **Finish** button to finalize the **Azure Function** creation. 
<img src="Azure_Images/Functions_v1/Azure_Function.png" alt="Creating app service" width="100%" Height="Auto"/>

Step 11: Click **Close** button.
<img src="Azure_Images/Functions_v1/Profile_Created.png" alt="Profile created" width="100%" Height="Auto"/>

Step 12: Click the **Publish** button.
<img src="Azure_Images/Functions_v1/Start_Publish.png" alt="Click Publish Button" width="100%" Height="Auto"/>

Step 13: Publish has been succeeded.
<img src="Azure_Images/Functions_v1/Publish_Success.png" alt="Publish succeeded" width="100%" Height="Auto"/>

Step 14: Now, go to Azure portal and select the App Services. After running the service, click **Get function URL by copying it**. Then, paste it in the below client sample (which will request the Azure Functions, to perform **Excel to PDF conversion** using the template Excel document). You will get the output PDF document as follows.
<img src="Azure_Images/Functions_v1/ExcelToPDF_Function_v1.png" alt="Excel to PDF in Azure Functions v1" width="100%" Height="Auto"/>

## Steps to post the request to Azure Functions

Step 1: Create a console application to request the Azure Functions API.

Step 2: Add the following code snippet into **Main** method to post the request to Azure Functions with template Excel document and get the resultant PDF document.
{% tabs %}
{% highlight c# tabtitle="C#" %}
//Reads the template Excel document.
FileStream excelStream = new FileStream("../../../Sample.xlsx", FileMode.Open, FileAccess.Read);
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

  //Saves the PDF stream.
  FileStream pdfStream = File.Create("Sample.pdf");
  res.GetResponseStream().CopyTo(pdfStream);

  //Dispose the streams
  inputStream.Dispose();
  pdfStream.Dispose();
}
catch (Exception ex)
{
    throw;
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Azure%20V1%20Function/Convert%20Excel%20to%20PDF). 

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net-core) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://ej2.syncfusion.com/aspnetcore/Excel/ExcelToPDF#/material3) in ASP.NET Core.
