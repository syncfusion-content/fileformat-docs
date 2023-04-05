---
title: How to apply rotation and transparency to background image | XlsIO | Syncfusion
description: This page explains how to apply rotation and transparency to background image using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to apply rotation and transparency to background image?

Syncfusion XlsIO do not have direct support to apply rotation and transparency to background image. But this can be achieved through below workaround.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  //Load an existing Excel file into IWorkbook
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  System.Drawing.Image image = System.Drawing.Image.FromFile("image.png");
  Bitmap bitmap = new Bitmap(image);

  //Rotate the image
  bitmap.RotateFlip(System.Drawing.RotateFlipType.Rotate90FlipNone);

  //Apply transparency
  bitmap.MakeTransparent(System.Drawing.Color.Black);

  bitmap.Save("image_M.png", ImageFormat.Png);

  FileStream imageStream = new FileStream("image_M.png", FileMode.Open, FileAccess.Read);
  worksheet.PageSetup.BackgoundImage = Syncfusion.Drawing.Image.FromStream(imageStream);

  #region Save
  //Saving the workbook
  FileStream outputStream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.Write);
  workbook.SaveAs(outputStream);
  #endregion

  //Dispose streams
  outputStream.Dispose();
  inputStream.Dispose();
}
{% endhighlight %}
{% endtabs %}
