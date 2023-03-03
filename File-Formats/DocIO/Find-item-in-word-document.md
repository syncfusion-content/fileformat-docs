---
title: Find item in Word document in .NET Word library | Syncfusion
description: Find an item in the Word document in C# using Syncfusion .NET Word (DocIO) library without Microsoft Word or interop dependencies
platform: file-formats
control: DocIO
documentation: UG
---

# Find item in Word document

Just like you can search for a text in a Word document, you can also search for an item (like image, content control, textbox, and so on). The .NET Word (DocIO) library supports to find an item in Word document based on its properties. With this functionality, you can:

* Find the first item based on one property.
* Find the first item based on multiple properties
* Find all the items based on one property.
* Find all the items based on multiple properties.

## Find item by property

Using FindItemByProperty API, find the first item in the Word document that has the specified property name and value.

The following code example illustrates how to find the first item based on one property.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load an existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    //Find picture by alternative text.
    WPicture picture = document.FindItemByProperty(EntityType.Picture, "AlternativeText", "Logo") as WPicture;
    //Resize the picture.  
    if (picture != null)
    {
        picture.Height = 75;
        picture.Width = 100;
    }
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
    'Find picture by alternative text.
    Dim picture As WPicture = TryCast(document.FindItemByProperty(EntityType.Picture, "AlternativeText", "Logo"), WPicture)
    'Resize the picture.  
    If picture IsNot Nothing Then
        picture.Height = 75
        picture.Width = 100
    End If
    'Save a Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Find picture by alternative text.
        WPicture picture = document.FindItemByProperty(EntityType.Picture, "AlternativeText", "Logo") as WPicture;
        //Resize the picture.  
        if (picture != null)
        {
            picture.Height = 75;
            picture.Width = 100;
        }
        //Save a Word document to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx"); 
    }
}
//Refer to the following link to save a Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as a Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Find picture by alternative text.
        WPicture picture = document.FindItemByProperty(EntityType.Picture, "AlternativeText", "Logo") as WPicture;
        //Resize the picture.  
        if (picture != null)
        {
            picture.Height = 75;
            picture.Width = 100;
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
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Find picture by alternative text.
        WPicture picture = document.FindItemByProperty(EntityType.Picture, "AlternativeText", "Logo") as WPicture;
        //Resize the picture.  
        if (picture != null)
        {
            picture.Height = 75;
            picture.Width = 100;
        }
        //Save a Word document to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing. 
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
    }
}
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}

## Find item by properties

Using FindItemByProperties API, find the first item in the Word document based on multiple property names and their corresponding values.

