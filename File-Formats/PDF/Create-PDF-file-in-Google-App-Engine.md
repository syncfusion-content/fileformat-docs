---
title: Create or Generate PDF document in Google App Engine| Syncfusion
description: Learn how to create or generate a PDF file in the Google App Engine using Syncfusion .NET Core PDF library without the dependency of Adobe Acrobat. 
platform: file-formats
control: PDF
documentation: UG
keywords: google app engine save pdf, app engine load pdf, c# save pdf, c# load pdf
---

# Create a PDF document in Google App Engine

The [Syncfusion .NET Core PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net-core) is used to create, read, and edit PDF documents programatically without the dependency on Adobe Acrobat. Using this library, you can **open and save PDF document in Google App Engine**.

## Set up App Engine

Step 1: Open the **Google Cloud Console** and click the **Activate Cloud Shell** button.
![Activate Cloud Shell](GettingStarted_images/Google_Cloud_Console.png)

Step 2: Click the **Cloud Shell Editor** button to view the **Workspace**.
![Open Editor in Cloud Shell](GettingStarted_images/Cloud_Shell.png)

Step 3: Open **Cloud Shell Terminal**, and run the following **command** to confirm authentication.
{% tabs %}
{% highlight c# tabtitle="CLI" %}

gcloud auth list

{% endhighlight %}
{% endtabs %}

![Authentication for App Engine](GettingStarted_images/Authorize_Command.png)

Step 4: Click the **Authorize** button.
![Click Authorize button](GettingStarted_images/Authorize_Button.png)

## Create an application for App Engine

Step 1: Open Visual Studio and select the ASP.NET Core Web app (Model-View-Controller) template.
![Create ASP.NET Core Web application in Visual Studio](GettingStarted_images/Create-Project.png)

Step 2: Configure your new project according to your requirements.
![Create ASP.NET Core Web application in Visual Studio](GettingStarted_images/Project-Name.png)

Step 3: Click the **Create** button.
![Create ASP.NET Core Web application in Visual Studio](GettingStarted_images/Additional-Information.png)

Step 4:Install the [Syncfusion.Pdf.Net.Core](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core/) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.DocIO.Net.Core NuGet package](GettingStarted_images/Google-NuGet-Package.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from the trial setup or from the NuGet feed, you also have to add the "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to learn about registering the Syncfusion license key in your application to use our components.

Step 5: Include the following namespaces in the **HomeController.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.Pdf.Graphics;
using Syncfusion.Drawing;
using System.IO;

{% endhighlight %}
{% endtabs %}

Step 6: A default action method named Index will be present in HomeController.cs. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 7: Add a new button in the Index.cshtml as shown in the following.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@{Html.BeginForm("CreateDocument", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Create PDF Document" style="width:200px;height:27px" />
        </div>
    }
    Html.EndForm();
}
{% endhighlight %}
{% endtabs %}

Step 8: Add a new action method **CreateDocument** in HomeController.cs and include the following code sample to **create PDF document** and download it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Load PDF document as stream.
using FileStream docStream = new FileStream(@"Data/Input.pdf", FileMode.Open, FileAccess.Read);
//Load an existing PDF document.
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Load the existing page.
PdfLoadedPage loadedPage = document.Pages[0] as PdfLoadedPage;
//Create PDF graphics for the page.
PdfGraphics graphics = loadedPage.Graphics;

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();
//Add values to the list.
List<object> data = new List<object>();
Object row1 = new { Product_ID = "1001", Product_Name = "Bicycle", Price = "10,000" };
Object row2 = new { Product_ID = "1002", Product_Name = "Head Light", Price = "3,000" };
Object row3 = new { Product_ID = "1003", Product_Name = "Break wire", Price = "1,500" };
data.Add(row1);
data.Add(row2);
data.Add(row3);
//Add list to IEnumerable.
IEnumerable<object> dataTable = data;
//Assign data source.
pdfGrid.DataSource = dataTable;
//Apply built-in table style.
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent3);
//Draw the grid to the page of PDF document.
pdfGrid.Draw(graphics, new RectangleF(40, 400, loadedPage.Size.Width - 80, 0));

//Create memory stream. 
MemoryStream stream = new MemoryStream();
//Save the PDF document to stream.
document.Save(stream);
//If the position is not set to '0' then the PDF will be empty.
stream.Position = 0;
//Close the document.
document.Close(true);
//Download Word document in the browser.
return File(stream, "application/pdf", "Sample.pdf");

