---
title: Troubleshooting
description: Explains various troubleshooting issues while using XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Troubleshooting

This section covers various troubleshooting issues while using XlsIO libraries.

## Patch does not work properly

**Cause**
This may occur when there is an assembly conflict between the GAC assemblies and local referenced assemblies. 

**Solution** 
Try deleting ‘bin’ and ‘obj’ folders from the project and clear GAC assemblies using Syncfusion assembly manager from Syncfusion dashboard and then try the patch. Removing the GAC assemblies is explained in the below link.

[http://help.syncfusion.com/ug/common/default.htm#!documents/assemblymanager.htm](http://help.syncfusion.com/ug/common/default.htm#!documents/assemblymanager.htm "")

## Could not load file or assembly 'Syncfusion.XlsIO.Base, Version=xxxx, Culture=neutral, PublicKeyToken=xxxxxxxxxx' or one of its dependencies. The system cannot find the file specified.

**Cause**

The error occurs when the referenced assemblies are not in the path corresponding to the build configuration or GAC. 

**Solution**

The following properties must be ensured during deployment.

* __**Specific**__ __**Version**__

  * Specific version should be set to **False** to always compile against the latest version of Syncfusion assemblies.

* __**Copy**__ __**Local**__

  * If the CopyLocal is set to **False** for all the Syncfusion assemblies in your project, then you have to deploy the Syncfusion assemblies into the GAC in your deployment machine.

  * If the CopyLocal is set to **True** for all the Syncfusion assemblies in your project, then you have to place the Syncfusion assemblies in the Bin/local folder to ensure it ends up in the output directory so it can be found at runtime.

For more details on Specific Version and Copy Local, see link. 



## Excel cannot open the file 'filename.xlsx' because the file format for the file extension is not valid. Verify that the file has not been corrupted and that the file extension matches the format of the file

**Cause**

This error occurs when there is a mismatch between the file format and its extension. 

**Solution**

The default workbook creation version in XlsIO is Excel97-2003 (.xls). The application version set to the required version should match its file format during save. The below code shows 

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Set application version

application.DefaultVersion = ExcelVersion.Excel2013;

//Do some manipulation

//Do some manipulation

//Workbook is saved in Excel2013 format

workbook.SaveAs("Sample.xlsx");



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'Set application version

application.DefaultVersion = ExcelVersion.Excel2013

'Do some manipulation

'Do some manipulation

'Workbook is saved in Excel2013 format

workbook.SaveAs("Sample.xlsx")



{% endhighlight %}

  {% endtabs %}  

If the application version is ignored, then the workbook version should be set properly during creation and save.

* To save a workbook in Excel2003 format, set the workbook version to Excel97to2003 and save the file with extension ‘.xls’ i.e. binary file format.

* To save a workbook in Excel 2007 and above formats, set the workbook version to Excel2007 and above and save the file with extension __‘.____xlsx’__ i.e. open xml file format.

These are represented in the below code snippet.

{% tabs %}  

{% highlight c# %}
workbook.Version = ExcelVersion.Excel97to2003;

workbook.SaveAs("Sample.xls");

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Sample.xlsx");



{% endhighlight %}

{% highlight vb %}
workbook.Version = ExcelVersion.Excel97to2003

workbook.SaveAs("Sample.xls")

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Sample.xlsx")



{% endhighlight %}

  {% endtabs %}  

