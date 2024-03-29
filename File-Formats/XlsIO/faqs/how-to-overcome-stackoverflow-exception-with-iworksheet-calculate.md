---
title: Avoid StackOverflow exception with IWorksheet Calculate() |Syncfusion
description: This page shows how to overcome StackOverflow exception while calling Calculate method of IWorksheet using XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# How to overcome StackOverflow exception with IWorksheet's Calculate()?

StackOverflow exception occurs when the number of **IterationMaxCount**, **MaximumRecursiveCalls** and **MaxStackDepth** exceeds in the [CalcEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_CalcEngine). To avoid this StackOverflow exception while computing the formulas iteratively exceeding the maximum capacity, you need to set the values for these properties before calling the [Calculate](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_Calculate) method of [IWorksheet](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html) interface.

The following code snippet explains this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
worksheet.EnableSheetCalculations(); 
worksheet.CalcEngine.UseFormulaValues = true; 
worksheet.CalcEngine.MaximumRecursiveCalls = 10000; 
worksheet.CalcEngine.IterationMaxCount = 10000; 
CalcEngine.MaxStackDepth = 10000; 
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
worksheet.EnableSheetCalculations(); 
worksheet.CalcEngine.UseFormulaValues = true; 
worksheet.CalcEngine.MaximumRecursiveCalls = 10000; 
worksheet.CalcEngine.IterationMaxCount = 10000; 
CalcEngine.MaxStackDepth = 10000; 
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
worksheet.EnableSheetCalculations()
worksheet.CalcEngine.UseFormulaValues = True
worksheet.CalcEngine.MaximumRecursiveCalls = 10000
worksheet.CalcEngine.IterationMaxCount = 10000
CalcEngine.MaxStackDepth = 10000
{% endhighlight %}
{% endtabs %}

## See Also

* [How to overcome UnauthorizedAccessException?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-overcome-unauthorizedaccessexception)
* [How to avoid exception when adding worksheets with same name?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-avoid-exception-when-adding-worksheets-with-same-name)
* [What are the known exceptions of XlsIO?](https://help.syncfusion.com/file-formats/xlsio/known-exceptions)
* [What is Calculation Engine?](https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#calculation-engine)
* [What are Calculate Options?](https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#calculate-options)
