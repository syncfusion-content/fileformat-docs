---
title: Custom XML Support in Syncfusion .NET Excel Library
description: In this section, you can learn how to create or edit Custom XML in Excel document using Syncfusion .NET Excel library
platform: file-formats
control: XlsIO
documentation: UG
---
# Custom XML Support in Syncfusion Excel Library

When you embed XML data in a document, the data is named as custom XML part, which is used to store arbitrary XML data in the workbook. 

Essential XlsIO supports the following functionalities with Custom XML:

* Adding CustomXmlPart to workbook
* Reading CustomXmlPart from workbook 

**Add** **Custom** **XML** 

Adding Custom XML part to workbook is achieved by using the [Add](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ICustomXmlPartCollection.html#Syncfusion_XlsIO_ICustomXmlPartCollection_Add_Syncfusion_XlsIO_ICustomXmlPart_) method of [ICustomXmlPartCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ICustomXmlPartCollection.html) interface. 

The following code snippet illustrates on how to add a Custom XML part.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding CustomXmlData to Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.Add("SD10003");

  //Add XmlData to CustomXmlPart
  byte[] xmlData = File.ReadAllBytes("Test.xml");
  customXmlPart.Data = xmlData;

  //Saving the workbook as stream
  FileStream stream = new FileStream("CustomXml.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding CustomXmlData to Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.Add("SD10003");

  //Add XmlData to CustomXmlPart
  byte[] xmlData = File.ReadAllBytes("Test.xml");
  customXmlPart.Data = xmlData;

  workbook.SaveAs("CustomXml.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Adding CustomXmlData to Workbook
  Dim customXmlPart As ICustomXmlPart = workbook.CustomXmlparts.Add("SD10003")

  'Add XmlData to CustomXmlPart
  Dim xmlData() As Byte = File.ReadAllBytes("Test.xml")
  customXmlPart.Data = xmlData

  workbook.SaveAs("CustomXml.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to add custom XML in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Custom%20XML%20Support/Add%20Custom%20XML). 

**Read** **Custom** **XML** 

Reading Custom XML part from workbook is achieved by using the [GetById](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ICustomXmlPartCollection.html#Syncfusion_XlsIO_ICustomXmlPartCollection_GetById_System_String_) method of [ICustomXmlPartCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ICustomXmlPartCollection.html) interface. The following code snippet illustrates on how to read Custom XML parts from workbook.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("CustomXml.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Access CustomXmlPart from Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.GetById("SD10003");

  //Access XmlData from CustomXmlPart
  byte[] xmlData = customXmlPart.Data;
  System.Text.Encoding.Default.GetString(xmlData);

  //Saving the workbook as stream
  FileStream stream = new FileStream("CustomXml1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("CustomXml.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Access CustomXmlPart from Workbook
  ICustomXmlPart customXmlPart = workbook.CustomXmlparts.GetById("SD10003");

  //Access XmlData from CustomXmlPart
  byte[] xmlData = customXmlPart.Data;
  System.Text.Encoding.Default.GetString(xmlData);

  workbook.SaveAs("CustomXml.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("CustomXml.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Access CustomXmlPart from Workbook
  Dim customXmlPart As ICustomXmlPart = workbook.CustomXmlparts.GetById("SD10003")

  'Access XmlData from CustomXmlPart
  Dim xmlData As Byte() = customXmlPart.Data
  System.Text.Encoding.Default.GetString(xmlData)

  workbook.SaveAs("CustomXml.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

A complete working example to read custom XML in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Custom%20XML%20Support/Read%20Custom%20XML). 

N> Custom XML cannot be modified when the file is saved in Excel 97-2003 (\*.xls) format.
N> Custom XML can be created and modified when the file is saved in Excel 2007 and later versions (\*.xlsx).