The following code example illustrates how to find the first item in Word document based on multiple property names and their corresponding values.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load an existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    string[] propertyNames = { "ChartType", "ChartTitle" };
    string[] propertyValues = { OfficeChartType.Pie.ToString(), "Sales" };
    //Find the chart by ChartType and ChartTitle.
    WChart chart = document.FindItemByProperties(EntityType.Chart, propertyNames, propertyValues) as WChart;
    //Rename the ChartTitle.
    if (chart != null)
    chart.ChartTitle = "Sales Analysis";

    propertyNames =  new string[] { "Title","Rows.Count" };
    propertyValues =  new string[]{ "SupplierDetails","6" };
    //Find the table by Title and Rows Count
    WTable table = document.FindItemByProperties(EntityType.Table, propertyNames,propertyValues) as WTable;
    //Remove the table in document.
    if (table != null)
    table.OwnerTextBody.ChildEntities.Remove(table);
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
    Dim propertyNames = {"ChartType", "ChartTitle"}
    Dim propertyValues As String() = {OfficeChartType.Pie.ToString(), "Sales"}
    'Find the chart by ChartType and ChartTitle.
    Dim chart As WChart = TryCast(document.FindItemByProperties(EntityType.Chart, propertyNames, propertyValues), WChart)

    'Rename the ChartTitle.
    If chart IsNot Nothing Then chart.ChartTitle = "Sales Analysis"

    propertyNames = New String() {"Title", "Rows.Count"}
    propertyValues = New String() {"SupplierDetails", "6"}
    'Find the table by Title and Rows Count
    Dim table As WTable = TryCast(document.FindItemByProperties(EntityType.Table, propertyNames, propertyValues), WTable)
    'Remove the table in document.
    If table IsNot Nothing Then table.OwnerTextBody.ChildEntities.Remove(table)
    'Save a Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        string[] propertyNames = { "ChartType", "ChartTitle" };
        string[] propertyValues = { OfficeChartType.Pie.ToString(), "Sales" };
        //Find the chart by ChartType and ChartTitle.
        WChart chart = document.FindItemByProperties(EntityType.Chart, propertyNames, propertyValues) as WChart;
        //Rename the ChartTitle.
        if (chart != null)
        chart.ChartTitle = "Sales Analysis";

        propertyNames =  new string[] { "Title","Rows.Count" };
        propertyValues =  new string[]{ "SupplierDetails","6" };
        //Find the table by Title and Rows Count
        WTable table = document.FindItemByProperties(EntityType.Table, propertyNames,propertyValues) as WTable;
        //Remove the table in document.
        if (table != null)
        table.OwnerTextBody.ChildEntities.Remove(table);
        //Save a Word document to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx"); 
    }
}
//Refer to the following link to save a Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as a Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        string[] propertyNames = { "ChartType", "ChartTitle" };
        string[] propertyValues = { OfficeChartType.Pie.ToString(), "Sales" };
        //Find the chart by ChartType and ChartTitle.
        WChart chart = document.FindItemByProperties(EntityType.Chart, propertyNames, propertyValues) as WChart;
        //Rename the ChartTitle.
        if (chart != null)
        chart.ChartTitle = "Sales Analysis";

        propertyNames =  new string[] { "Title","Rows.Count" };
        propertyValues =  new string[]{ "SupplierDetails","6" };
        //Find the table by Title and Rows Count
        WTable table = document.FindItemByProperties(EntityType.Table, propertyNames,propertyValues) as WTable;
        //Remove the table in document.
        if (table != null)
        table.OwnerTextBody.ChildEntities.Remove(table);
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
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        string[] propertyNames = { "ChartType", "ChartTitle" };
        string[] propertyValues = { OfficeChartType.Pie.ToString(), "Sales" };
        //Find the chart by ChartType and ChartTitle.
        WChart chart = document.FindItemByProperties(EntityType.Chart, propertyNames, propertyValues) as WChart;
        //Rename the ChartTitle.
        if (chart != null)
        chart.ChartTitle = "Sales Analysis";

        propertyNames =  new string[] { "Title","Rows.Count" };
        propertyValues =  new string[]{ "SupplierDetails","6" };
        //Find the table by Title and Rows Count
        WTable table = document.FindItemByProperties(EntityType.Table, propertyNames,propertyValues) as WTable;
        //Remove the table in document.
        if (table != null)
        table.OwnerTextBody.ChildEntities.Remove(table);
        //Save a Word document to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing. 
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
    }
}
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}

## Find all items by property

Using FindAllItemsByProperty API, find all the items in the Word document that has the specified property name and value.

