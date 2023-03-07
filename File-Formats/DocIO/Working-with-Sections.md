---
title: Working with Sections | Syncfusion
description: This section illustrates how to Work with Sections in the Word document using Syncfusion Word library (Essential DocIO)
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Sections

A section contains the contents present in Headers, Footers and main document through the instances of [WTextBody](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WTextBody.html). A section also has a specific set of properties used to define the page settings, number of columns, headers and footers and so on that decide how the text appears. [WTextBody](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WTextBody.html) represents group of paragraphs and tables etc. 

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to created section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new instance of WordDocument (Empty Word Document)
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new instance of WordDocument (Empty Word Document)
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Add-sections-in-Word-document).

You can add the multiple sections into the document. When you add more than one section into the word document, the section starts from the next page by default.

You can also add a new section that starts on a same page by specifying the [BreakCode](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WSection.html#Syncfusion_DocIO_DLS_WSection_BreakCode) as shown in following code example.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the new section to the document
section = document.AddSection();
//Sets a section break
section.BreakCode = SectionBreakCode.NoBreak;
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText); 
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds the section into Word document
Dim section As IWSection = document.AddSection()
'Adds a paragraph to created section
Dim paragraph As IWParagraph = section.AddParagraph()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Appends the text to the created paragraph
paragraph.AppendText(paraText)
'Adds the new section to the document
section = document.AddSection()
'Sets a section break
section.BreakCode = SectionBreakCode.NoBreak
'Adds a paragraph to created section
paragraph = section.AddParagraph()
'Appends the text to the created paragraph
paragraph.AppendText(paraText)
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the new section to the document
section = document.AddSection();
//Sets a section break
section.BreakCode = SectionBreakCode.NoBreak;
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the new section to the document
section = document.AddSection();
//Sets a section break
section.BreakCode = SectionBreakCode.NoBreak;
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the new section to the document
section = document.AddSection();
//Sets a section break
section.BreakCode = SectionBreakCode.NoBreak;
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Add-continuous-sections-in-Word).

## Specifying Page Properties

Each section has its own page setup properties such as page size, orientation, margins, borders, and more. 

The following code example shows how to set the page setup properties

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
IWSection section = document.AddSection();
//Sets page setup options
section.PageSetup.Orientation = PageOrientation.Landscape;
section.PageSetup.Margins.All = 72;
section.PageSetup.Borders.LineWidth = 2;
//Sets the PrinterPaperTray value for FirstPageTray in page setup options
section.PageSetup.FirstPageTray = PrinterPaperTray.EnvelopeFeed;
//Sets the PrinterPaperTray value for OtherPagesTray in page setup options     
section.PageSetup.OtherPagesTray = PrinterPaperTray.MiddleBin;
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."); 
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
Dim section As IWSection = document.AddSection()
'Sets page setup options
section.PageSetup.Orientation = PageOrientation.Landscape
section.PageSetup.Margins.All = 72
section.PageSetup.Borders.LineWidth = 2
'Sets the PrinterPaperTray value for FirstPageTray  in page setup options
section.PageSetup.FirstPageTray = PrinterPaperTray.EnvelopeFeed
'Sets the PrinterPaperTray value for OtherPagesTray in page setup options
section.PageSetup.OtherPagesTray = PrinterPaperTray.MiddleBin
'Adds a paragraph to created section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends the text to the created paragraph.
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document
WordDocument document = new WordDocument();
IWSection section = document.AddSection();
//Sets page setup options
section.PageSetup.Orientation = PageOrientation.Landscape;
section.PageSetup.Margins.All = 72;
section.PageSetup.Borders.LineWidth = 2;
//Sets the PrinterPaperTray value for FirstPageTray in page setup options
section.PageSetup.FirstPageTray = PrinterPaperTray.EnvelopeFeed;
//Sets the PrinterPaperTray value for OtherPagesTray in page setup options
section.PageSetup.OtherPagesTray = PrinterPaperTray.MiddleBin;
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document
WordDocument document = new WordDocument();
IWSection section = document.AddSection();
//Sets page setup options
section.PageSetup.Orientation = PageOrientation.Landscape;
section.PageSetup.Margins.All = 72;
section.PageSetup.Borders.LineWidth = 2;
//Sets the PrinterPaperTray value for FirstPageTray in page setup options
section.PageSetup.FirstPageTray = PrinterPaperTray.EnvelopeFeed;
//Sets the PrinterPaperTray value for OtherPagesTray in page setup options
section.PageSetup.OtherPagesTray = PrinterPaperTray.MiddleBin;
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document
WordDocument document = new WordDocument();
IWSection section = document.AddSection();
//Sets page setup options
section.PageSetup.Orientation = PageOrientation.Landscape;
section.PageSetup.Margins.All = 72;
section.PageSetup.Borders.LineWidth = 2;
//Sets the PrinterPaperTray value for FirstPageTray in page setup options
section.PageSetup.FirstPageTray = PrinterPaperTray.EnvelopeFeed;
//Sets the PrinterPaperTray value for OtherPagesTray in page setup options
section.PageSetup.OtherPagesTray = PrinterPaperTray.MiddleBin;
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Page-setup-properties).

## Creating Multi-column document