{% endhighlight %}
{% endtabs %}

## Move application to App Engine

Step 1: Open the **Cloud Shell editor**.

![Cloud Sell editor](GettingStarted_images/Cloud_Shell_Editor.png)

Step 2: Drag and drop the sample from your local machine to **Workspace**.

![Add Project](GettingStarted_images/Add_Project.png)

N> If you have your sample application in your local machine, drag and drop it into the Workspace. If you created the sample using the Cloud Shell terminal command, it will be available in the Workspace.

Step 3: Open the Cloud Shell Terminal and run the following **command** to view the files and directories within your **current Workspace**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

ls

{% endhighlight %}
{% endtabs %}

![ls command](GettingStarted_images/ls_Command.png)

Step 4: Run the following **command** to navigate which sample you want to run.

{% tabs %}
{% highlight c# tabtitle="C#" %}

cd Open-and-save-Word-document

{% endhighlight %}
{% endtabs %}

![Project Folder](GettingStarted_images/Project_Folder.png)

Step 5: To ensure that the sample is working correctly, please run the application using the following command.

{% tabs %}
{% highlight c# tabtitle="C#" %}

dotnet run --urls=http://localhost:8080

{% endhighlight %}
{% endtabs %}

![Run Application](GettingStarted_images/Run_Application.png)

Step 6: Verify that the application is running properly by accessing the **Web View -> Preview on port 8080**.

![Preview on Port](GettingStarted_images/Preview.png)

Step 7: Now you can see the sample output on the preview page.

![Output Button](GettingStarted_images/Console_Page.png)

Step 8: Close the preview page and return to the terminal then press **Ctrl+C** for which will typically stop the process.

![Work space](GettingStarted_images/Run_View.png)

## Publish the application

Step 1: Run the following command in the **Cloud Shell Terminal** to publish the application.

{% tabs %}
{% highlight c# tabtitle="C#" %}

dotnet publish -c Release

{% endhighlight %}
{% endtabs %}

![Release](GettingStarted_images/Publish_GCP.png)

Step 2: Run the following command in the **Cloud Shell Terminal** to navigate to the publish folder.

{% tabs %}
{% highlight c# tabtitle="C#" %}

cd bin/Release/net6.0/publish/

{% endhighlight %}
{% endtabs %}

![Publish Folder](GettingStarted_images/Publish_Folder.png)

## Configure app.yaml and docker file

Step 1: Add the app.yaml file to the publish folder with the following contents.

{% tabs %}
{% highlight c# tabtitle="C#" %}

cat <<EOT >> app.yaml
env: flex
runtime: custom   
EOT

{% endhighlight %}
{% endtabs %}

![yaml file to publish](GettingStarted_images/App_yaml.png)


Step 2: Add the Docker file to the publish folder with the following contents.

{% tabs %}
{% highlight c# tabtitle="C#" %}

cat <<EOT >> Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:6.0
RUN apt-get update -y && apt-get install libfontconfig -y
ADD / /app
EXPOSE 8080
ENV ASPNETCORE_URLS=http://*:8080
WORKDIR /app
ENTRYPOINT [ "dotnet", "Open-and-save-Word-document.dll"]
EOT

{% endhighlight %}
{% endtabs %}

![Docker file to publish](GettingStarted_images/Docker_File.png)

Step 3: You can ensure **Docker** and **app.yaml** files are added in **Workspace**.

![Docker file](GettingStarted_images/Docker.png)

## Deploy to App Engine

Step 1: To deploy the application to the App Engine, run the following command in Cloud Shell Terminal. Afterwards, retrieve the **URL** from the Cloud Shell Terminal.

{% tabs %}
{% highlight c# tabtitle="C#" %}

gcloud app deploy --version v0

{% endhighlight %}
{% endtabs %}

![Deploy](GettingStarted_images/Deploy.png)

Step 2: Open the **URL** to access the application, which has been successfully deployed.

![Output Console](GettingStarted_images/Console_Page.png)

You can download a complete working sample from [GitHub]().

By executing the program, you will get the **PDF document** as follows. The output will be saved in the **bin folder**.

![Output PDF Document](GettingStarted_images/Open_and_save_output.png)

Click [here]() to explore the rich set of Syncfusion PDF library features.





