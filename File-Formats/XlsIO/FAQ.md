---
title: FAQ Section
description: Frequently Asked Questions in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# FAQ Section  

The frequently asked questions in Essential XlsIO are listed below.

## How to open an existing Xlsx workbook and save it as Xls?

You can open and save an existing .xlsx file to the .xls file by using XlsIO. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Open an existing Excel 2013 file.

IWorkbook workbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

//Save it as "Excel 97 to 2003" format.

workbook.Version = ExcelVersion.Excel97to2003;

workbook.SaveAs("Output.xls");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'Open an existing Excel 2013 file.

Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)            

'Save it as "Excel 97 to 2003" format.

workbook.Version = ExcelVersion.Excel97to2003

workbook.SaveAs("Output.xls")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

N> Workbook must be saved in appropriate version, failing in this leads to file corruption.

## How to open an Excel file from Stream?

XlsIO provides support for opening a file that is stored as a stream. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

//Opening a File from a Stream

FileStream filestream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

IWorkbook workbook = application.Workbooks.Open(filestream);

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

'Opening a File from a Stream

Dim filestream As New FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite)

Dim workbook As IWorkbook = application.Workbooks.Open(filestream)

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to save a file to stream?

XlsIO provides support to save a worksheet to a .NET stream. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

//Save the workbook to stream.

FileStream filestream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);

workbook.SaveAs(filestream);

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

'Save the workbook to stream.

Dim filestream As New FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite)

workbook.SaveAs(filestream)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to create and open Excel Template files by using XlsIO?

**Creating** **Excel** **Template** **Files**

Excel template files (XLT or XLTX) can be created in XlsIO by saving a file as **Template** using **ExcelSaveType** enumeration. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Save as XLT.

workbook.Version = ExcelVersion.Excel97to2003;

workbook.SaveAs("XltFile.xlt", ExcelSaveType.SaveAsTemplate);

//Save as XLTX.

workbook.Version = ExcelVersion.Excel2007;

workbook.SaveAs("XltxFile.xltx", ExcelSaveType.SaveAsTemplate);

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Save as XLT.

workbook.Version = ExcelVersion.Excel97to2003

workbook.SaveAs("XltFile.xlt", ExcelSaveType.SaveAsTemplate)

'Save as XLTX.

workbook.Version = ExcelVersion.Excel2007

workbook.SaveAs("XltxFile.xltx", ExcelSaveType.SaveAsTemplate)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

**Opening** **Excel** **Template** **Files**

In XlsIO, an Excel template file is opened in the same way, as excel workbook (.xls and .xlsx) is opened. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

//Open Excel Template.

IWorkbook workbook = application.Workbooks.Open("Sample.xltx", ExcelOpenType.Automatic);

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();       



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

'Open Excel Template.

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xltx", ExcelOpenType.Automatic)

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to open an Excel 2013 Macro Enabled Template?

You can open and save an Excel 2013 Macro Enabled Template to XLSM (Excel 2013 Macro Enabled Document) format. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

//Open an existing XLTM file.

IWorkbook workbook = application.Workbooks.Open("Sample.xltm", ExcelOpenType.Automatic);

//Save the file as XLSM.

workbook.SaveAs("Output.xlsm");  

workbook.Close();

excelEngine.Dispose();       



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

'Open an existing XLTM file.

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xltm", ExcelOpenType.Automatic)

'Save the file as XLSM.

workbook.SaveAs("Output.xlsm")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to change the grid line color of the Excel sheet?

In Essential XlsIO, you can change the grid line color of the worksheet using **GridLineColor** property. The below code snippet illustrate this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//To change the grid line color using ExcelKnownColors

worksheet.GridLineColor = ExcelKnownColors.Blue;

workbook.SaveAs("GridLineColor.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'To change the grid line color using ExcelKnownColors

worksheet.GridLineColor = ExcelKnownColors.Blue

workbook.SaveAs("GridLineColor.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to copy and paste the values of the cells that contain only formulas?

You can copy and paste the values of the cell which contain only formula using CopyTo method by specifying the ExcelCopyRangeOptions as None. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Assigning formula to a cell

worksheet.Range["A3"].Formula="SUM(1+1)";

IRange sourceRange = worksheet.Range["A3"];

IRange destinationRange = worksheet.Range["B1"];

//Copy and paste the values using ExcelCopyRangeOption

sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None);

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose(); 



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Assigning formula to a cell

worksheet.Range("A3").Formula = "SUM(1+1)"

Dim sourceRange As IRange = worksheet.Range("A3")

Dim destinationRange As IRange = worksheet.Range("B1")

'Copy and paste the values using ExcelCopyRangeOption

sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None)

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to copy a range from one workbook to another?

You can copy the range from source workbook to the destination workbook through CopyTo method. 

