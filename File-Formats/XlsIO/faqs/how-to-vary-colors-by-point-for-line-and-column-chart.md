---
title: Vary colors by point for line and column chart | Syncfusion
description: This page shows how to vary colors by point for line and column chart using the Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to vary colors by point for line and column chart?

The following code snippet shows how to vary colors by point for a line chart series.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
chart.Series[0].SerieFormat.LineProperties.AutoFormat = true;
chart.Series[0].SerieFormat.CommonSerieOptions.IsVaryColor = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
chart.Series[0].SerieFormat.LineProperties.AutoFormat = true;
chart.Series[0].SerieFormat.CommonSerieOptions.IsVaryColor = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
chart.Series[0].SerieFormat.LineProperties.AutoFormat = True
chart.Series[0].SerieFormat.CommonSerieOptions.IsVaryColor = True
{% endhighlight %}
{% endtabs %}  

The following code snippet shows how to vary colors by point for a column chart series.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
chart.Series[0].SerieFormat.Interior.UseAutomaticFormat = true;
chart.Series[0].SerieFormat.CommonSerieOptions.IsVaryColor = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
chart.Series[0].SerieFormat.Interior.UseAutomaticFormat = true;
chart.Series[0].SerieFormat.CommonSerieOptions.IsVaryColor = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
chart.Series[0].SerieFormat.Interior.UseAutomaticFormat = True
chart.Series[0].SerieFormat.CommonSerieOptions.IsVaryColor = True
{% endhighlight %}
{% endtabs %}  