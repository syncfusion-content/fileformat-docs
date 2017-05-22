---
title: Excel to ODS Conversion
description: Briefs about Excel to ODS conversion in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Excel to ODS Conversion

The Open Document Format for Office Applications (ODF), also known as OpenDocument, is an XML-based file format for spreadsheets, charts, presentations and word processing documents. It was developed with the aim of providing an open, XML-based file format specification for office applications. OpenOffice uses ODF format as its default document format. OpenDocument Spreadsheet (ODS) is the file format for Excel documents. XlsIO supports conversion of XLS/XLSX documents to ODS.

The following code snippet illustrates the creation of simple Excel file and exporting the same to ODS format.

{% tabs %}

{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

worksheet.Range["A1"].Text = "Month";

worksheet.Range["B1"].Text = "Sales";

worksheet.Range["A5"].Text = "Total";

worksheet.Range["A2"].Text = "January";

worksheet.Range["A3"].Text = "February";

worksheet.AutofitColumn(1);

worksheet.Range["B2"].Number = 68878;

worksheet.Range["B3"].Number = 71550;

worksheet.Range["B5"].Formula = "SUM(B2:B4)";

//Comments
IComment comment = worksheet.Range["B5"].AddComment();

comment.RichText.Text = "This cell has formula.";

IRichTextString richText = comment.RichText;

IFont blueFont = workbook.CreateFont();

blueFont.Color = ExcelKnownColors.Blue;

richText.SetFont(0, 13, blueFont);

IFont redFont = workbook.CreateFont();

redFont.Color = ExcelKnownColors.Red;

richText.SetFont(14, 20, redFont);
			
//Formatting
IStyle style = workbook.Styles.Add("Style1");
style.Color = Color.DarkBlue;
style.Font.Color = ExcelKnownColors.WhiteCustom;

worksheet.Range["A1:B1"].CellStyleName = "Style1";
worksheet.Range["A5:B5"].CellStyleName = "Style1";

//Save in ODS format
workbook.SaveAs("Output.ods");

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}

Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

worksheet.Range("A1").Text = "Month"

worksheet.Range("B1").Text = "Sales"

worksheet.Range("A5").Text = "Total"

worksheet.Range("A2").Text = "January"

worksheet.Range("A3").Text = "February"

worksheet.AutofitColumn(1)

worksheet.Range("B2").Number = 68878

worksheet.Range("B3").Number = 71550

worksheet.Range("B5").Formula = "SUM(B2:B4)"

'Comments
Dim comment As IComment = worksheet.Range("B5").AddComment()

comment.RichText.Text = "This cell has formula."

Dim richText As IRichTextString = comment.RichText

Dim blueFont As IFont = workbook.CreateFont()

blueFont.Color = ExcelKnownColors.Blue

richText.SetFont(0, 13, blueFont)

Dim redFont As IFont = workbook.CreateFont()

redFont.Color = ExcelKnownColors.Red

richText.SetFont(14, 20, redFont)

'Formatting
Dim style As IStyle = workbook.Styles.Add("Style1")
style.Color = Color.DarkBlue
style.Font.Color = ExcelKnownColors.WhiteCustom

worksheet.Range("A1:B1").CellStyleName = "Style1"
worksheet.Range("A5:B5").CellStyleName = "Style1"

'Save in ODS format
workbook.SaveAs("Output.ods")

workbook.Close()

excelEngine.Dispose()

{% endhighlight %}

{% endtabs %}

## Saving ODS in different platforms

**ASP.NET**

The following code snippet illustrates how to download an OpenDocument Spreadsheet in browser after saving the document.

{% tabs %}

{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A3"].Text = "Hello World";

//Save in ODS format
workbook.SaveAs("Output.ods", ExcelSaveType.SaveAsODS, Response, ExcelDownloadType.PromptDialog);

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}

Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A3").Text = "Hello World"

'Save in ODS format
workbook.SaveAs("Output.ods", ExcelSaveType.SaveAsODS, Response, ExcelDownloadType.PromptDialog)

workbook.Close()

excelEngine.Dispose()

{% endhighlight %}

{% endtabs %}

**ASP.NET MVC**

The following code snippet illustrates how to save an OpenDocument Spreadsheet in ASP.NET MVC.

{% tabs %}