You can split the contents into two or more columns by specifying the column width and spacing between columns.

The following code example shows how to display contents in multiple columns.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
//Adds the column into the section
section.AddColumn(150, 20);
//Adds the column into the section
section.AddColumn(150, 20);
//Adds the column into the section
section.AddColumn(150, 20);
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
//Adds a paragraph to created section
paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak);
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak);
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds the section into Word document
Dim section As IWSection = document.AddSection()
'Adds the column into the section
section.AddColumn(150, 20)
'Adds the column into the section
section.AddColumn(150, 20)
'Adds the column into the section
section.AddColumn(150, 20)
'Adds a paragraph to created section
Dim paragraph As IWParagraph = section.AddParagraph()
'Adds a paragraph to created section
paragraph = section.AddParagraph()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Appends the text to the created paragraph
paragraph.AppendText(paraText)
'Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak)
'Adds a paragraph to created section
paragraph = section.AddParagraph()
'Appends the text to the created paragraph
paragraph.AppendText(paraText)
'Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak)
'Adds a paragraph to created section
paragraph = section.AddParagraph()
'Appends the text to the created paragraph
paragraph.AppendText(paraText)
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
//Adds the column into the section    
section.AddColumn(150, 20);
//Adds the column into the section
section.AddColumn(150, 20);
//Adds the column into the section
section.AddColumn(150, 20);
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
//Adds a paragraph to created section
paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak);
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak);
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
//Adds the column into the section
section.AddColumn(150, 20);
//Adds the column into the section
section.AddColumn(150, 20);
//Adds the column into the section
section.AddColumn(150, 20);
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
//Adds a paragraph to created section
paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak);
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak);
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph         
paragraph.AppendText(paraText);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to MemoryStream        
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
//Adds the column into the section
section.AddColumn(150, 20);
//Adds the column into the section
section.AddColumn(150, 20);
//Adds the column into the section
section.AddColumn(150, 20);
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
//Adds a paragraph to created section
paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak);
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Adds the column break
paragraph.AppendBreak(BreakType.ColumnBreak);
//Adds a paragraph to created section
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Create-multi-column-document).

## Creating document with different page settings

You can prefer to have more sections in a Word document when you need to have different page settings or headers and footers for a specific set of contents. The following code example illustrates how to create a Word document with multiple sections whose page orientation are portrait and landscape respectively.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Sets the page size
section.PageSetup.PageSize = PageSize.A4;
//Sets the page orientation as portrait
section.PageSetup.Orientation = PageOrientation.Portrait;
//Adds the new section to the document
section = document.AddSection();
//Sets the section break
section.BreakCode = SectionBreakCode.NewPage;
paragraph = section.AddParagraph();
//Sets the page size
section.PageSetup.PageSize = PageSize.A4;
//Sets the page orientation as land scape
section.PageSetup.Orientation = PageOrientation.Landscape;
//Appends the text to the paragraph
paragraph.AppendText(paraText);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds the section into Word document
Dim section As IWSection = document.AddSection()
'Adds a paragraph to created section
Dim paragraph As IWParagraph = section.AddParagraph()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Appends the text to the created paragraph
paragraph.AppendText(paraText)
'Sets the page size
section.PageSetup.PageSize = PageSize.A4;
'Sets the page orientation as portrait
section.PageSetup.Orientation = PageOrientation.Portrait
'Adds the new section to the document
section = document.AddSection()
'Sets the section break
section.BreakCode = SectionBreakCode.NewPage
paragraph = section.AddParagraph()
'Sets the page size
section.PageSetup.PageSize = PageSize.A4;
'Sets the page orientation as landscape
section.PageSetup.Orientation = PageOrientation.Landscape
'Appends the text to the paragraph
paragraph.AppendText(paraText)
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Sets the page size
section.PageSetup.PageSize = PageSize.A4;
//Sets the page orientation as portrait
section.PageSetup.Orientation = PageOrientation.Portrait;
//Adds the new section to the document
section = document.AddSection();
//Sets the section break
section.BreakCode = SectionBreakCode.NewPage;
paragraph = section.AddParagraph();
//Sets the page size
section.PageSetup.PageSize = PageSize.A4;
//Sets the page orientation as land scape
section.PageSetup.Orientation = PageOrientation.Landscape;
//Appends the text to the paragraph
paragraph.AppendText(paraText);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();  
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Sets the page size
section.PageSetup.PageSize = PageSize.A4;
//Sets the page orientation as portrait
section.PageSetup.Orientation = PageOrientation.Portrait;
//Adds the new section to the document
section = document.AddSection();
//Sets the section break
section.BreakCode = SectionBreakCode.NewPage;
paragraph = section.AddParagraph();
//Sets the page size
section.PageSetup.PageSize = PageSize.A4;
//Sets the page orientation as land scape
section.PageSetup.Orientation = PageOrientation.Landscape;
//Appends the text to the paragraph
paragraph.AppendText(paraText);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser       
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();        
//Adds a paragraph to created section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends the text to the created paragraph
paragraph.AppendText(paraText);
//Sets the page size
section.PageSetup.PageSize = PageSize.A4;
//Sets the page orientation as portrait
section.PageSetup.Orientation = PageOrientation.Portrait;
//Adds the new section to the document
section = document.AddSection();
//Sets the section break
section.BreakCode = SectionBreakCode.NewPage;
paragraph = section.AddParagraph();
//Sets the page size
section.PageSetup.PageSize = PageSize.A4;
//Sets the page orientation as land scape
section.PageSetup.Orientation = PageOrientation.Landscape;
//Appends the text to the paragraph
paragraph.AppendText(paraText);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Document-with-different-page-settings).
 
