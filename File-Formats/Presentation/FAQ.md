---
title: Frequently Asked Questions for PowerPoint Presentations | Syncfusion
description: This section illustrates about frequently asked questions in various options by using Essential Syncfusion Presentation library.
platform: file-formats
control: Presentation
documentation: UG
---
# FAQ’s for PowerPoint Presentations

1. **Why I get an exception when trying to load a PPT file?**

   The current version of Presentation library supports only .PPTX format - Microsoft Office 2007 and later version.

2. **Is it possible to print the Presentation slides?**

   Yes, you can print the PowerPoint presentations by using its ability to convert the slides as images and by using the [PrintDocument](https://msdn.microsoft.com/en-us/library/system.drawing.printing.printdocument(v=vs.110).aspx# "") class. For more details, refer to [Printing](http://www.google.com/# "")

3. **Does adding audio and video to a Presentation is supported?**

   At present, there is no support to add audio and video to Presentation by using Essential Presentation library.

4. **What measure does Essential Presentation use to add slide elements such as textbox, shape, picture and charts?**

   We use Points to add any slide elements in a Presentation.

5. **Does Essential Presentation supports cloning a slide in the Presentation?**

   Yes, Essential Presentation library supports cloning as follows:

   * Slide in the Presentation can be cloned from one Presentation to another or within a same Presentation.
   * An entire Presentation can also be cloned as an independent copy of the original.
   
6. **Could not find Syncfusion.OfficeChartToImageConverter assembly in .NET 3.5 Framework, does it mean there is no support for chart conversion in this framework?**

   Yes, OfficeChartToImageConverter assembly is not supported in .NET 3.5 Framework and it is available from .NET 4.0 Framework.

7. **Can chart data be refreshed?**

   Yes, Essential Presentation supports refreshing the chart data. For more details, refer to [Working with charts](/file-formats/presentation/working-with-charts)

8. **Is it possible to convert 3D charts to PDF or image?**

   Current version of the Essential Presentation library does not provide support for converting 3D charts to PDF or image format.

9. **How to improve the image quality while converting the Presentation slides to image?**
   
   You can improve the quality of converted images by specifying the image resolution. Refer – [Converting PowerPoint presentation to Images](/file-formats/presentation/getting-started#converting-powerpoint-presentation-to-images)

