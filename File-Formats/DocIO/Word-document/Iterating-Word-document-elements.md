---
title: Iterating Word document elements | DocIO | Syncfusion
description: This section illustrates how to modify an existing Word document by iterating through Word document elements without using Microsoft Word or Office interop.
platform: file-formats
control: DocIO
documentation: UG
---
# Iterating Word document elements

The following are the important points to be remembered while iterating the document elements

* Document consists of one or more sections.
* Section contains the contents present in Headers, Footers and main document through the instances of [WTextBody](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WTextBody.html).
* [WTextBody](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WTextBody.html) contains three type of elements – either paragraph, table or block content control.

## Remove paragraph with style

The following code example shows how to iterate throughout the Word document and remove the paragraph with a particular style.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing document from file system through constructor of WordDocument class
WordDocument document = new WordDocument(@"TestDocument.docx");
//Processes the body contents for each section in the Word document
foreach (WSection section in document.Sections)
{
    //Accesses the Body of section where all the contents in document are apart
    WTextBody sectionBody = section.Body;
    IterateTextBody(sectionBody);
    WHeadersFooters headersFooters = section.HeadersFooters;
    //Consider that OddHeader and OddFooter are applied to this document
    //Iterates through the TextBody of OddHeader and OddFooter
    IterateTextBody(headersFooters.OddHeader);
    IterateTextBody(headersFooters.OddFooter);
}
//Saves and closes the document instance
document.Save("Result.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing document from file system through constructor of WordDocument class
Dim document As New WordDocument("TestDocument.docx")
'Processes the body contents for each section in the Word document
For Each section As WSection In document.Sections
    'Accesses the Body of section where all the contents in document are apart
    Dim sectionBody As WTextBody = section.Body
    IterateTextBody(sectionBody)
    Dim headersFooters As WHeadersFooters = section.HeadersFooters
    'Consider that OddHeader and OddFooter are applied to this document
    'Iterates through the text body of OddHeader and OddFooter
    IterateTextBody(headersFooters.OddHeader)
    IterateTextBody(headersFooters.OddFooter)
Next
'Saves and closes the document instance
document.Save("Result.docx")
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx")), FormatType.Docx))
{
    foreach (WSection section in document.Sections)
    {
        //Accesses the Body of section where all the contents in document are apart
        WTextBody sectionBody = section.Body;
        IterateTextBody(sectionBody);
        WHeadersFooters headersFooters = section.HeadersFooters;
        //Consider that OddHeader and OddFooter are applied to this document
        //Iterates through the TextBody of OddHeader and OddFooter
        IterateTextBody(headersFooters.OddHeader);
        IterateTextBody(headersFooters.OddFooter);
    }
    MemoryStream stream = new MemoryStream();
    await document.SaveAsync(stream, FormatType.Docx);
    //Saves the stream as Word file in local machine
    Save(stream, "Result.docx");
    //Please refer the below link to save Word document in UWP platform
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Automatic))
{
    foreach (WSection section in document.Sections)
    {
        //Accesses the Body of section where all the contents in document are apart
        WTextBody sectionBody = section.Body;
        IterateTextBody(sectionBody);
        WHeadersFooters headersFooters = section.HeadersFooters;
        //Consider that OddHeader and OddFooter are applied to this document
        //Iterates through the TextBody of OddHeader and OddFooter
        IterateTextBody(headersFooters.OddHeader);
        IterateTextBody(headersFooters.OddFooter);
    }
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Closes the Word document
    document.Close();
    stream.Position = 0;
    //Download Word document in the browser
    return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx")), FormatType.Automatic))
{
    foreach (WSection section in document.Sections)
    {
        //Accesses the Body of section where all the contents in document are apart
        WTextBody sectionBody = section.Body;
        IterateTextBody(sectionBody);
        WHeadersFooters headersFooters = section.HeadersFooters;
        //Consider that OddHeader and OddFooter are applied to this document
        //Iterates through the TextBody of OddHeader and OddFooter
        IterateTextBody(headersFooters.OddHeader);
        IterateTextBody(headersFooters.OddFooter);
    }
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
    //Closes the Word document
    document.Close();
    //Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods for the above code.

{% tabs %}

{% highlight c# tabtitle="C#" %}
private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Checks for particular style name and removes the paragraph from DOM
                if (paragraph.StyleName == "MyStyle")
                {
                    int index = textBody.ChildEntities.IndexOf(paragraph);
                    textBody.ChildEntities.RemoveAt(index);
                }
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Shared Sub IterateTextBody(textBody As WTextBody)
'Iterates through the each of the child items of WTextBody
For i As Integer = 0 To textBody.ChildEntities.Count - 1
    'IEntity is the basic unit in DocIO DOM. 
    'Accesses the body items (should be either paragraph, table or block content control) as IEntity
    Dim bodyItemEntity As IEntity = textBody.ChildEntities(i)
    'A Text body has 3 types of elements - Paragraph, Table and Block Content Control
    'decide the element type using EntityType
    Select Case bodyItemEntity.EntityType
        Case EntityType.Paragraph
            Dim paragraph As WParagraph = TryCast(bodyItemEntity, WParagraph)
            'Checks for a particular style name and removes the paragraph from DOM
            If paragraph.StyleName = "MyStyle" Then
                Dim index As Integer = textBody.ChildEntities.IndexOf(paragraph)
                textBody.ChildEntities.RemoveAt(index)
            End If
        Exit Select
        Case EntityType.Table
            'Table is a collection of rows and cells
            'Iterates through table's DOM
            IterateTable(TryCast(bodyItemEntity, WTable))
        Exit Select
        Case EntityType.BlockContentControl
            Dim BlockContentControl As BlockContentControl = TryCast(bodyItemEntity, BlockContentControl)
            'Iterates to the body items of Block Content Control.
            IterateTextBody(BlockContentControl.TextBody)
        Exit Select
    End Select
Next
End Sub
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
async void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Checks for particular style name and removes the paragraph from DOM
                if (paragraph.StyleName == "MyStyle")
                {
                    int index = textBody.ChildEntities.IndexOf(paragraph);
                    textBody.ChildEntities.RemoveAt(index);
                }
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
                case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Checks for particular style name and removes the paragraph from DOM
                if (paragraph.StyleName == "MyStyle")
                {
                    int index = textBody.ChildEntities.IndexOf(paragraph);
                    textBody.ChildEntities.RemoveAt(index);
                }
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Checks for particular style name and removes the paragraph from DOM
                if (paragraph.StyleName == "MyStyle")
                {
                    int index = textBody.ChildEntities.IndexOf(paragraph);
                    textBody.ChildEntities.RemoveAt(index);
                }
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods for the above code.

{% tabs %}

{% highlight c# tabtitle="C#" %}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Shared Sub IterateTable(table As WTable)
'Iterates the row collection in a table
For Each row As WTableRow In table.Rows
    'Iterates the cell collection in a table row
    For Each cell As WTableCell In row.Cells
        'Table cell is derived from (also a) TextBody
        'Reusing the code meant for iterating TextBody
        IterateTextBody(cell)
    Next
Next
End Sub
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
async void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Remove-paragraph-with-style).

## Modify Hyperlink Uri

The following code example shows how to iterate throughout the paragraph and modify the hyperlink ([Hyperlink](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.Hyperlink.html)) Uri and specific text ([WTextRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WTextRange.html)) with another.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing document from file system through constructor of WordDocument class
WordDocument document = new WordDocument(@"TestDocument.docx");
//Processes the body contents for each section in the Word document
foreach (WSection section in document.Sections)
{
    //Accesses the Body of section where all the contents in document are apart
    WTextBody sectionBody = section.Body;
    IterateTextBody(sectionBody);
    WHeadersFooters headersFooters = section.HeadersFooters;
    //consider that OddHeader & OddFooter are applied to this document
    //Iterates through the TextBody of OddHeader and OddFooter
    IterateTextBody(headersFooters.OddHeader);
    IterateTextBody(headersFooters.OddFooter);
}
//Saves and closes the document instance
document.Save("Result.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim document As New WordDocument("TestDocument.docx")
    'Processes the body contents for each section in the Word document
    For Each section As WSection In document.Sections
        'Accesses the Body of section where all the contents in document are apart
        Dim sectionBody As WTextBody = section.Body
        IterateTextBody(sectionBody)
        Dim headersFooters As WHeadersFooters = section.HeadersFooters
        'Considers that OddHeader and OddFooter are applied to this document
        'Iterates through the TextBody of OddHeader and OddFooterIterateTextBody(headersFooters.OddHeader)
        IterateTextBody(headersFooters.OddFooter)
    Next
'Saves and closes the document instance
document.Save("Result.docx")
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx")), FormatType.Docx))
{
    foreach (WSection section in document.Sections)
    {
        //Accesses the Body of section where all the contents in document are apart
        WTextBody sectionBody = section.Body;
        IterateTextBody(sectionBody);
        WHeadersFooters headersFooters = section.HeadersFooters;
        //Consider that OddHeader and OddFooter are applied to this document
        //Iterates through the TextBody of OddHeader and OddFooter
        IterateTextBody(headersFooters.OddHeader);
        IterateTextBody(headersFooters.OddFooter);
    }
    MemoryStream stream = new MemoryStream();
    await document.SaveAsync(stream, FormatType.Docx);
    //Saves the stream as Word file in local machine
    Save(stream, "Result.docx");
    //Please refer the below link to save Word document in UWP platform
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Automatic))
{
    foreach (WSection section in document.Sections)
    {
        //Accesses the Body of section where all the contents in document are apart
        WTextBody sectionBody = section.Body;
        IterateTextBody(sectionBody);
        WHeadersFooters headersFooters = section.HeadersFooters;
        //Consider that OddHeader and OddFooter are applied to this document
        //Iterates through the TextBody of OddHeader and OddFooter
        IterateTextBody(headersFooters.OddHeader);
        IterateTextBody(headersFooters.OddFooter);
    }
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Closes the Word document
    document.Close();
    stream.Position = 0;
    //Download Word document in the browser
    return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx")), FormatType.Automatic))
{
    foreach (WSection section in document.Sections)
    {
        //Accesses the Body of section where all the contents in document are apart
        WTextBody sectionBody = section.Body;
        IterateTextBody(sectionBody);
        WHeadersFooters headersFooters = section.HeadersFooters;
        //Consider that OddHeader and OddFooter are applied to this document
        //Iterates through the TextBody of OddHeader and OddFooter
        IterateTextBody(headersFooters.OddHeader);
        IterateTextBody(headersFooters.OddFooter);
    }
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
    //Closes the Word document
    document.Close();
    //Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}
  
The following code example provides supporting methods for the above code.

{% tabs %}

{% highlight c# tabtitle="C#" %}
private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Processes the paragraph contents
                //Iterates through the paragraph's DOM
                IterateParagraph(paragraph.Items);
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Shared Sub IterateTextBody(textBody As WTextBody)
'Iterates through each of the child items of WTextBody
For i As Integer = 0 To textBody.ChildEntities.Count - 1
    'IEntity is the basic unit in DocIO DOM. 
    'Accesses the body items (should be either paragraph, table or block content control) as IEntity
    Dim bodyItemEntity As IEntity = textBody.ChildEntities(i)
    'A Text body has 3 types of elements - Paragraph, Table and Block Content Control
    'Decides the element type by using EntityType
    Select Case bodyItemEntity.EntityType
        Case EntityType.Paragraph
            Dim paragraph As WParagraph = TryCast(bodyItemEntity, WParagraph)
            'Processes the paragraph contents
            'Iterates through the paragraph's DOM
            IterateParagraph(paragraph.Items)
        Exit Select
        Case EntityType.Table
            'Table is a collection of rows and cells
            'Iterates through table's DOM
            IterateTable(TryCast(bodyItemEntity, WTable))
        Exit Select
        Case EntityType.BlockContentControl
            Dim BlockContentControl As BlockContentControl = TryCast(bodyItemEntity, BlockContentControl)
            'Iterates to the body items of Block Content Control.
            IterateTextBody(BlockContentControl.TextBody)
        Exit Select
    End Select
Next
End Sub
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
async void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Processes the paragraph contents
                //Iterates through the paragraph's DOM
                IterateParagraph(paragraph.Items);
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Processes the paragraph contents
                //Iterates through the paragraph's DOM
                IterateParagraph(paragraph.Items);
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Processes the paragraph contents
                //Iterates through the paragraph's DOM
                IterateParagraph(paragraph.Items);
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods for the above code.

{% tabs %}

{% highlight c# tabtitle="C#" %}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Shared Sub IterateTable(table As WTable)
'Iterates the row collection in a table
For Each row As WTableRow In table.Rows
    'Iterates the cell collection in a table row
    For Each cell As WTableCell In row.Cells
        'Table cell is derived from (also a) TextBody
        'Reusing the code meant for iterating TextBody
        IterateTextBody(cell)
    Next
Next
End Sub
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
async void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods for the above code.

{% tabs %}

{% highlight c# tabtitle="C#" %}
private static void IterateParagraph(ParagraphItemCollection paraItems)
{
    for (int i = 0; i < paraItems.Count; i++)
    {
        Entity entity = paraItems[i];
        //A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,
        //Decides the element type by using EntityType
        switch (entity.EntityType)
        {
            case EntityType.TextRange:
                //Replaces the text with another
                WTextRange textRange = entity as WTextRange;
                if (textRange.Text == "Andrew")
                {
                    (entity as WTextRange).Text = "Fuller";
                }
                break;
            case EntityType.Field:
                WField field = entity as WField;
                if (field.FieldType == FieldType.FieldHyperlink)
                {
                    //Creates hyperlink instance from field to manipulate the hyperlink
                    Hyperlink hyperlink = new Hyperlink(entity as WField);
                    //Modifies the Uri of the hyperlink
                    if (hyperlink.Type == HyperlinkType.WebLink && hyperlink.TextToDisplay == "HTML")
                    {
                        hyperlink.Uri = "http://www.w3schools.com/";
                    }
                }
                break;
            case EntityType.TextBox:
                //Iterates to the body items of textbox.
                WTextBox textBox = entity as WTextBox;
                IterateTextBody(textBox.TextBoxBody);
                break;
            case EntityType.Shape:
                //Iterates to the body items of shape.
                Shape shape = entity as Shape;
                IterateTextBody(shape.TextBody);
                break;
            case EntityType.InlineContentControl:
                //Iterates to the paragraph items of inline content control.
                InlineContentControl inlineContentControl = entity as InlineContentControl;
                IterateParagraph(inlineContentControl.ParagraphItems);
                break;
        }
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Shared Sub IterateParagraph(paraItems As ParagraphItemCollection)
For i As Integer = 0 To paraItems.Count - 1
    Dim entity As Entity = paraItems(i)
    'A Paragraph has child elements such as text, image, hyperlink, symbols, etc.,
    'Decides the element type by using EntityType
    Select Case entity.EntityType
        Case EntityType.TextRange
            'Replaces the text with another
            Dim textRange As WTextRange = TryCast(entity, WTextRange)
            If textRange.Text = "Andrew" Then
                TryCast(entity, WTextRange).Text = "Fuller"
            End If
        Exit Select
        Case EntityType.Field
            Dim field As WField = TryCast(entity, WField)
            If field.FieldType = FieldType.FieldHyperlink Then
                'Creates Hyperlink instance from field to manipulate the Hyperlink
                Dim hyperlink As New Hyperlink(TryCast(entity, WField))
                'Modifies the Uri of the hyperlink
                If hyperlink.Type = HyperlinkType.WebLink AndAlso hyperlink.TextToDisplay = "HTML" Then
                    hyperlink.Uri = "http://www.w3schools.com/"
                End If
            End If
        Exit Select
        Case EntityType.TextBox
            'Iterates to the body items of textbox.
            Dim textBox As WTextBox = TryCast(entity, WTextBox)
            IterateTextBody(textBox.TextBoxBody)
        Exit Select
        Case EntityType.Shape
            'Iterates to the body items of shape.
            Dim shape As Shape = TryCast(entity, Shape)
            IterateTextBody(shape.TextBody)
        Exit Select
        Case EntityType.InlineContentControl
            'Iterates to the paragraph items of inline content control.
            Dim inlineContentControl As InlineContentControl = TryCast(entity, InlineContentControl)
            IterateParagraph(inlineContentControl.ParagraphItems)
        Exit Select
    End Select
Next
End Sub
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
async void IterateParagraph(ParagraphItemCollection paraItems)
{
    for (int i = 0; i < paraItems.Count; i++)
    {
        Entity entity = paraItems[i];
        //A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,
        //Decides the element type by using EntityType
        switch (entity.EntityType)
        {
            case EntityType.TextRange:
                //Replaces the text with another
                WTextRange textRange = entity as WTextRange;
                if (textRange.Text == "Andrew")
                {
                    (entity as WTextRange).Text = "Fuller";
                }
                break;
            case EntityType.Field:
                WField field = entity as WField;
                if (field.FieldType == FieldType.FieldHyperlink)
                {
                    //Creates hyperlink instance from field to manipulate the hyperlink
                    Hyperlink hyperlink = new Hyperlink(entity as WField);
                    //Modifies the Uri of the hyperlink
                    if (hyperlink.Type == HyperlinkType.WebLink && hyperlink.TextToDisplay == "HTML")
                    {
                        hyperlink.Uri = "http://www.w3schools.com/";
                    }
                }
                break;
            case EntityType.TextBox:
                //Iterates to the body items of textbox.
                WTextBox textBox = entity as WTextBox;
                IterateTextBody(textBox.TextBoxBody);
                break;
            case EntityType.Shape:
                //Iterates to the body items of shape.
                Shape shape = entity as Shape;
                IterateTextBody(shape.TextBody);
                break;
            case EntityType.InlineContentControl:
                //Iterates to the paragraph items of inline content control.
                InlineContentControl inlineContentControl = entity as InlineContentControl;
                IterateParagraph(inlineContentControl.ParagraphItems);
                break;
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
private static void IterateParagraph(ParagraphItemCollection paraItems)
{
    for (int i = 0; i < paraItems.Count; i++)
    {
        Entity entity = paraItems[i];
        //A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,
        //Decides the element type by using EntityType
        switch (entity.EntityType)
        {
            case EntityType.TextRange:
                //Replaces the text with another
                WTextRange textRange = entity as WTextRange;
                if (textRange.Text == "Andrew")
                {
                    (entity as WTextRange).Text = "Fuller";
                }
                break;
            case EntityType.Field:
                WField field = entity as WField;
                if (field.FieldType == FieldType.FieldHyperlink)
                {
                    //Creates hyperlink instance from field to manipulate the hyperlink
                    Hyperlink hyperlink = new Hyperlink(entity as WField);
                    //Modifies the Uri of the hyperlink
                    if (hyperlink.Type == HyperlinkType.WebLink && hyperlink.TextToDisplay == "HTML")
                    {
                        hyperlink.Uri = "http://www.w3schools.com/";
                    }
                }
                break;
            case EntityType.TextBox:
                //Iterates to the body items of textbox.
                WTextBox textBox = entity as WTextBox;
                IterateTextBody(textBox.TextBoxBody);
                break;
            case EntityType.Shape:
                //Iterates to the body items of shape.
                Shape shape = entity as Shape;
                IterateTextBody(shape.TextBody);
                break;
            case EntityType.InlineContentControl:
                //Iterates to the paragraph items of inline content control.
                InlineContentControl inlineContentControl = entity as InlineContentControl;
                IterateParagraph(inlineContentControl.ParagraphItems);
                break;
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
private static void IterateParagraph(ParagraphItemCollection paraItems)
{
    for (int i = 0; i < paraItems.Count; i++)
    {
        Entity entity = paraItems[i];
        //A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,
        //Decides the element type by using EntityType
        switch (entity.EntityType)
        {
            case EntityType.TextRange:
                //Replaces the text with another
                WTextRange textRange = entity as WTextRange;
                if (textRange.Text == "Andrew")
                {
                    (entity as WTextRange).Text = "Fuller";
                }
                break;
            case EntityType.Field:
                WField field = entity as WField;
                if (field.FieldType == FieldType.FieldHyperlink)
                {
                    //Creates hyperlink instance from field to manipulate the hyperlink
                    Hyperlink hyperlink = new Hyperlink(entity as WField);
                    //Modifies the Uri of the hyperlink
                    if (hyperlink.Type == HyperlinkType.WebLink && hyperlink.TextToDisplay == "HTML")
                    {
                        hyperlink.Uri = "http://www.w3schools.com/";
                    }
                }
                break;
            case EntityType.TextBox:
                //Iterates to the body items of textbox.
                WTextBox textBox = entity as WTextBox;
                IterateTextBody(textBox.TextBoxBody);
                break;
            case EntityType.Shape:
                //Iterates to the body items of shape.
                Shape shape = entity as Shape;
                IterateTextBody(shape.TextBody);
                break;
            case EntityType.InlineContentControl:
                //Iterates to the paragraph items of inline content control.
                InlineContentControl inlineContentControl = entity as InlineContentControl;
                IterateParagraph(inlineContentControl.ParagraphItems);
                break;
        }
    }
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Iterate-document-elements).

T> Passing null for both the property names and property values in above APIs, you can also find an item in a Word document without relying on any property.

T> If you wish to find an item in Word document rather than iterating through each element one by one, you can use finding the item functionality to achieve it.