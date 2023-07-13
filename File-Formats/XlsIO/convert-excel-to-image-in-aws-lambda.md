---
title: Convert Excel to Image in AWS Lambda | Syncfusion
description: Convert Excel to Image in AWS Lambda using .NET Core Excel (XlsIO) library without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel document to Image in AWS Lambda

Syncfusion XlsIO is a [.NET Core Excel library](https://www.syncfusion.com/document-processing/excel-framework/net-core) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert a Excel document to Image in AWS Lambda**.

## Steps to convert Excel document to Image in AWS Lambda

Step 1: Create a new **AWS Lambda project** as follows.
<img src="AWS_Images/Lambda_Images/Create_Application.png" alt="Create AWS Lambda Project" width="100%" Height="Auto"/>

Step 2: Name the application.
<img src="AWS_Images/Lambda_Images/Name_the_Application_Image.png" alt="Name the application" width="100%" Height="Auto"/>

Step 3: Select Blueprint as Empty Function and click **Finish**.
<img src="AWS_Images/Lambda_Images/Empty_Function.png" alt="Select Blueprint" width="100%" Height="Auto"/>

Step 4: Install the following **NuGet packages** in your application from [Nuget.org](https://www.nuget.org/).

* [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core) 
* [SkiaSharp.NativeAssets.Linux v2.88.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.2)
* [HarfBuzzSharp.NativeAssets.Linux v2.8.2.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.2)

<img src="AWS_Images/Lambda_Images/Install_NuGet_Image.png" alt="Install Syncfusion.XlsIORenderer.Net.Core NuGet package" width="100%" Height="Auto"/>
<img src="AWS_Images/Lambda_Images/SkiaSharp_NuGet_Image.png" alt="Install SkiaSharp.NativeAssets.Linux NuGet package" width="100%" Height="Auto"/>
<img src="AWS_Images/Lambda_Images/HarfBuzz_NuGet_Image.png" alt="Install HarfBuzzSharp.NativeAssets.Linux NuGet package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Create a folder and copy the required data files and include the files to the project.
<img src="AWS_Images/Lambda_Images/Data_Folder_Image.png" alt="Create data folder" width="100%" Height="Auto"/>

Step 6: Set the **copy to output directory** to **Copy if newer** to all the data files.
<img src="AWS_Images/Lambda_Images/Data_Properties_Image.png" alt="File properties" width="100%" Height="Auto"/>

Step 7: Include the following namespaces in **Function.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.XlsIORenderer;
{% endhighlight %}
{% endtabs %}

step 8: Add the following code snippet in **Function.cs** to convert an Excel document to Image.

{% tabs %}
{% highlight c# tabtitle="C#" %}
public string FunctionHandler(string input, ILambdaContext context)
{
  using (ExcelEngine excelEngine = new ExcelEngine())
  {
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Initialize XlsIO renderer.
    application.XlsIORenderer = new XlsIORenderer();

    FileStream excelStream = new FileStream(@"Data/Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(excelStream);
    IWorksheet worksheet = workbook.Worksheets[0];
            
    //Create the MemoryStream to save the image.      
    MemoryStream imageStream = new MemoryStream();

    //Save the converted image to MemoryStream.
    worksheet.ConvertToImage(worksheet.UsedRange, imageStream);
    imageStream.Position = 0;
    return Convert.ToBase64String(imageStream.ToArray());
  }
}
{% endhighlight %}
{% endtabs %}

Step 9: Right-click the project and select **Publish to AWS Lambda**.
<img src="AWS_Images/Lambda_Images/Publish_Image.png" alt="Publish" width="100%" Height="Auto"/>

Step 10: Create a new AWS profile in the Upload Lambda Function Window. After creating the profile, add a name for the Lambda function to publish. Then, click **Next**.
<img src="AWS_Images/Lambda_Images/Upload.png" alt="Upload" width="100%" Height="Auto"/>

Step 11: In the Advanced Function Details window, specify the **Role Name** as based on AWS Managed policy. After selecting the role, click the **Upload** button to deploy your application.
<img src="AWS_Images/Lambda_Images/Advanced_Function_Details.png" alt="Advanced function details" width="100%" Height="Auto"/>

Step 12: After deploying the application, you can see the published Lambda function in **AWS console**.
<img src="AWS_Images/Lambda_Images/AWS_Console.png" alt="AWS Console" width="100%" Height="Auto"/>

Step 13: Edit Memory size and Timeout as maximum in Basic settings of the AWS Lambda function.
<img src="AWS_Images/Lambda_Images/Basic_Settings.png" alt="Basic Settings" width="100%" Height="Auto"/>

## Steps to post the request to AWS Lambda

Step 1: Create a new console project.
<img src="AWS_Images/Lambda_Images/Console_Application.png" alt="Create console application" width="100%" Height="Auto"/>

step 2: Install the following **NuGet packages** in your application from [Nuget.org](https://www.nuget.org/).

* [AWSSDK.Core](https://www.nuget.org/packages/AWSSDK.Core/)
* [AWSSDK.Lambda](https://www.nuget.org/packages/AWSSDK.Lambda/)
* [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)

<img src="AWS_Images/Lambda_Images/Core_NuGet.png" alt="Install AWSSDK.Core NuGet package" width="100%" Height="Auto"/>
<img src="AWS_Images/Lambda_Images/Lambda_NuGet.png" alt="Install AWSSDK.Lambda NuGet package" width="100%" Height="Auto"/>
<img src="AWS_Images/Lambda_Images/Newtonsoft_NuGet.png" alt="Install Newtonsoft.Json NuGet package" width="100%" Height="Auto"/>

Step 3: Include the following namespaces in **Program.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using Amazon;
using Amazon.Lambda;
using Amazon.Lambda.Model;
using Newtonsoft.Json;
{% endhighlight %}
{% endtabs %}

Step 4: Add the following code snippet in **Program.cs** to invoke the published AWS Lambda function using the function name and access keys.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Create a new AmazonLambdaClient
AmazonLambdaClient client = new AmazonLambdaClient("awsaccessKeyID", "awsSecreteAccessKey", RegionEndpoint.USEast2);
 
//Create new InvokeRequest with published function name.
InvokeRequest invoke = new InvokeRequest
{
  FunctionName = "MyNewFunction",
  InvocationType = InvocationType.RequestResponse,
  Payload = "\"Test\""
};

//Get the InvokeResponse from client InvokeRequest.
InvokeResponse response = client.Invoke(invoke);
 
//Read the response stream
var stream = new StreamReader(response.Payload);
JsonReader reader = new JsonTextReader(stream);
var serilizer = new JsonSerializer();
var responseText = serilizer.Deserialize(reader);

//Convert Base64String into Image
byte[] bytes = Convert.FromBase64String(responseText.ToString());
FileStream fileStream = new FileStream("Sample.jpeg", FileMode.Create);
BinaryWriter writer = new BinaryWriter(fileStream);
writer.Write(bytes, 0, bytes.Length);
writer.Close();
System.Diagnostics.Process.Start("Sample.jpeg");
{% endhighlight %}
{% endtabs %}

By executing the program, you will get the **Image** as follows.

<img src="AWS_Images/Lambda_Images/ExcelToImage_AWS_Lambda.png" alt="Excel to Image converted document" width="100%" Height="Auto"/>

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net-core) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to Image](https://ej2.syncfusion.com/aspnetcore/Excel/WorksheetToImage#/material3) in ASP.NET Core.
