---
title: Silverlight
description: Briefs about loading and saving an Excel document in Silverlight platform.
platform: file-formats
control: XlsIO
documentation: UG
---
# Silverlight 

In order to use XlsIO in your Silverlight application, please add the required assemblies in your Silverlight application. Refer [Assemblies Required](/File-Formats/XlsIO/Assemblies-Required).

## Loading the document

The below code snippet illustrates how to load an Excel file using stream in Silverlight.

{% tabs %}  

{% highlight C# %}
ExcelEngine excelEngine = new ExcelEngine();



//Load the file as stream

SaveFileDialog dialog = new SaveFileDialog();

dialog.Filter = "Excel Files(*.xlsx)|*.xlsx|Excel Files(*.xls)|*.xls";

if (dialog.ShowDialog() == true)

{

Stream fileStream = Assembly.GetExecutingAssembly().GetManifestResourceStream("sample.Resources.Data.sample.xlsx");

IWorkbook book = excelEngine.Excel.Workbooks.Open(fileStream, ExcelOpenType.Automatic);

using (Stream stream = dialog.OpenFile())

{

book.SaveAs(stream);

book.Close();

excelEngine.Dispose();

}

}



{% endhighlight %}

{% highlight VB.NET %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

'Load the file as stream

Dim dialog As SaveFileDialog = New SaveFileDialog()

dialog.Filter = "Excel Files(*.xlsx)|*.xlsx|Excel Files(*.xls)|*.xls"

If dialog.ShowDialog() = True Then

Dim fileStream As Stream = Assembly.GetExecutingAssembly().GetManifestResourceStream("sample.Resources.Data.sample.xlsx")

Dim book As IWorkbook = excelEngine.Excel.Workbooks.Open(fileStream, ExcelOpenType.Automatic)

Dim stream As Stream

Using (stream = dialog.OpenFile())

book.SaveAs(stream)

book.Close()

excelEngine.Dispose()

End Using

End If



{% endhighlight %}

  {% endtabs %}  

## Saving the document

The following code snippet illustrate how to save an Excel document in Silverlight.

{% tabs %}  

{% highlight C# %}
SaveFileDialog dialog = new SaveFileDialog();

dialog.Filter = "Excel Files(*.xlsx)|*.xlsx|Excel Files(*.xls)|*.xls";

if (dialog.ShowDialog() == true)

{

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2010;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Inserting sample text into the first cell of the first worksheet.

sheet.Range["A1:T130000"].Text = "Hello World";

IStyle style = workbook.Styles.Add("Style1");

style.ColorIndex = ExcelKnownColors.Aqua;

style.Font.Color = ExcelKnownColors.Red;

style.Borders.LineStyle = ExcelLineStyle.Thick;

style.Borders.Color = ExcelKnownColors.Violet;

sheet.UsedRange.CellStyle = style;

using (Stream stream = dialog.OpenFile())

{

workbook.SaveAs(stream);

workbook.Close();

excelEngine.Dispose();

}

}



{% endhighlight %}

{% highlight VB.NET %}
Dim dialog As SaveFileDialog = New SaveFileDialog()

dialog.Filter = "Excel Files(*.xlsx)|*.xlsx|Excel Files(*.xls)|*.xls"

If dialog.ShowDialog() = True Then

Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As Application = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2010

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Inserting sample text into the first cell of the first worksheet.

sheet.Range("A1:T130000").Text = "Hello World"

Dim style As IStyle = workbook.Styles.Add("Style1")

style.ColorIndex = ExcelKnownColors.Aqua

style.Font.Color = ExcelKnownColors.Red

style.Borders.LineStyle = ExcelLineStyle.Thick

style.Borders.Color = ExcelKnownColors.Violet

sheet.UsedRange.CellStyle = style

Imports(Stream stream = dialog.OpenFile())

workbook.SaveAs(stream)

workbook.Close()

excelEngine.Dispose()

End If



{% endhighlight %}

  {% endtabs %}  

