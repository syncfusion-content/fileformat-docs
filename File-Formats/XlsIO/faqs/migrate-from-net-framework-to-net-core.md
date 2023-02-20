---
title: Migrate from net framework to net core | XlsIO | Syncfusion
description: This section explains migrating Syncfusion .NET Excel (XlsIO) library from .NET Framework to .NET core.
platform: file-formats
control: XlsIO
documentation: UG
---

# Migrate-from-net-framework-to-net-core

In this section, we will see about the changes which need to be considered while migrating Syncfusion .NET Excel (XlsIO) library from .NET Framework to .NET Core.

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
				{{'[Syncfusion.XlsIO.Wpf](https://www.nuget.org/packages/Syncfusion.XlsIO.Wpf)'| markdownify}}
				{{'[Syncfusion.XlsIO.WinForms](https://www.nuget.org/packages/Syncfusion.XlsIO.WinForms)'| markdownify}}
                {{'[Syncfusion.XlsIO.AspNet](https://www.NuGet.org/packages/Syncfusion.XlsIO.AspNet)'| markdownify }}
                {{'[Syncfusion.XlsIO.AspNet.Mvc4](https://www.NuGet.org/packages/Syncfusion.XlsIO.AspNet.Mvc5)'| markdownify }}
                {{'[Syncfusion.XlsIO.AspNet.Mvc5](https://www.NuGet.org/packages/Syncfusion.XlsIO.AspNet.Mvc4)'| markdownify }}
            </td>
            <td>
               {{'[Syncfusion.XlsIO.Net.Core](https://www.NuGet.org/packages/Syncfusion.XlsIO.Net.Core)'| markdownify }}
            </td>
        </tr>
        <tr>
            <td>
			{{'[Syncfusion.ExcelToPdfConverter.WinForms](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.WinForms)'| markdownify }}
			{{'[Syncfusion.ExcelToPdfConverter.Wpf](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.Wpf)'| markdownify }}
			{{'[Syncfusion.ExcelToPdfConverter.AspNet](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.AspNet)'| markdownify }}
			{{'[Syncfusion.ExcelToPdfConverter.AspNet.Mvc4](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.AspNet.Mvc4)'| markdownify }}
                {{'[Syncfusion.ExcelToPdfConverter.AspNet.Mvc5](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.AspNet.Mvc5)'| markdownify }}
            </td>
            <td>
                {{'[Syncfusion.XlsIORenderer](https://www.NuGet.org/packages/Syncfusion.XlsIORenderer.Net.Core)'| markdownify }}
            </td>
        </tr>
        <tr>
            <td>
             {{'[Syncfusion.ExcelChartToImageConverter.Wpf](https://www.NuGet.org/packages/Syncfusion.ExcelChartToImageConverter.Wpf)'| markdownify }}
			{{'[Syncfusion.ExcelChartToImageConverter.AspNet](https://www.NuGet.org/packages/Syncfusion.ExcelChartToImageConverter.AspNet)'| markdownify }}
			{{'[Syncfusion.ExcelChartToImageConverter.AspNet.Mvc4](https://www.NuGet.org/packages/Syncfusion.ExcelChartToImageConverter.AspNet.Mvc4)'| markdownify }}
                {{'[Syncfusion.ExcelChartToImageConverter.AspNet.Mvc5](https://www.NuGet.org/packages/Syncfusion.ExcelChartToImageConverter.AspNet.Mvc5)'| markdownify }}
            </td>
            <td>
                Not needed. Same functionalities are moved to {{'[Syncfusion.XlsIORenderer](https://www.NuGet.org/packages/Syncfusion.XlsIORenderer.Net.Core)'| markdownify }}
            </td>
        </tr>
</table>

### Namespace changes

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
                {{'[Syncfusion.ExcelToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPdfConverter.html)'| markdownify}}
            </td>
            <td>
                Syncfusion.XlsIORenderer 
            </td>
        </tr>
		<tr>
            <td>
                {{'[Syncfusion.ExcelChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelChartToImageConverter.html)'| markdownify}}
            </td>
            <td>
                Syncfusion.XlsIORenderer 
            </td>
        </tr>
</table>

