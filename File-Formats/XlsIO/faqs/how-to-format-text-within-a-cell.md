---
title: FAQ Section| XlsIO | Syncfusion
description: This page demonstrates how to format text within a cell using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to format text within a cell?

In Essential XlsIO, You can use the rich text formatting option to format the text within a cell. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Insert Rich Text.

    IRange range = worksheet.Range["A1"];

    range.Text = "RichText";

    IRichTextString richText = range.RichText;

    //Formatting first 4 characters.

    IFont redFont = workbook.CreateFont();

    redFont.Bold = true;

    redFont.Italic = true;

    redFont.RGBColor = Color.Red;

    richText.SetFont(0, 3, redFont);

    //Formatting last 4 characters.

    IFont blueFont = workbook.CreateFont();

    blueFont.Bold = true;

    blueFont.Italic = true;

    blueFont.RGBColor = Color.Blue;

    richText.SetFont(4, 7, blueFont);

    workbook.SaveAs("FormattingText.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim workbook As IWorkbook = application.Workbooks.Create(1)

    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Insert Rich Text.

    Dim range As IRange = worksheet.Range("A1")

    range.Text = "RichText"

    Dim richText As IRichTextString = range.RichText

    'Formatting first 4 characters.

    Dim redFont As IFont = workbook.CreateFont()

    redFont.Bold = True

    redFont.Italic = True

    redFont.RGBColor = Color.Red

    richText.SetFont(0, 3, redFont)

    'Formatting last 4 characters.

    Dim blueFont As IFont = workbook.CreateFont()

    blueFont.Bold = True

    blueFont.Italic = True

    blueFont.RGBColor = Color.Blue

    richText.SetFont(4, 7, blueFont)

    workbook.SaveAs("FormattingText.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Insert Rich Text.

    IRange range = worksheet.Range["A1"];

    range.Text = "RichText";

    IRichTextString richText = range.RichText;

    //Formatting first 4 characters.

    IFont redFont = workbook.CreateFont();

    redFont.Bold = true;

    redFont.Italic = true;

    redFont.RGBColor = Color.FromArgb(255, 255, 0, 0);

    richText.SetFont(0, 3, redFont);

    //Formatting last 4 characters.

    IFont blueFont = workbook.CreateFont();

    blueFont.Bold = true;

    blueFont.Italic = true;

    blueFont.RGBColor = Color.FromArgb(255, 0, 0, 255);

    richText.SetFont(4, 7, blueFont);

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "FormattingText";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

    //Creates a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();

    //Saves changes to the specified storage file
    await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Insert Rich Text.

    IRange range = worksheet.Range["A1"];

    range.Text = "RichText";

    IRichTextString richText = range.RichText;

    //Formatting first 4 characters.

    IFont redFont = workbook.CreateFont();

    redFont.Bold = true;

    redFont.Italic = true;

    redFont.RGBColor = Color.Red;

    richText.SetFont(0, 3, redFont);

    //Formatting last 4 characters.

    IFont blueFont = workbook.CreateFont();

    blueFont.Bold = true;

    blueFont.Italic = true;

    blueFont.RGBColor = Color.Blue;

    richText.SetFont(4, 7, blueFont);

    FileStream stream = new FileStream("FormattingText.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(stream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Insert Rich Text.

    IRange range = worksheet.Range["A1"];

    range.Text = "RichText";

    IRichTextString richText = range.RichText;

    //Formatting first 4 characters.

    IFont redFont = workbook.CreateFont();

    redFont.Bold = true;

    redFont.Italic = true;

    redFont.RGBColor = Color.Red;

    richText.SetFont(0, 3, redFont);

    //Formatting last 4 characters.

    IFont blueFont = workbook.CreateFont();

    blueFont.Bold = true;

    blueFont.Italic = true;

    blueFont.RGBColor = Color.Blue;

    richText.SetFont(4, 7, blueFont);

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("FormattingText.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

{% endtabs %}  

## See Also

* [How to set a line break inside a cell?](faqs/how-to-set-a-line-break-inside-a-cell)
* [How to protect certain cells in a worksheet?](faqs/how-to-protect-certain-cells-in-a-worksheet)
* [How to copy/paste the cell values that contain only formula?](faqs/how-to-copy-paste-the-cell-values-that-contain-only-formula)
* [How to rich-text formatting?](https://help.syncfusion.com/file-formats/xlsio/working-with-cell-or-range-formatting#rich-text-formatting)
* [How to apply number formats?](https://help.syncfusion.com/file-formats/xlsio/working-with-cell-or-range-formatting#apply-number-formats)
* [How to apply cell text alignment?](https://help.syncfusion.com/file-formats/xlsio/working-with-cell-or-range-formatting#apply-cell-text-alignment)