## Working with Headers and Footers

Header and footer also represent the group of paragraphs and tables that occur at the top and bottom of the page respectively. Header and footer may vary for each section. The following are the types of Headers/Footers:

  * [FirstPageHeader](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WHeadersFooters.html#Syncfusion_DocIO_DLS_WHeadersFooters_FirstPageHeader) – Represents the first page header of the document.
  * [FirstPageFooter](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WHeadersFooters.html#Syncfusion_DocIO_DLS_WHeadersFooters_FirstPageFooter) – Represents the first page footer of the document. 
  * [OddHeader](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WHeadersFooters.html#Syncfusion_DocIO_DLS_WHeadersFooters_OddHeader) – Represents the odd page header of the document and it is the default header for the section. 
  * [OddFooter](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WHeadersFooters.html#Syncfusion_DocIO_DLS_WHeadersFooters_OddFooter) – Represents the odd page footer of the document and it is the default footer for the section.
  * [EvenHeader](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WHeadersFooters.html#Syncfusion_DocIO_DLS_WHeadersFooters_EvenHeader) – Represents the even page header of the document.
  * [EvenFooter](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WHeadersFooters.html#Syncfusion_DocIO_DLS_WHeadersFooters_EvenFooter) - Represents the even page footer of the document.

The following code example illustrates how to add simple header and footer into a Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default Page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new document
Dim document As New WordDocument()
'Adds the first section to the document
Dim section As IWSection = document.AddSection()
'Adds a paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Appends some text to the first page in document
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)
paragraph.ParagraphFormat.PageBreakAfter = True
'Appends some text to the second page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)
paragraph.ParagraphFormat.PageBreakAfter = True
'Appends some text to the third page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)
'Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph()
paragraph.AppendText("[ Default Page Header ]")
'Inserts the default Page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph()
paragraph.AppendText("[ Default Page Footer ]")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default Page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream        
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default Page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default Page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Simple-headers-and-footers).

You can have a specific header and footer contents for the first page in a Word document. The following code illustrates the same. 

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Sets DifferentFirstPage as true for inserting header and footer text
section.PageSetup.DifferentFirstPage = true;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the first page header
paragraph = section.HeadersFooters.FirstPageHeader.AddParagraph();
paragraph.AppendText("[First Page Header ]");
//Inserts the first page footer
paragraph = section.HeadersFooters.FirstPageFooter.AddParagraph();
paragraph.AppendText("[ First Page Footer ]");
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new document
Dim document As New WordDocument()
'Adds the first section to the document
Dim section As IWSection = document.AddSection()
'Sets DifferentFirstPage as true for inserting header and footer text
section.PageSetup.DifferentFirstPage = True
'Adds a paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Appends some text to the first page in document
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)
paragraph.ParagraphFormat.PageBreakAfter = True
'Appends some text to the second page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)
paragraph.ParagraphFormat.PageBreakAfter = True
'Appends some text to the third page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)
'Inserts the first page header
paragraph = section.HeadersFooters.FirstPageHeader.AddParagraph()
paragraph.AppendText("[First Page Header ]")
'Inserts the first page footer
paragraph = section.HeadersFooters.FirstPageFooter.AddParagraph()
paragraph.AppendText("[ First Page Footer ]")
'Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph()
paragraph.AppendText("[ Default Page Header ]")
'Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph()
paragraph.AppendText("[ Default Page Footer ]")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Sets DifferentFirstPage as true for inserting header and footer text
section.PageSetup.DifferentFirstPage = true;    
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the first page header
paragraph = section.HeadersFooters.FirstPageHeader.AddParagraph();
paragraph.AppendText("[First Page Header ]");
//Inserts the first page footer
paragraph = section.HeadersFooters.FirstPageFooter.AddParagraph();
paragraph.AppendText("[ First Page Footer ]");
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Sets DifferentFirstPage as true for inserting header and footer text
section.PageSetup.DifferentFirstPage = true;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the first page header
paragraph = section.HeadersFooters.FirstPageHeader.AddParagraph();
paragraph.AppendText("[First Page Header ]");
//Inserts the first page footer
paragraph = section.HeadersFooters.FirstPageFooter.AddParagraph();
paragraph.AppendText("[ First Page Footer ]");
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Sets DifferentFirstPage as true for inserting header and footer text
section.PageSetup.DifferentFirstPage = true;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the first page header
paragraph = section.HeadersFooters.FirstPageHeader.AddParagraph();
paragraph.AppendText("[First Page Header ]");
//Inserts the first page footer
paragraph = section.HeadersFooters.FirstPageFooter.AddParagraph();
paragraph.AppendText("[ First Page Footer ]");
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Header-and-footers-for-first-page).

A Word document can have different header and footer for odd and even pages.

The following code example shows how to set different header and footer for the odd and even pages of the document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Sets DifferentOddAndEvenPages as true for inserting header and footer text
section.PageSetup.DifferentOddAndEvenPages = true;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the odd page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Odd Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Odd Page Footer ]");
//Inserts the even page header
paragraph = section.HeadersFooters.EvenHeader.AddParagraph();
paragraph.AppendText("[Even Page Header ]");
//Inserts the even page footer
paragraph = section.HeadersFooters.EvenFooter.AddParagraph();
paragraph.AppendText("[ Even Page Footer ]");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new document
Dim document As New WordDocument()
'Adds the first section to the document
Dim section As IWSection = document.AddSection()
'Sets DifferentOddAndEvenPages as true for inserting header and footer text
section.PageSetup.DifferentOddAndEvenPages = True
'Adds a paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Appends some text to the first page in document
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)
paragraph.ParagraphFormat.PageBreakAfter = True
'Appends some text to the second page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)
paragraph.ParagraphFormat.PageBreakAfter = True
'Appends some text to the third page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)
'Inserts the odd page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph()
paragraph.AppendText("[ Odd Page Header ]")
'Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph()
paragraph.AppendText("[ Odd Page Footer ]")
'Inserts the even page header
paragraph = section.HeadersFooters.EvenHeader.AddParagraph()
paragraph.AppendText("[Even Page Header ]")
'Inserts the even page footer
paragraph = section.HeadersFooters.EvenFooter.AddParagraph()
paragraph.AppendText("[ Even Page Footer ]")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Sets DifferentOddAndEvenPages as true for inserting header and footer text
section.PageSetup.DifferentOddAndEvenPages = true;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the odd page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Odd Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Odd Page Footer ]");
//Inserts the even page header
paragraph = section.HeadersFooters.EvenHeader.AddParagraph();
paragraph.AppendText("[Even Page Header ]");
//Inserts the even page footer
paragraph = section.HeadersFooters.EvenFooter.AddParagraph();
paragraph.AppendText("[ Even Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Sets DifferentOddAndEvenPages as true for inserting header and footer text
section.PageSetup.DifferentOddAndEvenPages = true;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the odd page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Odd Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Odd Page Footer ]");
//Inserts the even page header
paragraph = section.HeadersFooters.EvenHeader.AddParagraph();
paragraph.AppendText("[Even Page Header ]");
//Inserts the even page footer
paragraph = section.HeadersFooters.EvenFooter.AddParagraph();
paragraph.AppendText("[ Even Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Sets DifferentOddAndEvenPages as true for inserting header and footer text
section.PageSetup.DifferentOddAndEvenPages = true;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the odd page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Odd Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Odd Page Footer ]");
//Inserts the even page header
paragraph = section.HeadersFooters.EvenHeader.AddParagraph();
paragraph.AppendText("[Even Page Header ]");
//Inserts the even page footer
paragraph = section.HeadersFooters.EvenFooter.AddParagraph();
paragraph.AppendText("[ Even Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Odd-and-even-page-header-footer).

You can use the previous section header and footer for the current section by using [LinkToPrevious](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WHeadersFooters.html#Syncfusion_DocIO_DLS_WHeadersFooters_LinkToPrevious) property.

The following code example shows how to link the previous section header and footer for the current section.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Inserts the first section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ First Section Header ]");
//Inserts the first section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ First Section Footer ]");
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
//Adds the second section to the document
section = document.AddSection();
//Inserts the second section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Second Section Header ]");
//Inserts the second section footer.
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Second Section Footer ]");
//Sets LinkToPrevious as true for retrieve the header and footer from previous section
section.HeadersFooters.LinkToPrevious = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
//Adds the third section to the document
section = document.AddSection();
//Inserts the third section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Third Section Header ]");
//Inserts the third section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Third Section Footer ]");
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new document
Dim document As New WordDocument()
'Adds the first section to the document
Dim section As IWSection = document.AddSection()
'Inserts the first section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ First Section Header ]")
'Inserts the first section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ First Section Footer ]")
'Adds a paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Appends some text to the first page in document
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)
'Adds the second section to the document
section = document.AddSection()
'Inserts the second section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Second Section Header ]")
'Inserts the second section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Second Section Footer ]")
'Sets LinkToPrevious as true for retrieve the header and footer from previous section
section.HeadersFooters.LinkToPrevious = True
'Appends some text to the second page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)
'Adds the third section to the document
section = document.AddSection()
'Inserts the third section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Third Section Header ]")
'Inserts the third section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Third Section Footer ]")
'Appends some text to the third page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Inserts the first section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ First Section Header ]");
//Inserts the first section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ First Section Footer ]");
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
//Adds the second section to the document
section = document.AddSection();
//Inserts the second section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Second Section Header ]");
//Inserts the second section footer.
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Second Section Footer ]");
//Sets LinkToPrevious as true for retrieve the header and footer from previous section
section.HeadersFooters.LinkToPrevious = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
//Adds the third section to the document
section = document.AddSection();
//Inserts the third section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Third Section Header ]");
//Inserts the third section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Third Section Footer ]");
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Inserts the first section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ First Section Header ]");
//Inserts the first section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ First Section Footer ]");
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
//Adds the second section to the document
section = document.AddSection();
//Inserts the second section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Second Section Header ]");
//Inserts the second section footer.
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Second Section Footer ]");
//Sets LinkToPrevious as true for retrieve the header and footer from previous section
section.HeadersFooters.LinkToPrevious = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
//Adds the third section to the document
section = document.AddSection();
//Inserts the third section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Third Section Header ]");
//Inserts the third section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Third Section Footer ]");
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Inserts the first section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ First Section Header ]");
//Inserts the first section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ First Section Footer ]");
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
//Adds the second section to the document
section = document.AddSection();
//Inserts the second section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Second Section Header ]");
//Inserts the second section footer.
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Second Section Footer ]");
//Sets LinkToPrevious as true for retrieve the header and footer from previous section
section.HeadersFooters.LinkToPrevious = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
//Adds the third section to the document
section = document.AddSection();
//Inserts the third section header
section.HeadersFooters.Header.AddParagraph().AppendText("[ Third Section Header ]");
//Inserts the third section footer
section.HeadersFooters.Footer.AddParagraph().AppendText("[ Third Section Footer ]");
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Link-previous-section).

