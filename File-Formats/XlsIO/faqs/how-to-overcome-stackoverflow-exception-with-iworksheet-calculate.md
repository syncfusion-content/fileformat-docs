---
title: FAQ Section| XlsIO | Syncfusion
description: This page shows how to overcome StackOverflow exception while calling Calculate method of IWorksheet using XlsIO.
platform: File-formats
control: XlsIO
documentation: UG
---

# How to overcome StackOverflow exception with IWorksheet's Calculate()?

StackOverflow exception occurs when the number of <i>IterationMaxCount</i>, <i>MaximumRecursiveCalls</i> and <i>MaxStackDepth</i> exceeds in the `CalcEngine`. To avoid this StackOverflow exception while computing the formulas iteratively exceeding the maximum capacity, you need to set the values for these properties before calling the <b>Calculate</b> method of <b>IWorksheet</b> interface.

The following code snippet explains this.

{% tabs %}
{% highlight C# %}
worksheet.EnableSheetCalculations(); 
worksheet.CalcEngine.UseFormulaValues = true; 
worksheet.CalcEngine.MaximumRecursiveCalls = 10000; 
worksheet.CalcEngine.IterationMaxCount = 10000; 
CalcEngine.MaxStackDepth = 10000; 
{% endhighlight %}

{% highlight vb %}
worksheet.EnableSheetCalculations()
worksheet.CalcEngine.UseFormulaValues = True
worksheet.CalcEngine.MaximumRecursiveCalls = 10000
worksheet.CalcEngine.IterationMaxCount = 10000
CalcEngine.MaxStackDepth = 10000
{% endhighlight %}

{% highlight UWP %}
worksheet.EnableSheetCalculations(); 
worksheet.CalcEngine.UseFormulaValues = true; 
worksheet.CalcEngine.MaximumRecursiveCalls = 10000; 
worksheet.CalcEngine.IterationMaxCount = 10000; 
CalcEngine.MaxStackDepth = 10000; 
{% endhighlight %}

{% highlight ASP.NET Core %}
worksheet.EnableSheetCalculations(); 
worksheet.CalcEngine.UseFormulaValues = true; 
worksheet.CalcEngine.MaximumRecursiveCalls = 10000; 
worksheet.CalcEngine.IterationMaxCount = 10000; 
CalcEngine.MaxStackDepth = 10000; 
{% endhighlight %}

{% highlight Xamarin %}
worksheet.EnableSheetCalculations(); 
worksheet.CalcEngine.UseFormulaValues = true; 
worksheet.CalcEngine.MaximumRecursiveCalls = 10000; 
worksheet.CalcEngine.IterationMaxCount = 10000; 
CalcEngine.MaxStackDepth = 10000; 
{% endhighlight %}
{% endtabs %}

## See Also

* [How to overcome UnauthorizedAccessException?](faqs/how-to-overcome-unauthorizedaccessexception)
* [How to avoid exception when adding worksheets with same name?](faqs/how-to-avoid-exception-when-adding-worksheets-with-same-name)
* [What are the known exceptions of XlsIO?](https://help.syncfusion.com/file-formats/xlsio/known-exceptions)
* [What is Calculation Engine?](https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#calculation-engine)
* [What are Calculate Options?](https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#calculate-options)