The following code example illustrates how to find all the items in Word document based on one property.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load an existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    //Find all footnote and endnote by EntityType in Word document.
    List<Entity> footNotes = document.FindAllItemsByProperty(EntityType.Footnote, null, null);
    //Remove the footnotes and endnotes.
    for (int i = 0; i < footNotes.Count; i++)
    {
        WFootnote footnote = footNotes[i] as WFootnote;
        footnote.OwnerParagraph.ChildEntities.Remove(footnote);
    }

    //Find all fields by FieldType.
    List<Entity> fields = document.FindAllItemsByProperty(EntityType.Field, "FieldType",FieldType.FieldHyperlink.ToString());
    //Iterate the hyperlink field and change URL.
    for (int i = 0; i < fields.Count; i++)
    {
        //Creates hyperlink instance from field to manipulate the hyperlink.
        Hyperlink hyperlink = new Hyperlink(fields[i] as WField);
        //Modifies the Uri of the hyperlink.
        if (hyperlink.Type == HyperlinkType.WebLink && hyperlink.TextToDisplay == "HTML")
            hyperlink.Uri = "http://www.w3schools.com/";
    }
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
    'Find all footnote and endnote by EntityType in Word document.
    Dim footNotes As List(Of Entity) = document.FindAllItemsByProperty(EntityType.Footnote, Nothing, Nothing)
    'Remove the footnotes and endnotes.
    For i = 0 To footNotes.Count - 1
        Dim footnote As WFootnote = TryCast(footNotes(i), WFootnote)
        footnote.OwnerParagraph.ChildEntities.Remove(footnote)
    Next

    'Find all fields by FieldType.
    Dim fields As List(Of Entity) = document.FindAllItemsByProperty(EntityType.Field, "FieldType", FieldType.FieldHyperlink.ToString())
    'Iterate the hyperlink field and change URL.
    For i = 0 To fields.Count - 1
        'Creates hyperlink instance from field to manipulate the hyperlink.
        Dim hyperlink As Hyperlink = New Hyperlink(TryCast(fields(i), WField))
        'Modifies the Uri of the hyperlink.
        If hyperlink.Type Is HyperlinkType.WebLink AndAlso hyperlink.TextToDisplay Is "HTML" Then hyperlink.Uri = "http://www.w3schools.com/"
    Next
    'Save a Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Find all footnote and endnote by EntityType in Word document.
        List<Entity> footNotes = document.FindAllItemsByProperty(EntityType.Footnote, null, null);
        //Remove the footnotes and endnotes.
        for (int i = 0; i < footNotes.Count; i++)
        {
            WFootnote footnote = footNotes[i] as WFootnote;
            footnote.OwnerParagraph.ChildEntities.Remove(footnote);
        }

        //Find all fields by FieldType.
        List<Entity> fields = document.FindAllItemsByProperty(EntityType.Field, "FieldType",FieldType.FieldHyperlink.ToString());
        //Iterate the hyperlink field and change URL.
        for (int i = 0; i < fields.Count; i++)
        {
            //Creates hyperlink instance from field to manipulate the hyperlink.
            Hyperlink hyperlink = new Hyperlink(fields[i] as WField);
            //Modifies the Uri of the hyperlink.
            if (hyperlink.Type == HyperlinkType.WebLink && hyperlink.TextToDisplay == "HTML")
                hyperlink.Uri = "http://www.w3schools.com/";
        }
        //Save a Word document to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx"); 
    }
}
//Refer to the following link to save a Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as a Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Find all footnote and endnote by EntityType in Word document.
        List<Entity> footNotes = document.FindAllItemsByProperty(EntityType.Footnote, null, null);
        //Remove the footnotes and endnotes.
        for (int i = 0; i < footNotes.Count; i++)
        {
            WFootnote footnote = footNotes[i] as WFootnote;
            footnote.OwnerParagraph.ChildEntities.Remove(footnote);
        }

        //Find all fields by FieldType.
        List<Entity> fields = document.FindAllItemsByProperty(EntityType.Field, "FieldType",FieldType.FieldHyperlink.ToString());
        //Iterate the hyperlink field and change URL.
        for (int i = 0; i < fields.Count; i++)
        {
            //Creates hyperlink instance from field to manipulate the hyperlink.
            Hyperlink hyperlink = new Hyperlink(fields[i] as WField);
            //Modifies the Uri of the hyperlink.
            if (hyperlink.Type == HyperlinkType.WebLink && hyperlink.TextToDisplay == "HTML")
                hyperlink.Uri = "http://www.w3schools.com/";
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
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Find all footnote and endnote by EntityType in Word document.
        List<Entity> footNotes = document.FindAllItemsByProperty(EntityType.Footnote, null, null);
        //Remove the footnotes and endnotes.
        for (int i = 0; i < footNotes.Count; i++)
        {
            WFootnote footnote = footNotes[i] as WFootnote;
            footnote.OwnerParagraph.ChildEntities.Remove(footnote);
        }

        //Find all fields by FieldType.
        List<Entity> fields = document.FindAllItemsByProperty(EntityType.Field, "FieldType",FieldType.FieldHyperlink.ToString());
        //Iterate the hyperlink field and change URL.
        for (int i = 0; i < fields.Count; i++)
        {
            //Creates hyperlink instance from field to manipulate the hyperlink.
            Hyperlink hyperlink = new Hyperlink(fields[i] as WField);
            //Modifies the Uri of the hyperlink.
            if (hyperlink.Type == HyperlinkType.WebLink && hyperlink.TextToDisplay == "HTML")
                hyperlink.Uri = "http://www.w3schools.com/";
        }
        //Save a Word document to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing. 
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
    }
}
//Download the helper files from the following link to save the stream as file and open the file for viewing in the Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}

