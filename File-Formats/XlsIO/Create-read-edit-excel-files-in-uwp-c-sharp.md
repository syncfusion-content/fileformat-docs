---
title: Create, read, and edit Excel files in UWP | Syncfusion
description: This section explains how to create, read, and edit Excel files in UWP applications using Syncfusion XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---
# Create, read, and edit Excel files in UWP

[Syncfusion Excel library for UWP platform](https://www.syncfusion.com/excel-framework/uwp/excel-library) can be used to create, read, edit Excel files. This also convert Excel files to PDF.

## Create a simple Excel report

The below steps illustrates creating an simple Invoice formatted Excel document in UWP application.

1.Create a new C# Blank App (Universal Windows) project.

![Create UWP application in Visual Studio](UWP_images/UWP_images_img1.png)

2.Install the [Syncfusion.XlsIO.UWP](https://www.nuget.org/packages/Syncfusion.XlsIO.UWP) NuGet package as reference to your .NET Framework applications from [NuGet.org](https://www.nuget.org).

![Add XlsIO reference to the project](UWP_images/UWP_images_img2.png)

3.Add a new button in the MainPage.xaml as shown below.

{% tabs %}  
{% highlight XAML %}
<Page
    x:Class="GettingStarted_UWP.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:GettingStarted_UWP"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <Button x:Name="button" Content="Create Document" Click="OnButtonClicked" HorizontalAlignment="Center" VerticalAlignment="Center"/>
    </Grid>
</Page>
{% endhighlight %}
{% endtabs %}  

4.Include the following namespaces in the MainPage.xaml.cs file.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Windows.Storage.Pickers;
using Windows.Storage;
using Windows.UI;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Imports Syncfusion.XlsIO
Imports Windows.Storage.Pickers
Imports Windows.Storage
Imports Windows.UI
{% endhighlight %}
{% endtabs %}   

5.Include the below code snippet in the click event of the button in MainPage.xaml.cs, to create an Excel file and save the Excel document as a physical file and open the file for viewing.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//Create an instance of ExcelEngine.
using (ExcelEngine excelEngine = new ExcelEngine())
{
	IApplication application = excelEngine.Excel;

	application.DefaultVersion = ExcelVersion.Xlsx;

	//Create a workbook with a worksheet
	IWorkbook workbook = application.Workbooks.Create(1);

	//Access first worksheet from the workbook instance.
	IWorksheet worksheet = workbook.Worksheets[0];

	Assembly executingAssembly = typeof(MainPage).GetTypeInfo().Assembly;
	Stream inputStream = executingAssembly.GetManifestResourceStream("GettingStarted_UWP.AdventureCycles-Logo.png");

	//Add a picture
	IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, inputStream, 20, 20);

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
	worksheet.Range["D1"].CellStyle.Font.RGBColor = ColorHelper.FromArgb(0, 42, 118, 189);
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
	worksheet.Range["D5:E5"].CellStyle.Color = ColorHelper.FromArgb(0, 42, 118, 189);
	worksheet.Range["D7:E7"].CellStyle.Color = ColorHelper.FromArgb(0, 42, 118, 189);

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
	worksheet.Range["A7"].CellStyle.Color = ColorHelper.FromArgb(0, 42, 118, 189);
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

	//Merge column A and B from row 15 to 22
	worksheet.Range["A15:B15"].Merge();
	worksheet.Range["A16:B16"].Merge();
	worksheet.Range["A17:B17"].Merge();
	worksheet.Range["A18:B18"].Merge();
	worksheet.Range["A19:B19"].Merge();
	worksheet.Range["A20:B20"].Merge();
	worksheet.Range["A21:B21"].Merge();
	worksheet.Range["A22:B22"].Merge();

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
	worksheet.Range["A15:E15"].CellStyle.Color = ColorHelper.FromArgb(0, 42, 118, 189);

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


	// Save the Workbook
	StorageFile storageFile;
	if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
		savePicker.SuggestedFileName = "Output";
		savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
		storageFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		storageFile = await local.CreateFileAsync("Output.xlsx", CreationCollisionOption.ReplaceExisting);
	}
	//Saving the workbook
	await workbook.SaveAsAsync(storageFile);

	// Launch the saved file
	await Windows.System.Launcher.LaunchFileAsync(storageFile);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub OnButtonClicked(ByVal sender As Object, ByVal args As EventArgs)
'Create an instance of ExcelEngine
Using excelEngine As ExcelEngine = New ExcelEngine()

	Dim application As IApplication = excelEngine.Excel

	application.DefaultVersion = ExcelVersion.Xlsx

	'Create a workbook
	Dim workbook As IWorkbook = application.Workbooks.Create(1)
	Dim worksheet As IWorksheet = workbook.Worksheets(0)

	'Adding a picture
	Dim executingAssembly As Assembly = GetType(MainPage).GetTypeInfo().Assembly
	Dim inputStream As Stream = executingAssembly.GetManifestResourceStream("GettingStarted_UWP.AdventureCycles-Logo.png")
	Dim shape As IPictureShape = worksheet.Pictures.AddPicture(1, 1, inputStream, 20, 20)

	'Disable gridlines in the worksheet
	worksheet.IsGridLinesVisible = False

	'Enter values to the cells from A3 to A5
	worksheet.Range("A3").Text = "46036 Michigan Ave"
	worksheet.Range("A4").Text = "Canton, USA"
	worksheet.Range("A5").Text = "Phone: +1 231-231-2310"

	'Make the text bold
	worksheet.Range("A3:A5").CellStyle.Font.Bold = True

	'Merge cells
	worksheet.Range("D1:E1").Merge()

	'Enter text to the cell D1 and apply formatting.
	worksheet.Range("D1").Text = "INVOICE"
	worksheet.Range("D1").CellStyle.Font.Bold = True
	worksheet.Range("D1").CellStyle.Font.RGBColor = ColorHelper.FromArgb(0, 42, 118, 189)
	worksheet.Range("D1").CellStyle.Font.Size = 35

	'Apply alignment in the cell D1
	worksheet.Range("D1").CellStyle.HorizontalAlignment = ExcelHAlign.HAlignRight
	worksheet.Range("D1").CellStyle.VerticalAlignment = ExcelVAlign.VAlignTop

	'Enter values to the cells from D5 to E8
	worksheet.Range("D5").Text = "INVOICE#"
	worksheet.Range("E5").Text = "DATE"
	worksheet.Range("D6").Number = 1028
	worksheet.Range("E6").Value = "12/31/2018"
	worksheet.Range("D7").Text = "CUSTOMER ID"
	worksheet.Range("E7").Text = "TERMS"
	worksheet.Range("D8").Number = 564
	worksheet.Range("E8").Text = "Due Upon Receipt"

	'Apply RGB back color to the cells from D5 to E8
	worksheet.Range("D5:E5").CellStyle.Color = ColorHelper.FromArgb(0, 42, 118, 189)
	worksheet.Range("D7:E7").CellStyle.Color = ColorHelper.FromArgb(0,42, 118, 189)

	'Apply known colors to the text in cells D5 to E8
	worksheet.Range("D5:E5").CellStyle.Font.Color = ExcelKnownColors.White
	worksheet.Range("D7:E7").CellStyle.Font.Color = ExcelKnownColors.White

	'Make the text as bold from D5 to E8
	worksheet.Range("D5:E8").CellStyle.Font.Bold = True

	'Apply alignment to the cells from D5 to E8
	worksheet.Range("D5:E8").CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter
	worksheet.Range("D5:E5").CellStyle.VerticalAlignment = ExcelVAlign.VAlignCenter
	worksheet.Range("D7:E7").CellStyle.VerticalAlignment = ExcelVAlign.VAlignCenter
	worksheet.Range("D6:E6").CellStyle.VerticalAlignment = ExcelVAlign.VAlignTop

	'Enter value and applying formatting in the cell A7
	worksheet.Range("A7").Text = "  BILL TO"
	worksheet.Range("A7").CellStyle.Color = ColorHelper.FromArgb(0, 42, 118, 189)
	worksheet.Range("A7").CellStyle.Font.Bold = True
	worksheet.Range("A7").CellStyle.Font.Color = ExcelKnownColors.White

	'Apply alignment
	worksheet.Range("A7").CellStyle.HorizontalAlignment = ExcelHAlign.HAlignLeft
	worksheet.Range("A7").CellStyle.VerticalAlignment = ExcelVAlign.VAlignCenter

	'Enter values in the cells A8 to A12
	worksheet.Range("A8").Text = "Steyn"
	worksheet.Range("A9").Text = "Great Lakes Food Market"
	worksheet.Range("A10").Text = "20 Whitehall Rd"
	worksheet.Range("A11").Text = "North Muskegon,USA"
	worksheet.Range("A12").Text = "+1 231-654-0000"

	'Create a Hyperlink for e-mail in the cell A13
	Dim hyperlink As IHyperLink = worksheet.HyperLinks.Add(worksheet.Range("A13"))
	hyperlink.Type = ExcelHyperLinkType.Url
	hyperlink.Address = "Steyn@greatlakes.com"
	hyperlink.ScreenTip = "Send Mail"

	'Merge column A and B from row 15 to 22
	worksheet.Range("A15:B15").Merge()
	worksheet.Range("A16:B16").Merge()
	worksheet.Range("A17:B17").Merge()
	worksheet.Range("A18:B18").Merge()
	worksheet.Range("A19:B19").Merge()
	worksheet.Range("A20:B20").Merge()
	worksheet.Range("A21:B21").Merge()
	worksheet.Range("A22:B22").Merge()

	'Enter details of products and prices
	worksheet.Range("A15").Text = "  DESCRIPTION"
	worksheet.Range("C15").Text = "QTY"
	worksheet.Range("D15").Text = "UNIT PRICE"
	worksheet.Range("E15").Text = "AMOUNT"
	worksheet.Range("A16").Text = "Cabrales Cheese"
	worksheet.Range("A17").Text = "Chocos"
	worksheet.Range("A18").Text = "Pasta"
	worksheet.Range("A19").Text = "Cereals"
	worksheet.Range("A20").Text = "Ice Cream"
	worksheet.Range("C16").Number = 3
	worksheet.Range("C17").Number = 2
	worksheet.Range("C18").Number = 1
	worksheet.Range("C19").Number = 4
	worksheet.Range("C20").Number = 3
	worksheet.Range("D16").Number = 21
	worksheet.Range("D17").Number = 54
	worksheet.Range("D18").Number = 10
	worksheet.Range("D19").Number = 20
	worksheet.Range("D20").Number = 30
	worksheet.Range("D23").Text = "Total"

	'Apply number format
	worksheet.Range("D16:E22").NumberFormat = "$.00"
	worksheet.Range("E23").NumberFormat = "$.00"

	'Apply incremental formula for column Amount by multiplying Qty and UnitPrice
	application.EnableIncrementalFormula = True
	worksheet.Range("E16:E20").Formula = "=C16*D16"

	'Formula for Sum the total
	worksheet.Range("E23").Formula = "=SUM(E16:E22)"

	'Apply borders
	worksheet.Range("A16:E22").CellStyle.Borders(ExcelBordersIndex.EdgeTop).LineStyle = ExcelLineStyle.Thin
	worksheet.Range("A16:E22").CellStyle.Borders(ExcelBordersIndex.EdgeBottom).LineStyle = ExcelLineStyle.Thin
	worksheet.Range("A16:E22").CellStyle.Borders(ExcelBordersIndex.EdgeTop).Color = ExcelKnownColors.Grey_25_percent
	worksheet.Range("A16:E22").CellStyle.Borders(ExcelBordersIndex.EdgeBottom).Color = ExcelKnownColors.Grey_25_percent
	worksheet.Range("A23:E23").CellStyle.Borders(ExcelBordersIndex.EdgeTop).LineStyle = ExcelLineStyle.Thin
	worksheet.Range("A23:E23").CellStyle.Borders(ExcelBordersIndex.EdgeBottom).LineStyle = ExcelLineStyle.Thin
	worksheet.Range("A23:E23").CellStyle.Borders(ExcelBordersIndex.EdgeTop).Color = ExcelKnownColors.Black
	worksheet.Range("A23:E23").CellStyle.Borders(ExcelBordersIndex.EdgeBottom).Color = ExcelKnownColors.Black

	'Apply font setting for cells with product details
	worksheet.Range("A3:E23").CellStyle.Font.FontName = "Arial"
	worksheet.Range("A3:E23").CellStyle.Font.Size = 10
	worksheet.Range("A15:E15").CellStyle.Font.Color = ExcelKnownColors.White
	worksheet.Range("A15:E15").CellStyle.Font.Bold = True
	worksheet.Range("D23:E23").CellStyle.Font.Bold = True

	'Apply cell color
	worksheet.Range("A15:E15").CellStyle.Color = ColorHelper.FromArgb(0, 42, 118, 189)

	'Apply alignment to cells with product details
	worksheet.Range("A15").CellStyle.HorizontalAlignment = ExcelHAlign.HAlignLeft
	worksheet.Range("C15:C22").CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter
	worksheet.Range("D15:E15").CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter

	'Apply row height and column width to look good
	worksheet.Range("A1").ColumnWidth = 36
	worksheet.Range("B1").ColumnWidth = 11
	worksheet.Range("C1").ColumnWidth = 8
	worksheet.Range("D1:E1").ColumnWidth = 18
	worksheet.Range("A1").RowHeight = 47
	worksheet.Range("A2").RowHeight = 15
	worksheet.Range("A3:A4").RowHeight = 15
	worksheet.Range("A5").RowHeight = 18
	worksheet.Range("A6").RowHeight = 29
	worksheet.Range("A7").RowHeight = 18
	worksheet.Range("A8").RowHeight = 15
	worksheet.Range("A9:A14").RowHeight = 15
	worksheet.Range("A15:A23").RowHeight = 18

	'Save the Workbook
	Dim storageFile As StorageFile
	If Not Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons") Then
		Dim savePicker As FileSavePicker = New FileSavePicker
		savePicker.SuggestedStartLocation = PickerLocationId.Desktop
		savePicker.SuggestedFileName = "Output"
		savePicker.FileTypeChoices.Add("Excel Files", New List(Of String))
		storageFile = savePicker.PickSaveFileAsync
	Else
		Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder
		storageFile = local.CreateFileAsync("Output.xlsx", CreationCollisionOption.ReplaceExisting)
	End If

	'Saving the workbook
	Function workbook_SaveAsAsync_((ByVal Unknown As storageFile) As await Implements workbook.SaveAsAsync.(Of
	End Function

	'Launch the saved file
	Function Windows_System_Launcher_LaunchFileAsync_((ByVal Unknown As storageFile) As await Implements Windows.System.Launcher.LaunchFileAsync.(Of
	End Function
End Using
{% endhighlight %}
{% endtabs %} 

A complete working example of how to create an Excel file in UWP in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/UWP/Create%20Excel).

By executing the program, you will get the Excel file as below.
![Output File](UWP_images/UWP_images_img3.png)

## Read and Edit Excel file

The below code illustrates how to read and edit an Excel file in UWP.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Create an instance of ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Instantiates the File Picker. 
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".xlsx");
openPicker.FileTypeFilter.Add(".xls");
StorageFile openFile = await openPicker.PickSingleFileAsync();

//Opens the workbook. 
IWorkbook workbook = await application.Workbooks.OpenAsync(openFile);

//Access first worksheet from the workbook.
IWorksheet worksheet = workbook.Worksheets[0];

//Set Text in cell A3.
worksheet.Range["A3"].Text ="Hello World";

//Access a cell value from Excel
var value = worksheet.Range["A1"].Value;

//Sets workbook version.
workbook.Version = ExcelVersion.Xlsx;

//Initializes FileSavePicker.
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "CreateSpreadsheet";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker.
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file.
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create an instance of ExcelEngine
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'Instantiates the File Save Picker.  
Dim openPicker As New FileOpenPicker()
openPicker.SuggestedStartLocation = PickerLocationId.Desktop 
openPicker.FileTypeFilter.Add(".xlsx") 
openPicker.FileTypeFilter.Add(".xls") 
Dim openFile As StorageFile = Await openPicker.PickSingleFileAsync()

'Opens the Workbook. 
Dim workbook As IWorkbook = Await application.Workbooks.OpenAsync(openFile)
Dim workbook.SaveAsAsyncCType(As await, openFile)

'Access first worksheet from the workbook.
Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Set Text in cell A3.
worksheet.Range("A3").Text ="Hello World"

'Access a cell value from Excel
Dim value As var = worksheet.Range("A1").Value

'Sets workbook version.
workbook.Version = ExcelVersion.Xlsx

'Initializes FileSavePicker.
Dim savePicker As New FileSavePicker()
savePicker.SuggestedStartLocation = PickerLocationId.Desktop
savePicker.SuggestedFileName = "CreateSpreadsheet"
savePicker.FileTypeChoices.Add("Excel Files", New List(Of String)() From {".xlsx"})

'Creates a storage file from FileSavePicker.
Dim storageFile As StorageFile = Await savePicker.PickSaveFileAsync()

'Saves changes to the specified storage file.
Await workbook.SaveAsAsync(storageFile)

workbook.Close()
excelEngine.Dispose()
{% endhighlight %}
{% endtabs %}  

A complete working example of how to read and edit an Excel file in UWP in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/UWP/Edit%20Excel).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your applications to use our components. You can also explore our [UWP Excel library demo](https://www.syncfusion.com/demos/fileformats/excel-library) that shows how to create and modify Excel files from C# with just five lines of code.
