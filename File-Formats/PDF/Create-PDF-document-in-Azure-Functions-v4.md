---
title: Create PDF document in Azure Functions v4 | Syncfusion
description: Create PDF document in Azure Functions v4 using .NET PDF library without the dependency of Adobe Acrobat. 
platform: file-formats
control: PDF
documentation: UG
---

# Create PDF document in Azure Functions v4

The [Syncfusion .NET PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net) is used to create, read, edit PDF documents programmatically without the dependency of Adobe Acrobat. Using this library, you can **create PDF document in Azure Functions v4**.

## Steps to create a PDF document in Azure Functions v4 

Step 1: Create a new Azure Functions project.
![Create a Azure Functions project](Azure_images/Azure-Functions-V4/Project_creation.png) 

Step 2: Create a project name and select the location.
![Create a project name](Azure_images/Azure-Functions-V4/Configuration_project.png)

Step 3: Select function worker as **.NET 6.0(Long-term support)**. 
![Select function worker](Azure_Images/Azure-Functions-V4/Additional_information.png)

Step 4: Install the [Syncfusion.Pdf.Net.Core](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core/) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.Pdf.AspNet NuGet package](Azure_Images/Azure-Functions-V4/NuGet_package_reference.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespaces in the **Function1.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf.Graphics;
using Syncfusion.Pdf.Grid;
using Syncfusion.Pdf;
using Syncfusion.Drawing;

{% endhighlight %}
{% endtabs %}

Step 5: Add the following code example in **Run** method of **Function1** class to perform **create a PDF document** in Azure Functions and return the resultant **PDF document**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Set the page size.
document.PageSettings.Size = PdfPageSize.A4;
//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;
//Load the image from the disk.
var assembly = Assembly.GetExecutingAssembly();
var imageStream = assembly.GetManifestResourceStream("Create_PDF_document.Data.AdventureCycle.jpg");
PdfBitmap image = new PdfBitmap(imageStream);
//Draw an image.
graphics.DrawImage(image, new RectangleF(130, 0, 250, 100));

//Draw header text. 
graphics.DrawString("Adventure Works Cycles", new PdfStandardFont(PdfFontFamily.TimesRoman, 20, PdfFontStyle.Bold), PdfBrushes.Gray, new PointF(150, 150));

//Add paragraph. 
string text = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";
//Create a text element with the text and font.
PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 12));
//Draw the text in the first column.
textElement.Draw(page, new RectangleF(0, 200, page.GetClientSize().Width, page.GetClientSize().Height));

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
pdfGrid.Draw(graphics, new RectangleF(0, 300, page.Size.Width - 80, 0));

MemoryStream memoryStream = new MemoryStream();
//Saves the PDF document file.
document.Save(memoryStream);
//Create the response to return.
HttpResponseMessage response = new HttpResponseMessage(HttpStatusCode.OK);
//Set the PDF document saved stream as content of response.
response.Content = new ByteArrayContent(memoryStream.ToArray());
//Set the contentDisposition as attachment.
response.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment")
{
    FileName = "Sample.pdf"
};
//Set the content type as PDF document mime type.
response.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("application/pdf");
//Return the response with output PDF document stream.
return response;

{% endhighlight %}
{% endtabs %}

Step 6: Right click the project and select **Publish**. Then, create a new profile in the Publish Window.
![Create a new profile in the Publish Window](Azure_Images/Azure-Functions-V4/Click_publish.png)

Step 7: Select the target as **Azure** and click **Next** button.
![Select the target as Azure](Azure_Images/Azure-Functions-V4/Set_Azure_target.png)

Step 8: Select the **Azure Function App (Windows)** and click **Next**. 
![Select Azure function app](Azure_Images/Azure-Functions-V4/Select_function_app.png)

Step 9: Select the **Create new** button.
![Configure Hosting Plan](Azure_Images/Azure-Functions-V4/Select_create_new_button.png)

Step 10: Click **Create** button. 
![Select the plan type](Azure_Images/Azure-Functions-V4/Hosting_plan.png)

Step 11: After creating app service then click **Finish** button. 
![Creating app service](Azure_Images/Azure-Functions-V4/Creating%20app%20service.png)

Step 12: Click the **Close** button.
![Click close button](Azure_Images/Azure-Functions-V4/publish-profile-creation-progress.png)

Step 13: Click the **Publish** button. 
![Click Publish button](Azure_Images/Azure-Functions-V4/successful_publish.png)

Step 13: Now, go to Azure portal and select the App Services. After running the service, click **Get function URL > Copy**. Include the URL as a query string in the URL. Then, paste it into the new browser tab. You will get the PDF document as follows. 
![Output document screenshot](Azure_Images/Azure-Functions-V4/Output_screenshot.png)

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Getting%20Started/Azure/Azure%20Function%20V4).

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core) to explore the rich set of Syncfusion PDF library features.

An online sample link to [create a PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HelloWorld#/material3) in ASP.NET Core.