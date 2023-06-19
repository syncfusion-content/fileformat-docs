---
title: Open and save PDF document in ASP.NET Core | Syncfusion
description: Open and save PDF document in ASP.NET Core application using Syncfusion .NET Core PDF library without the dependency of Adobe Acrobat. 
platform: file-formats
control: PDF
documentation: UG
keywords: .net core save pdf, .net core load pdf, c# save pdf, c# load pdf
---

# Open and save PDF document in ASP.NET Core 

The [Syncfusion .NET Core PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net-core) is used to create, read, and edit PDF documents programatically without the dependency of Adobe Acrobat. Using this library, you can **open and save PDF document in ASP.NET Core**. 

## Steps to open and save PDF document programatically: 

Step 1: Create a new ASP.NET Core Web application project. 
![Create ASP.NET Core Web application in Visual Studio](Images/Create_ASP_NET_Core_application.png)

Step 2: Install the [Syncfusion.Pdf.Net.Core](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core/) NuGet package as a reference to your project from the [NuGet.org](https://www.nuget.org/).
![Install NuGet package](Images/NuGet_package_ASP_NET_Core.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from the trial setup or from the NuGet feed, you also have to add the "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering the Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in the HomeController.cs file. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf.Parsing;
using Syncfusion.Pdf;
using Syncfusion.Pdf.Graphics;
using Syncfusion.Pdf.Grid;
using Syncfusion.Drawing;

{% endhighlight %}

{% endtabs %}

Step 4: A default action method named Index will be present in HomeController.cs file. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 5: Add a new button in the Index.cshtml as shown in the following.

{% tabs %}

{% highlight HTML %}

@{
    Html.BeginForm("OpenAndSaveDocument", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Open and save PDF document" style="width:300px;height:30px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}

{% endtabs %}

Step 6: Add a new action method **OpenAndSaveDocument** in HomeController.cs and include the following code sample to **open an existing PDF document in ASP.NET Core**. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load PDF document as stream.
FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read);
//Load an existing PDF document.
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

{% endhighlight %}

{% endtabs %}

Step 7: Add the below code example to add a table in the PDF document. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the existing page.
PdfLoadedPage loadedPage = document.Pages[0] as PdfLoadedPage;
//Create PDF graphics for the page.
PdfGraphics graphics = loadedPage.Graphics;

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

Step 8: Add below code example to **save the PDF document in ASP.NET Core**. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create memory stream. 
MemoryStream stream = new MemoryStream();
//Save the PDF document to stream.
document.Save(stream);
//If the position is not set to '0' then the PDF will be empty.
stream.Position = 0;
//Close the document.
document.Close(true);
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, ""application/pdf, "Sample.pdf");

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Open%20and%20Save%20PDF%20document/ASP.NET%20Core/Open_and_save_PDF_document).

By executing the program, you will get the PDF document as follows.
![ASP.Net Core output PDF document](Images/Open_and_save_output.png)