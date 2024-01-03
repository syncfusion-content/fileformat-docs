---
title: Working with LaTeX | DocIO | Syncfusion
description: Learn how to create mathematical equations in a Word document using LaTeX with the .NET Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Create Equation using LaTeX
The .NET Word (DocIO) library allows to create mathematical equation in Word document using **LaTeX**.

## Accent

Add **accent** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create accent equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an accent equation using LaTeX.
document.LastParagraph.AppendMath(@"\dot{a}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an accent equation using LaTeX.
document.LastParagraph.AppendMath(@"\dot{a}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an accent equation using LaTeX.
document.LastParagraph.AppendMath(@"\dot{a}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Accent/.NET).

The following table demonstrates the LaTeX equivalent to professional format accent equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent1.png" alt="Accent equation"></td>
<td>\dot{a}</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent2.png" alt="Accent equation"></td>
<td>\ddot{a}</td>
</tr>
<tr>
<td>3.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent3.png" alt="Accent equation"></td>
<td>\dddot{a}</td>
</tr>
<tr>
<td>4.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent4.png" alt="Accent equation"></td>
<td>\hat{a}</td>
</tr>
<tr>
<td>5.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent5.png" alt="Accent equation"></td>
<td>\check{a}</td>
</tr>
<tr>
<td>6.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent6.png" alt="Accent equation"></td>
<td>\acute{a}</td>
</tr>
<tr>
<td>7.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent7.png" alt="Accent equation"></td>
<td>\grave{a}</td>
</tr>
<tr>
<td>8.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent8.png" alt="Accent equation"></td>
<td>\breve{a}</td>
</tr>
<tr>
<td>9.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent9.png" alt="Accent equation"></td>
<td>\widetilde{a}</td>
</tr>
<tr>
<td>10.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent10.png" alt="Accent equation"></td>
<td>\bar{a}</td>
</tr>
<tr>
<td>11.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent11.png" alt="Accent equation"></td>
<td>\bar{\bar{a}}</td>
</tr>
<tr>
<td>12.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent12.png" alt="Accent equation"></td>
<td>\vec{a}</td>
</tr>
<tr>
<td>13.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent13.png" alt="Accent equation"></td>
<td>\hvec{a}</td>
</tr>
<tr>
<td>14.</td>
<td><img src="WorkingwithMathematicalEquation_images/Accent14.png" alt="Accent equation"></td>
<td>\widehat{AAA}</td>
</tr>
</table>

## Bar

Add **bar** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create bar equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an bar equation using LaTeX.
document.LastParagraph.AppendMath(@"\overline{a}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an bar equation using LaTeX.
document.LastParagraph.AppendMath(@"\overline{a}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an bar equation using LaTeX.
document.LastParagraph.AppendMath(@"\overline{a}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Bar/.NET).

The following table demonstrates the LaTeX equivalent to professional format bar equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/Bar1.png" alt="Bar equation"></td>
<td>\overline{a}</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/Bar2.png" alt="Bar equation"></td>
<td>\underline{abc}</td>
</tr>
</table>

## Box

Add **box** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create box equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an box equation using LaTeX.
document.LastParagraph.AppendMath(@"\box{a}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an box equation using LaTeX.
document.LastParagraph.AppendMath(@"\box{a}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an box equation using LaTeX.
document.LastParagraph.AppendMath(@"\box{a}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Box/.NET).

The following table demonstrates the LaTeX equivalent to professional format box equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/Box1.png" alt="Box equation"></td>
<td>\box{a}</td>
</tr>
</table>

## Border Box

Add **border box** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create border box equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an border box equation using LaTeX.
document.LastParagraph.AppendMath(@"\boxed{{x}^{2}+{y}^{2}={z}^{2}}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an border box equation using LaTeX.
document.LastParagraph.AppendMath(@"\boxed{{x}^{2}+{y}^{2}={z}^{2}}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an border box equation using LaTeX.
document.LastParagraph.AppendMath(@"\boxed{{x}^{2}+{y}^{2}={z}^{2}}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Border-Box/.NET).

The following table demonstrates the LaTeX equivalent to professional format border box equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/BorderBox1.png" alt="Border Box equation"></td>
<td>\boxed{{x}^{2}+{y}^{2}={z}^{2}}</td>
</tr>
</table>

## Delimiter

Add **delimiter** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create delimiter equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an delimiter equation using LaTeX.
document.LastParagraph.AppendMath(@"\left(a\right)");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an delimiter equation using LaTeX.
document.LastParagraph.AppendMath(@"\left(a\right)");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an delimiter equation using LaTeX.
document.LastParagraph.AppendMath(@"\left(a\right)")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Delimiter/.NET).

The following table demonstrates the LaTeX equivalent to professional format delimiter equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter1.png" alt="Delimiter equation"></td>
<td>\left(a\right)</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter2.png" alt="Delimiter equation"></td>
<td>\left[a\right]</td>
</tr>
<tr>
<td>3.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter3.png" alt="Delimiter equation"></td>
<td>\left\{a\right\}</td>
</tr>
<tr>
<td>4.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter5.png" alt="Delimiter equation"></td>
<td>\left\lfloora\right\rfloor</td>
</tr>
<tr>
<td>5.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter6.png" alt="Delimiter equation"></td>
<td>\left\lceila\right\rceil</td>
</tr>
<tr>
<td>6.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter7.png" alt="Delimiter equation"></td>
<td>\left|a\right|</td>
</tr>
<tr>
<td>7.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter9.png" alt="Delimiter equation"></td>
<td>\left[a\right[</td>
</tr>
<tr>
<td>8.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter10.png" alt="Delimiter equation"></td>
<td>\left]a\right]</td>
</tr>
<tr>
<td>9.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter11.png" alt="Delimiter equation"></td>
<td>\left]a\right[</td>
</tr>
<tr>
<td>10.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter13.png" alt="Delimiter equation"></td>
<td>\left(a\middle|b\right)</td>
</tr>
<tr>
<td>11.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter14.png" alt="Delimiter equation"></td>
<td>\left\{a\middle|b\right\}</td>
</tr>
<tr>
<td>12.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter15.png" alt="Delimiter equation"></td>
<td>\left\langlea\middle|b\right\rangle</td>
</tr>
<tr>
<td>13.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter16.png" alt="Delimiter equation"></td>
<td>\left\langlea\middle|b\middle|c\right\rangle</td>
</tr>
<tr>
<td>14.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter17.png" alt="Delimiter equation"></td>
<td>\left(a\right.</td>
</tr>
<tr>
<td>15.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter18.png" alt="Delimiter equation"></td>
<td>\left. a\right)</td>
</tr>
<tr>
<td>16.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter19.png" alt="Delimiter equation"></td>
<td>\left[a\right.</td>
</tr>
<tr>
<td>17.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter20.png" alt="Delimiter equation"></td>
<td>\left. a\right]</td>
</tr>
<tr>
<td>18.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter21.png" alt="Delimiter equation"></td>
<td>\left\{a\right.</td>
</tr>
<tr>
<td>19.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter22.png" alt="Delimiter equation"></td>
<td>\left. a\right\}</td>
</tr>
<tr>
<td>20.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter23.png" alt="Delimiter equation"></td>
<td>\left\langlea\right.</td>
</tr>
<tr>
<td>21.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter24.png" alt="Delimiter equation"></td>
<td>\left. a\right\rangle</td>
</tr>
<tr>
<td>22.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter25.png" alt="Delimiter equation"></td>
<td>\left\lfloora\right.</td>
</tr>
<tr>
<td>23.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter26.png" alt="Delimiter equation"></td>
<td>\left. a\right\rfloor</td>
</tr>
<tr>
<td>24.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter27.png" alt="Delimiter equation"></td>
<td>\left\lceila\right.</td>
</tr>
<tr>
<td>25.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter28.png" alt="Delimiter equation"></td>
<td>\left. a\right\rceil</td>
</tr>
<tr>
<td>26.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter29.png" alt="Delimiter equation"></td>
<td>\left|a\right.</td>
</tr>
<tr>
<td>27.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter30.png" alt="Delimiter equation"></td>
<td>\left. a\right|</td>
</tr>
<tr>
<td>28.</td>
<td><img src="WorkingwithMathematicalEquation_images/Delimiter31.png" alt="Delimiter equation"></td>
<td>\binom{a}{b}</td>
</tr>
</table>

## Fraction

Add **fraction** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create fraction equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an fraction equation using LaTeX.
document.LastParagraph.AppendMath(@"{\frac{dy}{dx}}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an fraction equation using LaTeX.
document.LastParagraph.AppendMath(@"{\frac{dy}{dx}}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an fraction equation using LaTeX.
document.LastParagraph.AppendMath(@"{\frac{dy}{dx}}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Fraction/.NET).

The following table demonstrates the LaTeX equivalent to professional format fraction equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/Fraction1.png" alt="Fraction equation"></td>
<td>frac{\mathbit{dy}}{\mathbit{dx}}</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/Fraction2.png" alt="Fraction equation"></td>
<td>\sfrac{dy}{dx}</td>
</tr>
<tr>
<td>3.</td>
<td><img src="WorkingwithMathematicalEquation_images/Fraction4.png" alt="Fraction equation"></td>
<td>{\frac{dy}{dx}}</td>
</tr>
</table>


## Function

Add **function** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create function equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an function equation using LaTeX.
document.LastParagraph.AppendMath(@"\sin{\theta}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an function equation using LaTeX.
document.LastParagraph.AppendMath(@"\sin{\theta}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an function equation using LaTeX.
document.LastParagraph.AppendMath(@"\sin{\theta}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Function/.NET).

The following table demonstrates the LaTeX equivalent to professional format function equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function1.png" alt="Function equation"></td>
<td>\sin{\theta}</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function2.png" alt="Function equation"></td>
<td>\cos{\theta}</td>
</tr>
<tr>
<td>3.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function3.png" alt="Function equation"></td>
<td>\tan{\theta}</td>
</tr>
<tr>
<td>4.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function4.png" alt="Function equation"></td>
<td>\csc{\theta}</td>
</tr>
<tr>
<td>5.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function5.png" alt="Function equation"></td>
<td>\sec{\theta}</td>
</tr>
<tr>
<td>6.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function6.png" alt="Function equation"></td>
<td>\cot{\theta}</td>
</tr>
<tr>
<td>7.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function7.png" alt="Function equation"></td>
<td>\sin^{-1}{\theta}</td>
</tr>
<tr>
<td>8.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function8.png" alt="Function equation"></td>
<td>\cos^{-1}{\theta}</td>
</tr>
<tr>
<td>9.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function9.png" alt="Function equation"></td>
<td>\tan^{-1}{\theta}</td>
</tr>
<tr>
<td>10.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function10.png" alt="Function equation"></td>
<td>\csc^{-1}{\theta}</td>
</tr>
<tr>
<td>11.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function11.png" alt="Function equation"></td>
<td>\sec^{-1}{\theta}</td>
</tr>
<tr>
<td>12.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function12.png" alt="Function equation"></td>
<td>\cot^{-1}{\theta}</td>
</tr>
<tr>
<td>13.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function13.png" alt="Function equation"></td>
<td>\sinh{\theta}</td>
</tr>
<tr>
<td>14.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function14.png" alt="Function equation"></td>
<td>\cosh{\theta}</td>
</tr>
<tr>
<td>15.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function15.png" alt="Function equation"></td>
<td>\tanh{\theta}</td>
</tr>
<tr>
<td>16.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function16.png" alt="Function equation"></td>
<td>\csch{\theta}</td>
</tr>
<tr>
<td>17.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function17.png" alt="Function equation"></td>
<td>\sech{\theta}</td>
</tr>
<tr>
<td>18.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function18.png" alt="Function equation"></td>
<td>\coth{\theta}</td>
</tr>
<tr>
<td>19.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function19.png" alt="Function equation"></td>
<td>\sinh^{-1}{\theta}</td>
</tr>
<tr>
<td>20.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function20.png" alt="Function equation"></td>
<td>\cosh^{-1}{\theta}</td>
</tr>
<tr>
<td>21.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function21.png" alt="Function equation"></td>
<td>\tanh^{-1}{\theta}</td>
</tr>
<tr>
<td>22.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function22.png" alt="Function equation"></td>
<td>\csch^{-1}{\theta}</td>
</tr>
<tr>
<td>23.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function23.png" alt="Function equation"></td>
<td>\sech^{-1}{\theta}</td>
</tr>
<tr>
<td>24.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function24.png" alt="Function equation"></td>
<td>\coth^{-1}{\theta}</td>
</tr>
<tr>
<td>25.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function25.png" alt="Function equation"></td>
<td>\arcsin{\theta}</td>
</tr>
<tr>
<td>26.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function26.png" alt="Function equation"></td>
<td>\arccos{\theta}</td>
</tr>
<tr>
<td>27.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function27.png" alt="Function equation"></td>
<td>\arctan{\theta}</td>
</tr>
<tr>
<td>28.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function28.png" alt="Function equation"></td>
<td>\arccsc{\theta}</td>
</tr>
<tr>
<td>29.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function29.png" alt="Function equation"></td>
<td>\arcsec{\theta}</td>
</tr>
<tr>
<td>30.</td>
<td><img src="WorkingwithMathematicalEquation_images/Function30.png" alt="Function equation"></td>
<td>\arccot{\theta}</td>
</tr>
</table>

## Group character

Add **group character** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create group character equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an group character equation using LaTeX.
document.LastParagraph.AppendMath(@"\overbrace{a-b}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an group character equation using LaTeX.
document.LastParagraph.AppendMath(@"\overbrace{a-b}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an group character equation using LaTeX.
document.LastParagraph.AppendMath(@"\overbrace{a-b}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Group-character/.NET).

The following table demonstrates the LaTeX equivalent to professional format group character equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/GroupCharacter1.png" alt="Group Character equation"></td>
<td>\overbrace{a-b}</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/GroupCharacter2.png" alt="Group Character equation"></td>
<td>\underbrace{a}</td>
</tr>
</table>

## Limit

Add **limit** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create limit equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an limit equation using LaTeX.
document.LastParagraph.AppendMath(@"\lim\below{b}{a}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an limit equation using LaTeX.
document.LastParagraph.AppendMath(@"\lim\below{b}{a}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an limit equation using LaTeX.
document.LastParagraph.AppendMath(@"\lim\below{b}{a}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Limit/.NET).

The following table demonstrates the LaTeX equivalent to professional format limit equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/Limit1.png" alt="Limit equation"></td>
<td>\lim\below{b}{a}</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/Limit2.png" alt="Limit equation"></td>
<td>\min\below{b}{a}</td>
</tr>
<tr>
<td>3.</td>
<td><img src="WorkingwithMathematicalEquation_images/Limit3.png" alt="Limit equation"></td>
<td>\max\below{b}{a}</td>
</tr>
</table>

## Matrix

Add **matrix** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create matrix equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an matrix equation using LaTeX.
document.LastParagraph.AppendMath(@"\begin{matrix}a&b\\\end{matrix}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an matrix equation using LaTeX.
document.LastParagraph.AppendMath(@"\begin{matrix}a&b\\\end{matrix}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an matrix equation using LaTeX.
document.LastParagraph.AppendMath(@"\begin{matrix}a&b\\\end{matrix}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Matrix/.NET).

The following table demonstrates the LaTeX equivalent to professional format matrix equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/Matrix1.png" alt="Matrix equation"></td>
<td>\begin{matrix}\mathbit{a}&\mathbit{b}\\\end{matrix}</td>
</tr>
</table>

## N-array

Add **N-array** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create N-array equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an N-array equation using LaTeX.
document.LastParagraph.AppendMath(@"\sum{a}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an N-array equation using LaTeX.
document.LastParagraph.AppendMath(@"\sum{a}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an N-array equation using LaTeX.
document.LastParagraph.AppendMath(@"\sum{a}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/N-array/.NET).

The following table demonstrates the LaTeX equivalent to professional format N-array equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray1.png" alt="N-Array equation"></td>
<td>\sum{a}</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray2.png" alt="N-Array equation"></td>
<td>\sum_{l}^{u}a</td>
</tr>
<tr>
<td>3.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray3.png" alt="N-Array equation"></td>
<td>\sum_{l}^{u}a</td>
</tr>
<tr>
<td>4.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray4.png" alt="N-Array equation"></td>
<td>\sum_{l}a</td>
</tr>
<tr>
<td>5.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray5.png" alt="N-Array equation"></td>
<td>\sum_{b}a</td>
</tr>
<tr>
<td>6.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray6.png" alt="N-Array equation"></td>
<td>\prod{a}</td>
</tr>
<tr>
<td>7.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray7.png" alt="N-Array equation"></td>
<td>\amalg{a}</td>
</tr>
<tr>
<td>8.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray8.png" alt="N-Array equation"></td>
<td>\bigcup{a}</td>
</tr>
<tr>
<td>9.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray9.png" alt="N-Array equation"></td>
<td>\bigcap{a}</td>
</tr>
<tr>
<td>10.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray10.png" alt="N-Array equation"></td>
<td>\bigvee{a}</td>
</tr>
<tr>
<td>11.</td>
<td><img src="WorkingwithMathematicalEquation_images/NArray11.png" alt="N-Array equation"></td>
<td>\bigwedge{a}</td>
</tr>
</table>

## Radical

Add **radical** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create radical equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an radical equation using LaTeX.
document.LastParagraph.AppendMath(@"\sqrt{a}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an radical equation using LaTeX.
document.LastParagraph.AppendMath(@"\sqrt{a}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an radical equation using LaTeX.
document.LastParagraph.AppendMath(@"\sqrt{a}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Radical/.NET).

The following table demonstrates the LaTeX equivalent to professional format radical equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/Radical1.png" alt="Radical equation"></td>
<td>\sqrt{a}</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/Radical2.png" alt="Radical equation"></td>
<td>\sqrt[b]{a}</td>
</tr>
</table>

## SubSuperScript

Add **SubSuperScript** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create SubSuperScript equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an SubSuperScript equation using LaTeX.
document.LastParagraph.AppendMath((@"{a}^{b}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an SubSuperScript equation using LaTeX.
document.LastParagraph.AppendMath((@"{a}^{b}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an SubSuperScript equation using LaTeX.
document.LastParagraph.AppendMath((@"{a}^{b}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/SubSuperScript/.NET).

The following table demonstrates the LaTeX equivalent to professional format SubSuperScript equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/SubSuperScript1.png" alt="SubSuperScript equation"></td>
<td>{\mathbit{a}}^{\mathbit{b}}</td>
</tr>
<tr>
<td>2.</td>
<td><img src="WorkingwithMathematicalEquation_images/SubSuperScript2.png" alt="SubSuperScript equation"></td>
<td>{\mathbit{a}}_{\mathbit{b}}</td>
</tr>
</table>

## Left SubSuperScript

Add **Left SubSuperScript** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create Left SubSuperScript equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an Left SubSuperScript equation using LaTeX.
document.LastParagraph.AppendMath(@"{_{40}^{20}}{100}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an Left SubSuperScript equation using LaTeX.
document.LastParagraph.AppendMath(@"{_{40}^{20}}{100}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an Left SubSuperScript equation using LaTeX.
document.LastParagraph.AppendMath(@"{_{40}^{20}}{100}");

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Left-SubSuperScript/.NET)

The following table demonstrates the LaTeX equivalent to professional format Left SubSuperScript equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/LeftSubSuperScript1.png" alt="Left SubSuperScript equation"></td>
<td>{_{\mathbf{40}}^{\mathbf{20}}}{\mathbf{100}}</td>
</tr>
</table>

## Right SubSuperScript

Add **Right SubSuperScript** equation to a Word document using the LaTeX through [AppendMath](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendMath_System_String_) API.

The following code example illustrates how to create Right SubSuperScript equation using LaTeX in Word document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an Right SubSuperScript equation using LaTeX.
document.LastParagraph.AppendMath(@"{100}_{40}^{20}");

//Save the Word document to MemoryStream
using MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);


{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Create a new Word document.
using WordDocument document = new WordDocument();

//Add one section and one paragraph to the document.
document.EnsureMinimal();

//Append an Right SubSuperScript equation using LaTeX.
document.LastParagraph.AppendMath(@"{100}_{40}^{20}");

//Save the Word document.
document.Save("Result.docx", FormatType.Docx);

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new Word document.
Dim document As WordDocument = New WordDocument()

'Add one section and one paragraph to the document.
document.EnsureMinimal()

'Append an Right SubSuperScript equation using LaTeX.
document.LastParagraph.AppendMath(@"{100}_{40}^{20}")

'Save the Word document.
document.Save("Result.docx", FormatType.Docx)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mathematical-Equation/LaTeX-equations/Right-SubSuperScript/.NET).

The following table demonstrates the LaTeX equivalent to professional format Right SubSuperScript equations.

<table>
<thead>
<tr>
<th width="20%">S.No</th>
<th width="40%">Professional</th>
<th width="40%">LaTeX</th>
</tr>
</thead>
<tr>
<td>1.</td>
<td><img src="WorkingwithMathematicalEquation_images/RightSubSuperScript1.png" alt="Right SubSuperScript equation"></td>
<td>{\mathbf{100}}_{\mathbf{40}}^{\mathbf{20}}</td>
</tr>
</table>