### Remove Headers and Footers

You can remove the headers and footers from an existing Word document. The following code example explains how to remove the headers and footers from an existing Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open an existing document.
WordDocument document = new WordDocument("Input.docx", FormatType.Automatic);
//Iterate to each section in the Word document.
foreach (WSection section in document.Sections)
{
    //Remove the first page header.
    section.HeadersFooters.FirstPageHeader.ChildEntities.Clear();
    //Remove the first page footer.
    section.HeadersFooters.FirstPageFooter.ChildEntities.Clear();
    //Remove the odd footer.
    section.HeadersFooters.OddFooter.ChildEntities.Clear();
    //Remove the odd header.
    section.HeadersFooters.OddHeader.ChildEntities.Clear();
    //Remove the even header.
    section.HeadersFooters.EvenHeader.ChildEntities.Clear();
    //Remove the even footer.
    section.HeadersFooters.EvenFooter.ChildEntities.Clear();
}
//Save the Word document.
document.Save("Output.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing document.
Dim document As WordDocument = New WordDocument("Input.docx", FormatType.Automatic)
'Iterate to each section in the Word document.
For Each section As WSection In document.Sections
    'Remove the first page header.
    section.HeadersFooters.FirstPageHeader.ChildEntities.Clear()
    'Remove the first page footer.
    section.HeadersFooters.FirstPageFooter.ChildEntities.Clear()
    'Remove the odd footer.
    section.HeadersFooters.OddFooter.ChildEntities.Clear()
    'Remove the odd header.
    section.HeadersFooters.OddHeader.ChildEntities.Clear()
    'Remove the even header.
    section.HeadersFooters.EvenHeader.ChildEntities.Clear()
    'Remove the even footer.
    section.HeadersFooters.EvenFooter.ChildEntities.Clear()
Next
'Save the Word document.
document.Save("Output.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//Open an existing document.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Input.docx"), FormatType.Docx);
//Iterate to each section in the Word document.
foreach (WSection section in document.Sections)
{
    //Remove the first page header.
    section.HeadersFooters.FirstPageHeader.ChildEntities.Clear();
    //Remove the first page footer.
    section.HeadersFooters.FirstPageFooter.ChildEntities.Clear();
    //Remove the odd footer.
    section.HeadersFooters.OddFooter.ChildEntities.Clear();
    //Remove the odd header.
    section.HeadersFooters.OddHeader.ChildEntities.Clear();
    //Remove the even header.
    section.HeadersFooters.EvenHeader.ChildEntities.Clear();
    //Remove the even footer.
    section.HeadersFooters.EvenFooter.ChildEntities.Clear();
}
//Save and close the Word document instance.
MemoryStream stream = new MemoryStream();
//Save the Word file to the MemoryStream.
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Save the stream a Word file in the local machine.
Save(stream, "Output.docx");
//Please refer to the below link to save the Word document in the UWP platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open an existing document.
FileStream inputStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read);
WordDocument document = new WordDocument(inputStream, FormatType.Automatic);
//Iterate to each section in the Word document.
foreach (WSection section in document.Sections)
{
    //Remove the first page header.
    section.HeadersFooters.FirstPageHeader.ChildEntities.Clear();
    //Remove the first page footer.
    section.HeadersFooters.FirstPageFooter.ChildEntities.Clear();
    //Remove the odd footer.
    section.HeadersFooters.OddFooter.ChildEntities.Clear();
    //Remove the odd header.
    section.HeadersFooters.OddHeader.ChildEntities.Clear();
    //Remove the even header.
    section.HeadersFooters.EvenHeader.ChildEntities.Clear();
    //Remove the even footer.
    section.HeadersFooters.EvenFooter.ChildEntities.Clear();
}
//Save and close the Word document instance.
MemoryStream stream = new MemoryStream();
//Save the Word document to the MemoryStream.
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download the Word document in the browser.
return File(stream, "application/msword", "Output.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Open an existing document.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("XamarinApp.Data.Template.docx");
WordDocument wordDocument = new WordDocument(fileStream, FormatType.Automatic);
//Iterate to each section in the Word document.
foreach (WSection section in document.Sections)
{
    //Remove the first page header.
    section.HeadersFooters.FirstPageHeader.ChildEntities.Clear();
    //Remove the first page footer.
    section.HeadersFooters.FirstPageFooter.ChildEntities.Clear();
    //Remove the odd footer.
    section.HeadersFooters.OddFooter.ChildEntities.Clear();
    //Remove the odd header.
    section.HeadersFooters.OddHeader.ChildEntities.Clear();
    //Remove the even header.
    section.HeadersFooters.EvenHeader.ChildEntities.Clear();
    //Remove the even footer.
    section.HeadersFooters.EvenFooter.ChildEntities.Clear();
}
//Save and close the Word document instance.
MemoryStream stream = new MemoryStream();
//Save the Word file to the MemoryStream.
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing.
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream a file and open the file for viewing in the Xamarin platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Remove-headers-and-footers).

