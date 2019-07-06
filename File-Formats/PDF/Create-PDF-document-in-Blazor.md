---
title: Create, read, and edit PDF document in Blazor | Syncfusion 
description: Create, read, and edit PDF document in Blazor using Syncfusion .NET Core PDF (Essential PDF) library
platform: file-formats
control: PDF
documentation: UG
---

# Create, read, and edit PDF document in Blazor

Syncfusion Essential PDF is a [.NET Core PDF library] (https://www.syncfusion.com/pdf-framework/net-core/pdf-library) using this library, you can create, read, and edit PDF documents in Blazor. This library also offers functionality to merge, split, stamp, forms, and secure PDF files. 

## Steps to create PDF document in Blazor Server-Side application

The below steps illustrate creating an PDF document in Blazor Server-Side application.

Step 1: Create a new C# Blazor Server-Side application project. Select ASP.NET Core Web Application from the template and click the Next button.

![Create Blazor Server Side application in Visual Studio](Create_PDF_Blazor/Blazor_create_project.png)

Step 2: Now, the project configuration window will popup. Click Create button to create a new project with the default project configuration.

![Create Blazor Server Side application in Visual Studio](Create_PDF_Blazor/Blazor_images_Server_Creation.png)

Step 3: Choose Blazor (server-side) from the dashboard and click Create button to create a new Blazor Server-Side application. Make sure .NET Core and ASP.NET Core 3.0 are selected at the top.

![Create Blazor Server Side application in Visual Studio](Create_PDF_Blazor/Blazor_images_Server.png)

Step 4: Install the [Syncfusion.PDF.Net.Core](https://www.nuget.org/packages/Syncfusion.pdf.Net.Core) NuGet package as reference to your Blazor application from [NuGet.org](https://www.nuget.org).

![Add PDF reference to the project](Create_PDF_Blazor/Blazor_reference.png)

Step 5: Create a new cs file with name as ``ExportService`` under ``Data`` folder and include the following namespaces in the file.

{% tabs %}
{% highlight c# %}
using Syncfusion.Pdf;
using Syncfusion.Pdf.Graphics;
using Syncfusion.Pdf.Grid;
using Syncfusion.Drawing;
{% endhighlight %}
{% endtabs %}

Add the following method in the ``ExportService`` class

{% tabs %}
{% highlight c# %}
//Export weather data to PDF document.
public MemoryStream CreatePdf(WeatherForecast[] forecasts)
{
    if (forecasts == null)
    {
        throw new ArgumentNullException("Forecast cannot be null");
    }
    //Create a new PDF document.
    using (PdfDocument pdfDocument = new PdfDocument())
    {

        int paragraphAfterSpacing = 8;
        int cellMargin = 8;

        //Add Page to the PDF document.
        PdfPage page = pdfDocument.Pages.Add();

        //Create a new font.
        PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 16);

        //Create a text element to draw a text in PDF page.
        PdfTextElement title = new PdfTextElement("Weather Forecast", font, PdfBrushes.Black);
        PdfLayoutResult result = title.Draw(page, new PointF(0, 0));


        PdfStandardFont contentFont = new PdfStandardFont(PdfFontFamily.TimesRoman, 12);
        PdfTextElement content = new PdfTextElement("This component demonstrates fetching data from a service and Exporting the data to PDF, Excel, Word and PowerPoint files using Syncfusion .NET file format libraries.", contentFont, PdfBrushes.Black);
        PdfLayoutFormat format = new PdfLayoutFormat();
        format.Layout = PdfLayoutType.Paginate;

        //Draw a text to the PDF document.
        result = content.Draw(page, new RectangleF(0, result.Bounds.Bottom + paragraphAfterSpacing, page.GetClientSize().Width, page.GetClientSize().Height), format);

        //Create a PdfGrid.
        PdfGrid pdfGrid = new PdfGrid();
        pdfGrid.Style.CellPadding.Left = cellMargin;
        pdfGrid.Style.CellPadding.Right = cellMargin;

        //Applying built-in style to the PDF grid
        pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent1);

        //Assign data source.
        pdfGrid.DataSource = forecasts;

        pdfGrid.Style.Font = contentFont;

        //Draw PDF grid into the PDF page.
        pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(0, result.Bounds.Bottom + paragraphAfterSpacing));

        using (MemoryStream stream = new MemoryStream())
        {
            //Saving the PDF document in-to the stream
            pdfDocument.Save(stream);
            //Closing the PDF document.
            pdfDocument.Close(true);
            return stream;
                
        }
    }
}
{% endhighlight %}
{% endtabs %}

Register your service in the method ``ConfigureServices`` available in the ``Startup.cs`` class as follow.
{% tabs %}
{% highlight c# %}
public void ConfigureServices(IServiceCollection services)
{
    services.AddRazorPages();
    services.AddServerSideBlazor();
    services.AddSingleton<WeatherForecastService>();
    services.AddSingleton<ExportService>();
}
{% endhighlight %}
{% endtabs %}


Step 6: Inject ``ExportService`` in-to ``FetchData.razor`` using following code

{% tabs %}
{% highlight CSHTML %}
@inject ExportToFileService exportService
@inject Microsoft.JSInterop.IJSRuntime JS
@using  System.IO;
{% endhighlight %}
{% endtabs %}

Create a button in the ``FetchData.razor`` using following code.

{% tabs %}
{% highlight CSHTML %}
<button class="btn btn-primary" onclick="@ExportToPdf">Export to PDF</button>
{% endhighlight %}
{% endtabs %}

Add the ``ExportToPdf`` method in ``FetchData.razor`` page to call the export service.

{% tabs %}
{% highlight C# %}
@functions
{

    protected async Task ExportToPdf()
    {
        using (MemoryStream excelStream = PDFExportService.CreatePdf(forecasts))
        {
            await JS.SaveAs("Sample.pdf", excelStream.ToArray());
        }
    }
}
{% endhighlight %}
{% endtabs %}

Step 7: Create a class file with ``FileUtil`` name and add the following code to invoke the JavaScript action to download the file in the browser.

{% tabs %}

{% highlight c# %}

public static class FileUtil
{
    public static Task SaveAs(this IJSRuntime js, string filename, byte[] data)
       => js.InvokeAsync<object>(
           "saveAsFile",
           filename,
           Convert.ToBase64String(data));
}

{% endhighlight %}

{% endtabs %}

8.Add the following JavaScript function in the ``_Host.cshtml`` available under the ``Pages`` folder.

{% tabs %}

{% highlight HTML %}

<script type="text/javascript">
    function saveAsFile(filename, bytesBase64) {
        var link = document.createElement('a');
        link.download = filename;
        link.href = "data:application/octet-stream;base64," + bytesBase64;
        document.body.appendChild(link); // Needed for Firefox
        link.click();
        document.body.removeChild(link);
    }
</script>

{% endhighlight %}

{% endtabs %}

By executing the program, you will get the following output in the browser

![Blazor Server-side browser output](Create_PDF_Blazor/Blazor_browser_output.png)

Click the export to PDF button and you will get the PDF document with following output

![Blazor Server-side PDF output](Create_PDF_Blazor/Blazor_PDF_output.png)

N> It is recommended to use Blazor Server-Side application to reduce the pay back load which is high in Blazor Client-Side.