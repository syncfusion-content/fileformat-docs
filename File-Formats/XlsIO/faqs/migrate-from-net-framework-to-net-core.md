---
title: Migrate from net framework to net core | XlsIO | Syncfusion
description: This page explains migration of .NET Framework to .NET Core
platform: file-formats
control: XlsIO
documentation: UG
---

# How to migrate from net framework to net core?

Syncfusion has deprecated the ASP.NET NuGet packages. We recommend that you use .NETCore NuGet packages instead. We have provided the major changes that need to be made in your application when migrating to .NETCore packages.

### NuGet Changes
<table>
        <tr>
            <td>
                <b>.NET Framework</b>
            </td>
            <td>
                <b>.NET Core</b>
            </td>
        </tr>
        <tr>
            <td>
                {{'[Syncfusion.XlsIO.AspNet](https://www.NuGet.org/packages/Syncfusion.XlsIO.AspNet)'| markdownify }}
            </td>
            <td>
               {{'[Syncfusion.XlsIO.Net.Core](https://www.NuGet.org/packages/Syncfusion.XlsIO.Net.Core)'| markdownify }}
            </td>
        </tr>
        <tr>
            <td>
                {{'[Syncfusion.ExcelToPdfConverter.AspNet](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.AspNet)'| markdownify }}
            </td>
            <td>
                {{'[Syncfusion.XlsIORenderer](https://www.NuGet.org/packages/Syncfusion.XlsIORenderer.Net.Core)'| markdownify }}
            </td>
        </tr>
        <tr>
            <td>
                {{'[Syncfusion.ExcelChartToImageConverter.AspNet](https://www.NuGet.org/packages/Syncfusion.ExcelChartToImageConverter.AspNet)'| markdownify }}
            </td>
            <td>
                Not needed. This functionalities are moved to {{'[Syncfusion.XlsIORenderer](https://www.NuGet.org/packages/Syncfusion.XlsIORenderer.Net.Core)'| markdownify }}
            </td>
        </tr>
</table>

### Namespaces

<table>
        <tr>
            <td>
                <b>.NET Framework</b> 
            </td>
            <td>
                <b>.NET Core</b> 
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.XlsIO 
            </td>
            <td>
                Syncfusion.XlsIO 
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.XlsIORenderer 
            </td>
            <td>
                Syncfusion.XlsIORenderer 
            </td>
        </tr>
</table>

### Missing Types
<table>
        <tr>
            <td>
                <b>Missing Types</b> 
            </td>
            <td>
                <b>Alternate Types</b> 
            </td>
        </tr>
        <tr>
            <td>
                ExcelToPDFConverter
            </td>
            <td>
                XlsIORenderer 
            </td>
        </tr>
        <tr>
            <td>
                ExcelChartToImageConverter 
            </td>
            <td>
                XlsIORenderer 
            </td>
        </tr>
</table>


### Missing Properties
<table>
        <tr>
            <td>
                <b>Missing Properties</b> 
            </td>
            <td>
                <b>Alternate Properties</b> 
            </td>
        </tr>
        <tr>
            <td>
                IApplication ChartToImageConverter 
            </td>
            <td>
                IApplication XlsIORenderer 
            </td>
        </tr>
</table>

### Missing methods
<table>
        <tr>
            <td>
                <b>Missing methods</b> 
            </td>
            <td>
                <b>Alternate methods</b> 
            </td>
        </tr>
        <tr>
            <td>
                IWorkbooks Open(string filename)   
            </td>
            <td>
			The document can be loaded into a file stream and it can be used as a input for XlsIO. 
                IWorkbooks Open(Stream stream)                   
            </td>
        </tr>
        <tr>
            <td>
                IWorkbook SaveAs(string filename, HttpResponse Response, ExcelDownloadType type) 
            </td>
            <td>
			The workbook can be saved into a stream and it can be downloaded with the API File(string fileName, string contentType) from controller.
                IWorkbook SaveAs(Stream stream) 
            </td>
        </tr>
        <tr>
            <td>
                IWorkbook SaveAsJson(string filename) 
            </td>
            <td>
                IWorkbook SaveAsJson(Stream stream) 
            </td>
        </tr>
        <tr>
            <td>
                IWorksheet ImportHtmlTable(string filename, int row, int column) 
            </td>
            <td>
                IWorksheet ImportHtmlTable(Stream stream, int row, int column) 
            </td>
        </tr>
		<tr>
            <td>
                IPictures Add(int row, int column, string filename) 
            </td>
            <td>
                IPictures Add(int row, int column, Stream stream) 
            </td>
        </tr>
        <tr>
            <td>
                IListObject Refresh() 
            </td>
            <td>
                Not supported due to .NET Framework limitation. 
            </td>
        </tr>
        <tr>
            <td>
                ExcelToPdfConverter ExcelToPdfConverter(IWorkbook workbook) 
            </td>
            <td>
                XlsIORenderer XlsIORenderer() 
            </td>
        </tr>
        <tr>
            <td>
                ExcelToPdfConverter Convert() 
            </td>
            <td>
                XlsIORenderer ConvertToPDF(IWorkbook workbook) 
            </td>
        </tr>
</table>


### Advantages
*	Supports Windows, macOS, and Linux.

### Known limitations
*	EMF and WMF images are not supported in .NET Core platforms.
*	Import data from DataGrid, GridView, and DataGridView are not supported in .NET Core platforms.

### Notable changes
*	Drawing library: In .NET Framework, our library makes use of System.Drawing for any text measuring and graphics related operations. Whereas in .NET Core, our library makes use of SkiaSharp graphics library to provide the same type of graphics operations in all the supported platforms.
*	The features such as Excel to PDF, Excel to image, and Chart to image which makes use of SkiaSharp graphics library are separated into a separate package “Syncfusion.XlsIORenderer.Net.Core”

### Alternate solution
If you want to migrate without any code changes, you can use of the below NuGet Packages when using .NET Framework in your application.

*	[Syncfusion.XlsIO.WinForms](https://www.NuGet.org/packages/Syncfusion.XlsIO.WinForms)
*	[Syncfusion.XlsIO.Wpf](https://www.NuGet.org/packages/Syncfusion.XlsIO.Wpf)
*	[Syncfusion.ExcelToPdfConverter.WinForms](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.WinForms)
*	[Syncfusion.ExcelToPdfConverter.Wpf](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.Wpf)
*	[Syncfusion.ExcelChartToImageConverter.Wpf](https://www.NuGet.org/packages/Syncfusion.ExcelChartToImageConverter.WPF)

The above approach is not recommended.