{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A3"].Text = "Hello World";

//Save in ODS format
return excelEngine.SaveAsActionResult(workbook, "ExcelToODS.ods", HttpContext.ApplicationInstance.Response, ExcelDownloadType.PromptDialog, ExcelHttpContentType.ODS);

{% endhighlight %}

{% highlight vb %}

Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A3").Text = "Hello World"

'Save in ODS format
Return excelEngine.SaveAsActionResult(workbook, "ExcelToODS.ods", HttpContext.ApplicationInstance.Response, ExcelDownloadType.PromptDialog, ExcelHttpContentType.ODS)

{% endhighlight %}

{% endtabs %}

The method SaveAsActionResult() can be referred from [here](https://help.syncfusion.com/file-formats/xlsio/asp-net-mvc#).

**UWP**

The following code snippet illustrates how to save an OpenDocument Spreadsheet in UWP using file save picker.

{% tabs %}

{% highlight c# %}

 ExcelEngine excelEngine = new ExcelEngine();

 IApplication application = excelEngine.Excel;

 application.DefaultVersion = ExcelVersion.Excel2013;
 
 //Initializes FileSavePicker.

 FileSavePicker savePicker = new FileSavePicker();

 savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

 savePicker.SuggestedFileName = "ExcelToODS";

 savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".ods" });

 StorageFile storageFile = await savePicker.PickSaveFileAsync();

 IWorkbook workbook = application.Workbooks.Create(1);

 //Save in ODS format
 await workbook.SaveAsAsync(storageFile, ExcelSaveType.SaveAsODS);

 workbook.Close();

 excelEngine.Dispose();
 
{% endhighlight %}

{% highlight vb %}

 Dim excelEngine As New ExcelEngine()

 Dim application As IApplication = excelEngine.Excel

 application.DefaultVersion = ExcelVersion.Excel2013

 'Initializes FileSavePicker.

 Dim savePicker As New FileSavePicker()

 savePicker.SuggestedStartLocation = PickerLocationId.Desktop

 savePicker.SuggestedFileName = "ExcelToODS"

 savePicker.FileTypeChoices.Add("Excel Files", New List(Of String)() From { ".ods" })

 Dim storageFile As StorageFile = Await savePicker.PickSaveFileAsync()

 'Save in ODS format
 IWorkbook workbook = application.Workbooks.Create(1)

 Await workbook.SaveAsAsync(storageFile, ExcelSaveType.SaveAsODS)

 workbook.Close()

 excelEngine.Dispose()
 
{% endhighlight %}

{% endtabs %}

## Supported and Unsupported Elements in ODS Conversion

<table>
<tr>
<td>
{{'**Category**'| markdownify }}
</td>
<td>
{{'**Subcategory**'| markdownify }}
</td>
<td>
{{'**Supported**'| markdownify }}
</td>
</tr>
<tr rowspan="10">
<td>
Formatting
</td>
<td>
Font settings<br/><br/></td>
<td>
Yes
</td>
</tr>
<tr>
<td>

</td>
<td>
Alignments
</td>
<td>
Yes (Except indent)
</td>
</tr>
<tr>
<td>

</td>
<td>
Number formatting
</td>
<td>
Yes (Partial)
</td>
</tr>
<tr>
<td>

</td>
<td>
Border settings<br/><br/></td>
<td>
Yes
</td>
</tr>
<tr>
<td>

</td>
<td>
Fill settings<br/><br/></td>
<td>
Yes
</td>
</tr>
<tr>
<td>

</td>
<td>
RGB colors 
</td>
<td>
Yes
</td>
</tr>
<tr>
<td>

</td>
<td>
Cell gradient<br/><br/></td>
<td>
No
</td>
</tr>
<tr>
<td>

</td>
<td>
Cell styles<br/><br/></td>
<td>
Yes
</td>
</tr>
<tr>
<td>

</td>
<td>
Themes
</td>
<td>
No
</td>
</tr>
<tr>
<td>

</td>
<td>
Conditional formatting<br/><br/></td>
<td>
Planned
</td>
</tr>
<tr>
<td>
Hyperlinks
</td>
<td>
-
</td>
<td>
 Yes
</td>
</tr>
<tr>
<td>
Cell Comments
</td>
<td>

</td>
<td>
Yes
</td>
</tr>
<tr>
<td>
Print
</td>
<td>
Page setup<br/><br/></td>
<td>
Yes
</td>
</tr>
<tr>
<td>

</td>
<td>
[Margin, Page size]<br/><br/></td>
<td>
Yes
</td>
</tr>
<tr>
<td>

</td>
<td>
Page breaks<br/><br/></td>
<td>
No
</td>
</tr>
<tr>
<td>

</td>
<td>
Background image<br/><br/></td>
<td>
No
</td>
</tr>
<tr>
<td>

</td>
<td>
Print settings [Print area, Print titles, Page order]<br/><br/></td>
<td>
No
</td>
</tr>
<tr>
<td>

</td>
<td>
Header/Footer<br/><br/></td>
<td>
Planned
</td>
</tr>
<tr>
<td>
Formulas
</td>
<td>

</td>
<td>
Yes (Partial)
</td>
</tr>
<tr>
<td>

</td>
<td>
Table Formulas
</td>
<td>
No
</td>
</tr>
<tr>
<td>

</td>
<td>
Names
</td>
<td>
Yes (Partial)
</td>
</tr>
<tr>
<td>
Group & Outline
</td>
<td>

</td>
<td>
Yes
</td>
</tr>
<tr>
<td>
Settings
</td>
<td>
Window Settings
</td>
<td>
No
</td>
</tr>
<tr>
<td>

</td>
<td>
Sheet/Book settings
</td>
<td>
No
</td>
</tr>
<tr>
<td>
Protection
</td>
<td>
Sheet Protection
</td>
<td>
No
</td>
</tr>
<tr>
<td>

</td>
<td>
Encryption
</td>
<td>
N/A
</td>
</tr>
<tr>
<td>
Hide/Unhide rows/cols<br/><br/></td>
<td>

</td>
<td>
Yes
</td>
</tr>
<tr>
<td>
Copy/Move worksheet<br/><br/></td>
<td>

</td>
<td>
Yes
</td>
</tr>
<tr>
<td>
Image<br/><br/></td>
<td>

</td>
<td>
No
</td>
</tr>
<tr>
<td>
Data Validation
</td>
<td>

</td>
<td>
No
</td>
</tr>
<tr>
<td>
Tables
</td>
<td>

</td>
<td>
Planned
</td>
</tr>
<tr>
<td>
PivotTable
</td>
<td>

</td>
<td>
No
</td>
</tr>
<tr>
<td>
Charts
</td>
<td>

</td>
<td>
Planned
</td>
</tr>
<tr>
<td>
Drawing
</td>
<td>

</td>
<td>
Planned
</td>
</tr>
<tr>
<td>
OLE Objects
</td>
<td>

</td>
<td>
No
</td>
</tr>
</table>
