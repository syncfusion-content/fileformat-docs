---
title: Create Excel files in ASP.NET Core Web API | Syncfusion
description: Explains how to create Excel files in ASP.NET Core Web API applications using Syncfusion XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Create an Excel files in ASP.NET Core Web API

[Syncfusion Excel library for ASP.NET Core platform](https://www.syncfusion.com/document-processing/excel-framework/net-core/excel-library) can be used to create, read, edit Excel files. This also convert Excel files to PDF.

## Create a simple Excel report

The below steps illustrates creating a simple Invoice formatted Excel document in ASP.NET Core Web API.

Step 1: Create a new C# ASP.NET Core Web API project.

![Create ASP.NET Core Web API project in Visual Studio](ASP-NET-Core-Web-API_images/ASP-NET-Core-Web-API_images_img1.png)

Step 2: Name the project.

![Name the project](ASP-NET-Core-Web-API_images/ASP-NET-Core-Web-API_images_img2.png)

Step 3: Install the [Syncfusion.XlsIO.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIO.Net.Core) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org).

![Add Syncfusion.XlsIO.Net.Core reference to the project](ASP-NET-Core-Web-API_images/ASP-NET-Core-Web-API_images_img3.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components. 

Step 4: Add new API controller empty file in the project. 

![Add empty API controller to the project](ASP-NET-Core-Web-API_images/ASP-NET-Core-Web-API_images_img4.png)

Step 5: Include the following namespaces in the **ValuesController.cs** file.
{% capture codesnippet1 %}
{% tabs %}  
{% highlight c# tabtitle="C#" %}
using Syncfusion.Drawing;
using Syncfusion.XlsIO;
using Microsoft.AspNetCore.Mvc;
{% endhighlight %}
{% endtabs %}  
{% endcapture %}
{{ codesnippet1 | OrderList_Indent_Level_1 }}

Step 6: Add a new action method CreateDocument in **ValuesController.cs** and include the below code snippet to create an Excel file and download it.

{% capture codesnippet2 %}
{% tabs %}  
{% highlight c# tabtitle="C#" %}
[HttpGet]
[Route("api/Excel")]
public IActionResult CreateDocument()
{
    try
    {
        var fileDownloadName = $"Output.xlsx";
        const string contentType = "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet";
        var stream = ExportTimecardDailyDetail();
        stream.Position = 0;
        return File(stream, contentType, fileDownloadName);
    }
    catch (Exception ex)
    {
        // Log or handle the exception
        return BadRequest($"Error occurred while creating Excel file: {ex.Message}");
    }
}

public static MemoryStream ExportTimecardDailyDetail()
{
    //Create an instance of ExcelEngine
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        IApplication application = excelEngine.Excel;
        application.DefaultVersion = ExcelVersion.Xlsx;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);
        IWorksheet worksheet = workbook.Worksheets[0];

        //Adding a picture
        FileStream imageStream = new FileStream("AdventureCycles-Logo.png", FileMode.Open, FileAccess.Read);
        IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, imageStream, 20, 20);

        //Disable gridlines in the worksheet
        worksheet.IsGridLinesVisible = false;

        //Enter values to the cells from A3 to A5
        worksheet.Range["A3"].Text = "46036 Michigan Ave";
        worksheet.Range["A4"].Text = "Canton, USA";
        worksheet.Range["A5"].Text = "Phone: +1 231-231-2310";

        //Make the text bold
        worksheet.Range["A3:A5"].CellStyle.Font.Bold = true;

        //Merge cells
        worksheet.Range["D1:E1"].Merge();

        //Enter text to the cell D1 and apply formatting.
        worksheet.Range["D1"].Text = "INVOICE";
        worksheet.Range["D1"].CellStyle.Font.Bold = true;
        worksheet.Range["D1"].CellStyle.Font.RGBColor = Color.FromArgb(42, 118, 189);
        worksheet.Range["D1"].CellStyle.Font.Size = 35;

        //Apply alignment in the cell D1
        worksheet.Range["D1"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignRight;
        worksheet.Range["D1"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignTop;

        //Enter values to the cells from D5 to E8
        worksheet.Range["D5"].Text = "INVOICE#";
        worksheet.Range["E5"].Text = "DATE";
        worksheet.Range["D6"].Number = 1028;
        worksheet.Range["E6"].Value = "12/31/2018";
        worksheet.Range["D7"].Text = "CUSTOMER ID";
        worksheet.Range["E7"].Text = "TERMS";
        worksheet.Range["D8"].Number = 564;
        worksheet.Range["E8"].Text = "Due Upon Receipt";

        //Apply RGB backcolor to the cells from D5 to E8
        worksheet.Range["D5:E5"].CellStyle.Color = Color.FromArgb(42, 118, 189);
        worksheet.Range["D7:E7"].CellStyle.Color = Color.FromArgb(42, 118, 189);

        //Apply known colors to the text in cells D5 to E8
        worksheet.Range["D5:E5"].CellStyle.Font.Color = ExcelKnownColors.White;
        worksheet.Range["D7:E7"].CellStyle.Font.Color = ExcelKnownColors.White;

        //Make the text as bold from D5 to E8
        worksheet.Range["D5:E8"].CellStyle.Font.Bold = true;

        //Apply alignment to the cells from D5 to E8
        worksheet.Range["D5:E8"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter;
        worksheet.Range["D5:E5"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignCenter;
        worksheet.Range["D7:E7"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignCenter;
        worksheet.Range["D6:E6"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignTop;

        //Enter value and applying formatting in the cell A7
        worksheet.Range["A7"].Text = "  BILL TO";
        worksheet.Range["A7"].CellStyle.Color = Color.FromArgb(42, 118, 189);
        worksheet.Range["A7"].CellStyle.Font.Bold = true;
        worksheet.Range["A7"].CellStyle.Font.Color = ExcelKnownColors.White;

        //Apply alignment
        worksheet.Range["A7"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignLeft;
        worksheet.Range["A7"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignCenter;

        //Enter values in the cells A8 to A12
        worksheet.Range["A8"].Text = "Steyn";
        worksheet.Range["A9"].Text = "Great Lakes Food Market";
        worksheet.Range["A10"].Text = "20 Whitehall Rd";
        worksheet.Range["A11"].Text = "North Muskegon,USA";
        worksheet.Range["A12"].Text = "+1 231-654-0000";

        //Create a Hyperlink for e-mail in the cell A13
        IHyperLink hyperlink = worksheet.HyperLinks.Add(worksheet.Range["A13"]);
        hyperlink.Type = ExcelHyperLinkType.Url;
        hyperlink.Address = "Steyn@greatlakes.com";
        hyperlink.ScreenTip = "Send Mail";

        //Merge column A and B from row 15 to 22
        worksheet.Range["A15:B15"].Merge();
        worksheet.Range["A16:B16"].Merge();
        worksheet.Range["A17:B17"].Merge();
        worksheet.Range["A18:B18"].Merge();
        worksheet.Range["A19:B19"].Merge();
        worksheet.Range["A20:B20"].Merge();
        worksheet.Range["A21:B21"].Merge();
        worksheet.Range["A22:B22"].Merge();

        //Enter details of products and prices
        worksheet.Range["A15"].Text = "  DESCRIPTION";
        worksheet.Range["C15"].Text = "QTY";
        worksheet.Range["D15"].Text = "UNIT PRICE";
        worksheet.Range["E15"].Text = "AMOUNT";
        worksheet.Range["A16"].Text = "Cabrales Cheese";
        worksheet.Range["A17"].Text = "Chocos";
        worksheet.Range["A18"].Text = "Pasta";
        worksheet.Range["A19"].Text = "Cereals";
        worksheet.Range["A20"].Text = "Ice Cream";
        worksheet.Range["C16"].Number = 3;
        worksheet.Range["C17"].Number = 2;
        worksheet.Range["C18"].Number = 1;
        worksheet.Range["C19"].Number = 4;
        worksheet.Range["C20"].Number = 3;
        worksheet.Range["D16"].Number = 21;
        worksheet.Range["D17"].Number = 54;
        worksheet.Range["D18"].Number = 10;
        worksheet.Range["D19"].Number = 20;
        worksheet.Range["D20"].Number = 30;
        worksheet.Range["D23"].Text = "Total";

        //Apply number format
        worksheet.Range["D16:E22"].NumberFormat = "$.00";
        worksheet.Range["E23"].NumberFormat = "$.00";

        //Apply incremental formula for column Amount by multiplying Qty and UnitPrice
        application.EnableIncrementalFormula = true;
        worksheet.Range["E16:E20"].Formula = "=C16*D16";

        //Formula for Sum the total
        worksheet.Range["E23"].Formula = "=SUM(E16:E22)";

        //Apply borders
        worksheet.Range["A16:E22"].CellStyle.Borders[ExcelBordersIndex.EdgeTop].LineStyle = ExcelLineStyle.Thin;
        worksheet.Range["A16:E22"].CellStyle.Borders[ExcelBordersIndex.EdgeBottom].LineStyle = ExcelLineStyle.Thin;
        worksheet.Range["A16:E22"].CellStyle.Borders[ExcelBordersIndex.EdgeTop].Color = ExcelKnownColors.Grey_25_percent;
        worksheet.Range["A16:E22"].CellStyle.Borders[ExcelBordersIndex.EdgeBottom].Color = ExcelKnownColors.Grey_25_percent;
        worksheet.Range["A23:E23"].CellStyle.Borders[ExcelBordersIndex.EdgeTop].LineStyle = ExcelLineStyle.Thin;
        worksheet.Range["A23:E23"].CellStyle.Borders[ExcelBordersIndex.EdgeBottom].LineStyle = ExcelLineStyle.Thin;
        worksheet.Range["A23:E23"].CellStyle.Borders[ExcelBordersIndex.EdgeTop].Color = ExcelKnownColors.Black;
        worksheet.Range["A23:E23"].CellStyle.Borders[ExcelBordersIndex.EdgeBottom].Color = ExcelKnownColors.Black;

        //Apply font setting for cells with product details
        worksheet.Range["A3:E23"].CellStyle.Font.FontName = "Arial";
        worksheet.Range["A3:E23"].CellStyle.Font.Size = 10;
        worksheet.Range["A15:E15"].CellStyle.Font.Color = ExcelKnownColors.White;
        worksheet.Range["A15:E15"].CellStyle.Font.Bold = true;
        worksheet.Range["D23:E23"].CellStyle.Font.Bold = true;

        //Apply cell color
        worksheet.Range["A15:E15"].CellStyle.Color = Color.FromArgb(42, 118, 189);

        //Apply alignment to cells with product details
        worksheet.Range["A15"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignLeft;
        worksheet.Range["C15:C22"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter;
        worksheet.Range["D15:E15"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter;

        //Apply row height and column width to look good
        worksheet.Range["A1"].ColumnWidth = 36;
        worksheet.Range["B1"].ColumnWidth = 11;
        worksheet.Range["C1"].ColumnWidth = 8;
        worksheet.Range["D1:E1"].ColumnWidth = 18;
        worksheet.Range["A1"].RowHeight = 47;
        worksheet.Range["A2"].RowHeight = 15;
        worksheet.Range["A3:A4"].RowHeight = 15;
        worksheet.Range["A5"].RowHeight = 18;
        worksheet.Range["A6"].RowHeight = 29;
        worksheet.Range["A7"].RowHeight = 18;
        worksheet.Range["A8"].RowHeight = 15;
        worksheet.Range["A9:A14"].RowHeight = 15;
        worksheet.Range["A15:A23"].RowHeight = 18;

        //Saving the Excel to the MemoryStream 
        MemoryStream stream = new MemoryStream();
        workbook.SaveAs(stream);

        //Set the position as '0'.
        stream.Position = 0;

        return stream;
    }
}
{% endhighlight %}
{% endtabs %} 
{% endcapture %}
{{ codesnippet2 | OrderList_Indent_Level_1 }}

A complete working example of how to create an Excel file in ASP.NET Core Web API in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/ASP.NET%20Core%20Web%20API/Create%20Excel).

## Steps for accessing the Web API using HTTP requests

Step 1: Create a console application.
![Create console app in Visual Studio](ASP-NET-Core-Web-API_images/ASP-NET-Core-Web-API_images_img5.png)

Step 2: Name the Application.
![Name the project](ASP-NET-Core-Web-API_images/ASP-NET-Core-Web-API_images_img6.png)

Step 3: Add the below code snippet in the **Program.cs** file for accessing the Web API using HTTP requests. 

{% capture codesnippet3 %}
{% tabs %}  
{% highlight c# tabtitle="C#" %}
// Create an HttpClient instance
using (HttpClient client = new HttpClient())
{
    try
    {
        // Send a GET request to a URL
        HttpResponseMessage response = await client.GetAsync("https://localhost:7000/api/Values/api/Excel");

        // Check if the response is successful
        if (response.IsSuccessStatusCode)
        {
            // Read the content as a string
            Stream responseBody = await response.Content.ReadAsStreamAsync();
            FileStream fileStream = File.Create("Output.xlsx");
            responseBody.CopyTo(fileStream);
            fileStream.Close();
        }
        else
        {
            Console.WriteLine($"HTTP error status code: {response.StatusCode}");
        }
    }
    catch (HttpRequestException e)
    {
        Console.WriteLine($"Request exception: {e.Message}");
    }
}
{% endhighlight %}
{% endtabs %} 
{% endcapture %}
{{ codesnippet3 | OrderList_Indent_Level_1 }}


A complete working example of how to create a client application for accessing the Web API using HTTP requests in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/ASP.NET%20Core%20Web%20API/Client%20Application).

By executing the program, you will get the Excel file as below.
![Output File](ASP-NET-Core-Web-API_images/ASP-NET-Core-Web-API_images_img7.png)

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net-core) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [create an Excel document](https://ej2.syncfusion.com/aspnetcore/Excel/Create#/material3) in ASP.NET Core.

