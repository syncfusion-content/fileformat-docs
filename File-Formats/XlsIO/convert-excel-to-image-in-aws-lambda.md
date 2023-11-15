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

![Create AWS Lambda Project in visual studio](AWS_Images/Lambda_Images/Create_Application.png)

Step 2: Name the application.

![Name the application](AWS_Images/Lambda_Images/Name_the_Application_Image.png)

Step 3: Select Blueprint as Empty Function and click **Finish**.

![Select Blueprint](AWS_Images/Lambda_Images/Empty_Function.png)

Step 4: Install the following **NuGet packages** in your application from [Nuget.org](https://www.nuget.org/).

* [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core) 
* [SkiaSharp.NativeAssets.Linux v2.88.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.2)
* [HarfBuzzSharp.NativeAssets.Linux v2.8.2.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.2)

![Install Syncfusion.XlsIORenderer.Net.Core NuGet package](AWS_Images/Lambda_Images/Install_NuGet_Image.png)
![Install SkiaSharp.NativeAssets.Linux NuGet package](AWS_Images/Lambda_Images/SkiaSharp_NuGet_Image.png)
![Install HarfBuzzSharp.NativeAssets.Linux NuGet package](AWS_Images/Lambda_Images/HarfBuzz_NuGet_Image.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Create a folder and copy the required data files and include the files to the project.

![Create data folder](AWS_Images/Lambda_Images/Data_Folder_Image.png)

Step 6: Set the **copy to output directory** to **Copy if newer** to all the data files.

![File properties](AWS_Images/Lambda_Images/Data_Properties_Image.png)

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

![Publish](AWS_Images/Lambda_Images/Publish_Image.png)

Step 10: Create a new AWS profile in the Upload Lambda Function Window. After creating the profile, add a name for the Lambda function to publish. Then, click **Next**.

![Upload](AWS_Images/Lambda_Images/Upload.png)

Step 11: In the Advanced Function Details window, specify the **Role Name** as based on AWS Managed policy. After selecting the role, click the **Upload** button to deploy your application.

![Advanced function details](AWS_Images/Lambda_Images/Advanced_Function_Details.png)

Step 12: After deploying the application, you can see the published Lambda function in **AWS console**.

![AWS Console](AWS_Images/Lambda_Images/AWS_Console.png)

Step 13: Edit Memory size and Timeout as maximum in Basic settings of the AWS Lambda function.

![Basic Settings](AWS_Images/Lambda_Images/Basic_Settings.png)

## Steps to post the request to AWS Lambda

Step 1: Create a new console project.

![Create console application in visual studio](AWS_Images/Lambda_Images/Console_Application.png)

step 2: Install the following **NuGet packages** in your application from [Nuget.org](https://www.nuget.org/).

* [AWSSDK.Core](https://www.nuget.org/packages/AWSSDK.Core/)
* [AWSSDK.Lambda](https://www.nuget.org/packages/AWSSDK.Lambda/)
* [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)

![Install AWSSDK.Core NuGet package](AWS_Images/Lambda_Images/Core_NuGet.png)
![Install AWSSDK.Lambda NuGet package](AWS_Images/Lambda_Images/Lambda_NuGet.png)
![Install Newtonsoft.Json NuGet package](AWS_Images/Lambda_Images/Newtonsoft_NuGet.png)

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

![Output File](AWS_Images/Lambda_Images/ExcelToImage_AWS_Lambda.png)

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net-core) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to Image](https://ej2.syncfusion.com/aspnetcore/Excel/WorksheetToImage#/material3) in ASP.NET Core.
