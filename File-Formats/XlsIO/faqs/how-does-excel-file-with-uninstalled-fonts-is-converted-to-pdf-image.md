---
title: FAQ Section| XlsIO | Syncfusion
description: This page tells what happens when an Excel file containing uninstalled fonts is converted to PDF/Image using XlsIO.
platform: File-formats
control: XlsIO
documentation: UG
---

# How does Excel file with uninstalled fonts is converted to PDF/Image?

When the fonts used in particular Excel document are not installed in the machine, the desired characters will be missing in the PDF/Image conversion. However, XlsIO comes up with a font substitution method through **SubstituteFontEventHandler** event. This will enable user to specify alternate font name to render the characters in the specified alternate font. Otherwise, Microsoft Sans Serif is used as the default one.

N> Due to this font substitution, there might be a slight difference with the rendered text in the generated PDF/Image files during Excel to PDF/Image conversion.

The following code snippet shows how to use font substitution in Excel to PDF conversion using XlsIO.

{% tabs %}
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initializes the SubstituteFont event to perform font substitution during Excel to PDF conversion
  application.SubstituteFont += new SubstituteFontEventHandler(SubstituteFont);

  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);
  PdfDocument pdf = converter.Convert();

  Stream stream = File.Create("Output.pdf");
  pdf.Save(stream);
}

private static void SubstituteFont(object sender, SubstituteFontEventArgs args)
{
  //Sets the alternate font when a specified font is not installed in the production environment
  if (args.OriginalFontName == "Wingdings Regular")
	args.AlternateFontName = "Bauhaus 93";
  else
	args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initializes the SubstituteFont event to perform font substitution during Excel to PDF conversion
  AddHandler application.SubstituteFont, AddressOf SubstituteFont

  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)
  Dim pdf As PdfDocument = converter.Convert()

  Dim stream As Stream = File.Create("Output.pdf")
  pdf.Save(stream)
End Using

Private Shared Sub SubstituteFont(ByVal sender As Object, ByVal args As SubstituteFontEventArgs)
  'Sets the alternate font when a specified font is not installed in the production environment.
  If args.OriginalFontName = "Wingdings Regular" Then
	args.AlternateFontName = "Bauhaus 93"
  Else
	args.AlternateFontName = "Times New Roman"
  End If
End Sub
{% endhighlight %}
{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    //Initializes the SubstituteFont event to perform font substitution during Excel to PDF conversion
    application.SubstituteFont += new SubstituteFontEventHandler(SubstituteFont);

    XlsIORenderer renderer = new XlsIORenderer();
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

    FileStream stream = new FileStream("Output.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    pdfDocument.Save(stream);
}

private static void SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    if (args.OriginalFontName == "Wingdings Regular")
        args.AlternateFontName = "Bauhaus 93";
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    //Initializes the SubstituteFont event to perform font substitution during Excel to PDF conversion
    application.SubstituteFont += new SubstituteFontEventHandler(SubstituteFont);

    XlsIORenderer renderer = new XlsIORenderer();
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

    FileStream stream = new FileStream("Output.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    pdfDocument.Save(stream);
}

private static void SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    if (args.OriginalFontName == "Wingdings Regular")
        args.AlternateFontName = "Bauhaus 93";
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream fileStream = assembly.GetManifestResourceStream("App.Sample.xlsx");
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    //Initializes the SubstituteFont event to perform font substitution during Excel to PDF conversion
    application.SubstituteFont += new SubstituteFontEventHandler(SubstituteFont);

    XlsIORenderer renderer = new XlsIORenderer();
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}

private static void SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    if (args.OriginalFontName == "Wingdings Regular")
        args.AlternateFontName = "Bauhaus 93";
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}
{% endtabs %}

## See Also

* [How to use Substitute Font in Excel-to-PDF Conversion?](https://help.syncfusion.com/file-formats/xlsio/excel-to-pdf-conversion#substitute-font-in-excel-to-pdf-conversion)
* [How to Embed Fonts?](https://help.syncfusion.com/file-formats/xlsio/excel-to-pdf-converter-settings#embed-fonts)
* [How to Capture Warnings in Excel-to-PDF Conversion?](https://help.syncfusion.com/file-formats/xlsio/excel-to-pdf-converter-settings#capture-warnings-in-excel-to-pdf-conversion)
* [What is the image quality when using the ExportQualityImage property?](faqs/what-is-the-image-quality-when-using-the-exportqualityimage-property)
* [How to convert a Worksheet to Image?](https://help.syncfusion.com/file-formats/xlsio/worksheet-to-image-conversion)
* [How to convert a Chart to Image?](https://help.syncfusion.com/file-formats/xlsio/chart-to-image-conversion)

