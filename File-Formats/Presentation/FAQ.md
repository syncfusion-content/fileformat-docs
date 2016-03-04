---
title: Frequently Asked Questions
description: Frequently asked questions on Essential Presentation library
platform: file-formats
control: Presentation
documentation: UG
---
# FAQ’s

1. **Why I get an exception when trying to load a PPT file?**

   The current version of Presentation library supports only .PPTX format - Microsoft Office 2007 and later version.

2. **Is it possible to print the presentation slides?**

   Yes, you can print the PowerPoint presentations by using its ability to convert the slides as images and by using the [PrintDocument](https://msdn.microsoft.com/en-us/library/system.drawing.printing.printdocument(v=vs.110).aspx# "") class. For more details, refer to [Printing](http://www.google.com/# "")

3. **Does adding audio and video to a presentation is supported?**

   At present, there is no support to add audio and video to presentation by using Essential Presentation library.

4. **What measure does Essential Presentation use to add slide elements such as textbox, shape, picture and charts?**

   We use Points to add any slide elements in a presentation.

5. **Does Essential presentation supports cloning a slide in the presentation?**

   Yes, Essential presentation library supports cloning as follows:

   * Slide in the presentation can be cloned from one presentation to another or within a same presentation.
   * An entire presentation can also be cloned as an independent copy of the original.
   
6. **Could not find Syncfusion.OfficeChartToImageConverter assembly in .NET 3.5 Framework, does it mean there is no support for chart conversion in this framework?**

   Yes, OfficeChartToImageConverter assembly is not supported in .NET 3.5 Framework and it is available from .NET 4.0 Framework.

7. **Can chart data be refreshed?**

   Yes, Essential Presentation supports refreshing the chart data. For more details, refer to [Working with charts](/file-formats/presentation/working-with-charts)

8. **Is it possible to convert 3D charts to PDF or image?**

   Current version of the Essential Presentation library does not provide support for converting 3D charts to PDF or image format.

