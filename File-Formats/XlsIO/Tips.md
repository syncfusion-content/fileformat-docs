---
title: Tips
description: Explains tips for efficient usage of XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Tips

T> This section gives you a necessary tips for efficient usage of Essential XlsIO. Following tips are most commonly used in XlsIO.

**How** **to** **apply** **same** **styles** **to** **entire** **rows** **or** **columns****?**

You can use [default styles](/file-formats/xlsio/working-with-cell-or-range-formatting#set-default-style-for-rowcolumn), to apply styles for a whole column instead of applying in each cell.

**How** **to** **assign** **a** **value** **to** **a** **range** **without** **know** **their** **types****?**

You can use **Value** and **Value2** property only when the data type is unknown. Value/Value2 property checks the data type of the given string and hence this consumes time. Following points to be remembered while working with Value and Value2

* If you have an object, and independent of its type, use Value2.
* If you have a string that can have different data types and do not want to parse it, use Value property.
* When you know the exact data (value of cell) type, use typed properties.

LINK- API reference to the Value and Value2

**How** **to** **set** **a** **Text****/****Number** **to** **a** **range** **without** **accessing** **its** **range****?**

You can use of **GetText**, **SetText**, **GetNumber** and **SetNumber** methods from worksheet object that enable users to get/set values without range object. LINK – API reference to these method.

**How** **to** **work** **with** **multiple** **worksheet** **in** **XlsIO** **efficiently****?**

If the workbook contains multiple worksheet, then the parsing of the workbook will consume time. You can use **ExcelParseOptions****.****ParseWorksheetsOnDemand** in IWorkbooks.Open method which parses the worksheet only when their accessed. This option can be used in a scenario where workbook contains multiple worksheets but you are going to use few worksheets among them.

{% tabs %}  

{% highlight c# %}
IWorkbook workbook = application.Workbooks.Open(fileName,ExcelParseOptions.ParseWorksheetsOnDemand);



{% endhighlight %}

{% highlight vb %}
Dim workbook As IWorkbook = application.Workbooks.Open(fileName, ExcelParseOptions.ParseWorksheetsOnDemand)



{% endhighlight %}

  {% endtabs %}  

**How** **to** **improve** **the** **performance** **of** **Value2** **property** **in** **IRange****?** 

You can set **IWorkbook**.**DetectDateTimeInValue** property as ‘false’ with Value2 property, if you are sure that the given value is not of DateTime data type which improves time performance. 

{% tabs %}  

{% highlight c# %}
workbook.DetectDateTimeInValue = false;



{% endhighlight %}

{% highlight vb %}
workbook.DetectDateTimeInValue = False



{% endhighlight %}

  {% endtabs %}  

**How** **to** **optimizes** **excel** **parsing** **in** **XlsIO****?**

Files parsing can be optimized by setting **IApplication****.****UseFastRecordParsing** = **false** or **true** (true –fast mode, but less error checks and false – slower but more reliable).

{% tabs %}  

{% highlight c# %}
application.UseFastRecordParsing = true;



{% endhighlight %}

{% highlight vb %}
application.UseFastRecordParsing = True



{% endhighlight %}

  {% endtabs %}  

**How** **to** **retrieve** **or** **delete** **rows** **and** **columns** **efficiently****?**

To extract values little faster or to delete a larger number of rows and columns, use Un-Safe code option of **IApplication** interface as follows

{% tabs %}  

{% highlight c# %}
application.DataProviderType = ExcelDataProviderType.Unsafe;



{% endhighlight %}

{% highlight vb %}
application.DataProviderType = ExcelDataProviderType.Unsafe



{% endhighlight %}

  {% endtabs %}  

**How** **to** **reduce** **the** **size** **of** **the** **generated** **excel** **file** **in** **XlsIO****?**

You can use CompressionLevel to reduce the size of the file. LINK- Reference to compression level section.

**How** **to** **prevent** **the** **data** **loss** **while** **unfortunately** **closing** **the** **workbook** **or** **disposing** **excel** **engine** **without** **saving** **contents****?**

You can use ThrowNotSavedOnDestroy property of ExcelEngine object in this scenario. If it is set to true, then ExcelWorkbookNotSavedException will be thrown when you forgot to save the workbook before closing them. Following code illustrates how to set ThrowNotSavedOnDestroy property of ExcelEngine object.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

excelEngine.ThrowNotSavedOnDestroy = true;



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

excelEngine.ThrowNotSavedOnDestroy = True



{% endhighlight %}

  {% endtabs %}  

## Filling large data using IMigrantRange

The **IMigrantRange** interface can be used to access and manipulate worksheet range. This is an optimal method of writing values with better memory performance. 

The following code example illustrates how the **IMigrantRange** is accessed.

{% tabs %}  

{% highlight c# %}
IMigrantRange migrantRange = workbook.Worksheets[0].MigrantRange; 

// Writing Data.
for (int row = 1; row <= rowCount; row++)
{
for (int column = 1; column <= colCount; column++)
{
// Writing values.

migrantRange.ResetRowColumn(row, column);

// Setting value of this migrant range which is similar to IRange object.

migrantRange.Value = "Syncfusion";        

}
}



{% endhighlight %}

{% highlight vb %}
'Writing Data.
Dim row As Integer 
Dim migrantRange As IMigrantRange = workbook.Worksheets(0).MigrantRange
For row = 1 To rowCount Step row + 1
Dim column As Integer
For column = 1 To colCount Step column + 1 
'Writing values.
migrantRange.ResetRowColumn(row, column)

' Setting value of this migrant range which is similar to IRange object.

migrantRange.Value = "Syncfusion"

Next
Next



{% endhighlight %}

  {% endtabs %}  

**IMigrantRange** provides us a SetValue method in which different value for the range can be assigned. Following code snippet illustrates regarding this.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

excelEngine.Excel.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = excelEngine.Excel.Workbooks.Create();

IWorksheet sheet = workbook.Worksheets[0];

IMigrantRange migrantRange = workbook.Worksheets[0].MigrantRange;

// Writing values.

migrantRange.ResetRowColumn(1, 1);

//Setting boolean value

migrantRange.SetValue(true);

migrantRange.ResetRowColumn(1, 2);

//Setting DateTime value

migrantRange.SetValue(DateTime.Now);

migrantRange.ResetRowColumn(1, 3);

//Setting double value

migrantRange.SetValue(5.5);

migrantRange.ResetRowColumn(1, 4);

//Setting int value

migrantRange.SetValue(5);

migrantRange.ResetRowColumn(1, 5);

//Setting string value

migrantRange.SetValue("Syncfusion");

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("MigirantRange.xlsx");

workbook.Close();

excelEngine.Dispose();            



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

excelEngine.Excel.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Create()

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim migrantRange As IMigrantRange = workbook.Worksheets(0).MigrantRange

' Writing values.

migrantRange.ResetRowColumn(1, 1)

'Setting boolean value

migrantRange.SetValue(True)

migrantRange.ResetRowColumn(1, 2)

'Setting DateTime value

migrantRange.SetValue(DateTime.Now)

migrantRange.ResetRowColumn(1, 3)

'Setting double value

migrantRange.SetValue(5.5)

migrantRange.ResetRowColumn(1, 4)

'Setting int value

migrantRange.SetValue(5)

migrantRange.ResetRowColumn(1, 5)

'Setting string value

migrantRange.SetValue("Syncfusion")

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("MigirantRange.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

