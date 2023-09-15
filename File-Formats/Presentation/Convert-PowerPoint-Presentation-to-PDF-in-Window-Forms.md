---
title: Convert PowerPoint to PDF in Windows Forms | Syncfusion
description: Convert PowerPoint to PDF in Windows Forms using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to PDF in Windows Forms

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to PDF in Windows Forms**.

## Steps to convert PowerPoint to PDF programmatically

Step 1: Create a new C# Windows Forms application project.

![Create Windows Forms project](Workingwith_Windows/Project-Open-and-Save.png)

Step 2: Install the [Syncfusion.PresentationToPdfConverter.WinForms](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.WinForms) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.PresentationToPdfConverter.WinForms Nuget Package](Workingwith_Windows/Nuget-Package-PPTXtoPDF.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in the **Form1.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.Presentation;
using Syncfusion.PresentationToPdfConverter;

{% endhighlight %}
{% endtabs %}

Step 4: Add a new button in **Form1.Designer.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

private Button btnCreate;
private Label label;
private void InitializeComponent()
{
    this.label = new System.Windows.Forms.Label();
    this.btnCreate = new System.Windows.Forms.Button();
    this.SuspendLayout();
    // 
    // label
    // 
    this.label.Location = new System.Drawing.Point(0, 40);
    this.label.Name = "label";
    this.label.Size = new System.Drawing.Size(426, 35);
    this.label.TabIndex = 0;
    this.label.Text = "Click the button to convert PowerPoint to PDF";
    this.label.TextAlign = System.Drawing.ContentAlignment.MiddleCenter;
    // 
    // btnCreate
    // 
    this.btnCreate.Location = new System.Drawing.Point(180, 110);
    this.btnCreate.Name = "btnCreate";
    this.btnCreate.Size = new System.Drawing.Size(85, 36);
    this.btnCreate.TabIndex = 1;
    this.btnCreate.Text = "Convert PPTX to PDF";
    this.btnCreate.Click += new System.EventHandler(this.btnConvert_Click);
}

{% endhighlight %}
{% endtabs %}

Step 5: Add the following code in **btnConvert_Click** to **convert a PowerPoint to PDF in Windows Forms**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Opens a PowerPoint Presentation
using (IPresentation pptxDoc = Presentation.Open("Data/Input.pptx"))
{
    //Converts the PowerPoint Presentation into PDF document
    using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
    {
        //Saves the PDF document
        pdfDocument.Save("Sample.pdf");
    }
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from GitHub.

By executing the program, you will get the **PDF** as follows.

![PowerPoint to PDF in Windows Forms](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-PDF.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features. 

An online sample link to [convert PowerPoint Presentation to PDF](https://ej2.syncfusion.com/aspnetcore/PowerPoint/PPTXToPDF#/material3) in ASP.NET Core. 