### Type Changes
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
                {{'[ExcelToPDFConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPdfConverter.ExcelToPdfConverter.html)'| markdownify}}
            </td>
            <td>
                XlsIORenderer 
            </td>
        </tr>
        <tr>
            <td>
                {{'[ExcelChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelChartToImageConverter.ChartToImageConverter.html)'| markdownify}}
            </td>
            <td>
                XlsIORenderer 
            </td>
        </tr>
	   <tr>
            <td>
                {{'[ExcelToPdfConverterSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPdfConverter.ExcelToPdfConverterSettings.html)'| markdownify}}
            </td>
            <td>
                XlsIORendererSettings
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
                {{'[IApplication ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IApplication.html#Syncfusion_XlsIO_IApplication_ChartToImageConverter)'| markdownify}}
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
                {{'[IWorkbooks Open(string filename)](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_String_)'| markdownify}}
            </td>
            <td>
			The document can be opened as a file stream from the file system using IWorkbooks Open(Stream stream)                   
            </td>
        </tr>
        <tr>
            <td>
                {{'[IWorkbook SaveAs(string filename, HttpResponse Response, ExcelDownloadType type)](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_String_Syncfusion_XlsIO_ExcelSaveType_System_Web_HttpResponse_)'| markdownify}}
            </td>
            <td>
			The document can be saved as a file stream to the file system using IWorkbook SaveAs(Stream stream) 
            </td>
        </tr>
        <tr>
            <td>
                {{'[IWorkbook SaveAsJson(string filename)](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAsJson_System_String_)'| markdownify}}
            </td>
            <td>
                The document can be saved as a file stream to the file system using IWorkbook SaveAsJson(Stream stream) 
            </td>
        </tr>
        <tr>
            <td>
                {{'[IWorksheet ImportHtmlTable(string filename, int row, int column)](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_ImportHtmlTable_System_String_System_Int32_System_Int32_)'| markdownify}}
            </td>
            <td>
                The HTML table can be imported as a file stream from the file system using IWorksheet ImportHtmlTable(Stream stream, int row, int column) 
            </td>
        </tr>
		<tr>
            <td>
                {{'[IPictures Add(int row, int column, string filename)](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPictures.html#Syncfusion_XlsIO_IPictures_AddPicture_System_Int32_System_Int32_System_Int32_System_Int32_System_String_)'| markdownify}}
            </td>
            <td>
                A picture can be added as a stream from the file system using IPictures Add(int row, int column, Stream stream) 
            </td>
        </tr>
        <tr>
            <td>
                {{'[IListObject Refresh()](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IListObject.html#Syncfusion_XlsIO_IListObject_Refresh)'| markdownify}}
            </td>
            <td>
                Not supported due to .NET Framework limitation. 
            </td>
        </tr>
        <tr>
            <td>
                {{'[ExcelToPdfConverter ExcelToPdfConverter(IWorkbook workbook)](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPdfConverter.ExcelToPdfConverter.html#Syncfusion_ExcelToPdfConverter_ExcelToPdfConverter__ctor_Syncfusion_XlsIO_IWorkbook_)'| markdownify}}
            </td>
            <td>
                XlsIORenderer XlsIORenderer() 
            </td>
        </tr>
        <tr>
            <td>
                {{'[ExcelToPdfConverter Convert()](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPdfConverter.ExcelToPdfConverter.html#Syncfusion_ExcelToPdfConverter_ExcelToPdfConverter_Convert)'| markdownify}}
            </td>
            <td>
                XlsIORenderer ConvertToPDF(IWorkbook workbook) 
            </td>
        </tr>
</table>


### Advantages
*	Supports Windows, macOS, Linux, docker, Azure, and AWS environments.

### Known limitations
*	EMF and WMF images are not supported in .NET Core platforms.
*	Import data from DataGrid, GridView, and DataGridView are not supported in .NET Core platforms.

### Notable changes
*	Drawing library: In .NET Framework, our library makes use of System.Drawing for any text measuring and graphics related operations. Whereas in .NET Core, our library makes use of SkiaSharp graphics library to provide the same type of graphics operations in all the supported platforms.
*	The features such as Excel to PDF, Excel to image, and Chart to image which makes use of SkiaSharp graphics library are separated into a separate package [Syncfusion.XlsIORenderer.Net.Core](https://www.NuGet.org/packages/Syncfusion.XlsIORenderer.Net.Core)

N>If you want to migrate without any code changes, you can use of the below NuGet Packages when using .NET Framework in your application.
N>*	[Syncfusion.XlsIO.WinForms](https://www.NuGet.org/packages/Syncfusion.XlsIO.WinForms)
N>*	[Syncfusion.XlsIO.Wpf](https://www.NuGet.org/packages/Syncfusion.XlsIO.Wpf)
N>*	[Syncfusion.ExcelToPdfConverter.WinForms](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.WinForms)
N>*	[Syncfusion.ExcelToPdfConverter.Wpf](https://www.NuGet.org/packages/Syncfusion.ExcelToPdfConverter.Wpf)
N>*	[Syncfusion.ExcelChartToImageConverter.Wpf](https://www.NuGet.org/packages/Syncfusion.ExcelChartToImageConverter.WPF)
N>The above approach is not recommended.