## Adding Page Numbers

You can insert the current page number within the document contents. The following code example illustrates how to insert current page number within footer.   

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
section.PageSetup.PageStartingNumber = 1;
section.PageSetup.RestartPageNumbering = true;
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;
//Adds a footer paragraph text to the document
IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();
paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);
//Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015");
//Adds page number field to the document
paragraph.AppendText("\tPage ");
paragraph.AppendField("Page", FieldType.FieldPage);
//Adds the paragraph
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds the section into Word document
Dim section As IWSection = document.AddSection()
section.PageSetup.PageStartingNumber = 1
section.PageSetup.RestartPageNumbering = True
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic
'Adds a footer paragraph text to the document
Dim paragraph As IWParagraph = section.HeadersFooters.Footer.AddParagraph()
paragraph.ParagraphFormat.Tabs.AddTab(523.0F, TabJustification.Right, TabLeader.NoLeader)
'Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015")
'Adds page number field to the document
paragraph.AppendText(vbTab & "Page ")
paragraph.AppendField("Page", FieldType.FieldPage)
'Adds the paragraph
paragraph = section.AddParagraph()
'Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
section.PageSetup.PageStartingNumber = 1;
section.PageSetup.RestartPageNumbering = true;
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;
//Adds a footer paragraph text to the document
IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();
paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);
//Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015");
//Adds page number field to the document
paragraph.AppendText("\tPage ");
paragraph.AppendField("Page", FieldType.FieldPage);
//Adds the paragraph
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
section.PageSetup.PageStartingNumber = 1;
section.PageSetup.RestartPageNumbering = true;
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;
//Adds a footer paragraph text to the document
IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();
paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);
//Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015");
//Adds page number field to the document
paragraph.AppendText("\tPage ");
paragraph.AppendField("Page", FieldType.FieldPage);
//Adds the paragraph
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
section.PageSetup.PageStartingNumber = 1;
section.PageSetup.RestartPageNumbering = true;
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;
//Adds a footer paragraph text to the document
IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();
paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);
//Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015");
//Adds page number field to the document
paragraph.AppendText("\tPage ");
paragraph.AppendField("Page", FieldType.FieldPage);
//Adds the paragraph
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

