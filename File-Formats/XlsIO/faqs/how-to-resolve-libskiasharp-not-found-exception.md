---
title: How to resolve LibSkiaSharp not found exception? | Syncfusion
description: This page shows how to resolve LibSkiaSharp not found exception using the Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to resolve LibSkiaSharp not found exception?

* In Docker container, ensure whether the libfontconfig package properly installed by adding the following line in your Docker file.
{% tabs %} 

{% highlight Dockerfile %}
RUN apt-get update -y && apt-get install libfontconfig -y
{% endhighlight %}

{% endtabs %}  


* In production environment (hosted server machine), ensure whether the Visual C++ Redistributable is properly installed.

	[Download](https://www.microsoft.com/en-us/download/details.aspx?id=53587) and install Visual C++, if not installed.