## Find all items by properties

Using FindAllItemsByProperties API, find all the items in the Word document based on multiple property names and their corresponding values.

The following code example illustrates how to find all the items in Word document based on multiple property names and their corresponding values.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load an existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    string[] propertyNames = { "ContentControlProperties.Title", "ContentControlProperties.Tag" };
    string[] propertyValues = { "CompanyName", "CompanyName" };

    //Find all block content controls by Title and Tag.
    List<Entity> blockContentControls = document.FindAllItemsByProperties(EntityType.BlockContentControl,propertyNames,propertyValues);

    //Iterate the block content controls and remove the block content controls.
    for (int i = 0; i < blockContentControls.Count; i++)
    {
        BlockContentControl blockContentControl = blockContentControls[i] as BlockContentControl;
        blockContentControl.OwnerTextBody.ChildEntities.Remove(blockContentControl);
    }

    propertyNames = new string[] { "ContentControlProperties.Title", "ContentControlProperties.Tag" };
    propertyValues = new string[] { "Contact", "Contact" };

    //Find all the inline content controls by Title and Tag. 
    List<Entity> inlineContentControls = document.FindAllItemsByProperties(EntityType.InlineContentControl,propertyNames,propertyValues);

    //Iterate the inline content controls and remove the inline content controls.
    for (int i = 0; i < inlineContentControls.Count; i++)
    {
        InlineContentControl inlineContentControl = inlineContentControls[i] as InlineContentControl;
        inlineContentControl.OwnerParagraph.ChildEntities.Remove(inlineContentControl);
    }

    propertyNames = new string[] { "CharacterFormat.Bold", "CharacterFormat.Italic" };
    propertyValues = new string[] { true.ToString(), true.ToString() };

    //Find all the bold and italic text.
    List<Entity> textRanges = document.FindAllItemsByProperties(EntityType.TextRange,propertyNames,propertyValues);

    //Iterate the textRanges and remove the bold and italic.
    for (int i = 0; i < textRanges.Count; i++)
    {
        WTextRange textRange = textRanges[i] as WTextRange;
        textRange.CharacterFormat.Bold = false;
        textRange.CharacterFormat.Italic= false;
    }
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
    Dim propertyNames = {"ContentControlProperties.Title", "ContentControlProperties.Tag"}
    Dim propertyValues = {"CompanyName", "CompanyName"}

    'Find all block content controls by Title and Tag. 
    Dim blockContentControls As List(Of Entity) = document.FindAllItemsByProperties(EntityType.BlockContentControl, propertyNames, propertyValues)

    'Iterate the block content controls and remove the block content controls.
    For i = 0 To blockContentControls.Count - 1
        Dim blockContentControl As BlockContentControl = TryCast(blockContentControls(i), BlockContentControl)
        blockContentControl.OwnerTextBody.ChildEntities.Remove(blockContentControl)
    Next

    propertyNames = New String() {"ContentControlProperties.Title", "ContentControlProperties.Tag"}
    propertyValues = New String() {"Contact", "Contact"}

    'Find all inline content controls by Title and Tag. 
    Dim inlineContentControls As List(Of Entity) = document.FindAllItemsByProperties(EntityType.InlineContentControl, propertyNames, propertyValues)

    'Iterate the inline content controls and remove the inline content controls.
    For i = 0 To inlineContentControls.Count - 1
        Dim inlineContentControl As InlineContentControl = TryCast(inlineContentControls(i), InlineContentControl)
        inlineContentControl.OwnerParagraph.ChildEntities.Remove(inlineContentControl)
    Next

    propertyNames = New String() {"CharacterFormat.Bold", "CharacterFormat.Italic"}
    propertyValues = New String() {True.ToString(), True.ToString()}

    'Find all the bold and italic text.
    Dim textRanges As List(Of Entity) = document.FindAllItemsByProperties(EntityType.TextRange, propertyNames, propertyValues)

    'Iterate the textRanges and remove the bold and italic
    For i = 0 To textRanges.Count - 1
        Dim textRange As WTextRange = TryCast(textRanges(i), WTextRange)
        textRange.CharacterFormat.Bold = False
        textRange.CharacterFormat.Italic = False
    Next
    'Save a Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        string[] propertyNames = { "ContentControlProperties.Title", "ContentControlProperties.Tag" };
        string[] propertyValues = { "CompanyName", "CompanyName" };

        //Find all block content controls by Title and Tag. 
        List<Entity> blockContentControls = document.FindAllItemsByProperties(EntityType.BlockContentControl,propertyNames,propertyValues);

        //Iterate the block content controls and remove the block content controls.
        for (int i = 0; i < blockContentControls.Count; i++)
        {
            BlockContentControl blockContentControl = blockContentControls[i] as BlockContentControl;
            blockContentControl.OwnerTextBody.ChildEntities.Remove(blockContentControl);
        }

        propertyNames = new string[] { "ContentControlProperties.Title", "ContentControlProperties.Tag" };
        propertyValues = new string[] { "Contact", "Contact" };

        //Find all the inline content controls by Title and Tag. 
        List<Entity> inlineContentControls = document.FindAllItemsByProperties(EntityType.InlineContentControl,propertyNames,propertyValues);

        //Iterate the inline content controls and remove the inline content controls.
        for (int i = 0; i < inlineContentControls.Count; i++)
        {
            InlineContentControl inlineContentControl = inlineContentControls[i] as InlineContentControl;
            inlineContentControl.OwnerParagraph.ChildEntities.Remove(inlineContentControl);
        }

        propertyNames = new string[] { "CharacterFormat.Bold", "CharacterFormat.Italic" };
        propertyValues = new string[] { true.ToString(), true.ToString() };

        //Find all the bold and italic text.
        List<Entity> textRanges = document.FindAllItemsByProperties(EntityType.TextRange,propertyNames,propertyValues);

        //Iterate the textRanges and remove the bold and italic
        for (int i = 0; i < textRanges.Count; i++)
        {
            WTextRange textRange = textRanges[i] as WTextRange;
            textRange.CharacterFormat.Bold = false;
            textRange.CharacterFormat.Italic= false;
        }
        //Save a Word document to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx"); 
    }
}
//Refer to the following link to save a Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as a Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        string[] propertyNames = { "ContentControlProperties.Title", "ContentControlProperties.Tag" };
        string[] propertyValues = { "CompanyName", "CompanyName" };

        //Find all block content controls by Title and Tag. 
        List<Entity> blockContentControls = document.FindAllItemsByProperties(EntityType.BlockContentControl,propertyNames,propertyValues);

        //Iterate the block content controls and remove the block content controls.
        for (int i = 0; i < blockContentControls.Count; i++)
        {
            BlockContentControl blockContentControl = blockContentControls[i] as BlockContentControl;
            blockContentControl.OwnerTextBody.ChildEntities.Remove(blockContentControl);
        }

        propertyNames = new string[] { "ContentControlProperties.Title", "ContentControlProperties.Tag" };
        propertyValues = new string[] { "Contact", "Contact" };

        //Find all the inline content controls by Title and Tag. 
        List<Entity> inlineContentControls = document.FindAllItemsByProperties(EntityType.InlineContentControl,propertyNames,propertyValues);

        //Iterate the inline content controls and remove the inline content controls.
        for (int i = 0; i < inlineContentControls.Count; i++)
        {
            InlineContentControl inlineContentControl = inlineContentControls[i] as InlineContentControl;
            inlineContentControl.OwnerParagraph.ChildEntities.Remove(inlineContentControl);
        }

        propertyNames = new string[] { "CharacterFormat.Bold", "CharacterFormat.Italic" };
        propertyValues = new string[] { true.ToString(), true.ToString() };

        //Find all the bold and italic text.
        List<Entity> textRanges = document.FindAllItemsByProperties(EntityType.TextRange,propertyNames,propertyValues);

        //Iterate the textRanges and remove the bold and italic.
        for (int i = 0; i < textRanges.Count; i++)
        {
            WTextRange textRange = textRanges[i] as WTextRange;
            textRange.CharacterFormat.Bold = false;
            textRange.CharacterFormat.Italic= false;
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
//Open the file as a Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        string[] propertyNames = { "ContentControlProperties.Title", "ContentControlProperties.Tag" };
        string[] propertyValues = { "CompanyName", "CompanyName" };

        //Find all the block content controls by Title and Tag. 
        List<Entity> blockContentControls = document.FindAllItemsByProperties(EntityType.BlockContentControl,propertyNames,propertyValues);

        //Iterate the block content controls and remove the block content controls.
        for (int i = 0; i < blockContentControls.Count; i++)
        {
            BlockContentControl blockContentControl = blockContentControls[i] as BlockContentControl;
            blockContentControl.OwnerTextBody.ChildEntities.Remove(blockContentControl);
        }

        propertyNames = new string[] { "ContentControlProperties.Title", "ContentControlProperties.Tag" };
        propertyValues = new string[] { "Contact", "Contact" };

        //Find all the inline content controls by Title and Tag. 
        List<Entity> inlineContentControls = document.FindAllItemsByProperties(EntityType.InlineContentControl,propertyNames,propertyValues);

        //Iterate the inline content controls and remove the inline content controls.
        for (int i = 0; i < inlineContentControls.Count; i++)
        {
            InlineContentControl inlineContentControl = inlineContentControls[i] as InlineContentControl;
            inlineContentControl.OwnerParagraph.ChildEntities.Remove(inlineContentControl);
        }

        propertyNames = new string[] { "CharacterFormat.Bold", "CharacterFormat.Italic" };
        propertyValues = new string[] { true.ToString(), true.ToString() };

        //Find all the bold and italic text.
        List<Entity> textRanges = document.FindAllItemsByProperties(EntityType.TextRange,propertyNames,propertyValues);

        //Iterate the textRanges and remove the bold and italic.
        for (int i = 0; i < textRanges.Count; i++)
        {
            WTextRange textRange = textRanges[i] as WTextRange;
            textRange.CharacterFormat.Bold = false;
            textRange.CharacterFormat.Italic= false;
        }
        //Save a Word document to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing. 
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
    }
}
//Download the helper files from the following link to save the stream as file and open the file for viewing in the Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}

T> Passing null for both the property names and property values in the above APIs, you can also find an item in a Word document without relying on any property.