The following code example illustrates how to add the current page number and total number of pages in header/footer. 

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
section.PageSetup.PageStartingNumber = 1;
section.PageSetup.RestartPageNumbering = true;
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;
//Adds a footer paragraph text to the document
IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();
paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);
// Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015\t");
//Adds the text
paragraph.AppendText(" Page ");
//Adds page number field to the document
paragraph.AppendField("CurrentPageNumber", FieldType.FieldPage);
// Adds the text
paragraph.AppendText(" of ");
//Adds number of page field to the document
paragraph.AppendField("TotalNumberOfPages", FieldType.FieldNumPages);
//Adds the paragraph
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds the section into Word document
Dim section As IWSection = document.AddSection()
section.PageSetup.PageStartingNumber = 1
section.PageSetup.RestartPageNumbering = True
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic
'Adds a footer paragraph text to the document
Dim paragraph As IWParagraph = section.HeadersFooters.Footer.AddParagraph()
paragraph.ParagraphFormat.Tabs.AddTab(523.0F, TabJustification.Right, TabLeader.NoLeader)
'Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015" & vbTab)
'Adds the text
paragraph.AppendText(" Page ")
'Adds page number field to the document
paragraph.AppendField("CurrentPageNumber", FieldType.FieldPage)
'Adds the text
paragraph.AppendText(" of ")
'Adds number of page field to the document
paragraph.AppendField("TotalNumberOfPages", FieldType.FieldNumPages)
'Adds the paragraph
paragraph = section.AddParagraph()
'Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
section.PageSetup.PageStartingNumber = 1;
section.PageSetup.RestartPageNumbering = true;
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;
//Adds a footer paragraph text to the document
IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();
paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);
//Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015\t");
//Adds the text
paragraph.AppendText(" Page ");
//Adds page number field to the document
paragraph.AppendField("CurrentPageNumber", FieldType.FieldPage);
// Adds the text
paragraph.AppendText(" of ");
//Adds number of page field to the document
paragraph.AppendField("TotalNumberOfPages", FieldType.FieldNumPages);
//Adds the paragraph
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
section.PageSetup.PageStartingNumber = 1;
section.PageSetup.RestartPageNumbering = true;
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;
//Adds a footer paragraph text to the document
IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();
paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);
// Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015\t");
//Adds the text
paragraph.AppendText(" Page ");
//Adds page number field to the document
paragraph.AppendField("CurrentPageNumber", FieldType.FieldPage);
//Adds the text
paragraph.AppendText(" of ");
//Adds number of page field to the document
paragraph.AppendField("TotalNumberOfPages", FieldType.FieldNumPages);
//Adds the paragraph
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into Word document
IWSection section = document.AddSection();
section.PageSetup.PageStartingNumber = 1;
section.PageSetup.RestartPageNumbering = true;
section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;
//Adds a footer paragraph text to the document
IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();
paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);
//Adds text for the footer paragraph
paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015\t");
//Adds the text
paragraph.AppendText(" Page ");
//Adds page number field to the document
paragraph.AppendField("CurrentPageNumber", FieldType.FieldPage);
//Adds the text
paragraph.AppendText(" of ");
//Adds number of page field to the document
paragraph.AppendField("TotalNumberOfPages", FieldType.FieldNumPages);
//Adds the paragraph
paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

