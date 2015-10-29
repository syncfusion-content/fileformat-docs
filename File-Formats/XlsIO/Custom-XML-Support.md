---
title: Custom XML Support
description: Briefs about Custom XML Support in XlsIO
platform: File-Formats
control: XlsIO
documentation: UG
---
# Custom XML Support

When you embed XML data in a document, the data is named as custom XML part which are used to store arbitrary xml data in the workbook. 

Essential XlsIO supports the following functionalities with Custom XML such as,

* Adding CustomXmlPart to workbook
* Reading CustomXmlPart from workbook 

**Add** **Custom** **XML** 

Adding Custom XML part to workbook is achieved by using **Add** method of **ICustomXmlPart** interface. 

The following code snippet illustrates on how to add a Custom XML part.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

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

workbook.Close();

excelEngine.Dipose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Adding CustomXmlData to Workbook

Dim customXmlPart As ICustomXmlPart = workbook.CustomXmlparts.Add("SD10003")

'Add XmlData to CustomXmlPart

Dim xmlData() As Byte = File.ReadAllBytes("Test.xml")

customXmlPart.Data = xmlData

workbook.SaveAs("CustomXml.xlsx");

workbook.Close()

excelEngine.Dipose()



{% endhighlight %}

  {% endtabs %}  

**Read** **Custom** **XML** 

Reading Custom XML part from workbook is achieved by using **GetById** method of **ICustomXmlPart** interface. The following code snippet illustrates on how to read Custom XML parts from workbook.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

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

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("CustomXml.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Access CustomXmlPart from Workbook

Dim customXmlPart As ICustomXmlPart = workbook.CustomXmlparts.GetById("SD10003")

'Access XmlData from CustomXmlPart

Dim xmlData As Byte() = customXmlPart.Data

System.Text.Encoding.[Default].GetString(xmlData)

workbook.SaveAs("CustomXml.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

I> Custom Xml cannot be modified when the file is saved in Excel 97-2003 (*.xls) format.

I> Custom Xml can be created and modified when the file is saved in Excel 2007 and later versions (*.xlsx).