The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook sourceWorkbook = application.Workbooks.Open("SourceWorkbook.xlsx", ExcelOpenType.Automatic);

IWorkbook destinationWorkbook = application.Workbooks.Open("DestinationWorkbook.xlsx", ExcelOpenType.Automatic);

IWorksheet SourceWorksheet = SourceWorkbook.Worksheets[0];

//The first worksheet object in the worksheets collection in the Destination Workbook is accessed.

IWorksheet DestinationWorksheet = DestinationWorkbook.Worksheets[0];

//Assigning an object to the range of cells (90 rows) both for source and destination.

IRange sourceRange = SourceWorksheet.Range[1, 1, 90, 100];

IRange destinationRange = DestinationWorksheet.Range[1, 1, 90, 100];

//Copying (90 rows) from Source to Destination worksheet.

sourceRange.CopyTo(destinationRange);

destinationWorkbook.SaveAs("CopyingRange.xlsx");

destinationWorkbook.Close();

excelEngine.Dispose();         



{% endhighlight %}



{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013Dim sourceWorkbook As IWorkbook = application.Workbooks.Open("SourceWorkbook.xlsx", ExcelOpenType.Automatic)

Dim destinationWorkbook As IWorkbook = application.Workbooks.Open("DestinationWorkbook.xlsx", ExcelOpenType.Automatic)

'The first worksheet object in the worksheets collection in the Source Workbook is accessed.

Dim SourceWorksheet As Syncfusion.XlsIO.IWorksheet = SourceWorkbook.Worksheets(0)

'The first worksheet object in the worksheets collection in the Destination Workbook is accessed.

Dim DestinationWorksheet As Syncfusion.XlsIO.IWorksheet = DestinationWorkbook.Worksheets(0)

'Assigning an object to the range of cells (90 rows) both for source and destination.

Dim sourceRange As Syncfusion.XlsIO.IRange = SourceWorksheet.Range(1, 1, 90, 100)

Dim destinationRange As Syncfusion.XlsIO.IRange = DestinationWorksheet.Range(1, 1, 90, 100)

'Copying (90 rows) from Source to Destination worksheet.

sourceRange.CopyTo(destinationRange)

destinationWorkbook.SaveAs("CopyingRange.xlsx")

destinationWorkbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to merge several excel files from more than one workbook to a single file?

You can merge several excel files from more than one work book to a single file. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
//Loads the all template document from Data folder. 

string[] files = Directory.GetFiles(@"../../Data/");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

//Create empty Excel workbook instance with one empty worksheet 

IWorkbook workbook = application.Workbooks.Create(1);

//Enumerates all the workbook files from the data folder and clone and merge it into new workbook.

foreach (string file in files)

{

//Loads the all template document from data folder. 

FileStream inputStream = new FileStream(file, FileMode.Open, FileAccess.Read);



//Opens the template workbook from stream

IWorkbook tempWorkbook = application.Workbooks.Open(inputStream);

//Disposes the stream

inputStream.Dispose();

//Cloning all workbook's worksheets

workbook.Worksheets.AddCopy(tempWorkbook.Worksheets);

}

//removing the first empty worksheet

workbook.Worksheets.Remove(0);

workbook.SaveAs("MergingFiles.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}



{% highlight vb %}
'Loads the all template document from data folder. 

Dim files As String() = Directory.GetFiles("../../Data/")

Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

'Create empty Excel workbook instance with one empty worksheet 

Dim workbook As IWorkbook = application.Workbooks.Create(1)

'Enumerates all the workbook files from the data folder and clone and merge it into new workbook.

For Each file As String In files

'Loads the all template document from data folder. 

Dim inputStream As New FileStream(file, FileMode.Open, FileAccess.Read)

'Opens the template workbook from stream

Dim tempWorkbook As IWorkbook = application.Workbooks.Open(inputStream)

'Disposes the stream

inputStream.Dispose()

'Cloning all workbook's worksheets

workbook.Worksheets.AddCopy(tempWorkbook.Worksheets)

Next

'removing the first empty worksheet

workbook.Worksheets.Remove(0)

workbook.SaveAs("MergingFiles.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to ignore the green error marker in worksheets?

When there exists data that are of different formats, the error marker appears in cells. In XlsIO You can ignore this by using **IgnoreErrorOptions** property. The following code snippet illustrate this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Ignore Error Options.

worksheet.Range["B3"].IgnoreErrorOptions = ExcelIgnoreError.All;

workbook.SaveAs("IgnoreGreenError.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Ignore Error Options.

worksheet.Range("B3").IgnoreErrorOptions = ExcelIgnoreError.All

workbook.SaveAs("IgnoreGreenError.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to protect certain cells in a worksheet?

All the cells in an Excel worksheet have a Locked property, which determines if the cell will be editable. When a worksheet is protected, all the cells in the worksheet get locked, by default.

However, there is often a need to protect only certain cells in a worksheet. In this scenario, you need to protect a worksheet, and set the **IsLocked** property as false for the cells that need to be made editable. 

The following code snippet illustrate this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;            

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Sample data

worksheet.Range["A1:K20"].Text = "Locked";

//A1:A10 will not be protected, hence it is editable.

worksheet.Range["A1:A10"].CellStyle.Locked = false;

worksheet.Range["A1:A10"].Text = "UnLocked";

worksheet.Protect("syncfusion", ExcelSheetProtection.All);

workbook.SaveAs("Protectcells.xlsx");

workbook.Close();

excelEngine.Dispose();   



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Sample data

worksheet.Range("A1:K20").Text = "Locked"

'A1:A10 will not be protected.

worksheet.Range("A1:A10").CellStyle.Locked = False

worksheet.Range("A1:A10").Text = "UnLocked"

worksheet.Protect("syncfusion", ExcelSheetProtection.All)

workbook.SaveAs("Protectcells.xlsx")

workbook.Close()

excelEngine.Dispose()            



{% endhighlight %}

  {% endtabs %}  

N> Locking/Unlocking cells in an unprotected worksheet has no effect.

## How to set a line break inside a cell?

In order to set a line break inside a cell, you have to enable Text Wrapping for the cell, and then break the text. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();       

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Save the line break inside the cell

worksheet.Range["A1"].CellStyle.WrapText = true;

worksheet.Range["A1"].Text = String.Format("Hello\nworld");

workbook.SaveAs("Linebreak.xlsx");

workbook.Close();

excelEngine.Dispose();   



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Save the line break inside the cell

worksheet.Range("A1").CellStyle.WrapText = True

worksheet.Range("A1").Text = String.Format("Hello" & vbLf & "world")

workbook.SaveAs("Linebreak.xlsx")

workbook.Close()

excelEngine.Dispose()     



{% endhighlight %}

  {% endtabs %}  

## How to set or format a Header/Footer?

Script commands are used to set header/ footer formatting. The following code snippet illustrate this. For more information on formatting the string, see [Inserting and Formatting Text in Headers and Footers](http://support.microsoft.com/?kbid=213618)

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Format the header

worksheet.PageSetup.CenterHeader = @"&""Gothic,bold""Center Header Text";

workbook.SaveAs("Headerformat.xlsx");

workbook.Close();

excelEngine.Dispose();     



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Format the header

worksheet.PageSetup.CenterHeader = "&""Gothic,bold""Center Header Text"

workbook.SaveAs("Headerformat.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

N> Go to “ View -> Page Layout” option to view the header and footer in MS Excel. 

## How to set print titles?

**Printing** **Title** **Rows**

XlsIO allows to designate row header to repeat on all pages of a printed workbook using **PrintTitleRows** property. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Print Rows 1 to 3 on every printed page.

worksheet.PageSetup.PrintTitleRows = "$A$1:$IV$3";

workbook.SaveAs("TitleRows.xlsx");

workbook.Close();

excelEngine.Dispose();    



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Print Rows 1 to 3 on every printed page.

worksheet.PageSetup.PrintTitleRows = "$A$1:$IV$3"

workbook.SaveAs("TitleRows.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

**Printing** **Title** **Columns**

XlsIO allows to designate column header to repeat on all pages of a printed workbook using **PrintTitleColumns** property. The following code illustrates printing Title Columns.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Print Columns 1 to 3 on every printed page.

worksheet.PageSetup.PrintTitleColumns = "$A$1:$C$65536";

workbook.SaveAs("TitleColumns.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Print Columns 1 to 3 on every printed page.

worksheet.PageSetup.PrintTitleColumns = "$A$1:$C$65536"

workbook.SaveAs("TitleColumns.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

For information on Print settings, refer to section [Page Setup Settings](/file-formats/xlsio/working-with-excel-worksheet#page-setup-settings).

## How to unfreeze the rows and columns in XlsIO?

You can unfreeze rows and columns in XlsIO by using the RemovePanes method. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Freeze the panes.

worksheet.Range[8, 1].FreezePanes();

//Unfreeze the panes

worksheet.RemovePanes();

workbook.SaveAs("Unfreeze.xlsx");

workbook.Close();

excelEngine.Dispose();      



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Freeze the panes.

worksheet.Range(8, 1).FreezePanes()

'Unfreeze the panes

worksheet.RemovePanes()

workbook.SaveAs("Unfreeze.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## What is the maximum range of Rows and Columns?

XlsIO has support below worksheet size for Excel 97 to 2003, Excel 2007 and later versions.

* **Excel** **97** **to** **2003****(.****xls** **format****)** – 65,536 by 256 rows and columns.
* **Excel** **2007** **and** **Later** **versions****(.****xlsx** **format****)**  – 1,048,576 by 16,384 rows and columns

The above specification is the worksheet size of Excel. For more information, see [Excel specifications and limits](https://support.office.com/en-nz/article/Excel-specifications-and-limits-1672b34d-7043-467e-8e27-269d656771c3)

## How to use Named Ranges with XlsIO?

A named range can be added to worksheet or workbook based on the required scope, the following code snippet illustrate this. For more information, see [Named Range](https://support.office.com/en-us/article/Define-and-use-names-in-formulas-4d0f13ac-53b7-422e-afd2-abd7ff379c64)

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Adding named range to the workbook            

IName workBookName = workbook.Names.Add("WorkBookName");

workBookName.RefersToRange = worksheet.Range["I8"];

//Looping through the Named Ranges in a workbook.

foreach (IName workbookname in workbook.Names)

{

MessageBox.Show(workbookname.Name.ToString());

}

//Adding named range to the worksheet

IName worksheetName = worksheet.Names.Add("WorkSheetName");

worksheetName.RefersToRange = worksheet.Range["J8"];



//Looping through the Named Ranges in a worksheet.

foreach (IName worksheetname in worksheet.Names)

{

MessageBox.Show(worksheetname.Name.ToString());

}

workbook.SaveAs("NamedRange.Xlsx");

workbook.Close();

excelEngine.Dispose();  



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Adding named range to the workbook

Dim workBookName__1 As IName = workbook.Names.Add("WorkBookName")

workBookName__1.RefersToRange = worksheet.Range("I8")

'Looping through the Named Ranges in a workbook.

For Each workbookname__2 As IName In workbook.Names

MessageBox.Show(workbookname__2.Name.ToString())

Next

'Adding named range to the worksheet

Dim worksheetName__3 As IName = worksheet.Names.Add("WorkSheetName")

worksheetName__3.RefersToRange = worksheet.Range("J8")

'Looping through the Named Ranges in a worksheet.

For Each worksheetname__4 As IName In worksheet.Names

MessageBox.Show(worksheetname__4.Name.ToString())

Next

workbook.SaveAs("NamedRange.Xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to add chart labels to scatter points?

The following code illustrates adding chart labels to the scatter points of the chart.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Get the chart from the charts collection

IChart chart = worksheet.Charts[0];

//Get the first series from the Series collection

IChartSerie serieOne = chart.Series[0];

//Set the Series name to the Data Labels through Data Points

serieOne.DataPoints[0].DataLabels.IsSeriesName = true;

//Set the Value to the Data Labels through Data Points

serieOne.DataPoints[0].DataLabels.IsValue = true;

workbook.SaveAs("Chartlabels.xlsx");

workbook.Close();

excelEngine.Dispose();     



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Get the chart from the charts collection

Dim chart As IChart = worksheet.Charts(0)

'Get the first series from the Series collection

Dim serieOne As IChartSerie = chart.Series(0)

'Set the Series name to the Data Labels through Data Points

serieOne.DataPoints(0).DataLabels.IsSeriesName = True

'Set the Value to the Data Labels through Data Points

serieOne.DataPoints(0).DataLabels.IsValue = True

workbook.SaveAs("Chartlabels.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to create a Chart with a discontinuous range?

The following code example illustrates creating a chart with discontinuous data ranges.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Entering the data for the chart.

worksheet.Range["A1"].Text = "Texas books Unit sales";

worksheet.Range["A1:D1"].Merge();

worksheet.Range["A1"].CellStyle.Font.Bold = true;

worksheet.Range["B2"].Text = "Jan";

worksheet.Range["C2"].Text = "Feb";

worksheet.Range["D2"].Text = "Mar";

worksheet.Range["A3"].Text = "Austin";

worksheet.Range["A4"].Text = "Dallas";

worksheet.Range["A5"].Text = "Houston";

worksheet.Range["A6"].Text = "San Antonio";

worksheet.Range["B3"].Number = 53.75;

worksheet.Range["B4"].Number = 52.85;

worksheet.Range["B5"].Number = 59.77;

worksheet.Range["B6"].Number = 96.15;

worksheet.Range["C3"].Number = 79.79;

worksheet.Range["C4"].Number = 59.22;

worksheet.Range["C5"].Number = 10.09;

worksheet.Range["C6"].Number = 73.02;

worksheet.Range["D3"].Number = 26.72;

worksheet.Range["D4"].Number = 33.71;

worksheet.Range["D5"].Number = 45.81;

worksheet.Range["D6"].Number = 12.17;

worksheet.Range["F1"].Number = 26.72;

worksheet.Range["F2"].Number = 33.71;

worksheet.Range["F3"].Number = 45.81;

worksheet.Range["F4"].Number = 12.17;

//Discontiguous range.

IRanges rangesOne = worksheet.CreateRangesCollection();

rangesOne.Add(worksheet.Range["B3:B6"]);

rangesOne.Add(worksheet.Range["F1:F2"]);

IRanges rangesTwo = worksheet.CreateRangesCollection();

rangesTwo.Add(worksheet.Range["D3:D6"]);

rangesTwo.Add(worksheet.Range["F3:F4"]);

//Adding a New (Embedded chart) to the Worksheet.

IChartShape shape = worksheet.Charts.Add();

shape.PrimaryCategoryAxis.Title = "City";

shape.PrimaryValueAxis.Title = "Sales (in Dollars)";

shape.ChartTitle = "Texas Books Unit Sales";

//Setting the Series Names in a Legend.

IChartSerie serieOne = shape.Series.Add();

serieOne.Name = "Jan";

serieOne.Values = rangesOne;

IChartSerie serietwo = shape.Series.Add();

serietwo.Name = "March";

serietwo.Values = rangesTwo;

//Setting the (Rows & Columns) Property for the Embedded chart.

shape.BottomRow = 40;

shape.TopRow = 10;

shape.LeftColumn = 3;

shape.RightColumn = 15;

workbook.SaveAs("DiscontinuousRange.xlsx");

workbook.Close();

excelEngine.Dispose();    





{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Entering the data for the chart.

worksheet.Range("A1").Text = "Texas books Unit sales"

worksheet.Range("A1:D1").Merge()

worksheet.Range("A1").CellStyle.Font.Bold = True

worksheet.Range("B2").Text = "Jan"

worksheet.Range("C2").Text = "Feb"

worksheet.Range("D2").Text = "Mar"

worksheet.Range("A3").Text = "Austin"

worksheet.Range("A4").Text = "Dallas"

worksheet.Range("A5").Text = "Houston"

worksheet.Range("A6").Text = "San Antonio"

worksheet.Range("B3").Number = 53.75

worksheet.Range("B4").Number = 52.85

worksheet.Range("B5").Number = 59.77

worksheet.Range("B6").Number = 96.15

worksheet.Range("C3").Number = 79.79

worksheet.Range("C4").Number = 59.22

worksheet.Range("C5").Number = 10.09

worksheet.Range("C6").Number = 73.02

worksheet.Range("D3").Number = 26.72

worksheet.Range("D4").Number = 33.71

worksheet.Range("D5").Number = 45.81

worksheet.Range("D6").Number = 12.17

worksheet.Range("F1").Number = 26.72

worksheet.Range("F2").Number = 33.71

worksheet.Range("F3").Number = 45.81

worksheet.Range("F4").Number = 12.17

'Discontiguous range.

Dim rangesOne As IRanges = worksheet.CreateRangesCollection()

rangesOne.Add(worksheet.Range("B3:B6"))

rangesOne.Add(worksheet.Range("F1:F2"))

Dim rangesTwo As IRanges = worksheet.CreateRangesCollection()

rangesTwo.Add(worksheet.Range("D3:D6"))

rangesTwo.Add(worksheet.Range("F3:F4"))

'Adding a New (Embedded chart) to the Worksheet.

Dim shape As IChartShape = worksheet.Charts.Add()

shape.PrimaryCategoryAxis.Title = "City"

shape.PrimaryValueAxis.Title = "Sales (in Dollars)"

shape.ChartTitle = "Texas Books Unit Sales"

'Setting the Series Names in a Legend.

Dim serieOne As IChartSerie = shape.Series.Add()

serieOne.Name = "Jan"

serieOne.Values = rangesOne

Dim serietwo As IChartSerie = shape.Series.Add()

serietwo.Name = "March"

serietwo.Values = rangesTwo

'Setting the (Rows & Columns)Property for the Embedded chart.

shape.BottomRow = 40

shape.TopRow = 10

shape.LeftColumn = 3

shape.RightColumn = 15

workbook.SaveAs("DiscontinuousRange.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to define discontinuous ranges?

You can define a discontinuous range by adding different ranges to the Range collection. The following code example illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Create Range collection.

IRanges rangeCollection = worksheet.CreateRangesCollection();

//Add different ranges to the Range collection.

rangeCollection.Add(worksheet.Range["D2:D3"]);

rangeCollection.Add(worksheet.Range["D10:D11"]);

rangeCollection.Text = "Welcome";

workbook.SaveAs("DiscontinuousRange.xlsx");

workbook.Close();

excelEngine.Dispose();   



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Create Range collection.

Dim range As IRanges = worksheet.CreateRangesCollection()

'Add different ranges to the Range collection.

range.Add(worksheet.Range("D2:D3"))

range.Add(worksheet.Range("D10:D11"))

range.Text = "Welcome"

workbook.SaveAs("DiscontinuousRange.xlsx")

workbook.Close()

excelEngine.Dispose()        



{% endhighlight %}

  {% endtabs %}  

## How to format text within a cell?

In Essential XlsIO, You can use the rich text formatting option to format the text within a cell. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Insert Rich Text.

IRange range = worksheet.Range["A1"];

range.Text = "RichText";

IRichTextString rtf = range.RichText;

//Formatting first 4 characters.

IFont redFont = workbook.CreateFont();

redFont.Bold = true;

redFont.Italic = true;

redFont.RGBColor = Color.Red;

rtf.SetFont(0, 3, redFont);

//Formatting last 4 characters.

IFont blueFont = workbook.CreateFont();

blueFont.Bold = true;

blueFont.Italic = true;

blueFont.RGBColor = Color.Blue;

rtf.SetFont(4, 7, blueFont);

workbook.SaveAs("FormattingText.xlsx");

workbook.Close();

excelEngine.Dispose();      



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Insert Rich Text.

Dim range As IRange = worksheet.Range("A1")

range.Text = "RichText"

Dim rtf As IRichTextString = range.RichText

'Formatting first 4 characters.

Dim redFont As IFont = workbook.CreateFont()

redFont.Bold = True

redFont.Italic = True

redFont.RGBColor = Color.Red

rtf.SetFont(0, 3, redFont)

'Formatting last 4 characters.

Dim blueFont As IFont = workbook.CreateFont()

blueFont.Bold = True

blueFont.Italic = True

blueFont.RGBColor = Color.Blue

rtf.SetFont(4, 7, blueFont)

workbook.SaveAs("FormattingText.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to hide the summary rows and columns using XlsIO?

You can hide the summary rows and columns by using the **IsSummaryRowBelow** and **IsSummaryColumnRight** properties. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Hide the summary rows at the bottom.

worksheet.PageSetup.IsSummaryRowBelow = false;

//Hide the summary columns to the right.

worksheet.PageSetup.IsSummaryColumnRight = false;

workbook.SaveAs("Suppressrowscolumns.xlsx");

workbook.Close();

excelEngine.Dispose();   



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Hide the summary rows at the bottom.

worksheet.PageSetup.IsSummaryRowBelow = False

'Suppress the summary columns to the right.

worksheet.PageSetup.IsSummaryColumnRight = False

workbook.SaveAs("Suppressrowscolumns.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## How to zip files using the Syncfusion.Compression.Zip namespace?

You can compress the file using Syncfusion.Compression.Zip namespace. The following code illustrate this.

{% tabs %}  

{% highlight c# %}
using Syncfusion.Compression.Zip;

ZipArchive zipArchive = new Syncfusion.Compression.Zip.ZipArchive();

zipArchive.DefaultCompressionLevel = Syncfusion.Compression.CompressionLevel.Best;

//Add the file you want to zip.

zipArchive.AddFile("SampleFile.cs");

//Zip file name and location.

zipArchive.Save("SyncfusionCompressFileSample.zip");

zipArchive.Close();



{% endhighlight %}

{% highlight vb %}
Imports Syncfusion.Compression.Zip

Dim zipArchive As ZipArchive = New Syncfusion.Compression.Zip.ZipArchive()

zipArchive.DefaultCompressionLevel = Syncfusion.Compression.CompressionLevel.Best

'Add the file you want to zip.

zipArchive.AddFile("SampleFile.cs")

'Zip file name and location.

zipArchive.Save("SyncfusionCompressFileSample.zip")

zipArchive.Close()



{% endhighlight %}

  {% endtabs %}  

T>You can use CompressionLevel to reduce the size of the file.  

For compressing directories, you can make use of the **AddDirectory** method which adds an empty directory file to a ZipArchive. If you want to add all the files inside the directory, then you should manually add these files by using the **AddItem** method.

The following code snippet illustrate how to add the file from the local drive.

{% tabs %}  

{% highlight c# %}
string fileName = @"SampleFile.cs";

ZipArchive zipArchive = new Syncfusion.Compression.Zip.ZipArchive();

zipArchive.DefaultCompressionLevel =CompressionLevel.Best;

Stream stream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

FileAttributes attributes = File.GetAttributes(fileName);

ZipArchiveItem item = new ZipArchiveItem(zipArchive, "SampleFile.cs", stream, true, attributes);

zipArchive.AddItem(item);

zipArchive.Save(@"SyncfusionCompressFileSample.zip");

zipArchive.Close();



{% endhighlight %}

{% highlight vb %}
Dim fileName As String = "SampleFile.cs"

Dim zipArchive As ZipArchive = New Syncfusion.Compression.Zip.ZipArchive()

zipArchive.DefaultCompressionLevel = CompressionLevel.Best

Dim stream As Stream = New FileStream(fileName, FileMode.Open, FileAccess.Read)

Dim attributes As FileAttributes = File.GetAttributes(fileName)

Dim item As New ZipArchiveItem(zipArchive, "SampleFile.cs", stream, True, attributes)

zipArchive.AddItem(item)

zipArchive.Save("SyncfusionCompressFileSample.zip")

zipArchive.Close()



{% endhighlight %}

  {% endtabs %}  

  
## How to zip all the files in subfolders using the Syncfusion.Compression.Zip namespace?

You can compress and decompress the files with our Compression library. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
private static void SubFoldersFiles(string path)

{

DirectoryInfo dInfo = new DirectoryInfo(path);

foreach (DirectoryInfo d in dInfo.GetDirectories())

{

SubFoldersFiles(d.FullName);

arrOfItems.Add(d);

}

}

// Zip and save the file.

private static void ZipandSave()

{

SubFoldersFiles(folderPath);

if (Directory.Exists(folderPath))

{

AddRootFiles();

AddSubFoldersFiles();



// Saving zipped file.

zipArchive.Save(folderPath);

zipArchive.Close();

Console.WriteLine("Files Zipped successfully!");

}

}

private static void AddRootFiles()

{

string fileName = "";

foreach (string rootfiles in Directory.GetFiles(folderPath))

{

//Creating the stream from file

FileStream stream = new FileStream(rootfiles, FileMode.Open, FileAccess.ReadWrite);

//Getting the File Name alone and ignoring the directoty path

fileName=Path.GetFileName(rootfiles);

FileAttributes attribute = File.GetAttributes(rootfiles);

zipArchive.AddItem(fileName,stream,false,attribute);

}

}

private static void AddSubFoldersFiles()

{

foreach (DirectoryInfo dInfo in arrOfItems)

{

FileInfo[] fInfo = dInfo.GetFiles();

string mainDirectoryPath = Path.GetFullPath(folderPath);

foreach (FileInfo file in fInfo)

{

//Get the File name with its current folder and ignoring the Main Directory

string fileName = file.FullName.Replace(mainDirectoryPath, "");

//Read the file stream by its Full name

FileStream stream = new FileStream(file.FullName, FileMode.Open, FileAccess.ReadWrite);

FileAttributes attributes = File.GetAttributes(file.FullName);

//Add the item to the zip Archive

zipArchive.AddItem(fileName, stream, true, attributes);

}

}

}

//Unzipping the Folder

private static void UnZipFiles()

{

ZipArchive zip = new ZipArchive();

string path = @"..\..\UnzippedFile\";

if (!Directory.Exists(path))

Directory.CreateDirectory(path);

//Saving the contents of zip file to disk.

for (int i = 0; i < zip.Count; i++)

{

ZipArchiveItem item = zip[i];

string itemName = path + item.ItemName;

//checking whether the item is root file

if (itemName.Contains("/"))

{

itemName = itemName.Replace("/", "\\");

}

//Check whether the Directory is present or not

if (!Directory.Exists(itemName) || itemName.Contains("\\"))

{

int index = itemName.LastIndexOf("\\");

string directoryPath = itemName.Remove(index, itemName.Length - index);

Directory.CreateDirectory(directoryPath);

}

FileStream fileStream = new FileStream(itemName, FileMode.OpenOrCreate, FileAccess.ReadWrite);

MemoryStream memoryStream = item.DataStream as MemoryStream;

memoryStream.WriteTo(fileStream);

fileStream.Flush();

fileStream.Close();

}

Console.WriteLine("File has been Unzipped");

}



{% endhighlight %}

{% highlight vb %}
Private Shared Sub SubFoldersFiles(path As String)

Dim dInfo As New DirectoryInfo(path)

For Each d As DirectoryInfo In dInfo.GetDirectories()

SubFoldersFiles(d.FullName)

arrOfItems.Add(d)

Next

End Sub

' Zip and save the file.

Private Shared Sub ZipandSave()

SubFoldersFiles(folderPath)

If Directory.Exists(folderPath) Then

AddRootFiles()

AddSubFoldersFiles()

' Saving zipped file.

zipArchive.Save(folderPath)

zipArchive.Close()

Console.WriteLine("Files Zipped successfully!")

End If

End Sub

Private Shared Sub AddRootFiles()

Dim fileName As String = ""

For Each rootfiles As String In Directory.GetFiles(folderPath)

'Creating the stream from file

Dim stream As New FileStream(rootfiles, FileMode.Open, FileAccess.ReadWrite)

'Getting the File Name alone and ignoring the directoty path

fileName = Path.GetFileName(rootfiles)

Dim attribute As FileAttributes = File.GetAttributes(rootfiles)

zipArchive.AddItem(fileName, stream, False, attribute)

Next

End Sub

Private Shared Sub AddSubFoldersFiles()

For Each dInfo As DirectoryInfo In arrOfItems

Dim fInfo As FileInfo() = dInfo.GetFiles()

Dim mainDirectoryPath As String = Path.GetFullPath(folderPath)

For Each file__1 As FileInfo In fInfo

'Get the File name with its current folder and ignoring the Main Directory

Dim fileName As String = file__1.FullName.Replace(mainDirectoryPath, "")

'Read the file stream by its Full name

Dim stream As New FileStream(file__1.FullName, FileMode.Open, FileAccess.ReadWrite)

Dim attributes As FileAttributes = File.GetAttributes(file__1.FullName)

'Add the item to the zip Archive

zipArchive.AddItem(fileName, stream, True, attributes)

Next

Next

End Sub

'Unzipping the Folder

Private Shared Sub UnZipFiles()

Dim zip As New ZipArchive()

Dim path As String = "..\..\UnzippedFile\"

If Not Directory.Exists(path) Then

Directory.CreateDirectory(path)

End If

'Saving the contents of zip file to disk.

For i As Integer = 0 To zip.Count - 1

Dim item As ZipArchiveItem = zip(i)

Dim itemName As String = path + item.ItemName

'checking whether the item is root file

If itemName.Contains("/") Then

itemName = itemName.Replace("/", "\")

End If

'Check whether the Directory is present or not

If Not Directory.Exists(itemName) OrElse itemName.Contains("\") Then

Dim index As Integer = itemName.LastIndexOf("\")

Dim directoryPath As String = itemName.Remove(index, itemName.Length - index)

Directory.CreateDirectory(directoryPath)

End If

Dim fileStream As New FileStream(itemName, FileMode.OpenOrCreate, FileAccess.ReadWrite)

Dim memoryStream As MemoryStream = TryCast(item.DataStream, MemoryStream)

memoryStream.WriteTo(fileStream)

fileStream.Flush()

fileStream.Close()

Next

Console.WriteLine("File has been Unzipped")

End Sub 



{% endhighlight %}

  {% endtabs %}  

## Does Essential XlsIO provide support for Client profile?

Yes, Essential XlsIO provides support for Client profile. In order to use Essential XlsIO in an application (which targeted to Client profile), the user should include the following assemblies.

* Syncfusion.Core.dll
* Syncfusion.Compresssion.Base.dll
* Syncfusion.XlsIO.ClientProfile.dll

N> Syncfusion.Core is no longer needed from 13.2 version onwards. 

## How to resolve the “File does not contain workbook stream” error in Syncfusion.XlsIO.Base.dll?

XlsIO does not support files generated prior to 97-2003 version. Hence the exception "File does not contain workbook stream" occurs. This can be checked in prior with the below code snippet. 

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//To check whether the file is supported

var isSupported = application.IsSupported("Sample.xls");

excelEngine.Dispose();    



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'To check whether the file is supported

Dim isSupported = application.IsSupported("Sample.xls")

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

N> This method is available from 12.4 version onwards.

## How to resolve "Excel cannot open the file 'filename.xlsx' because the file format for the file extension is not valid. Verify that the file has not been corrupted and that the file extension matches the format of the file" error?

This error occurs when there is a mismatch between the file format and its extension. The default workbook creation version in XlsIO is Excel97-2003 (.xls). The application version set to the required version should match its file format during save, as in the below code. 

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Set application version

application.DefaultVersion = ExcelVersion.Excel2013;

//Do some manipulation

//Do some manipulation

//Workbook is saved in Excel2013 format

workbook.SaveAs("Sample.xlsx");



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'Set application version

application.DefaultVersion = ExcelVersion.Excel2013

'Do some manipulation

'Do some manipulation

'Workbook is saved in Excel2013 format

workbook.SaveAs("Sample.xlsx")



{% endhighlight %}

  {% endtabs %}  

If the application version is ignored, then the workbook version should be set properly during creation and save.

* To save a workbook in Excel2003 format, set the workbook version to Excel97to2003 and save the file with extension ‘.xls’ i.e. binary file format.

* To save a workbook in Excel 2007 and above formats, set the workbook version to Excel2007 and above and save the file with extension __‘.____xlsx’__ i.e. open xml file format.

These are represented in the below code snippet.

{% tabs %}  

{% highlight c# %}
workbook.Version = ExcelVersion.Excel97to2003;

workbook.SaveAs("Sample.xls");

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Sample.xlsx");



{% endhighlight %}

{% highlight vb %}
workbook.Version = ExcelVersion.Excel97to2003

workbook.SaveAs("Sample.xls")

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Sample.xlsx")



{% endhighlight %}

  {% endtabs %}  