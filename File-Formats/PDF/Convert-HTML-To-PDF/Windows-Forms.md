---
title: Convert a HTML to PDF file in Windows-Forms | Syncfusion
description: Learn how to convert a HTML to PDF file in Windows-Forms with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in Windows Forms

The Syncfusion HTML to PDF converter is a .NET library used to convert HTML or web pages to PDF document in Windows Forms application.

## Steps to convert Html to PDF document in Windows Forms

1. Create a new Windows Forms application project.
   <img src="htmlconversion_images/Windows_Forms_step1.png" alt="Convert HTMLToPDF Windows Forms Step1" width="100%" Height="Auto"/>
   In project configuration window, name your project and select Create.
   <img src="htmlconversion_images/Windows_Forms_step2.png" alt="Convert HTMLToPDF Windows Forms Step2" width="100%" Height="Auto"/>

2. Install the [Syncfusion.HtmlToPdfConverter.WinForms](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.WinForms) NuGet package as a reference to your WinForms application [NuGet.org](https://www.nuget.org/).
   <img src="htmlconversion_images/Windows_Forms_step3.png" alt="Convert HTMLToPDF Windows Forms Step3" width="100%" Height="Auto"/>

3. Add the following namespaces into Form1.Designer.cs file.

   {% highlight c# tabtitle="C#" %}

   using System;
   using System.Windows.Forms;

   {% endhighlight %}

4. Add a new button in Form1.Designer.cs to convert HTML to PDF document as follows.

   {% highlight c# tabtitle="C#" %}

   private Button btnCreate;
   private Label label;
   private void InitializeComponent()
   {
        btnCreate = new Button();
        label = new Label();

        //Label
        label.Location = new System.Drawing.Point(0, 40);
        label.Size = new System.Drawing.Size(426, 35);
        label.Text = "Click the button to convert Html to PDF file";
        label.TextAlign = System.Drawing.ContentAlignment.MiddleCenter;

        //Button
        btnCreate.Location = new System.Drawing.Point(180, 110);
        btnCreate.Size = new System.Drawing.Size(85, 26);
        btnCreate.Text = "Convert Html to PDF";
        btnCreate.Click += new EventHandler(btnCreate_Click);

        //Create PDF
        ClientSize = new System.Drawing.Size(450, 150);
        Controls.Add(label);
        Controls.Add(btnCreate);
        Text = "Convert Html to PDF";
   }

   {% endhighlight %}

5. Include the following namespaces in the Form1.cs file.

   {% highlight c# tabtitle="C#" %}

   using Syncfusion.HtmlConverter;
   using Syncfusion.Pdf;
   using System;

   {% endhighlight %}

6. Create the btnCreate_Click event and add the following code in btnCreate_Click to convert HTML to PDF document.

   {% highlight c# tabtitle="C#" %}

   //Initialize HTML to PDF converter.
   HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
   BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();
   //Set Blink viewport size.
   blinkConverterSettings.ViewPortSize = new System.Drawing.Size(1280, 0);
   //Assign Blink converter settings to HTML converter.
   htmlConverter.ConverterSettings = blinkConverterSettings;
   //Convert URL to PDF document.
   PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com");
   //Create file stream.
   FileStream stream = new FileStream("HTML-to-PDF.pdf", FileMode.CreateNew);
   //Save the document into stream.
   document.Save(stream);
   //If the position is not set to '0' then the PDF will be empty.
   stream.Position = 0;
   //Close the document.
   document.Close();
   stream.Dispose();

   {% endhighlight %}

   By executing the program, you will get the PDF document as follows.
   <img src="htmlconversion_images/htmltopdfoutput.png" alt="Convert HTMLToPDF Windows Forms output" width="100%" Height="Auto"/>

   A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-dotnet-examples/blob/master/Windows%20Forms)

