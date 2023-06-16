---
title: Open and Save PDF document on Mac OS | Syncfusion
description: Open and save PDF documents on Mac OS using Syncfusion .NET Core PDF library without the dependency of Adobe Acrobat.
platform: file-formats
control: PDF
documentation: UG
keywords: mac os save pdf, mac os load pdf, c# save pdf, c# load pdf
---

# Open and Save PDF document on Mac OS

The [Syncfusion .NET Core PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net-core) is used to create, read, and edit PDF documents programatically without the dependency on Adobe Acrobat. Using this library, you can **open and save PDF document on Mac OS**. 

## Steps to open and save the PDF documents programmatically:

Step 1: Create a new .NET Core console application project.
![Mac OS console application](Images/Mac_OS_Console.png)
Step 2: Select the project version.

Step 3: Install the [Syncfusion.Pdf.Net.Core](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Mac OS NuGet path](Images/Mac_OS_NuGet_path.png)
Step 2: Select the project version.


N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from the trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following Namespaces in the Program.cs file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.Pdf.Graphics;
using Syncfusion.Drawing;
using System.IO;

{% endhighlight %}

{% endtabs %}

Step 5: Add the following code sample to the Program.cs file to **open an existing PDF document in .NET Core application on Mac OS**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open an existing PDF document.
FileStream document = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(stream);
{% endhighlight %}

{% endtabs %}

Step 6: Add the following code example to add paragraph and table to the PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Get the first page from a document.
PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();
//Add values to the list.
List<object> data = new List<object>();
Object row1 = new { Product_ID = "1001", Product_Name = "Bicycle" , Price ="10,000"};
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
pdfGrid.Draw(graphics, new RectangleF(40, 400,page.Size.Width-80,0));
{% endhighlight %}

{% endtabs %}

Step 7: Add the following code example to **save the PDF document in the .NET Core application on Mac OS**.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Create a FileStream to save the PDF document.
using(FileStream outputStream = new FileStream("Result.pdf", FileMode.Create, FileAccess.ReadWrite))
{
//Save the PDF file.
document.Save(outputStream);
}
{% endhighlight %}

{% endtabs %}

A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Open%20and%20Save%20PDF%20document/Mac/Open_and_Save_PDF_Mac).

By executing the program, you will get the **PDF document** as follows.
![Mac OS output PDF document](Images/Open_and_save_output.png)
