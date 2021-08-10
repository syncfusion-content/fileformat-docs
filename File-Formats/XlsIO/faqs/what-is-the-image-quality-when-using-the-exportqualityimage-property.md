---
title: Image quality when using the ExportQualityImage property | Syncfusion
description: This page explains about the impact on image quality when using the ExportQualityImage property of XlsIO.
platform: File-formats
control: XlsIO
documentation: UG
---

# What is the image quality when using the ExportQualityImage property?

Normally, the image in the PDF will be saved in PNG format. With this property, the TIFF format is used for exporting the images into PDF. 

**TIFF (non-default):**
TIFF uses a lossless compression algorithm in order to preserve as much quality in the image. They are high resolution files with larger sizes. They are no longer supported on many websites, due to their slower loading time. If you can still open the file, it will take much longer to download or load in the browser due to their size. Since they preserve the most quality, they are best used for printing to paper and even billboard signs.

**PNG (default):**
PNG is ideal even for complex images. If you require more detail in graphics, then PNG is better. PNG provides the best support for transparency. PNG is ideal for static images, logos, prints and other images with transparent background.

Hence, we have used PNG format as default for exporting the images into PDF. If you are concerned only about the image quality and not about file size and loading time, then you can use the non-default with the **ExportQualityImage** property.

## See Also

* [How to export quality image?](https://help.syncfusion.com/file-formats/xlsio/excel-to-pdf-converter-settings#export-quality-image)
* [How to convert Worksheet to Image?](https://help.syncfusion.com/file-formats/xlsio/worksheet-to-image-conversion)
* [How to convert Chart to Image?](https://help.syncfusion.com/file-formats/xlsio/chart-to-image-conversion)
