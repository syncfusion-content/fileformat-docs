---
title: Create or Generate PDF file in MAUI | Syncfusion
description: Learn how to create or generate a PDF file in .NET MAUI with easy steps using Syncfusion .NET Core PDF library without depending on Adobe.
platform: file-formats
control: PDF
documentation: UG
---

# Create PDF file in .NET MAUI

The Syncfusion [.NET MAUI PDF library](https://www.syncfusion.com/document-processing/pdf-framework/maui/pdf-library) is used to create, read, and edit **PDF** documents. This library also includes functions for merging, splitting, stamping, forms, and securing PDF files and more. Using this library, you can **create a PDF document in the .NET MAUI application.**

**Prerequisites:**

To create .NET Multi-platform App UI (.NET MAUI) apps, you need the latest versions of Visual Studio 2022 and .NET 6. For more details, refer [here](https://docs.microsoft.com/en-us/dotnet/maui/get-started/installation).


## Steps to create PDF document programmatically in .NET MAUI

N> Our PDF library is currently supported in .NET MAUI applications on the Android, iOS, and Windows platform. Currently, the PDF library is not supported in the Mac Catalyst platform. 

1.Create a new project in VS2022, select the .NET MAUI App (Preview) template, and click the **Next** button.

![Create the .NET MaUI  app in Visual Studio](MaUI_Images/Create_Project.png)

2.Enter the project name and click **Create**.

![Create a project name for your new project](MaUI_Images/Configure_Project.png)

3.Install the [Syncfusion.Pdf.Net](https://www.nuget.org/packages/Syncfusion.Pdf.NET/) NuGet package as a reference to your project from the [NuGet.org](https://www.nuget.org/).

![Install the PDF .NET Core NuGet package](MaUI_Images/Install_Nuget.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add the "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering a Syncfusion license key in your application to use our components.

4.Add a new button to the **MainWindow.xaml** as shown below.

{% tabs %}

{% highlight c# tabtitle="C#" %}

<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="CreatePdfDemoSample.MainPage"
             BackgroundColor="{DynamicResource SecondaryColor}">
     <ScrollView>
    
       <Button 
                Text="Create PDF"
                FontAttributes="Bold"
                Grid.Row="3"
                Clicked="createPdf_Click"
                HorizontalOptions="Center" 
                VerticalOptions="Center"/>
      </ScrollView>
</ContentPage>


{% endhighlight %}

{% endtabs %}

5.Include the following namespaces in the **MainWindow.xaml.cs** file.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.Pdf.Graphics;
using Syncfusion.Pdf.Grid;
using Syncfusion.Drawing;
using System.Reflection;
using System.Xml.Linq;

{% endhighlight %}

{% endtabs %}

6.Add a new action method **createPdf_Click** in MainWindow.xaml.cs and include the below code snippet to **create a PDF document**. Include helper classes, methods and required files in the assets folder.

{% tabs %}

{% highlight c# tabtitle="C#" %}
            
			RectangleF TotalPriceCellBounds = RectangleF.Empty;
            RectangleF QuantityCellBounds = RectangleF.Empty;

            //Create a new PDF document.
            PdfDocument document = new PdfDocument();
            //Add a page to the document.
            PdfPage page = document.Pages.Add();
            //Create PDF graphics for the page.
            PdfGraphics graphics = page.Graphics;

            //Get the page width and height.
            float pageWidth = page.GetClientSize().Width;
            float pageHeight = page.GetClientSize().Height;

            //Set the header height.
            float headerHeight = 90;
            //Create a brush with a light blue color. 
            PdfColor lightBlue = Color.FromArgb(255, 91, 126, 215);
            PdfBrush lightBlueBrush = new PdfSolidBrush(lightBlue);
            //Create a brush with a dark blue color. 
            PdfColor darkBlue = Color.FromArgb(255, 65, 104, 209);
            PdfBrush darkBlueBrush = new PdfSolidBrush(darkBlue);
            //Create a brush with a white color. 
            PdfBrush whiteBrush = new PdfSolidBrush(Color.FromArgb(255, 255, 255, 255));

            //Get the font file stream from the assembly. 
            Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
            string basePath = "CreatePdfDemoSample.Resources.Fonts.";
            Stream fontStream = assembly.GetManifestResourceStream(basePath + "OpenSans-Regular.ttf");

            //Create a PdfTrueTypeFont from the stream with the different sizes. 
            PdfTrueTypeFont headerFont = new PdfTrueTypeFont(fontStream, 30, PdfFontStyle.Regular);
            PdfTrueTypeFont arialRegularFont = new PdfTrueTypeFont(fontStream, 18, PdfFontStyle.Regular);
            PdfTrueTypeFont arialBoldFont = new PdfTrueTypeFont(fontStream, 9, PdfFontStyle.Bold);

            //Create a string format.
            PdfStringFormat format = new PdfStringFormat();
            format.Alignment = PdfTextAlignment.Center;
            format.LineAlignment = PdfVerticalAlignment.Middle;

            float y = 0;
            float x = 0;

            //Set the margins of the address.
            float margin = 30;

            //Set the line space.
            float lineSpace = 10;

            //Create a border pen and draw the border to on the PDF page. 
            PdfColor borderColor = Color.FromArgb(255, 142, 170, 219);
            PdfPen borderPen = new PdfPen(borderColor, 1f);
            graphics.DrawRectangle(borderPen, new RectangleF(0, 0, pageWidth, pageHeight));

            //Create a new PdfGrid. 
            PdfGrid grid = new PdfGrid();

            //Add five columns to the grid.
            grid.Columns.Add(5);

            //Create the header row of the grid.
            PdfGridRow[] headerRow = grid.Headers.Add(1);

            //Set style to the header row and set value to the header cells. 
            headerRow[0].Style.BackgroundBrush = new PdfSolidBrush(new PdfColor(68, 114, 196));
            headerRow[0].Style.TextBrush = PdfBrushes.White;
            headerRow[0].Cells[0].Value = "Product ID";
            headerRow[0].Cells[0].StringFormat.Alignment = PdfTextAlignment.Center;
            headerRow[0].Cells[1].Value = "Product Name";
            headerRow[0].Cells[2].Value = "Price ($)";
            headerRow[0].Cells[3].Value = "Quantity";
            headerRow[0].Cells[4].Value = "Total ($)";

            //Add products to the grid table.
            AddProducts("CA-1098", "AWC Logo Cap", 8.99, 2, 17.98, grid);
            AddProducts("LJ-0192", "Long-Sleeve Logo Jersey,M", 49.99, 3, 149.97, grid);
            AddProducts("So-B909-M", "Mountain Bike Socks,M", 9.50, 2, 19, grid);
            AddProducts("LJ-0192", "Long-Sleeve Logo Jersey,M", 49.99, 4, 199.96, grid);
            AddProducts("FK-5136", "ML Fork", 175.49, 6, 1052.94, grid);
            AddProducts("HL-U509", "Sports-100 Helmet,Black", 34.99, 1, 34.99, grid);

            #region Header         

            //Fill the header with a light blue brush. 
            graphics.DrawRectangle(lightBlueBrush, new RectangleF(0, 0, pageWidth, headerHeight));

            string title = "INVOICE";

            //Specificy the bounds for the total value. 
            RectangleF headerTotalBounds = new RectangleF(400, 0, pageWidth - 400, headerHeight);

            //Measure the string size using the font. 
            SizeF textSize = headerFont.MeasureString(title);
            graphics.DrawString(title, headerFont, whiteBrush, new RectangleF(0, 0, textSize.Width + 50, headerHeight), format);
            //Draw a rectangle in the PDF page. 
            graphics.DrawRectangle(darkBlueBrush, headerTotalBounds);
            //Draw the total value to the PDF page. 
            graphics.DrawString("$" + GetTotalAmount(grid).ToString(), arialRegularFont, whiteBrush, new RectangleF(400, 0, pageWidth - 400, headerHeight + 10), format);
            //Create a font from the font stream. 
            arialRegularFont = new PdfTrueTypeFont(fontStream, 9, PdfFontStyle.Regular);
            //Set the bottom line alignment and draw the text to the PDF page. 
            format.LineAlignment = PdfVerticalAlignment.Bottom;
            graphics.DrawString("Amount", arialRegularFont, whiteBrush, new RectangleF(400, 0, pageWidth - 400, headerHeight / 2 - arialRegularFont.Height), format);
            #endregion
            //Measure the string size using the font. 
            SizeF size = arialRegularFont.MeasureString("Invoice Number: 2058557939");
            y = headerHeight + margin;
            x = (pageWidth - margin) - size.Width;
            //Draw text to a PDF page with the provided font and location. 
            graphics.DrawString("Invoice Number: 2058557939", arialRegularFont, PdfBrushes.Black, new PointF(x, y));
            //Measure the string size using the font.
            size = arialRegularFont.MeasureString("Date :" + DateTime.Now.ToString("dddd dd, MMMM yyyy"));
            x = (pageWidth - margin) - size.Width;
            y += arialRegularFont.Height + lineSpace;
            //Draw text to a PDF page with the provided font and location. 
            graphics.DrawString("Date: " + DateTime.Now.ToString("dddd dd, MMMM yyyy"), arialRegularFont, PdfBrushes.Black, new PointF(x, y));

            y = headerHeight + margin;
            x = margin;
            //Draw text to a PDF page with the provided font and location. 
            graphics.DrawString("Bill To:", arialRegularFont, PdfBrushes.Black, new PointF(x, y));
            y += arialRegularFont.Height + lineSpace;
            graphics.DrawString("Abraham Swearegin,", arialRegularFont, PdfBrushes.Black, new PointF(x, y));
            y += arialRegularFont.Height + lineSpace;
            graphics.DrawString("United States, California, San Mateo,", arialRegularFont, PdfBrushes.Black, new PointF(x, y));
            y += arialRegularFont.Height + lineSpace;
            graphics.DrawString("9920 BridgePointe Parkway,", arialRegularFont, PdfBrushes.Black, new PointF(x, y));
            y += arialRegularFont.Height + lineSpace;
            graphics.DrawString("9365550136", arialRegularFont, PdfBrushes.Black, new PointF(x, y));

            #region Grid
            //Set the width of theto grid columns. 
            grid.Columns[0].Width = 110;
            grid.Columns[1].Width = 150;
            grid.Columns[2].Width = 110;
            grid.Columns[3].Width = 70;
            grid.Columns[4].Width = 100;

            for (int i = 0; i < grid.Headers.Count; i++)
            {
                //Set the height ofto the grid header row. 
                grid.Headers[i].Height = 20;
                for (int j = 0; j < grid.Columns.Count; j++)
                {
                    //Create a string format for the header cell. 
                    PdfStringFormat pdfStringFormat = new PdfStringFormat();
                    pdfStringFormat.LineAlignment = PdfVerticalAlignment.Middle;
                    pdfStringFormat.Alignment = PdfTextAlignment.Left;

                    //Set cell padding for header cell. 
                    if (j == 0 || j == 2)
                        grid.Headers[i].Cells[j].Style.CellPadding = new PdfPaddings(30, 1, 1, 1);
                    //Set a string format to the grid header cell. 
                    grid.Headers[i].Cells[j].StringFormat = pdfStringFormat;
                    //Set font to the grid header cell. 
                    grid.Headers[i].Cells[j].Style.Font = arialBoldFont;

                }
                //Set the value ofto the grid header cell. 
                grid.Headers[0].Cells[0].Value = "Product ID";
            }
            for (int i = 0; i < grid.Rows.Count; i++)
            {
                //Set the height ofto the grid row. 
                grid.Rows[i].Height = 23;
                for (int j = 0; j < grid.Columns.Count; j++)
                {
                    //Create a string format for the grid row. 
                    PdfStringFormat pdfStringFormat = new PdfStringFormat();
                    pdfStringFormat.LineAlignment = PdfVerticalAlignment.Middle;
                    pdfStringFormat.Alignment = PdfTextAlignment.Left;

                    //Set cell padding for grid row cell. 
                    if (j == 0 || j == 2)
                        grid.Rows[i].Cells[j].Style.CellPadding = new PdfPaddings(30, 1, 1, 1);

                    //Seta string format to the grid row cell. 
                    grid.Rows[i].Cells[j].StringFormat = pdfStringFormat;
                    //Set the font to the grid row cell. 
                    grid.Rows[i].Cells[j].Style.Font = arialRegularFont;
                }
            }
            //Apply built-in table style to the grid. 
            grid.ApplyBuiltinStyle(PdfGridBuiltinStyle.ListTable4Accent5);
            //Subscribeing to begin the cell layout event.
            grid.BeginCellLayout += Grid_BeginCellLayout;
            //Draw the PDF grid to the PDF page and get the layout result. 
            PdfGridLayoutResult result = grid.Draw(page, new PointF(0, y + 40));

            //Using the layout result, continue to draw the text. 
            y = result.Bounds.Bottom + lineSpace;
            format = new PdfStringFormat();
            format.Alignment = PdfTextAlignment.Center;
            RectangleF bounds = new RectangleF(QuantityCellBounds.X, y, QuantityCellBounds.Width, QuantityCellBounds.Height);
            //Draw the text to the PDF page based on the layout result. 
            page.Graphics.DrawString("Grand Total:", arialBoldFont, PdfBrushes.Black, bounds, format);
            //Draw the total amount value to the PDF page based on the layout result. 
            bounds = new RectangleF(TotalPriceCellBounds.X, y, TotalPriceCellBounds.Width, TotalPriceCellBounds.Height);
            page.Graphics.DrawString("$" + GetTotalAmount(grid).ToString(), arialBoldFont, PdfBrushes.Black, bounds);
            #endregion
            //Create a border pen with the custom dash style and draw the border to the page. 
            borderPen.DashStyle = PdfDashStyle.Custom;
            borderPen.DashPattern = new float[] { 3, 3 };
            graphics.DrawLine(borderPen, new PointF(0, pageHeight - 100), new PointF(pageWidth, pageHeight - 100));
      
            basePath = "CreatePdfDemoSample.Resources.Images.";
            //Get the image file stream from the assembly.
            Stream imageStream = assembly.GetManifestResourceStream(basePath + "AdventureWork.png");

            //Create a PDF bitmap image from the stream.
            PdfBitmap bitmap = new PdfBitmap(imageStream);
            //Draw the image to the PDF page. 
            graphics.DrawImage(bitmap, new RectangleF(10, pageHeight - 90, 80, 80));

            //Calculate the text position and draw the text to the PDF page. 
            y = pageHeight - 100 + margin;
            size = arialRegularFont.MeasureString("800 Interchange Blvd.");
            x = pageWidth - size.Width - margin;
            graphics.DrawString("800 Interchange Blvd.", arialRegularFont, PdfBrushes.Black, new PointF(x, y));

            //Calculate the text position and draw the text to the PDF page. 
            y += arialRegularFont.Height + lineSpace;
            size = arialRegularFont.MeasureString("Suite 2501,  Austin, TX 78721");
            x = pageWidth - size.Width - margin;
            graphics.DrawString("Suite 2501,  Austin, TX 78721", arialRegularFont, PdfBrushes.Black, new PointF(x, y));

            //Calculate the text position and draw the text to the PDF page. 
            y += arialRegularFont.Height + lineSpace;
            size = arialRegularFont.MeasureString("Any Questions? support@adventure-works.com");
            x = pageWidth - size.Width - margin;
            graphics.DrawString("Any Questions? support@adventure-works.com", arialRegularFont, PdfBrushes.Black, new PointF(x, y));

            using MemoryStream ms = new();
            //Saves the presentation to the memory stream.
            document.Save(ms);
            ms.Position = 0;
            //Saves the memory stream as a file.
            DependencyService.Get<ISave>().SaveAndView("Invoice.pdf", "application/pdf", ms);
        }


        #region Helper Methods
        //Create and row for the grid.
        void AddProducts(string productId, string productName, double price, int quantity, double total, PdfGrid grid)
        {
            //Add a new row and set the product value to the grid row cells. 
            PdfGridRow row = grid.Rows.Add();
            row.Cells[0].Value = productId;
            row.Cells[1].Value = productName;
            row.Cells[2].Value = price.ToString();
            row.Cells[3].Value = quantity.ToString();
            row.Cells[4].Value = total.ToString();
        }
        /// <summary>
        /// Get the Total amount of the purcharsed items.
        /// </summary>
        private float GetTotalAmount(PdfGrid grid)
        {
            float Total = 0f;
            for (int i = 0; i < grid.Rows.Count; i++)
            {
                string cellValue = grid.Rows[i].Cells[grid.Columns.Count - 1].Value.ToString();
                float result = float.Parse(cellValue, System.Globalization.CultureInfo.InvariantCulture);
                Total += result;
            }
            return Total;

        }
        #endregion

{% endhighlight %}

{% endtabs %}

A complete working example of creating a PDF document in the .NET MAUI Desktop app can be downloaded from this [link](https://www.syncfusion.com/downloads/support/directtrac/general/ze/PdfSampleMaUI-1356433164).

By executing the program in windows, you will get the **PDF document** as follows.

![MaUI Desktop output PDF document](MaUI_Images/invoice.png)

By executing the program in android, you will get the **PDF document** as follows,

![MaUI Mobile output PDF document](MaUI_Images/invoice_android.png)

By executing the program in iOS, you will get the **PDF document** as follows,

![MaUI iOS output PDF document](MaUI_Images/invoice_ios.png)

N> You can also explore our [MAUI PDF library demo](https://www.syncfusion.com/demos/fileformats/pdf-library) that shows how to create and modify PDF files from C# with just five lines of code.

## Helper files for .NET MAUI

Download the helper files from this [link](https://www.syncfusion.com/downloads/support/directtrac/general/ze/Helper_files-1664336865) and add them into the mentioned project. These helper files allow you to save the stream as a physical file and open the file for viewing.

<table>
  <tr>
  <td>
    <b>Folder Name</b>
  </td>
  <td>
    <b>File Name</b>
  </td>
  <td>
    <b>Summary</b>
  </td>
  </tr>
  <tr>
  <td>
    .NET MAUI Project
  </td>
  <td>
    SaveService.cs
  </td>
  <td>Represent the base class for save operation.
  </td>
  </tr>
  <tr>
  <td>
    Windows
  </td>
  <td>
    SaveWindows.cs
  </td>
  <td>Save implementation for Windows.
  </td>
  </tr>
  <tr>
  <td>
    Android
  </td>
  <td>
    SaveAndroid.cs
  </td>
  <td>Save implementation for Android device.
  </td>
  </tr>
  <tr>
  <td>
    Mac Catalyst
  </td>
  <td>
    SaveMac.cs
  </td>
  <td>Save implementation for Mac Catalyst device.
  </td>
  </tr>
  <tr>
  <td rowspan="2">
    iOS
  </td>
  <td>
    SaveIOS.cs
  </td>
  <td>
    Save implementation for iOS device
  </td>
  </tr>
  <tr>
  <td>
    PreviewControllerDS.cs<br/>QLPreviewItemFileSystem.cs
  </td>
  <td>
    Helper classes for viewing the <b>Pdf document</b> in iOS device
  </td>
  </tr>
</table>


