---
title: Find item in Word document | DocIO | Syncfusion
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
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
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
        //Save a Word document to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx"); 
    }
}
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
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
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
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
        //Save a Word document to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx"); 
    }
}
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
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
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
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
        //Save a Word document to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx"); 
    }
}
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
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

## Find all items by properties

Using FindAllItemsByProperties API, find all the items in the Word document based on multiple property names and their corresponding values.

The following code example illustrates how to find all the items in Word document based on multiple property names and their corresponding values.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load an existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
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
        //Save a Word document to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx"); 
    }
}
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
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

T> Passing null for both the property names and property values in above APIs, you can also find an item in a Word document without relying on any property.

T> If you wish to find an item in Word document rather than iterating through each element one by one, you can use finding the item functionality to achieve it.