---
title: Working with Silverlight
description: Creating a Silverlight application and load the document
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Silverlight 

## Loading the document 

The following code example illustrates how to load the file by using URI in Silverlight.

{% tabs %}

{% highlight c# %}

//Load the file as url

Uri uri = new Uri(@"\Resources\data\Sample.docx", UriKind.Relative);

Stream docStream = ResourceManager.Load(uri);

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Loads or opens an existing word document through open method of WordDocument class

document.Open(docStream, FormatType.Docx);

MemoryStream stream = new MemoryStream();

//Save the document 

document.SaveAsDocx();

//close the document

document.Close();

public static class Extensions

{

public static void SaveAsDoc(this WordDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

Filter = "Doc files (*.doc)|*.doc",

DefaultExt = ".doc",

FilterIndex = 1

};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream, FormatType.Doc);

}

}       
    
}

public static void SaveAsDocx(this WordDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

Filter = "Docx files (*.docx)|*.docx",

DefaultExt = ".docx",
				
FilterIndex = 1
				
};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream, FormatType.Docx);

}

}

}

}

{% endhighlight %}

{% highlight vb.net %}

'Load the file as url

Dim uri As New Uri("\Resources\data\Sample.docx", UriKind.Relative)

Dim docStream As Stream = ResourceManager.Load(uri)

'Creates an empty Word document instance

Dim document As New WordDocument()

'Loads or opens an existing word document through open method of WordDocument class

document.Open(docStream, FormatType.Docx)

Dim stream As New MemoryStream()

'Save the document into memory stream

document.SaveAsDocx()

'close the document

document.Close()

Public Module  Extensions
	
<System.Runtime.CompilerServices.Extension> _
	
Public Sub SaveAsDoc(ByVal document As WordDocument)

Dim sfd As New SaveFileDialog() With {  .Filter = "Doc files (*.doc)|*.doc",  .DefaultExt = ".doc", .FilterIndex = 1 }

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream, FormatType.Doc)

End Using

End If

End Sub

<System.Runtime.CompilerServices.Extension> _

Public Sub SaveAsDocx(ByVal document As WordDocument)

Dim sfd As New SaveFileDialog() With {  .Filter = "Docx files (*.docx)|*.docx",  .DefaultExt = ".docx",  .FilterIndex = 1 }

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream, FormatType.Docx)

End Using

End If

End Sub

End Module 

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to load the file by using stream in Silverlight.

{% tabs %}

{% highlight c# %}

//Load the file as stream

Stream docStream = Assembly.GetExecutingAssembly().GetManifestResourceStream("sample.Resources.Data.sample.docx");

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Loads or opens an existing word document through open method of WordDocument class

document.Open(docStream, FormatType.Docx);

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

document.SaveAsDocx();

//close the document

document.Close();

public static class Extensions

{

public static void SaveAsDoc(this WordDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

Filter = "Doc files (*.doc)|*.doc",

DefaultExt = ".doc",

FilterIndex = 1

};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream, FormatType.Doc);

}

}       
    
}

public static void SaveAsDocx(this WordDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

Filter = "Docx files (*.docx)|*.docx",

DefaultExt = ".docx",
				
FilterIndex = 1
				
};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream, FormatType.Docx);

}

}

}

}

{% endhighlight %}

{% highlight vb.net %}

'Load the file as stream

Dim docStream As Stream = System.Reflection.Assembly.GetExecutingAssembly().GetManifestResourceStream("sample.Resources.Data.sample.docx")

'Creates an empty Word document instance

Dim document As New WordDocument()

'Loads or opens an existing word document through open method of WordDocument class

document.Open(docStream, FormatType.Docx)

Dim stream As New MemoryStream()

'Save the document into memory stream

document.SaveAsDocx()

'close the document

document.Close()

Public Module  Extensions
	
<System.Runtime.CompilerServices.Extension> _
	
Public Sub SaveAsDoc(ByVal document As WordDocument)

Dim sfd As New SaveFileDialog() With {  .Filter = "Doc files (*.doc)|*.doc",  .DefaultExt = ".doc", .FilterIndex = 1 }

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream, FormatType.Doc)

End Using

End If

End Sub

<System.Runtime.CompilerServices.Extension> _

Public Sub SaveAsDocx(ByVal document As WordDocument)

Dim sfd As New SaveFileDialog() With {  .Filter = "Docx files (*.docx)|*.docx",  .DefaultExt = ".docx",  .FilterIndex = 1 }

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream, FormatType.Docx)

End Using

End If

End Sub

End Module

{% endhighlight %}

{% endtabs %}

## Save the document 

The following code example illustrates how to save the PDF document in Silverlight.

{% tabs %}

{% highlight c# %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save the document

document.SaveAsDocx();

//close the document

document.Close();

public static class Extensions

{

public static void SaveAsDoc(this WordDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

Filter = "Doc files (*.doc)|*.doc",

DefaultExt = ".doc",

FilterIndex = 1

};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream, FormatType.Doc);

}

}       
    
}

public static void SaveAsDocx(this WordDocument document)

{

SaveFileDialog sfd = new SaveFileDialog()

{

Filter = "Docx files (*.docx)|*.docx",

DefaultExt = ".docx",
				
FilterIndex = 1
				
};

if (sfd.ShowDialog() == true)

{

using (Stream stream = sfd.OpenFile())

{

document.Save(stream, FormatType.Docx);

}

}

}

}

{% endhighlight %}

{% highlight vb.net %}
VB:

'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

'Save the document

document.SaveAsDocx()

'close the document

document.Close()

Public Module  Extensions
	
<System.Runtime.CompilerServices.Extension> _
	
Public Sub SaveAsDoc(ByVal document As WordDocument)

Dim sfd As New SaveFileDialog() With {  .Filter = "Doc files (*.doc)|*.doc",  .DefaultExt = ".doc", .FilterIndex = 1 }

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream, FormatType.Doc)

End Using

End If

End Sub

<System.Runtime.CompilerServices.Extension> _

Public Sub SaveAsDocx(ByVal document As WordDocument)

Dim sfd As New SaveFileDialog() With {  .Filter = "Docx files (*.docx)|*.docx",  .DefaultExt = ".docx",  .FilterIndex = 1 }

If sfd.ShowDialog() = True Then

Using stream As Stream = sfd.OpenFile()

document.Save(stream, FormatType.Docx)

End Using

End If

End Sub

End Module

{% endhighlight %}

{% endtabs %}