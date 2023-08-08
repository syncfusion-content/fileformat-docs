---
title: Convert HTML to PDF in AWS | Syncfusion
description: Learn how to convert HTML to PDF in AWS with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in AWS using C#

The Syncfusion [HTML to PDF converter](https://www.syncfusion.com/pdf-framework/net/html-to-pdf) is a .NET library for converting webpages, SVG, MHTML, and HTML to PDF using C#. The result preserves all graphics, images, text, fonts, and the layout of the original HTML document or webpage. Using this library, you can convert HTML to PDF using C# with Blink rendering engine in AWS.

## Setting up the AWS Toolkit for Visual Studio

* You can create an AWS account by referring to this [link](https://aws.amazon.com/).
* Download and install the AWS Toolkit for Visual Studio, you can download the AWS toolkit from this [link](https://aws.amazon.com/visualstudio/).
* The Toolkit can be installed from Tools/Extension and updates options in Visual Studio. 

Refer to the following steps to convert HTML to PDF in AWS Lambda

* Create an AWS Lambda function to convert HTML to PDF and publish it to AWS.
* Invoke the AWS Lambda function in your main application using AWS SDKs.

## AWS Lambda

**Steps to convert HTML to PDF in AWS Lambda**

Step 1: Create a new AWS Lambda project as follows.
![Convert HTMLToPDF AWS Step1](htmlconversion_images/AWS1.png)
 
Step 2: In configuration window, name the project and select Create.
![Convert HTMLToPDF AWS Step2](htmlconversion_images/AWS2.png)

Step 3: Select Blueprint as Empty Function and click Finish.
![Convert HTMLToPDF AWS Step3](htmlconversion_images/AWS3.png)

Step 4: Install the [Syncfusion.HtmlToPdfConverter.Net.Aws](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Aws/) NuGet package as a reference to your AWS lambda project from [NuGet.org.](https://www.nuget.org/)
![NuGet package installation](htmlconversion_images/AWS4.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Using the following namespaces in the *Function.cs* file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;
using System.IO;

{% endhighlight %}

Step 6: Add the following code snippet in Function.cs to convert HTML to PDF document using [Convert](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html#Syncfusion_HtmlConverter_HtmlToPdfConverter_Convert_System_String_) method in [HtmlToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html) class.

{% highlight c# tabtitle="C#" %}

//Initialize HTML to PDF converter with Blink rendering engine.
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert URL to PDF.
PdfDocument document = htmlConverter.Convert(input);
//Save the document into stream.
MemoryStream memoryStream = new MemoryStream();
//Save and Close the PDF Document.
document.Save(memoryStream);
document.Close(true);
return Convert.ToBase64String(memoryStream.ToArray());

{% endhighlight %}

Step 7: Right-click the project and select Publish to AWS Lambda. 
![Convert HTMLToPDF AWS Step5](htmlconversion_images/AWS5.png)

Step 8: Create a new AWS profile in the Upload Lambda Function Window. After creating the profile, add a name for the Lambda function to publish. Then, click Next.   
![Convert HTMLToPDF AWS Step6](htmlconversion_images/AWS6.png)   

Step 9: In the Advanced Function Details window, specify the Role Name as based on AWS Managed policy. After selecting the role, click the Upload button to deploy your application.
![Convert HTMLToPDF AWS Step7](htmlconversion_images/AWS7.png)     

Step 10: After deploying the application, Sign in your AWS account and you can see the published Lambda function in AWS console. 
![Convert HTMLToPDF AWS Step8](htmlconversion_images/AWS8.png)    

**Steps to invoke the AWS Lambda function from the console application**

Step 1: Create a new console project.  
![Convert HTMLToPDF AWS Step9](htmlconversion_images/AWS9.png)    

Step 2: In project configuration windows, name the project and select Create.
![Convert HTMLToPDF AWS Step10](htmlconversion_images/AWS10.png)   

Step 3: Install the [AWSSDK.Core](https://www.nuget.org/packages/AWSSDK.Core), [AWSSDK.Lambda](https://www.nuget.org/packages/AWSSDK.Lambda) and [Newtonsoft.Json package](https://www.nuget.org/packages/Newtonsoft.Json/13.0.2-beta3) as a reference to your main application from the [NuGet.org](https://www.nuget.org/).    
![Convert HTMLToPDF AWS Step11](htmlconversion_images/AWS11.png)    
 
Step 4: Include the following namespaces in Program.cs file.

{% highlight c# tabtitle="C#" %}

using Amazon;
using Amazon.Lambda;
using Amazon.Lambda.Model;
using Newtonsoft.Json;
using System.IO;

{% endhighlight %}

Step 5: Add the following code snippet in Program class to invoke the published AWS Lambda function using the function name and access keys.

{% highlight c# tabtitle="C#" %}

//Create a new AmazonLambdaClient
AmazonLambdaClient client = new AmazonLambdaClient("awsaccessKeyID", "awsSecreteAccessKey", RegionEndpoint.USEast1);
//Create new InvokeRequest with the published function name
InvokeRequest invoke = new InvokeRequest
{
    FunctionName = "AwsLambdaFunctionHtmlToPdfConversion",
    InvocationType = InvocationType.RequestResponse,
    Payload = "\" https://www.google.co.in/ \""
};
//Get the InvokeResponse from client InvokeRequest
InvokeResponse response = client.Invoke(invoke);
//Read the response stream
var stream = new StreamReader(response.Payload);
JsonReader reader = new JsonTextReader(stream);
var serilizer = new JsonSerializer();
var responseText = serilizer.Deserialize(reader);
//Convert Base64String into PDF document
byte[] bytes = Convert.FromBase64String(responseText.ToString());
FileStream fileStream = new FileStream("Sample.pdf", FileMode.Create);
BinaryWriter writer = new BinaryWriter(fileStream);
writer.Write(bytes, 0, bytes.Length);
writer.Close();
System.Diagnostics.Process.Start("Sample.pdf");

{% endhighlight %}
 
By executing the program, you will get the PDF document as follows. 
![Convert HTMLToPDF AWS Step12](htmlconversion_images/AWS12.png)  

A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/AWS).

## AWS Lambda with NET 6 container image

**Steps to convert HTML to PDF in AWS Lambda with NET 6 container image**

Step 1: Create a new AWS Lambda project with Tests as follows.
![Convert HTMLToPDF AWS Lambda Step1](htmlconversion_images/awslambda1.png)

Step 2: In configuration window, name the project and select Create.
![Convert HTMLToPDF AWS Lambda Step2](htmlconversion_images/awslambda2.png)

Step 3: Select Blueprint as .NET 6 (Container Image) Function and click Finish.
![Convert HTMLToPDF AWS Lambda Step3](htmlconversion_images/awslambda3.png)

Step 4: Install the [Syncfusion.HtmlToPdfConverter.Net.Aws](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Aws/) and [AWSSDK.Lambda](https://www.nuget.org/packages/AWSSDK.Lambda) NuGet package as a reference to your AWS lambda project from [NuGet.org](https://www.nuget.org/).
![NuGet package installation](htmlconversion_images/awslambda4.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Using the following namespaces in the Function.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;
using System.IO;

{% endhighlight %}

Step 6: Add the following code sample in the Function.cs to convert HTML to PDF document using [Convert](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html#Syncfusion_HtmlConverter_HtmlToPdfConverter_Convert_System_String_) method in [HtmlToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html) class. The Blink command line arguments based on the given [CommandLineArguments](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html#Syncfusion_HtmlConverter_BlinkConverterSettings_CommandLineArguments) property of [BlinkConverterSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html) class.

{% highlight c# tabtitle="C#" %}

public string FunctionHandler(string input, ILambdaContext context)
{
   //Initialize HTML to a PDF converter with the Blink rendering engine.
   HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);
       
   BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();
   blinkConverterSettings.BlinkPath = Path.GetFullPath("BlinkBinariesAws");
   blinkConverterSettings.CommandLineArguments.Add("--no-sandbox");
   blinkConverterSettings.CommandLineArguments.Add("--disable-setuid-sandbox");
   blinkConverterSettings.AdditionalDelay = 3000;
   htmlConverter.ConverterSettings = blinkConverterSettings;
 
   //Convert the HTML string to PDF.
   PdfDocument document = htmlConverter.Convert(input, PathToFile());        
 
   //Save the document into a stream.
   MemoryStream memoryStream = new MemoryStream();
   //Save and close the PDFDocument.
   document.Save(memoryStream);
   document.Close(true);
   string base64 = Convert.ToBase64String(memoryStream.ToArray());
   memoryStream.Close();
   memoryStream.Dispose();
 
   return base64;
}

public static string PathToFile()
{
   string? path = System.IO.Path.GetDirectoryName(System.Reflection.Assembly.GetExecutingAssembly().GetName().CodeBase);
   if (string.IsNullOrEmpty(path))
   {
      path = Environment.OSVersion.Platform == PlatformID.Unix ? @"/" : @"\";
   }
   return Environment.OSVersion.Platform == PlatformID.Unix ? string.Concat(path.Substring(5), @"/") : string.Concat(path.Substring(6), @"\");
}

{% endhighlight %}

Step 7: Create a new folder as Helper and add a class file as AWSHelper.cs. Add the following namespaces and code samples in the AWSHelper class to invoke the published AWS Lambda function using the function name and access keys.

{% highlight c# tabtitle="C#" %}

Using Amazon.Lambda;
using Amazon.Lambda.Model;
using Newtonsoft.Json;

public class AWSHelper
{
   public static async Task<byte[]> RunLambdaFunction(string html)
   {
      try
      {
         var AwsAccessKeyId = "awsaccessKeyID";
         var AwsSecretAccessKey = "awsSecretAccessKey";
 
         AmazonLambdaClient client = new AmazonLambdaClient(AwsAccessKeyId, AwsSecretAccessKey, Amazon.RegionEndpoint.USEast1);
         InvokeRequest invoke = new InvokeRequest
         {
            FunctionName = "AWSLambdaDockerContainer",
            InvocationType = InvocationType.RequestResponse,
            Payload = Newtonsoft.Json.JsonConvert.SerializeObject(html)
         };
         //Get the InvokeResponse from the client InvokeRequest.
         InvokeResponse response = await client.InvokeAsync(invoke);
 
         //Read the response stream.
         Console.WriteLine($"Response: {response.LogResult}");
         Console.WriteLine($"Response: {response.StatusCode}");
         Console.WriteLine($"Response: {response.FunctionError}");
         var stream = new StreamReader(response.Payload);
         JsonReader reader = new JsonTextReader(stream);
         var serilizer = new JsonSerializer();
         var responseText = serilizer.Deserialize(reader);
 
         //Convert Base64String into a PDF document.
         return Convert.FromBase64String(responseText.ToString());
      }
      catch (Exception ex)
      {
          Console.WriteLine($"Exception Occured HTMLToPDFHelper: {ex}");
      }
   return Convert.FromBase64String("");
   }
}

{% endhighlight %}

Step 8: Right-click the project and select **Publish to AWS Lambda**.

![Convert HTMLToPDF AWS Lambda Step5](htmlconversion_images/awslambda5.png)

Step 9: Create a new AWS profile in the Upload Lambda Function Window. After creating the profile, add a name for the Lambda function to publish. Then, click **Next**.  

![Convert HTMLToPDF AWS Lambda Step6](htmlconversion_images/awslambda6.png)

Step 10: In the Advanced Function Details window, specify the **Role Name** as based on AWS Managed policy. After selecting the role, click the Upload button to deploy your application.

![Convert HTMLToPDF AWS Lambda Step7](htmlconversion_images/awslambda7.png)
![Convert HTMLToPDF AWS Lambda Step8](htmlconversion_images/awslambda8.png)

Step 11: After deploying the application, Sign in to your AWS account, and you can see the published Lambda function in the AWS console.

![Convert HTMLToPDF AWS Lambda Step9](htmlconversion_images/awslambda9.png)

**Steps to invoke the AWS Lambda function from the Test application**:

Step 12: Add the following code to invoke the AWS lambda function with the HTML string from the Function Test.

{% highlight c# tabtitle="C#" %}

public class FunctionTest
{
    [Fact]
    public void HtmlToPDFFunction()
    {
        string path = System.IO.Path.GetDirectoryName(System.Reflection.Assembly.GetExecutingAssembly().GetName().CodeBase);
        string filePath = Environment.OSVersion.Platform == PlatformID.Unix ? string.Concat(path.Substring(5), @"/") : string.Concat(path.Substring(6), @"\");
 
        var html = File.ReadAllText($"{filePath}/HtmlSample.html");
        byte[] base64 = null;
        base64 = AWSHelper.RunLambdaFunction(html).Result;
 
        FileStream file = new FileStream($"{filePath}/file{DateTime.Now.Ticks}.pdf", FileMode.Create, FileAccess.Write);
        var ms = new MemoryStream(base64);
        ms.WriteTo(file);
        file.Close();
        ms.Close();
    }
}

{% endhighlight %}

Step 13: Right click the test application and select **Run Tests**.

![Convert HTMLToPDF AWS Lambda Step10](htmlconversion_images/awslambda10.png)

Step 14: By executing the program, you will get the PDF document as follows.

![Convert HTMLToPDF AWS Lambda Step11](htmlconversion_images/awslambda11.png)

A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/AWS/HTML_to_PDF_Lambda_Docker_Container).

## AWS Elastic Beanstalk

**Steps to convert HTML to PDF using Blink in AWS Elastic Beanstalk**

Step 1: Create a new C# ASP.NET Core Web Application project.
![AWS Elastic Beanstalk Step1](htmlconversion_images/AWS_Elastic_Beanstalk1.png)

Step 2: In configuration windows, name your project and select **Next**.
![AWS Elastic Beanstalk Step2](htmlconversion_images/AWS_Elastic_Beanstalk2.png)

![AWS Elastic Beanstalk Step2.1](htmlconversion_images/AWS_Elastic_Beanstalk3.png)

Step 3: Install the [Syncfusion.HtmlToPdfConverter.Net.Aws](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Aws/) NuGet package as a reference to your AWS Elastic Beanstalk project from [NuGet.org.](https://www.nuget.org/).
![AWS Elastic Beanstalk Step3](htmlconversion_images/AWS_Elastic_Beanstalk4.png)

Step 4: A default controller named HomeController.cs gets added to create the ASP.NET Core MVC project. Include the following namespaces in that HomeController.cs file<br>
{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.HtmlConverter;
using System.IO;

{% endhighlight %}

Step 5: Add a new button in index.cshtml as follows.

{% highlight c# tabtitle="C#" %}

@{
    Html.BeginForm("BlinkToPDF", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="HTML To PDF" style="width:150px;height:27px" />
            <br />
            <div class="text-danger">
                @ViewBag.Message
            </div>
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}

Step 6: Add a new action method named BlinkToPDF in HomeController.cs and include the following code example to convert HTML to PDF document using the Convert method in [HtmlToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html) class. The HTML content will be scaled based on the given [ViewPortSize](https://help.syncfusion.com/cr/fileformats/Syncfusion.HtmlConverter.BlinkConverterSettings.html#Syncfusion_HtmlConverter_BlinkConverterSettings_ViewPortSize) property of the [BlinkConverterSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html) class.

{% highlight c# tabtitle="C#" %}

public IActionResult BlinkToPDF()
{
          //Initialize HTML to PDF converter.
          HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);
          BlinkConverterSettings settings = new BlinkConverterSettings();
          //Set command line arguments to run without the sandbox.
          settings.CommandLineArguments.Add("--no-sandbox");
          settings.CommandLineArguments.Add("--disable-setuid-sandbox");
          //Set Blink viewport size.
          settings.ViewPortSize = new Syncfusion.Drawing.Size(1280, 0);
          //Assign Blink settings to the HTML converter.
          htmlConverter.ConverterSettings = settings;
          //Convert URL to PDF document.
          PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com");
          //Create the memory stream.
          MemoryStream stream = new MemoryStream();
          //Save the document to the memory stream.
          document.Save(stream);
          return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Application.Pdf, "BlinkLinuxDockerAWSBeanstalk.pdf");
}


{% endhighlight %}

Step 7: Click the **Publish to AWS Elastic Beanstalk (Legacy)** option by right-clicking the project to
publish the application in the AWS Elastic Beanstalk environment.
![AWS Elastic Beanstalk Step7](htmlconversion_images/AWS_Elastic_Beanstalk5.png)

Step 8: Select the **Create a new application environment** and click **Next** from Publish to AWS Elastic Beanstalk window.
![AWS Elastic Beanstalk Step8](htmlconversion_images/AWS_Elastic_Beanstalk6.png)

Step 9: Please give any valid name to the environment and URL text box. Check whether the URL link is available while clicking the **Check availability** option. If the requested link is available means,
click **NEXT** in the Application Environment window.
![AWS Elastic Beanstalk Step9](htmlconversion_images/AWS_Elastic_Beanstalk7.png)

Step 10: Select **t3a.micro** from the Instance Type text box and select **Next** in the AWS Options
Window.
![AWS Elastic Beanstalk Step10](htmlconversion_images/AWS_Elastic_Beanstalk8.png)

Step 11: Select the Roles and **Next** option from the Permissions window.
![AWS Elastic Beanstalk Step11](htmlconversion_images/AWS_Elastic_Beanstalk9.png)

Step 12: Click **Next** from the Application Options window.
![AWS Elastic Beanstalk Step12](htmlconversion_images/AWS_Elastic_Beanstalk10.png)

Step 13: Click **Deploy** from the Review window.
![AWS Elastic Beanstalk Step13](htmlconversion_images/AWS_Elastic_Beanstalk11.png)

Step 14: Click the **URL link** to launch the application once the Environment is updated successfully and
![AWS Elastic Beanstalk Step14](htmlconversion_images/AWS_Elastic_Beanstalk12.png)

Environment status is healthy.
Step 15: Now, the webpage will open in the browser. Click the button to convert the webpage to a PDF document.
![AWS Elastic Beanstalk Step15](htmlconversion_images/AWS_Elastic_Beanstalk13.png)

By executing the program, you will get a PDF document as follows.
![HTML to PDF output](htmlconversion_images/AWS_Elastic_Beanstalk14.png)

A complete working sample for converting an HTML to PDF using Linux docker in AWS Elastic Beanstalk can be downloaded from [GitHub](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/AWS/AWSElasticBeanstalkSample).

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core/html-to-pdf) to explore the rich set of Syncfusion HTML to PDF converter library features. 

An online sample link to [convert HTML to PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HtmltoPDF#/material3) in ASP.NET Core. 

