---
title: Convert PowerPoint to PDF in Windows Forms | Syncfusion
description: Convert PowerPoint to PDF in Windows Forms using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to PDF in Windows Forms

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and **convert PowerPoint documents** programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to PDF in Windows Forms**.

## Steps to convert PowerPoint to PDF programmatically

Step 1: Create a new C# Windows Forms application project.

![Create Windows Forms project](Workingwith_Windows/Project-Open-and-Save.png)

Step 2: Install the [Syncfusion.Presentation.WinForms](https://www.nuget.org/packages/Syncfusion.Presentation.WinForms/) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.Presentation.WinForms Nuget Package](Workingwith_Windows/Nuget-Package-Open-and-Save.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in the **Form1.Designer.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;
using Syncfusion.PresentationToPdfConverter;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}

Step 4: Add a new button in **Form1.Designer.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

private Button btnCreate;
private Label label;
private void InitializeComponent()
{
    label = new Label();
    btnCreate = new Button();
    //Label
    label.Location = new System.Drawing.Point(0, 40);
    label.Size = new System.Drawing.Size(426, 35);
    label.Text = "Click the button to Convert PowerPoint to PDF.";
    label.TextAlign = System.Drawing.ContentAlignment.MiddleCenter;

    //Button
    btnCreate.Location = new System.Drawing.Point(180, 110);
    btnCreate.Size = new System.Drawing.Size(85, 36);
    btnCreate.Text = "Convert";
    btnCreate.Click += new EventHandler(btnConvert_Click);

    ClientSize = new System.Drawing.Size(450, 150);
    Controls.Add(label);
    Controls.Add(btnCreate);
    Text = "Convert PowerPoint to PDF";
}

{% endhighlight %}
{% endtabs %}

Step 5: Add the following code in **btnOpenAndSave_Click** to **convert a PowerPoint to PDF in Windows Forms**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Opens a PowerPoint Presentation
using (IPresentation pptxDoc = Presentation.Open(Path.GetFullPath(@"../../Data/Input.pptx")))
{
    //Converts the PowerPoint Presentation into PDF document
    PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
    //Saves the PDF document
    pdfDocument.Save(Path.GetFullPath(@"../../Sample.pdf"));
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Read-and-save-PowerPoint-presentation/Open-and-save-PowerPoint/Windows-Forms).

By executing the program, you will get the **PDF** as follows.

![PowerPoint to PDF in Windows Forms](Workingwith_Core/Open-and-Save-output-image.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features.