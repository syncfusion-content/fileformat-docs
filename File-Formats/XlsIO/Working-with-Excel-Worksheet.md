---
title: Working with Excel Worksheet
description: Briefs about worksheet operations in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Working with Excel Worksheet 

A Workbook contains a collection of worksheets where the actual contents resides and IWorksheet instance represents a worksheet. With XlsIO, You can add and manipulate worksheets.

## Create a Worksheet 

You can add a new worksheet into the Workbook through Create method of IWorkbook interface. You can also specify the required number of worksheets, if not specified, XlsIO will create three worksheets by default.

The following code snippet shows how to create worksheets within a workbook.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

//The new workbook will have 5 worksheets.

IWorkbook workbook = application.Workbooks.Create(5);

//Creating a Sheet.

IWorksheet sheet = workbook.Worksheets.Create();

//Creating a Sheet with name “Sample”

IWorksheet namedSheet = workbook.Worksheets.Create("Sample");

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

' The new workbook will have 5 worksheets.

Dim workbook As IWorkbook = application.Workbooks.Create(5)

' Creating a sheet.

Dim sheet As IWorksheet = workbook.Worksheets.Create()

' Creating a Sheet with name “Sample”.

Dim namedSheet As IWorksheet = workbook.Worksheets.Create("Sample")

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Access a Worksheet 

Worksheets collection holds one or more worksheets present in a workbook. Accessing a particular worksheet can be done by the following ways. 

1. Specifying the index 
2. Specifying the sheet name. 

The below codes illustrate how to access a worksheet from its worksheets collection.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(2);

//Accesing via index

IWorksheet sheet = workbook.Worksheets[0];

//Accesing via sheet Name

IWorksheet NamedSheet = workbook.Worksheets["Sample"];

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(2)

' Accesing via index.

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Accesing via Sheet Name.

Dim NamedSheet As IWorksheet = workbook.Worksheets("Sample")

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

T>If the workbook contains multiple worksheet, then the parsing of the workbook will consume time. You can use **ExcelParseOptions****.****ParseWorksheetsOnDemand** in IWorkbooks.Open method which parses the worksheet only when their accessed. This option can be used in a scenario where workbook contains multiple worksheets but you are going to use few worksheets among them.

{% tabs %}  