The following code example shows how to adjust the height of header and footer.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Specifies the value to header distance
section.PageSetup.HeaderDistance = 100;
//Specifies the value to footer distance
section.PageSetup.FooterDistance = 100;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new document
Dim document As New WordDocument()
'Adds the first section to the document
Dim section As IWSection = document.AddSection()
'Specifies the value to header distance
section.PageSetup.HeaderDistance = 100
'Specifies the value to footer distance
section.PageSetup.FooterDistance = 100
'Adds a paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Appends some text to the first page in document
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)
paragraph.ParagraphFormat.PageBreakAfter = True
'Appends some text to the second page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)
paragraph.ParagraphFormat.PageBreakAfter = True
'Appends some text to the third page in document
paragraph = section.AddParagraph()
paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)
'Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph()
paragraph.AppendText("[ Default Page Header ]")
'Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph()
paragraph.AppendText("[ Default Page Footer ]")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Specifies the value to header distance
section.PageSetup.HeaderDistance = 100;
//Specifies the value to footer distance
section.PageSetup.FooterDistance = 100;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();        
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Specifies the value to header distance
section.PageSetup.HeaderDistance = 100;
//Specifies the value to footer distance
section.PageSetup.FooterDistance = 100;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds the first section to the document
IWSection section = document.AddSection();
//Specifies the value to header distance
section.PageSetup.HeaderDistance = 100;
//Specifies the value to footer distance
section.PageSetup.FooterDistance = 100;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Appends some text to the first page in document
paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the second page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);
paragraph.ParagraphFormat.PageBreakAfter = true;
//Appends some text to the third page in document
paragraph = section.AddParagraph();
paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);
//Inserts the default page header
paragraph = section.HeadersFooters.OddHeader.AddParagraph();
paragraph.AppendText("[ Default Page Header ]");
//Inserts the default page footer
paragraph = section.HeadersFooters.OddFooter.AddParagraph();
paragraph.AppendText("[ Default Page Footer ]");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Add-page-number-in-footer).

## Add Line Numbers

Line numbers can be displayed beside a text in a Word document, which can be achieved using the following APIs.

  * [LineNumberingDistanceFromText](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WPageSetup.html#Syncfusion_DocIO_DLS_WPageSetup_LineNumberingDistanceFromText) - Represents the distance between the text and the line number.
  * [LineNumberingMode](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WPageSetup.html#Syncfusion_DocIO_DLS_WPageSetup_LineNumberingMode) - Represents how the line number runs, that is, continuous, restart each page, restart each section.
  * [LineNumberingStartValue](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WPageSetup.html#Syncfusion_DocIO_DLS_WPageSetup_LineNumberingStartValue) - Represents the starting value of the line number.
  * [LineNumberingStep](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WPageSetup.html#Syncfusion_DocIO_DLS_WPageSetup_LineNumberingStep) - Represents the incremental value of the line number.

The following code example illustrates how to add line numbers in a Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load an existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    //Iterate each section.
    foreach (WSection section in document.Sections)
    {
        //Set the line number distance from the text.
        section.PageSetup.LineNumberingDistanceFromText = 10;
        //Set the numbering mode.
        section.PageSetup.LineNumberingMode = LineNumberingMode.Continuous;
        //Set the starting line number value.
        section.PageSetup.LineNumberingStartValue = 1;
        //Set the increment value for line numbering.
        section.PageSetup.LineNumberingStep = 2;
    }
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
    //Iterate each section.
    For Each section As WSection In document.Sections
        'Set the line number distance from the text.
        section.PageSetup.LineNumberingDistanceFromText = 10
        'Set the numbering mode.
        section.PageSetup.LineNumberingMode = LineNumberingMode.Continuous
        'Set the starting line number value.
        section.PageSetup.LineNumberingStartValue = 1
        'Set the increment value for line numbering.
        section.PageSetup.LineNumberingStep = 2
    Next
    'Save a Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using

{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Iterate each section.
        foreach (WSection section in document.Sections)
        {
            //Set the line number distance from the text.
            section.PageSetup.LineNumberingDistanceFromText = 10;
            //Set the numbering mode.
            section.PageSetup.LineNumberingMode = LineNumberingMode.Continuous;
            //Set the starting line number value.
            section.PageSetup.LineNumberingStartValue = 1;
            //Set the increment value for line numbering.
            section.PageSetup.LineNumberingStep = 2;
        }
        //Save a Word document to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx");
    }
}
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Iterate each section.
        foreach (WSection section in document.Sections)
        {
            //Set the line number distance from the text.
            section.PageSetup.LineNumberingDistanceFromText = 10;
            //Set the numbering mode.
            section.PageSetup.LineNumberingMode = LineNumberingMode.Continuous;
            //Set the starting line number value.
            section.PageSetup.LineNumberingStartValue = 1;
            //Set the increment value for line numbering.
            section.PageSetup.LineNumberingStep = 2;
        }
        //Save a  Word document to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        outputStream.Position = 0;
        //Download as a Word document in the browser.
        return File(outputStream, "application/msword", "Sample.docx");
    }
}
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Iterate each section.
        foreach (WSection section in document.Sections)
        {
            //Set the line number distance from the text.
            section.PageSetup.LineNumberingDistanceFromText = 10;
            //Set the numbering mode.
            section.PageSetup.LineNumberingMode = LineNumberingMode.Continuous;
            //Set the starting line number value.
            section.PageSetup.LineNumberingStartValue = 1;
            //Set the increment value for line numbering.
            section.PageSetup.LineNumberingStep = 2;
        }
        //Save a Word document to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing. 
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
    }
}
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Add-line-numbers).

