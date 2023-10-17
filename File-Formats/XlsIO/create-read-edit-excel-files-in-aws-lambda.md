---
title: Create, read, and edit Excel files in AWS Lambda | Syncfusion
description: Explains how to create, read, and edit Excel files in AWS Lambda.
platform: file-formats
control: XlsIO
documentation: UG
---

# Create, read, and edit Excel files in AWS Lambda

[Syncfusion Excel library for ASP.NET Core platform](https://www.syncfusion.com/document-processing/excel-framework/net-core/excel-library) can be used to create, read, edit Excel files. This also convert Excel files to PDF.

## Create a simple Excel report

The below steps illustrates creating a simple Invoice formatted Excel document in ASP.NET Core.

Step 1: Create a new **AWS Lambda project** as follows..

<img src="ASP-NET-Core_images/ASP-NET-Core_images_img1.png" alt="Create ASP.NET Core web application in Visual Studio" width="100%" Height="Auto"/>

Step 2: Select Blueprint as Empty Function and click **Finish**.

<img src="ASP-NET-Core_images/ASP-NET-Core_images_img2.png" alt="Select Web application pattern" width="100%" Height="Auto"/>

Step 3: Install the [Syncfusion.XlsIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

<img src="ASP-NET-Core_images/ASP-NET-Core_images_img3.png" alt="Add XlsIO reference to the project" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components. 

Step 4: Create a folder and copy the required data files and include the files to the project.

<img src="ASP-NET-Core_images/ASP-NET-Core_images_img3.png" alt="Add XlsIO reference to the project" width="100%" Height="Auto"/>

Step 5: Set the **copy to output directory** to **Copy if newer** to all the data files.
![Property change for data files](AWS_Images/Lambda_Images/Data-Folder-Create-Word-Document.png)