{% highlight c# %}
IWorkbook workbook = application.Workbooks.Open(fileName,ExcelParseOptions.ParseWorksheetsOnDemand);



{% endhighlight %}

{% highlight vb %}
Dim workbook As IWorkbook = application.Workbooks.Open(fileName, ExcelParseOptions.ParseWorksheetsOnDemand)



{% endhighlight %}

  {% endtabs %}  
  
## Remove a Worksheet

Deletes the worksheets from the workbook collection by accessing the worksheet.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(2);

//Removing the sheet

workbook.Worksheets[0].Remove();

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(2)

'Removing the sheet.

workbook.Worksheets(0).Remove()

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Move or Copy a Worksheet

Essential XlsIO allows to move or create a copy of a worksheet, and insert that worksheet before or after an existing worksheet in the workbook.

### Copying Worksheets

You can copy a worksheet to one another workbook or within the same workbook.

The following code example illustrates how to copy a sheet with its entire contents to another workbook.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook sourceWorkbook = application.Workbooks.Open("SourceWorkbookTemplate.xlsx");

IWorkbook destinationWorkbook = application.Workbooks.Open("DestinationWorkbookTemplate.xlsx");

//Copy first worksheet from the Source workbook to the destination workbook.

destinationWorkbook.Worksheets.AddCopy(sourceWorkbook.Worksheets[0]);

destinationWorkbook.ActiveSheetIndex = 1;

destinationWorkbook.SaveAs("CopiedWorkbook.xlsx");

sourceWorkbook.Close();

destinationWorkbook.Close();

excelEngine.Dispose();   



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim sourceWorkbook As IWorkbook = application.Workbooks.Open("SourceWorkbookTemplate.xlsx")

Dim destinationWorkbook As IWorkbook = application.Workbooks.Open("DestinationWorkbookTemplate.xlsx")

' Copy first worksheet from the Source workbook to the destination workbook.

destinationWorkbook.Worksheets.AddCopy(sourceWorkbook.Worksheets(0))

destinationWorkbook.ActiveSheetIndex = 1

destinationWorkbook.SaveAs("CopiedWorkbook.xlsx")

sourceWorkbook.Close()

destinationWorkbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

You can specify copy options while copying a worksheet, which helps to achieve customized copying by ignore the certain formatting. For more information about copy options, please refer **ExcelWorksheetCopyFlags** .


### Moving a Worksheet

XlsIO allows moving worksheets from one position to another by using the **Move** method. The following code example illustrates how a worksheet is moved.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(3);

IWorksheet sheet = workbook.Worksheets[0];

//Move the Sheet

sheet.Move(1);

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(3)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Move the sheet.

sheet.Move(1)

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Highlight Worksheet Tabs 

You can highlight the worksheet tab of a particular sheet to denote its importance. You can set the tab color through the **TabColor** property, as given below.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Highlighting sheet tab.

sheet.TabColor = ExcelKnownColors.Red;

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Highlighting sheet tab.

sheet.TabColor = ExcelKnownColors.Red

Dim fileName As String = "Output.xlsx"

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Freeze Panes 	

You can [freeze](https://support.office.com/en-au/article/Freeze-rows-and-columns-32b23056-d13b-4b2d-aabb-de55a4c2f708) a portion of the sheet to keep it visible while you scroll through the rest of the sheet. The following code snippet shows how to freeze panes through the FreezePanes method of **IRange**. 


{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Applying Freeze Pane to the sheet by specifying a cell.

sheet.Range["B2"].FreezePanes();

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Applying Freeze Pane to the sheet by specifying a cell.

sheet.Range("B2").FreezePanes()

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

You can set first visible row and first visible column in frozen area, by setting the FirstVisibleRow and FirstVisibleColumn as shown below

N> FirstVisibleColumn and FirstVisibleRow indexes are "zero-based".

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Set first visible row in the bottom pane.

sheet.FirstVisibleRow = 2;

//Set first visible column in the right pane.

sheet.FirstVisibleColumn = 2;

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Set first visible row in the bottom pane.

sheet.FirstVisibleRow = 2

' Set first visible column in the right pane.

sheet.FirstVisibleColumn = 2

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Split Panes 

You can divide the window into different [panes](https://support.office.com/en-AU/article/Split-panes-to-lock-rows-or-columns-in-separate-worksheet-areas-516a7001-b3ed-4122-a6bb-fd6d4a9d6434) that each scroll separately. The following code snippets illustrates how to split the window through the **HorizontalSplit** and **VerticalSplit** properties.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//split panes

sheet.FirstVisibleColumn = 5;

sheet.FirstVisibleRow = 11;

sheet.VerticalSplit = 110;

sheet.HorizontalSplit = 100;

sheet.ActivePane = 1;

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Split Panes

sheet.FirstVisibleColumn = 5

sheet.FirstVisibleRow = 11

sheet.VerticalSplit = 110

sheet.HorizontalSplit = 100

sheet.ActivePane = 1

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Page Setup Settings

You can select the size, orientation of the paper, margins, page breaks, scaling, paper size, header/ footer settings and background settings. The following code snippet shows how to set the page setup. To more about, please refer **Page** **setup**.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A1:M20"].Text = "PageBreak";

//Set Horizontal Page Breaks.

sheet.HPageBreaks.Add(sheet.Range["A5"]);

//Set Vertical Page Breaks.

sheet.VPageBreaks.Add(sheet.Range["B5"]);

//Set print title

sheet.PageSetup.PrintTitleColumns = "B1:E1";

sheet.PageSetup.PrintTitleRows = string.Empty;

//Set Page Orientation as Portrait or Landscape        

sheet.PageSetup.Orientation = ExcelPageOrientation.Landscape;

workbook.SaveAs("pageSetup.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A1:M20").Text = "PageBreak"

' Set Horizontal Page Breaks.

sheet.HPageBreaks.Add(sheet.Range("A5"))

' Set Vertical Page Breaks.

sheet.VPageBreaks.Add(sheet.Range("B5"))

' Set print titles

sheet.PageSetup.PrintTitleColumns = "B1:E1"

sheet.PageSetup.PrintTitleRows = string.Empty

'Set Page Orientation as Portrait or Landscape        

sheet.PageSetup.Orientation = ExcelPageOrientation.Landscape

workbook.SaveAs("pageSetup.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Show or Hide Worksheet 

The following code snippet shows how to hide the sheets using **Visibility** property.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(2);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A1:M20"].Text = "visiblity";

//Set visibility.

sheet.Visibility = WorksheetVisibility.Hidden;

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(2)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A1:M20").Text = "Visibility"

' Set visibility.

sheet.Visibility = WorksheetVisibility.Hidden

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Activate a Worksheet

You can set a worksheet as active sheet in the workbook by using the **Activate** method.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(2);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A1:M20"].Text = "Activate";

//Activate the sheet.

sheet.Activate();

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(2)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A1:M20").Text = "Activate"

' Activate the sheet.

sheet.Activate()

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Show or Hide Worksheet Tabs 

The following code snippet shows how to hide the worksheet tab using **DisplayWorkbookTabs** property.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(2);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A1:M20"].Text = "Tabs";

//Hide the tab

workbook.DisplayWorkbookTabs = false;

//set the display tab

workbook.DisplayedTab = 2;

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(2)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A1:M20").Text = "Tabs"

'Hide the tab

workbook.DisplayWorkbookTabs = False

'set the display tab

workbook.DisplayedTab = 2

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  
 
## View Settings

**Show** **or** **Hide** **Row** **and** **Column** **Headers** 

You can show/hide row and column headings by using the **IsRowColumnHeadersVisible** property of IWorksheet.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A1:M20"].Text = "RowColumnHeader";

sheet.IsRowColumnHeadersVisible = false;

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A1:M20").Text = "RowColumnHeader"

sheet.IsRowColumnHeadersVisible = False

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

### Show or Hide Grid Lines 

The following code snippet shows how to hide the grid lines using IsGridLinesVisible property.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A1:M20"].Text = "Gridlines";

//Hide grid line.

sheet.IsGridLinesVisible = false;

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A1:M20").Text = "GridLines"

' Hide grid line.

sheet.IsGridLinesVisible = False

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

### Set Zoom Level

The following code snippet shows how to set the zoom level by using **Zoom** property.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A1:M20"].Text = "Zoom level";

//set zoom percentage

sheet.Zoom = 70

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
[VB.NET]

Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A1:M20").Text = "Zoom level"

' set Zoom percentage

sheet.Zoom = 70

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Save Worksheet as CSV

The following code example illustrates how to save a worksheet as CSV file.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Save the sheet as CSV

sheet.SaveAs("Sample.csv", ",");

workbook.SaveAs(Output.xlsx);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

'Save the sheet as CSV 
sheet.SaveAs("Sample.csv", ",")

workbook.SaveAs(Output.xlsx)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  
 
### Save worksheet as text (*.txt)

Essential XlsIO allows to save worksheet as a text file. This can be done by leaving the delimiter with a space as shown in the below codes.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A1:M20"].Text = "Text document";

//Save the sheet as text

sheet.SaveAs("Sample.txt", " ");

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A1:M20").Text = "Text document"

'Save the sheet as text
sheet.SaveAs("Sample.txt", " ")

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

## Save Worksheet as HTML

XlsIO provides support to convert a worksheet or workbook to HTML with basic formatting preserved. The supporting formats in this conversion are:

1. Styles.
2. Hyperlinks.
3. Images.
4. 2D Charts.

The following code example illustrates on how to do this.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A1:M20"].Text = "Html Document";

//Save an Excel sheet as HTML file.

sheet.SaveAsHtml("Sample.html");

//Save the workbook as HTML file.

workbook.SaveAsHtml("Sample.html",Implementation.HtmlSaveOptions.Default);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A1:M20").Text = "Html Document"

' Save an Excel sheet as HTML file.

sheet.SaveAsHtml("Sample.html")

' Save a workbook as HTML file.

workbook.SaveAsHtml("Sample.html", Implementation.HtmlSaveOptions.Default)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}   

### Save Options

XlsIO also provides options to save a worksheet with the displayed text or value in the cell to HTML file. The following code example illustrates this.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Create the instant for SaveOptions.

HtmlSaveOptions options = new HtmlSaveOptions();

options.TextMode = HtmlSaveOptions.GetText.DisplayText;

options.ImagePath = @"..\..\Images\";

//Save the sheet as HTML
sheet.SaveAsHtml("Sample.html", options);

workbook.SaveAs(Output.xlsx);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Create the instant for SaveOptions.

Dim options As New HtmlSaveOptions()

options.TextMode = HtmlSaveOptions.GetText.DisplayText

options.ImagePath = "..\..\Images\"

' Save the sheet as HTML

sheet.SaveAsHtml("Sample.html", options)

workbook.SaveAs(Output.xlsx)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  



