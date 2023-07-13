---
title: Open and save Word document in AWS Lambda | Syncfusion
description: Open and save Word document in AWS Lambda using .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Open and save Word document in AWS Lambda

Syncfusion DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) used to create, read, edit and convert Word documents programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **open and save a Word document in AWS Lambda**.

## Steps to open and save Word document in AWS Lambda

Step 1: Create a new **AWS Lambda project** as follows.
![AWS Lambda project](AWS_Images/Lambda_Images/Project-Template-WordtoPDF.png)

Step 2: Select Blueprint as Empty Function and click **Finish**.
![Select Blueprint as Empty Function](AWS_Images/Lambda_Images/Blueprint-AWS-WordtoPDF.png)

Step 3: Install the [Syncfusion.DocIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.DocIO.Net.Core NuGet package](ASP-NET-Core_images/Install_Nuget.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Create a folder and copy the required data files and include the files to the project.
![Create a folder](AWS_Images/Lambda_Images/Data-Folder-WordtoPDF.png)

Step 5: Set the **copy to output directory** to **Copy if newer** to all the data files.
![Property change for data files](AWS_Images/Lambda_Images/Property-WordtoPDF.png)

Step 6: Include the following namespaces in **Function.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;

{% endhighlight %}
{% endtabs %}

step 7: Add the following code snippet in **Function.cs** to **open a Word document in AWS Lambda**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

string filePath = Path.GetFullPath(@"Data/Input.docx");
//Load the file from the disk
using FileStream fileStream = new FileStream(filePath, FileMode.Open, FileAccess.Read);
using WordDocument document = new WordDocument(fileStream, FormatType.Docx);

{% endhighlight %}
{% endtabs %}

Step 8: Add below code example to add a paragraph in the Word document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Access the section in a Word document
IWSection section = document.Sections[0];
//Add new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.ParagraphFormat.FirstLineIndent = 36;
paragraph.BreakCharacterFormat.FontSize = 12f;
//Add new text to the paragraph
IWTextRange textRange = paragraph.AppendText("In 2000, AdventureWorks Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.") as IWTextRange;
textRange.CharacterFormat.FontSize = 12f;

{% endhighlight %}
{% endtabs %}

Step 9: Add below code example to **save the Word document in AWS Lambda**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the Word document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream,FormatType.Docx);
return Convert.ToBase64String(stream.ToArray());

{% endhighlight %}
{% endtabs %}

Step 10: Right-click the project and select **Publish to AWS Lambda**.
![Publish to AWS Lambda](AWS_Images/Lambda_Images/Publish-WordtoPDF.png)

Step 11: Create a new AWS profile in the Upload Lambda Function Window. After creating the profile, add a name for the Lambda function to publish. Then, click **Next**.
![Upload Lambda Function](AWS_Images/Lambda_Images/Upload-Lampda-WordtoPDF.png)

Step 12: In the Advanced Function Details window, specify the **Role Name** as based on AWS Managed policy. After selecting the role, click the **Upload** button to deploy your application.
![Advance Function Details](AWS_Images/Lambda_Images/Advanced-AWS-WordtoPDF.png)

Step 13: After deploying the application, you can see the published Lambda function in **AWS console**.
![After deploying the application](AWS_Images/Lambda_Images/Function-WordtoPDF.png)

Step 14: Edit Memory size and Timeout as maximum in Basic settings of the AWS Lambda function.
![AWS Lambda Function](AWS_Images/Lambda_Images/Basic-Settings-WordtoPDF.png)

## Steps to post the request to AWS Lambda

Step 1: Create a new console project.
![Create a console project](AWS_Images/Lambda_Images/Console-APP-WordtoPDF.png)

step 2: Install the following **Nuget packages** in your application from [Nuget.org](https://www.nuget.org/).

* [AWSSDK.Core](https://www.nuget.org/packages/AWSSDK.Core/)
* [AWSSDK.Lambda](https://www.nuget.org/packages/AWSSDK.Lambda/)
* [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)
![Install AWSSDK.Core Nuget Package](AWS_Images/Lambda_Images/Nuget-Package-AWSSDK-Core-WordtoPDF.png)
![Install AWSSDK.Lambda Nuget Package](AWS_Images/Lambda_Images/Nuget-Package-AWSSDK-Lambda-WordtoPDF.png)
![Install Newtonsoft.Json Nuget Package](AWS_Images/Lambda_Images/Nuget-Package-Newton-Json-WordtoPDF.png)

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
//Convert Base64String into Word document
byte[] bytes = Convert.FromBase64String(responseText.ToString());
FileStream fileStream = new FileStream("Sample.docx", FileMode.Create);
BinaryWriter writer = new BinaryWriter(fileStream);
writer.Write(bytes, 0, bytes.Length);
writer.Close();
System.Diagnostics.Process.Start("Sample.docx");

{% endhighlight %}
{% endtabs %}

By executing the program, you will get the **Word document** as follows.

![Open and save a Word document in AWS Lambda](ASP-NET-Core_images/GettingStartedOutput.jpg)

From GitHub, you can download the [console application](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Convert-Word-to-image/AWS/Console_Application) and [AWS Lambda](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Convert-Word-to-image/AWS/AWS_Lambda) project.

Click [here](https://www.syncfusion.com/document-processing/word-framework/net-core) to explore the rich set of Syncfusion Word library (DocIO) features. 
