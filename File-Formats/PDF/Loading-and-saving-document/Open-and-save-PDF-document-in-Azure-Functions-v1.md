---
title: Open and save PDF document in Azure Functions v1 | Syncfusion
description: Open and save PDF document in Azure Functions v1 using .NET PDF library without the dependency of Adobe Acrobat. 
platform: file-formats
control: PDF
documentation: UG
---

# Open and save PDF document in Azure Functions v1

The [Syncfusion .NET PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net) is used to create, read, edit PDF documents programmatically without the dependency of Adobe Acrobat. Using this library, you can **Open and save PDF document in Azure Functions v1**.

## Steps to open and save PDF document in Azure Functions v1

Step 1: Create a new Azure Functions project.
![Create a Azure Functions project](Azure_Images/Azure-functions-v1/Project_creation.png) 

Step 2: Create a project name and select the location.
![Create a project name](Azure_Images/Azure-functions-v1/Project_configuration.png)

Step 3: Select function worker as **.NET Framework**. 
![Select function worker](Azure_Images/Azure-functions-v1/Additional_information.png)

Step 4: Install the [Syncfusion.PDF.AspNet](https://www.nuget.org/packages/Syncfusion.Pdf.AspNet) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.Pdf.AspNet NuGet package](Azure_Images/Azure-functions-v1/NuGet_package.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Include the following namespaces in the **Function1.cs** file.   

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf.Grid;
using Syncfusion.Pdf;
using Syncfusion.Pdf.Parsing;
using System.Drawing;

{% endhighlight %}
{% endtabs %}

Step 6: Add the following code snippet in **Run** method of **Function1** class to perform ***open an existing PDF document**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Load an existing PDF document from the disk.
var assembly = Assembly.GetExecutingAssembly();
var docStream = assembly.GetManifestResourceStream("Open_and_save_PDF_document.Data.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

{% endhighlight %}
{% endtabs %}

Step 7: Add below code example to add a table in the PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();
//Add values to the list.
List<object> data = new List<object>();
Object row1 = new { Product_ID = "1001", Product_Name = "Bicycle", Price = "10,000" };
Object row2 = new { Product_ID = "1002", Product_Name = "Head Light", Price = "3,000" };
Object row3 = new { Product_ID = "1003", Product_Name = "Break wire", Price = "1,500" };
data.Add(row1);
data.Add(row2);
data.Add(row3);
//Add list to IEnumerable.
IEnumerable<object> dataTable = data;
//Assign data source.
pdfGrid.DataSource = dataTable;
//Apply built-in table style.
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent3);
//Draw the grid to the page of PDF document.
pdfGrid.Draw(graphics, new RectangleF(40, 400, loadedPage.Size.Width - 80, 0));

{% endhighlight %}
{% endtabs %}

Step 8: Add below code example to **save the PDF document**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save and close the PDF document  
MemoryStream ms = new MemoryStream();
loadedDocument.Save(ms);
loadedDocument.Close();
ms.Position = 0;

HttpResponseMessage response = new HttpResponseMessage(HttpStatusCode.OK);
response.Content = new ByteArrayContent(ms.ToArray());
response.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment")
{
    FileName = "Sample.pdf"
};
response.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("application/pdf");
return response;

{% endhighlight %}
{% endtabs %}

Step 9: Right click the project and select **Publish**. Then, create a new profile in the Publish Window.
![Create a new profile in the Publish Window](Azure_Images/Azure-functions-v1/Publish_button.png)

Step 10: Select the target as **Azure** and click **Next** button.
![Select the target as Azure](Azure_Images/Azure-functions-v1/Set_Azure_target.png)

Step 11: Select the **Create new** button.
![Configure Hosting Plan](Azure_Images/Azure-functions-v1/Function_insane.png)

Step 12: Click **Create** button. 
![Select the plan type](Azure_Images/Azure-functions-v1/Hosting_sample.png)

Step 13: After creating app service then click **Finish** button. 
![Creating app service](Azure_Images/Azure-functions-v1/Finish_function.png)

Step 14: Click the **Publish** button.
![Click Publish Button](Azure_Images/Azure-functions-v1/Ready_for_publish.png)

Step 15: Publish has been succeed.
![Publish succeeded](Azure_Images/Azure-functions-v1/Published_link.png)

Step 16: Now, go to Azure portal and select the App Services. After running the service, click **Get function URL > Copy**. Include the URL as a query string in the URL. Then, paste it into the new browser tab. You will get the PDF document as follows. 
![Output document screenshot](Azure_Images/Azure-functions-v1/Output_screenshot.png)

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Open%20and%20Save%20PDF%20document/Azure/Azure_Functions/Azure-functions-v1).

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core) to explore the rich set of Syncfusion PDF library features.

An online sample link to [create a PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HelloWorld#/material3) in ASP.NET Core.