## Removing a Section

The following code example illustrates how to remove a particular section from the Word document

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an input Word template
WordDocument document = new WordDocument(inputFileName);
//Removes the second section from the collection
document.Sections.RemoveAt(1);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an input Word template
Dim document As New WordDocument(inputFileName)
'Removes the second section from the collection
document.Sections.RemoveAt(1)
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputFileStream = assembly.GetManifestResourceStream(inputFileName);
//Opens an input Word template
WordDocument document = new WordDocument(inputFileStream);
//Removes the second section from the collection
document.Sections.RemoveAt(1);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream inputFileStream = new FileStream(inputFileName, FileMode.Open, FileAccess.ReadWrite);
//Opens an input Word template
WordDocument document = new WordDocument(inputFileStream, FormatType.Automatic);
//Removes the second section from the collection
document.Sections.RemoveAt(1);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputFileStream = assembly.GetManifestResourceStream(inputFileName);
//Loads an existing Word document into DocIO instance
WordDocument document = new WordDocument(inputFileStream, FormatType.Automatic);
//Removes the second section from the collection
document.Sections.RemoveAt(1);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Sections/Remove-section-from-document).

N> * The Word document is a flow document in which contents will not be preserved page by page; instead the contents will be preserved sequentially section by section. Each section may extend to various pages based on its contents like table, text, images etc.
N> * Word viewer/editor renders the contents of the Word document page by page dynamically when opened for viewing or editing and this page wise rendered information will not be preserved in the document level as per the Word file format specification.
N> * Whereas Essential DocIO is a non-UI component that provides a full-fledged document object model to manipulate the Word document contents. Hence it is not feasible to set different page margins or page settings to each page instead we can do the same for each section.
N> * And also, it is not feasible to get the page-wise details from Word document and split the Word document in page by page. 

## See Also

* [How to copy the HeaderFooter content from one Word document and insert them into first page header footer of another Word document](https://www.syncfusion.com/kb/12923/how-to-copy-the-headerfooter-content-from-one-word-document-and-insert-them-into-first-page)
* [How to determine the page number of a particular text within a Word document](https://www.syncfusion.com/kb/12931/how-to-determine-the-page-number-of-a-particular-text-within-a-word-document)
* [How to remove empty page at end of Word document](https://www.syncfusion.com/kb/10724/how-to-remove-empty-page-at-end-of-word-document)
* [How to merge the sections in an already existing document to a new document](https://www.syncfusion.com/kb/274/how-do-i-merge-the-sections-in-an-already-existing-document-to-a-new-document)
* [How to insert headers and footers in a document](https://www.syncfusion.com/kb/275/how-do-i-insert-headers-and-footers-in-a-document)
* [Is it possible to create different Header and footer in a word document](https://www.syncfusion.com/kb/291/is-it-possible-to-create-different-header-and-footer-in-a-word-document)
* [How to change section break in Word document as page break?](https://www.syncfusion.com/support/kb/13649/how-to-change-section-break-in-word-document-as-page-break)
* [How to add multiple page number formats in Word document?](https://www.syncfusion.com/kb/13701/how-to-add-multiple-page-number-formats-in-word-document)
* [How to merge two Word documents without header and footer from the source document?](https://www.syncfusion.com/kb/13930/how-to-merge-two-word-documents-without-header-and-footer-from-the-source-document)
* [How to add different header and footer for last page alone in the Word document?](https://www.syncfusion.com/kb/13948/how-to-add-different-header-and-footer-for-last-page-alone-in-the-word-document)